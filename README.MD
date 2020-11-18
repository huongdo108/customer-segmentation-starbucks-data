# Overview 


The objective of this repository is to study a Starbuck dataset about customer purchasing behavior during promotion period. This dataset is provided by Udacity. 

There are two main tasks in the study:

- Study how customers behave towards different types of offer and promotion in order to identify which offer type is the most effective in turning customers into buying as well as which offer type is problematic. As a result, marketing team can develop a more effective promotion strategy for future campaigns. (By further develop the most effective offer type for example)

- Segmentize customers based on their demographics, purchasing behaviour, and reaction towards different offer types for more future effective targeted marketing. For example, what type of offer should be sent to a specific customer who will best respond to it. 

# Data

**Dataset**

**portfolio.json** - offer ids and their meta data

- id (string): id of an offer
- offer_type (string): offer type (BOGO (Buy one get one), discount, informational)
- difficulty (int): minimum required spent to complete an offer
- reward (int): reward for completing an offer
- duration (int): length of days that the offer is valid
- channels (list of strings): type of channel that an offer is sent to a customer

**profile.json** - customer demographic info

- age (int): age
- became_member_on (int): year that customer create an account on the app
- gender (str):  gender
- id (str): customer id
- income (float): income

**transcript.json** - records of offers: received, viewed, and completed as well as records of transactions made by customers

- event (str): type of record
- person (str): customer id
- time (int): length of hours since start of test. The data begins at time t=0
- value (dict of strings): either an offer id or transaction amount depending on the record

# Notebook content

The notebook contains the following parts:

- Understand the datasets.
- Preprocess the 3 original datasets to create a master customers dataframe.
    - Impute missing data
    - Convert dates to Datetime
    - One hot encoding for categorical features
    - Examine and handle duplicate records in offers dataframe
    - Drop implausible records
    - Compute statistics related to offers features: conversion rates
    - Compute statistics related to transactions features: frequency, recency, monetary
    - Create master customers dataframe
- Data exploratory analysis for master customers dataframe
- Data preprocessing for master customers dataframe with standardization and PCA
- Models
    - Kmeans
        - Find number of clusters with Elbow, silhouette, calinski harabasz, and davies bouldin scores
        - Fit the model
        - Evaluate clusters on PCA visualization
    - DBSCAN
        - Search for parameters
        - Fit the model
        - Evaluate model
- Cluster evaluation 

# Analysis result

## Offer type effectiveness

<img src="https://github.com/huongdo108/customer-segmentation-starbucks-data/blob/master/images/offer_counts.PNG" align="centre">


The number of customers viewing offers is more than two third of the number of customers receiving offers. However, the number of customers completing offers is just less than half of the number of customers viewing offers because of BOGO and Information. 


<img src="https://github.com/huongdo108/customer-segmentation-starbucks-data/blob/master/images/conversion_rates.PNG" align="centre">

BOGO has the highest viewed_vs_received conversion rate among three types, but lower completed_vs_viewed and completed_vs_received conversion rates than Discount. High viewed_vs_received conversion rate indicates that customers seem to be more interested in BOGO idea than Discount and Information. However, low completed_vs_viewed conversion rate indicates that the content of BOGO offer is not that appealing to get customers into buying as after viewing the offer, many customers decide not to complete the offer.

<img src="https://github.com/huongdo108/customer-segmentation-starbucks-data/blob/master/images/cr_by_bogo_discount.PNG" align="centre">

The reason behind low BOGO conversion rate (even though with a very high view rate) is because of the difficulty/reward levels and duration. The least difficult and longest duration BOGO offer yields the highest completed_vs_viewed/completed_vs_received conversion rates. The most difficult and shortest duration BOGO offer yields the least completed_vs_viewed/completed_vs_received conversion rates.

It does not seem there is much difference in conversion rates among different types of DISCOUNT offer.

Overall, Discount drives higher conversion rates than BOGO.

Customers seems to be more interested in BOGO idea than DISCOUNT as they view more BOGO than DISCOUNT. However, the difficulty, reward, and duration level of BOGO drive customers away from completing offers. It is observed that the BOGO offer with low difficulty level and long duration has even higher completed_vs_viewed conversion rate than any type of DISCOUNT offer. Marketing team can design an easier BOGO offer for future campaigns.

## Customer segmentation

<img src="https://github.com/huongdo108/customer-segmentation-starbucks-data/blob/master/images/clusters.PNG" align="centre">

**Cluster 0** regular customers who make regular transactions without being incentivised by offers.

**Cluster 1** male, receive all three types of offer but do not response to any.

**Cluster 2** convert very well with Discount offer type. 

**Cluster 3** receive only BOGO and INFO offers, and convert quite well with BOGO offer type.