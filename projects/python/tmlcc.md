[<<Home](https://pakkawatk.github.io/portfolio)<br />
## Thailand Machine Learning Competition for Chemistry.
36th rank from 76 competitors as "Team Koalas" in Thailand Machine Learning for Chemistry Competition.<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/tmlcc.PNG?raw=true)<br />
**Objective:** To predict "CO2 Working Capacity" of "MOF" by Machine Learning with the lowest log of MAE score.<br />
**Dataset:** Properties (x) of MOF which y = CO2 Working Capacity.<br />
**Exploratory Data Analysis:**<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/mof1.PNG?raw=true)<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/mof2.PNG?raw=true)<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/mof3.PNG?raw=true)<br /><br />
**Process:**<br />
- From Data Understanding, Void Fraction, Void Volume can't be < 0 and Surface Area can't be <= 0.<br />
- Feature Engineering for Density by Density = Weight/Volume<br />
- Replace Void Fraction <= 0 by Void Fraction = Void Fraction/Density<br />
- Replace Void Volume <= 0 by Void Volume = Void Fraction/Density<br />
- Drop NA records.<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/mof4.PNG?raw=true)<br />
- Replace Surface Area <= 0 by "Surface Area Simulation function". (The function won't be mentioned in here)<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/mof5.PNG?raw=true)<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/mof6.PNG?raw=true)<br />
**Machine Learning Neural Network:**
- Apply one-hot encodeing for nominal features to binary features.<br />
- Normalize by Standard Scaler to balance values.<br />
- Split train data size = 0.3.<br />
- Apply Neural Network rulu = 12 layers, epochs=5000, batch_size=10000<br />
- Apply train data set and predict test data set.
- log_mae test = 3.28<br />
- load and predict submission test data ( No y column ) for submit in Codalab.
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/mof7.PNG?raw=true)<br />
**Machine Learning XGBoost:**
- Find Best Model via AutoML and the best model is XGBoost.<br />
- Normalize by Standard Scaler to balance values.<br />
- Split train data<br />
- Apply train data set and predict test data set.
- Apply XGBoost<br />
- Log_MAE Train: 2.96, Log_MAE Test: 3.05
- load and predict submission test data ( No y column ) for submit in Codalab.
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/mof8.PNG?raw=true)<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/mof9.PNG?raw=true)<br /><br />

**Conclusion:** Finally, we got two models and send submisstion file to Codalab and then Codalab predict by using unseen dataset and the best model of my team is XGBoost that we got 32th rank of log MAE = 1.27 in competition.  <br />

## Code

```

#Importing Requierd Libraries
import pandas as pd
import matplotlib.pyplot as plt
from IPython.display import display
import numpy as np

```

```

# Read dataset
df = pd.read_csv('../SP_Programming/dataset/MOFtrain.csv')

```

```

# Making a function for examining data
def data_research(data, data_name='data', un=False):
    #basic
    print(f'Examining "{data_name}"')
    display(data.head(2))
    display(data.info())
    display(data.describe( include='all'))
    #display(data.columns)
    
    #duplicates
    duplicates = data.duplicated().sum()
    if duplicates > 0:
        print('There are no duplicated entries.')
    else:
        print(f'There are {duplicates} duplicates.')
        
    #missing
    data_missing = pd.DataFrame(round(data.isnull().sum()))
    if data_missing[0].sum() > 0:
        data_missing.plot(kind='bar')
        plt.grid()
        plt.title('Missing values');
    else:
        print(f'There are no missing values in "{data_name}".')

    #unique values
    if un == True:
        for i in data.columns:
            if data[i].dtype == 'object' or data[i].dtype == 'str':
                print(data[i].unique()
data_research(df, data_name='MOF data')

```

```

#Find negative value to zero
data_neg = pd.DataFrame(df.isin([-9999, 0]).sum())
if data_neg[0].sum() > 0:
    data_neg.plot(kind='bar')
    plt.grid()
    plt.title('Negative values');
else:
    print("No data")
    
```

