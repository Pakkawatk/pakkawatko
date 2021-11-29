[<<Home](https://pakkawatk.github.io/portfolio)<br />
## Market Basket Analysis and Association Rules.
**Objective:** To find frequent item sets of online retail for making sale promotions.<br />
**Dataset:** Transactions of online retail.<br />
**Exploratory Data Analysis:**<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_MBA1.PNG?raw=true)<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_MBA2.PNG?raw=true)<br />
**Process:**<br />
  - Drop NA records, filter only positive "Quantity" and "Customers" in "UK".<br />
  - Encode numerical into binary value.<br />
  - Filter the Transactions those buying more than 1 item.<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_MBA3.PNG?raw=true)<br />
  - Apply Apriori Algorithm which minimum support = 0.03 (3%).<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_MBA4.PNG?raw=true)<br />
  - Apply Association Rules with Lift >= 1.<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_MBA5.PNG?raw=true)<br /><br />
**Conclusion:** Finally, we got item sets for making sale promotions those are based on % confidence and lift > 1.00.<br />

### Code

```

# Import library 
import pandas as pd
import matplotlib.pyplot as plt

```

```

# Read dataset 
df = pd.read_excel('../SP_Programming/dataset/online_retail_II.xlsx')

```

```

# Making a function for examining data
def data_research(data, data_name='data', un=False):
    #basic
    print(f'Examining "{data_name}"')
    display(data.head(2))
    display(data.info())
    display(data.describe( include='all', datetime_is_numeric=True))
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
data_research(df, data_name='Online Retail')

```

```

#Drop Na
df = df.dropna() 
print (df.info())

```

```

#Fillter Quantity >=0
df_positive = df[df["Quantity"] >= 0] 
df_positive.info()

```

```
#Filter Country = UK, Fill NA by 0
basket_positive = (df_positive[df_positive["Country"] == "United Kingdom"]).groupby( 
["Invoice","Description"])["Quantity"].sum().unstack().reset_index().fillna(0).set_index("Invoice") 
basket_positive

```

```

#Encoding Quantity from numerical to binary.
def encode_units(x): 
 if x <= 0: 
     return 0 
 if x >= 1: 
     return 1 
 
basket_encoding_positive = basket_positive.applymap(encode_units) 
basket_encoding_positive

```

```

# Filter transaction >= 2 item.
basket_filter_positive = basket_encoding_positive[(basket_encoding_positive>0).sum(axis=1) >= 2] 
basket_filter_positive

```

```

# Install Apriori Algorithm
pip install mlxtend

```

```

# Apriori Algorithm
from mlxtend.frequent_patterns import apriori 
frequent_itemsets_positive = apriori(basket_filter_positive, min_support = 0.03,use_colnames=True).sort_values(
"support", ascending=False).reset_index(drop=True) 
frequent_itemsets_positive["length"]=frequent_itemsets_positive["itemsets"].apply(lambda x: len(x)) 
frequent_itemsets_positive

```

```

# Association Rules, Lift >= 1.
from mlxtend.frequent_patterns import association_rules 
association_rules(frequent_itemsets_positive, metric="lift", min_threshold=1).sort_values("lift", 
ascending=False).reset_index(drop=True)

```

[<<Home](https://pakkawatk.github.io/portfolio)<br />
