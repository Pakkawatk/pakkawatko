[<<Home](https://pakkawatk.github.io/portfolio)<br />
# Data Analytics Projects with Rapid Miner Studio.
This page briefly indicates data projects by Rapid Miner Studio while I'm studying at DPU.<br />
## 1. Association Rules.
**Objective:** To find Frequent Item Sets and Association Rules for making Maketing Promotions.<br />
**Dataset:** Basic example transactions of Super Market.<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_asso1.PNG?raw=true)<br /><br />
**Process:**<br />
  - Transform table by pivot product name and sum value.
  - Transform number to binomial. ( True and False )
  - Apply FP-Growth method, minimum support = 0.5.
  - Apply Association Rules, Minimum confidence = 0.8.
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_asso2.PNG?raw=true)<br /><br />
Result of FP-Growth method to find frequent item sets at minimum support = 0.5.<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_asso3.PNG?raw=true)<br /><br />
Result of Association Rules, to find Lift at minimum confidence = 0.8.<br /> 
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_asso4.PNG?raw=true)<br />
**Conclusion:** We can make promotions by above frequent item sets with confident pick up set = 100% and the pick up set (Lift) is 1.333 times of pick up one.<br /><br />

## 2. Segmentation.
**Objective:** To segment the customers by RFMB method and frequent shopping time of each customers for making Marketing Campaigns.<br />
**Dataset:** Transactions of Shopping Mall.<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_rfm1.PNG?raw=true)<br /><br />
**Process:**
  - Filter customers in UK and do feature engineering by creating and aggregating sum total prize attribute.
  - Extract Days and Hours from Transactions and discretize into Day of Week and Period of Times.
  - Do RFM segmentation by generating Recency, Frequency, Monetary and Basket Size.
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_rfm2.PNG?raw=true)<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_rfm2_1.PNG?raw=true)<br /><br />
**RFMB for each customers.**<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_rfm3.PNG?raw=true)<br /><br />
**Shopping period of each customers.**<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_rfm4.PNG?raw=true)<br /><br />
**Conclusion:** We got RFMB table and shopping period for analyzing Marketing Campaign and Clustering.<br />

## 3. Clustering.
**Objective:** To define cluster of customers which grouping by RFMB in order to making Marketing Campaign for individual clusters.<br />
**Dataset:** RFMB segmentation.<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_clus1.PNG?raw=true)<br /><br />
**Process:**
- Normalize the imbalance data into range 0 - 1.
- Clustering by k-Means = 5.
- After getting clusters, de-normalize into actual values.
- Average values of Recency, Frequency, Monetary and Basket size group by cluster.
- Discretize data into range 1-5 and set RFMB score (( R+F+M+B)/4).
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_clus2.PNG?raw=true)<br /><br />
**RFMB cluster and score.**<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_clus4.PNG?raw=true)<br /><br />
- **Conclusion:** Marketing Team can name the clusters and design individual campaigns for each cluster by RFMB score table.<br />

## 4. Machine Learning.
**Objective:** To define sentimental from words.<br />
**Dataset:** Table of 300 words in columns with labels.<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_ML1.PNG?raw=true)<br /><br />
**Process:**
- Transform numerical to binomial ( True, False )
- Class of positive and negative are imbalance. So, we use under sampling method to balance the class.
- Apply feature selection FCBF method for reducing features from 300 to 30.
- Apply Naive Bayes method with 10 Fold Cross Validation.
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_ML2.PNG?raw=true)<br /><br />
**Confusion Matrix.**<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/rap_ML3.PNG?raw=true)<br /><br />
[<<Home](https://pakkawatk.github.io/portfolio)<br />
