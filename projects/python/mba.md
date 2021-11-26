[<<Home](https://pakkawatk.github.io/portfolio)<br />
### Market Basket Analysis and Association Rules.
**Objective:** To find frequent item sets of online retail for making sale promotions.<br />
**Dataset:** Transactions of online retail.<br /><br />
**Exploratory Data Analysis:**<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_MBA1.PNG?raw=true)<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_MBA2.PNG?raw=true)<br /><br />
**Process:**<br />
  - Drop NA records, filter only positive "Quantity" and "Customers" in "UK".<br />
  - Encode numerical into binary value.<br />
  - Filter the Transactions those buying more than 1 item.<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_MBA3.PNG?raw=true)<br /><br />
  - Apply Apriori Algorithm which minimum support = 0.03 (3%).<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_MBA4.PNG?raw=true)<br /><br />
  - Apply Association Rules.<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_MBA5.PNG?raw=true)<br /><br />
**Conclusion:** Finally, we got item sets for making Sales Promotion based on % confidence and lift > 1.00.<br /><br />

### Code

```

```