```

#Feature Engineering for Density
df.insert(
    loc=3,
    column="density [g/cm^3]",
    value=(df["weight [u]"] / df["volume [A^3]"]) * 1.66054,
)

```

```

#Replace Void Fraction <= 0 by calculation
df.void_fraction = np.where(
        df.void_fraction <= 0, df['density [g/cm^3]']*df['void_volume [cm^3/g]'],df.void_fraction
 )
 
```

```

#Replace Void Volume <= 0 by calculation
df['void_volume [cm^3/g]'] = np.where(
        df['void_volume [cm^3/g]'] <= 0, df['void_fraction']/df['density [g/cm^3]'],df['void_volume [cm^3/g]']
)

```

```

#Drop NA
df.dropna(inplace=True)
#Find negative value to zero
data_neg = pd.DataFrame(df.isin([-9999, 0]).sum())
if data_neg[0].sum() > 0:
    data_neg.plot(kind='bar')
    plt.grid()
    plt.title('Negative to Zero values');
else:
    print("No data")

```

### Neural Network

```

pip install tensorflow
import math

```
```

#Loaded cleaned train dataset from dir.
df = pd.read_csv('C:/TMLCC/Dataset/df_train.csv')

```

```

#Added new feature in test df
df_test.insert(
    loc=3,
    column="density [g/cm^3]",
    value=(df_test["weight [u]"] / df_test["volume [A^3]"]) * 1.66054,
)

```

```

# separate features and target
df_x = df.iloc[:, 1:14]
df_y = df.iloc[:, -1]

df_test = df_test.iloc[:, 1:]

```

```

# one-hot encodeing
one_hot = pd.get_dummies(df_x[['functional_groups', 'topology']], drop_first=True)
one_hot_test = pd.get_dummies(df_test[['functional_groups', 'topology']], drop_first=True)
df_x = df_x.drop(['functional_groups', 'topology'],axis = 1)
df_x = df_x.join(one_hot)

```

```

# normalize features
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X = scaler.fit_transform(df_x)
y = df_y

X_testset = scaler.transform(df_x_test)

```

```

# split data
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.3, random_state = 123)


```

```

# import tensorflow
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense

model = Sequential()
model.add(Dense(395, input_dim=(X_train.shape[1]), activation='relu')) # input
model.add(Dense(500, activation='relu')) # hidden 1
model.add(Dense(500, activation='relu')) # hidden 2
model.add(Dense(500, activation='relu')) # hidden 3
model.add(Dense(500, activation='relu')) # hidden 4
model.add(Dense(500, activation='relu')) # hidden 5
model.add(Dense(500, activation='relu')) # hidden 6
model.add(Dense(500, activation='relu')) # hidden 7
model.add(Dense(500, activation='relu')) # hidden 8
model.add(Dense(500, activation='relu')) # hidden 9
model.add(Dense(500, activation='relu')) # hidden 10
model.add(Dense(500, activation='relu')) # hidden 11
model.add(Dense(500, activation='relu')) # hidden 12
model.add(Dense(1, activation='linear')) # output

```

```

model.compile(loss='mae', optimizer='adam', metrics=['accuracy'])
model.fit(X_train, y_train, epochs=5000, batch_size=10000)

```

```

#from sklearn.metrics import mean_absolute_error

log_mae = np.log(mean_absolute_error(y_pred, y_test))
log_mae

```

```

#Predict Submission Model
test_pred = model.predict(X_testset)
test_pred

```

### XGBoost Model

```

conda install -c conda-forge shap
pip install evalml
import evalml
evalml.problem_types.problem_types.ProblemTypes.all_problem_types
evalml.objectives.get_all_objective_names()

```

