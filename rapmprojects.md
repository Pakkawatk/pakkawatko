# Data Analytics Projects with Rapid Miner Studio.
This page is about demonstrations of Data Mining by Rapid Miner Studio.<br />
## 1. Association Rules
**Objective:** To find Frequent Item Sets and Association Rules<br />
**Dataset:** Basic example transactions of Super Market.<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_asso1.PNG?raw=true)<br /><br />
**Process:**
- Transform table by pivot product name and sum value.<br />
- Transform value number to Binomial ( True and False )<br />
- FP-Growth, minimum support = 0.5<br />
- Association Rules, Minimum confidence = 0.8<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_asso2.PNG?raw=true)<br /><br />
Using FP-Growth method to find frequent item sets at minimum support = 0.5<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_asso3.PNG?raw=true)<br /><br />
**Association Rules:** Minimum confidence = 0.8<br /> 
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_asso4.PNG?raw=true)<br />
**Result:** We can make promotions by above frequent item sets with confident pick up set = 100% and the pick up set (Lift) is 1.333 times of pick up one. <br />

### 2. Segmentation

**Objective:** To Segment the customers by RFM method and frequent shopping time of each customers<br />
**Dataset:** Transactions of Shopping Mall.<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_rfm1.PNG?raw=true)<br /><br />
**Process:**
- Do feature engineering, sum total prize<br />
- Extract Days and Hours from Transactions and discretize by Day of Week and Period of times.<br />
- Do RFM segmentation by generating Recency, Frequency, Monetary and Basket Size.<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_rfm2.PNG?raw=true)<br /><br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_rfm2_1.PNG?raw=true)<br /><br />
RFM for each customers.<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_rfm3.PNG?raw=true)<br /><br />
Access period of times for each customer.<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_rfm4.PNG?raw=true)<br />
**Result:** We got RFM table for analyzing marketing campains in appropriate shopping times for individual customers .<br />

### 3. Clustering

Imbalance data
Feature Selectin
Evaluation models
