[<<Home](https://pakkawatk.github.io/portfolio)<br />
## Customer Segmentation by Recency, Frequency, Monetary (RFM).
**Objective:** To segment the customers in order to analyze shopping behavior and making campaign for each segments by RFM method.<br />
**Dataset:** Transactions of e-commerce.<br />
**Exploratory Data Analysis:**<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_RFM1.PNG?raw=true)<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_RFM2.PNG?raw=true)<br />
**Process:**<br />
  - Convert InvoiceDate from object into datetime.<br />
  - Create TotalSum column.<br />
  - Create snapshot date ( Recency = snapshot_date (Maxdate of AllInvoiceDate + 1) - MaxDate of each Customer)<br />
  - Generate Recency, Frequency, Monetary and group by CustomerID.<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_RFM2_1.PNG?raw=true)<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_RFM3.PNG?raw=true)<br />
- Discretize RFM by quantile.<br />
- Calculate RFM score and define customer level.<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_RFM4.PNG?raw=true)<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_RFM5.PNG?raw=true)<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_RFM6.PNG?raw=true)<br /><br />
**Conclusion:** Finally, we got result for making marketing campaign for each segments.<br />
**Reference:** [https://towardsdatascience.com](https://towardsdatascience.com/recency-frequency-monetary-model-with-python-and-how-sephora-uses-it-to-optimize-their-google-d6a0707c5f17?gi=58e1b18d9f9c)<br />
**Reference:** [https://facebook.com/nerd](https://facebook.com/nerd)<br />

### Code

```

#Importing Requierd Libraries
pip install squarify
import pandas as pd
import matplotlib.pyplot as plt
from datetime import timedelta
import squarify
from IPython.display import display

```

```

# Read dataset
df = pd.read_csv('../SP_Programming/dataset/ecommerce_dataset.csv')

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
                print(data[i].unique())
data_research(df, data_name='ecommerce data')

```

```

# Convert InvoiceDate from object into datetime 
df['InvoiceDate'] = pd.to_datetime(df['InvoiceDate'])

```

```

# Create TotalSum column 
df['TotalSum'] = df['Quantity'] * df['UnitPrice'] 

```

```

# Create snapshot date ( Recency = snapshot_date (Maxdate of AllInvoiceDate + 1) - MaxDate of each Customer) 
snapshot_date = df['InvoiceDate'].max() + timedelta(days=1) 
print(snapshot_date)

```

```

# Group by CustomerID and generate RFM.
df_process = df.groupby(['CustomerID']).agg({ 
 'InvoiceDate': lambda x: (snapshot_date - x.max()).days, 
 'InvoiceNo': 'count', 
 'TotalSum': 'sum'})
 #Change Column name.
 df_process.rename(columns={'InvoiceDate': 'Recency', 'InvoiceNo': 'Frequency', 
 'TotalSum': 'MonetaryValue'}, inplace=True)
 
 ```
 
 ```
 
 # Print top 5 rows & shape 
print(df_process.head()) 
print('{:,} rows; {:,} columns' 

```

```
# Plot distribution.
plt.figure(figsize=(12,10)) 
plt.subplot(3, 1, 1); sns.distplot(df_process['Recency']) 
plt.subplot(3, 1, 2); sns.distplot(df_process['Frequency']) 
plt.subplot(3, 1, 3); sns.distplot(df_process['MonetaryValue']) 
plt.show()

```

```

# Create labels for R, F, M 
r_labels = range(4, 0, -1) 
f_labels = range(1, 5) 
m_labels = range(1, 5)

```

```

# Assign these labels to 4 equal percentile groups
r_groups = pd.qcut(df_process['Recency'], q=4, labels=r_labels) 
f_groups = pd.qcut(df_process['Frequency'], q=4, labels=f_labels) 
m_groups = pd.qcut(df_process['MonetaryValue'], q=4, labels=m_labels)

```

```

# Create new columns R, F, M 
df_process = df_process.assign(
 R = r_groups.values,
 F = f_groups.values,
 M = m_groups.values) 
df_process.head()

```

```

# Calculate RFM_Score 
df_process['RFM_Score'] = (df_process[['R','F','M']].sum(axis=1))
print(df_process['RFM_Score'].head())

```

```

# Define rfm_level
def rfm_level(df): 
 if df['RFM_Score'] >= 9: 
     return 'Can\'t Loose Them' 
 elif ((df['RFM_Score'] >= 8) and (df['RFM_Score'] < 9)): 
     return 'Champions' 
 elif ((df['RFM_Score'] >= 7) and (df['RFM_Score'] < 8)): 
     return 'Loyal' 
 elif ((df['RFM_Score'] >= 6) and (df['RFM_Score'] < 7)): 
     return 'Potential' 
 elif ((df['RFM_Score'] >= 5) and (df['RFM_Score'] < 6)): 
     return 'Promising' 
 elif ((df['RFM_Score'] >= 4) and (df['RFM_Score'] < 5)): 
     return 'Needs Attention' 
 else: 
     return 'Require Activation'

```

```

# Create a new variable RFM_Level 
df_process['RFM_Level'] = df_process.apply(rfm_level, axis=1)
rfm = df_process
# Print the top 5 rows
rfm.head()

```

```

# Calculate average values for each RFM_Level, and return a size of each segment
rfm_level_agg = rfm.groupby('RFM_Level').agg({ 
 'Recency': 'mean', 
 'Frequency': 'mean', 
 'MonetaryValue': ['mean', 'count'] 
}).round(1)
print(rfm_level_agg)

```

```

# Mosaic plot.
rfm_level_agg.columns = rfm_level_agg.columns.droplevel() 
rfm_level_agg.columns = ['RecencyMean','FrequencyMean','MonetaryMean',
 'Count']
fig = plt.gcf() 
ax = fig.add_subplot() 
fig.set_size_inches(16, 9) 
squarify.plot(sizes=rfm_level_agg['Count'],
 label=['Can\'t Loose Them', 
 'Champions', 
 'Loyal', 
 'Needs Attention', 
 'Potential',
 'Promising',
 'Require Activation'], alpha=.6 ) 
plt.title("RFM Segments",fontsize=18,fontweight="bold") 
plt.axis('off') 
plt.show()

```
[<<Home](https://pakkawatk.github.io/portfolio)<br />