```

# Split data
X = df.drop(['MOFname', 'CO2_working_capacity [mL/g]'], axis=1)
y = df['CO2_working_capacity [mL/g]']

X_train, X_test, y_train, y_test = evalml.preprocessing.split_data(X, y, problem_type='regression', test_size=.3)

print("Size of training data : ", X_train.shape[0])
print("Size of test data : ", X_test.shape[0])

```

```

# Auto ML
from evalml.automl import AutoMLSearch

automl = AutoMLSearch(X_train=X_train, y_train=y_train, problem_type='regression', objective='mae')
automl.search()
automl.rankings
automl.describe_pipeline(automl.rankings.iloc[0]["id"])
best_pipeline = automl.best_pipeline
best_pipeline.graph()
best_pipeline.score(X_test, y_test, objectives=['mae', 'mse', 'root mean squared error'])

```

```

# Drop id and y
df_feat = df.drop(columns=['MOFname', 'CO2_working_capacity [mL/g]'], axis=1)
df_feat.info()

```

```

# One-Hot Encoding for Category Features
from sklearn.preprocessing import OneHotEncoder

encoder = OneHotEncoder(drop='if_binary', sparse=False)

X_ohe = encoder.fit_transform(df_feat[['functional_groups', 'topology']])
X_ohe.shape

```

```

# Save One-Hot Encoding
import joblib
joblib.dump(encoder, 'ohe_encoder_2.pkl')

```

```

# Concat X_num and X_ohe
X = np.append(X_num, X_ohe, axis=1)
X.shape

```

```

X_num = df_feat.iloc[:,:11].values
X_num.shape

```

```

# Normalize Features
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
X = scaler.fit_transform(X)
X.shape
# Save StandardScaler
joblib.dump(scaler, 'ss_scaler_2.pkl')

```

```

# Assign y
y = df['CO2_working_capacity [mL/g]'].values

```

```

# Split Data
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.3, random_state = 123)


```

```

# XGBoost
from xgboost import XGBRegressor

model = XGBRegressor(eta=0.1, max_depth=6, min_child_weight=1, n_estimators=100, n_jobs=-1)

model.fit(X_train, y_train)
model.score(X_train, y_train)

```

```

# Validation
from sklearn.metrics import mean_absolute_error

y_model = model.predict(X_train)
y_pred = model.predict(X_test)

log_mae_train = np.log(mean_absolute_error(y_model, y_train))
log_mae_test = np.log(mean_absolute_error(y_pred, y_test))

print('Log_MAE Train:', log_mae_train)
print('Log_MAE Test:', log_mae_test)

```

```

# Save model
joblib.dump(model, 'xgb_model.sav')

```

```

# Load Submission Test Data
df_test = pd.read_csv('test.csv')
df_test.info()

# Transform Submission Test Data
df_test.insert(
    loc=3,
    column="density [g/cm^3]",
    value=(df_test["weight [u]"] / df_test["volume [A^3]"]) * 1.66054,
)

# Drop columns 'MOFname' and reoder
df_x = df_test.drop('MOFname', axis=1)
df_x = df_x[['volume [A^3]', 'weight [u]', 'density [g/cm^3]',
       'surface_area [m^2/g]', 'void_fraction', 'void_volume [cm^3/g]',
       'metal_linker', 'organic_linker1', 'organic_linker2',
       'CO2/N2_selectivity', 'heat_adsorption_CO2_P0.15bar_T298K [kcal/mol]',
       'functional_groups', 'topology']]

# One-Hot Encoding
import joblib
encoder = joblib.load('ohe_encoder_2.pkl')
X_ohe = encoder.transform(df_x[['functional_groups', 'topology']])
X_ohe.shape
X_num = df_x.iloc[:,:11].values
X_num.shape

# Concat X_num and X_ohe
X = np.append(X_num, X_ohe, axis=1)
X.shape

# Normalize Features
scaler = joblib.load('ss_scaler_2.pkl')
X = scaler.transform(X)
X.shape
# Predict submission data
result = model.predict(X)
result

```

[<<Home](https://pakkawatk.github.io/portfolio)<br />
