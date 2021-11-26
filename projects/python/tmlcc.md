[<<Home](https://pakkawatk.github.io/portfolio)<br />
### Thailand Machine Learning Competition for Chemistry.
36th rank from 76 competitors as "Team Koalas" in Thailand Machine Learning for Chemistry Competition.<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/tmlcc.PNG?raw=true)<br />
**Objective:** To predict "CO2 Working Capacity" of "MOF" by Machine Learning with the lowest log of MAE score.<br />
**Dataset:** Features and label of MOF.<br /><br />
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
**Conclusion:** Finally, we got item sets for making sale promotions those are based on % confidence and lift > 1.00.<br /><br />

### Code

```

```
[<<Home](https://pakkawatk.github.io/portfolio)<br />
