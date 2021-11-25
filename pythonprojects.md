# My Python Data Science Projects.
[<<Home](https://pakkawatk.github.io/portfolio)<br />
This page briefly indicates my Data Analytics projects with Python.<br />
## 1. Customer Segmentation by Recency, Frequency, Monetary (RFM).
**Objective:** To segment the customers in order to analyze shopping behavior and making campaign for each segments by RFM method.<br />
**Dataset:** Transactions of Shopping Mall.<br /><br />
**Exploratory Data Analysis**<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_RFM1.PNG?raw=true)<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_RFM2.PNG?raw=true)<br /><br />
**Process**<br />
  - Convert InvoiceDate from object into datetime.<br />
  - Create TotalSum column.<br />
  - Create snapshot date ( Recency = snapshot_date (Maxdate of AllInvoiceDate + 1) - MaxDate of each Customer)<br />
  - Generate Recency, Frequency, Monetary and group by CustomerID.<br />
  - Discretize RFM by quantile.<br />
  - Calculate RFM score and define customer level.<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_RFM3.PNG?raw=true)<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_RFM4.PNG?raw=true)<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/py_RFM5.PNG?raw=true)<br /><br />
**Conclusion:** Finally, we got result for making Marketing Campaign for each segments.
