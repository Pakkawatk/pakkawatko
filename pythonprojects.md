[<<Home](https://pakkawatk.github.io/portfolio)<br />
# My Python Data Science Projects.
This page briefly indicates my Data Analytics projects with Python.<br />
### 1. Customer Segmentation by Recency, Frequency, Monetary (RFM).
[View Code>>](https://pakkawatk.github.io/portfolio)<br /><br />
**Objective:** To segment the customers in order to analyze shopping behavior and making campaign for each segments by RFM method.<br />
**Dataset:** Transactions of e-commerce.<br /><br />
**Exploratory Data Analysis**<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_RFM1.PNG?raw=true)<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_RFM2.PNG?raw=true)<br /><br />
**Process**<br />
  - Convert InvoiceDate from object into datetime.<br />
  - Create TotalSum column.<br />
  - Create snapshot date ( Recency = snapshot_date (Maxdate of AllInvoiceDate + 1) - MaxDate of each Customer)<br />
  - Generate Recency, Frequency, Monetary and group by CustomerID.<br />
  - Discretize RFM by quantile.<br />
  - Calculate RFM score and define customer level.<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_RFM3.PNG?raw=true)<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_RFM4.PNG?raw=true)<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_RFM5.PNG?raw=true)<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_RFM6.PNG?raw=true)<br /><br />
**Conclusion:** Finally, we got result for making Marketing Campaign for each segments.<br />

### 2. Market Basket Analysis and Association Rules.
[View Code>>](https://pakkawatk.github.io/portfolio)<br /><br />
**Objective:** To find frequent item sets of online retail for making Sale Promotions.<br />
**Dataset:** Transactions of online retail.<br /><br />
**Exploratory Data Analysis**<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_MBA1.PNG?raw=true)<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_MBA2.PNG?raw=true)<br /><br />
**Process**<br />
  - Drop NA records, Filter only positive Quantity and Customers in "UK".<br />
  - Encode numerical into binary value.<br />
  - Filter the Transactions those buying more than 1 item.<br />
  - Apply Apriori Algorithm which minimum support = 0.03 (3%).<br />
  - Apply Association Rules.<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_MBA3.PNG?raw=true)<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_MBA4.PNG?raw=true)<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_MBA5.PNG?raw=true)<br /><br />
**Conclusion:** Finally, we got result for making Sales Promotion based on % Confidence and Lift > 1.00.<br />
