# Project Summary
## Introduction
A Bank has outsourced an already cleansed dataset, in hope that actionable insights can be gained to reduce customer churn within their company, particularly among credit card holders. By analysing the uncovered most influential factors of custoemr churn through Data
Exploration and Predictive Modelling these insights can be leveraged to lower rates of customer churn for the Bank.

The dataset provided for this Analysis has been taken from Kaggle - https://www.kaggle.com/datasets/gauravtopre/bank-customer-churn-dataset. This dataset cotains the following fields: 

- customer_id, unused variable.
- credit_score, used as input.
- country, used as input.
- gender, used as input.
- age, used as input.
- tenure, used as input.
- balance, used as input.
- products_number, used as input.
- credit_card, used as input.
- active_member, used as input.
- estimated_salary, used as input.
- churn, used as the target. 1 if the client has left the bank during some period or 0 if he/she has not.

# Data Exploration
Overview
Provide an overview of the dataset, including its size, features, and target variable (churn).
The dataset contained 1000 entries, each with no null data for the 12 fields. Datatypes were correctly assigned for all fields. 

The features of the dataset were ranked corrleation-wise using Pearson Correlation Coefficients. All fields were compared with another using a Correlation Matrix: 
<br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/56bf57d7-72ec-4e3b-bacd-c605c663f357)

Descriptive statistics for each field were obtained along with data distribution to gain a better understanding of the data and decide if anomoly detection and removal was required. A greater focus for analysis was given to the fields which showed a higher correlation with the target variable of churn, which were as follows: 

- age (ρ = 0.29) - as age increases, so does the rate of churn
- active member (-0.16) - higher churn rate amongst active customers
- balance (ρ = 0.12) - as balance increases, so does the rate of churn

# Preliminary Explorative Insights
**Age** - The predictor of age within the dataset has a median of 38.9 years, with 50% of data points between 32 (Q1) and 44 years (Q3), however there may be many outliers for customer age within the dataset. 
<br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/fc28ebc1-825c-428e-801b-84df906ddba8)

**Salary** - Very Even distribution of a estimated salary count for customers, This could indicate wide target audience. 
<br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/d51f07c6-a48f-46ca-8b02-120ddfe26b0f)

**Balance** - Mean balance of $76,485, could be interpreted both positively or negatively. The Bank does on one hand have increased Liquidity for investing and lending and potential high customer retention. However, this could also mean higher interest expenses and idle funds. 
<br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/58e9f0d0-e23f-49bb-82de-ad0f9b261d7a)

**Customer Activity** - When also considering that a higher number of customers are inactive then active, this could point towards the more negative implications of high average customer balance being true (though the figures are not too dissimilar). 
<br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/33300922-e845-496a-8035-11de3679368b)

**Credit Score** - The credit scores of customers displays a mean of 650.5. Given the capital within the current dataset is in USD, the credit scores will be interpreted using the United States FICO Scoring System.
<br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/9eb5e982-f380-45ff-8c72-880fde8c024b)

FICO Bracket Interpretations (ranges from 300 to 850):
***
###### Excellent: 800 to 850
***
###### Very Good: 740 to 799
***
###### Good: 670 to 739
***
###### Fair: 580 to 669
***
###### Poor: 300 to 579
***

Thus the majority of customers within the dataset are of 'fair' credit scores. Conversely, There is also some clear outliers within the dataset that fall into the 'Poor' bracket. This could be an indication of a business imitative proposed by the bank such as subprime lending or a credit repair programme. When observing a Histogram distribution, negative skew can be seen, which is less indicative of the former mentioned initiatives.

**Tenure** - Customer tenure appears normally distributed, with a mean of 5.01 years. 
<br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/ab416614-b46c-491e-875a-91229c4a2710)

**Products Number** - The number of products utilised by customers sits on average at around 1 (with up to 4 products being on offer). 
<br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/d43b8e0c-3d06-4d6e-af19-e9d5ceed8bfe)

**Credt card** - When coupled with the fact a significantly greater number of customers have a credit card with the bank than do not, this would suggest that that credit cards is the primary product of interest for customers. This is of use given the Bank being analysed wants particular focus towards customers who use credit cards. 
<br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/4477aa62-4c14-42ed-846e-4473210d1229)

After looking at the boxplots of certain metrics (age,  credit score and product number) there may be some need to outlier detection and removal.
Further, there is clearly a much higher number of customers within the dataset who have a credit card, and so indicates that it is a popular product with the current bank being analysed and could provide opportunity to upsell other products given that customers appear receptive to such products. Thus, this predictor may be an area which I focus on more heavily, despite the aforementioned negligible negative Pearson correlation score. 

Possible anomolous data was only observed for the age variable and porducts number of the customer. Anomolous data was determined as follows: 
<br></br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/9475936b-60cd-4060-8a02-bf7cab508b3f)

After further consideration, the anomolous data for both fields was included in all subsequent analysis techniques, given the outliers from the each filed were explained by a lower count of elderly customers or customers utilising the maximum number of products provided from the Bank.

In summary when examining the correlation heatmap, it seems of benefit to isolate variables such as age, balance, and customer activity status concerning customer churn. This focused analysis aims to gain insight into any underlying trends or patterns that may exist within these specific predictors in relation to churn propensity. Whether the customer has a credit card should also be explored further to help solve the proposed problem statement (possibly in tandem with the higher correlators mentioned). 

## Refined Exploration - Age 

When taking a more focused approach to the predictor of age, there is a clear negative skew for the 'likelihood' of churn, as customers approach 'older age' (with a median age of 56 for the highest likelihood of customer churn). Further, the increase of customer churn appears to begin around the age of 39 and tapers off around 71 (although the later may be due to a lack of data points for these ages resulting in misleading insights).
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/c804a14d-72c1-4b5b-b7cd-d34de744e273)

## Refined Exploration - Balance 

After further analysis, there appears to be a higher number of customers who have been retained by the bank who would be deemed 'small depositors'/'debtor Customers' than those who have churned. The opposite can be observed for the 'large depositors', whereby more have churned than have been retained. This could be due to many factors, such as customer behaviour/needs as a result of their standings as a depositor, the banks customer retention strategies, the bank's perceived risk of customers given their financial standing or Economic factors related to current market conditions such as interest rates or overall economic uncertainty.
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/6eda79dd-c7f1-478a-8d8b-8a5880757d62)

## Refined Exploration - Active/Inactive Members

A higher chance of churn can be observed for active members of the bank. This in fact is common amongst different industries, given that the inactive members are sometime treated by businesses as 'idle' and so simply do not engage with their bank, obviously this is not always the case. Rather the banks active customers may have higher expectations and therefore if their expectations as a customer are not met, they may look elsewhere for investment/lending opportunities. Other factors may also be at play, such as service fatigue or simply the changing needs of the customer as their financial situation changes over time. It should be in the banks interest to adapt policy and targeted strategies to retain more active customers however, to increase opportunities to upsell products to said customer base. 
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/cbcd8f3d-9faf-4f7f-a57e-1e3c89c88b60)

After 'drilling down' more deeply into key predictors (based off correlation coefficients). Greater insight into these proposed key predictors with respect to customer churn has been obtained. It has therefore been deemed appropriate to perform some final exploration into these predictors, with a focus on customer who do/do not own a credit card with the bank: 

### - Exploration of Age and Churn by Credit Card Status
### - Exploration of Balance and Churn by Credit Card Status
### - Exploration of Active Member Status and Churn by Credit Card Status
<br>

## Concluding Examinations of Churn Rate- Age and Credit Cards:
There can be an observed set of spikes in churn rate for non-holders for the ages of 47, 57 and 68. An irregular rise in churn was observed ages 65 and 70 for credit card holders. These changes given the sample size (2495 records) may be due to chance and so it would be of use to perform a significance test to determine as such. We will presume that these age groups display true higher churn and as a result these ages for non-credit and credit card holders should be targeted by the bank, to improve general customer retention and increase retained credit card customers. Further, Given that the churn of credit card holders occurs in their 'retirement period', there is opportunity for the bank to incorporate incentivised reward packages such as travel or health and wellness benefits to preserve more of said demographic. 

![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/441a6591-e6a1-4d8e-9c0c-f7f4d70dcd51)

## Concluding Examinations of Churn Rate - Balance and Credit Cards:

<br>

##### From observation, the customer density order for 'small depositors' appears as follows:
***
1.) Retained and Credit Card holders
***
2.) Retained and not Credit Card holders
*** 
3.) Churned and Credit Card holders
*** 
4.) Churned and not Credit Card Holders 

<br>

##### From observation, the customer density order for 'large depositors' appears as follows:
***
1.) Churned and Credit Card holders
***
2.) Churned and not Credit Card holders
*** 
3.) Retained and not Credit Card holders
*** 
4.) Retained and Credit Card holders 

It appears that there is a higher density of retained small depositor customers, both with and without credit cards. Conversely, a higher density of large deposit customers, both with and without credit cards, are churning rather than being retained by the bank. This could be due to a greater focus by the bank on smaller depositors. The retention of small deposit customers suggests that the availability of credit cards has been an effective retention tool. On the other hand, the high churn of large depositors may not be a significant concern, as these customers are likely less reliant on credit cards as a source of capital, which could explain the higher density of churn among this customer segment. Overall, further analysis through predictive modelling using Multivariate Regression Analysis will help gain more insights for identifying customers at risk of churning.

## Concluding Examinations of Churn Rate - Balance and Credit Cards:
There appears to be a slightly higher churn rate for credit card customers who are active with the bank. When looking at inactive customers,  there is a large difference between the higher churn rate for customers who do not have a credit card compared to those who do. Overall it seems that the credit card may hold some influence on customer retention for inactive members. It would be of use to the bank to obtain greater customer segmentation insight so that expectations can be met for active members with a credit card to improve retention rates. This might be achieved through more personalised customers offerings, to increased percieved customer choice/bespoke features associated with the credit card. Lastly, it would be of use to the bank to perform further segmentation analysis to validate these findings. 

![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/6b7fd1c3-e237-4fe5-9491-4ce62da5bbc0)

### Next Steps:

### To gain further understanding of customer churn amongst credit card holders, analysis through predictive modelling using Multivariate Regression Analysis will be undertaken and if the model does not capture the complexity of the dataset, other models will be considered. This may help in understanding the underlying drivers of churn behavior specific to credit card holders and provide a more rigorous method of analysis than data exploration alone.

# Predictive Modeling
## Introduction

It is important that the training variables used within the model as those which likely have impact on customer churn, such as; age, gender, member activity, balance and credit card (given the problem statement). Additionally, it is important to avoid multicollinearity issues due to predictors used within the model correlating highly with other predictors. Hence the exclusion of product number from this analysis, given it's medium negative correlation score with products number (-0.30).

The objective of this Model is to use the following variables as part of <b>Multivariate Regression Analysis</b> to predict churn: 
#### - Gender
#### - Age
#### - Member Activity
#### - Balance
#### - Credit Card

The primary model of choice was Multivariate Linear Regression, given it's ability to facilitate the analysis that the impact of several predictors has on the target variable simultaneously. This might therefore be useful for predicting the likelihood/rate of a customer churning. Additionally it could potentially be used to quantify the contribution each predictor variable has towards customer churn with the Bank.

## Model Performance
### Multivariate Linear Regression model (MLR) 
Following Model fitting and training an r-Squared scored of 0.13 (2 d.p.) was obtained, meaning the model was performing very poorly. This was deemed to be due to output of the target variable needing to be either 1 (churned) or 1 (retained) and so categorical in nature. However, MLR is not suitable for predicting categorical outputs, but instead suited for continous target variables. 

To try and combat this, it was decided that a threshold of 0.5 would be used for binary classification (i.e. a predicted value of >=0.5 would evaluate to 0 or retained for said customer and a predicted value of >0.5 would evaluate to 1 or churned). With the threshold applied, a confusion matrix and aaccuracy scores were instead used to gain a deeper understanding of the; true negatives (TN), false positives (FP), false negatives (FN) and true positives (TP) which were as such: 

#### TN: 2333 cases were correctly predicted as not churned
#### FP: 46 cases were incorrectly predicted as churned (Type I error)
#### FN: 566 cases were incorrectly predicted as not churned (Type II error)
#### TP: 55 cases were correctly predicted as churned
<br></br>
Precision: Precision measures how many of the predicted positive cases (churned) are actually positive were calcuated.
#### Precision = TP / (TP + FP) = 55 / (55 + 46) ≈ 0.544
Meaning about 54.4% of the customers predicted as churned actually churned through model predictions.
<br></br>

Recall (Sensitivity): Recall measures how many of the actual positive cases (churned) were predicted correctly.
#### Recall = TP / (TP + FN) = 55 / (55 + 566) ≈ 0.088
So the model identified only about 8.8% of all churned customers.
<br></br>

Clearly this model was not effective at predicting churn, so a better model for predicting categorical target variables such as churn might be to use a Logistic Regression Model. This will allow me to pass predictor variables into the model so that a definitive 0 (no churn) or 1 (churn) can be outputted for each given customer - this avoids the need for a threshold. 
***
### Logistic Regression Model (LR) 
Therefore with respect to the MLR model, it was decided that a new approach through the Logistic Regression Model. This was justified by it's ability to be applied to binary target variables such as churn. In order for this to be possible however, all predictors were one-hot encoded through dummy variable fields of any categorical predictors. Secondly, standard scalers were applied to all predictors to ensure that LR model would not be negatively impacted by different predictor's scale having a greater influence on the model (namely customer balance). The following model performance was recorded: 

#### Accuracy Score: 0.80 (2 d.p.)
Meaning the model predicted customer churn correctly approximately 80% of test data. 

#### TN: 2304 cases were correctly predicted as not churned
#### FP: 75 cases were incorrectly predicted as churned (Type I error)
#### FN: 514 cases were incorrectly predicted as not churned (Type II error)
#### TP: 107 cases were correctly predicted as churned

#### Precision ≈ 0.587
Meaning about 58.7% of the customers predicted as churned actually churned through model predictions.
<br></br>

#### Recall = 0.172
So the model identified only about 17.2% of all churned customers, so still poor.
<br></br>

Clearly, the LR model still was not effectively identifying specifically customers who have churned. This is concerning and needed to be further refined to minimise this recall error as it was essential for the Bank. Further, class weight was balanced to avoid the minority class of churning being underpredicted by the model to try and improve the evident high number of customers predicted to have not churn, when the opposite was true. After this adjustment to the LR model, the following performance measures were observed: 

#### Accuracy Score: 0.70 (2 d.p.)
Meaning the model predicted customer churn correctly approximately 70% of test data. 

#### TN: 1660 cases were correctly predicted as not churned
#### FP: 719 cases were incorrectly predicted as churned (Type I error)
#### FN: 175 cases were incorrectly predicted as not churned (Type II error)
#### TP: 446 cases were correctly predicted as churned

#### Precision ≈ 0.383
Meaning about 38.3% of the customers predicted as churned actually churned through model predictions.
<br></br>

#### Recall = 0.718
So the model identified only about 71.8% of all churned customers, so still poor.
<br></br>
Thus the Model improved significantly with respect to recall, at the sacrafice of precision (to be expected). So the last adjustment tried was further refinement of the LR model through fitting using more features from the dataset which led to little improvement of LR model performance. Therefore alternative predictive models were considered.
***
### Random Forest Model (RF) 
When fitting the dataset to the RF model when comparing training (0.999) and test (0.854) scores a large difference of 14.5% was observed, this would suggest possible overfitting towards the training dataset's noise and outliers and so may not generalise well to unseen datasets. To combat this, hyperparameters were systematically searched over to find the best combination for your RF model (see below).

![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/648b2b7b-021b-4687-ac40-843f80d2afdc)

This would further optimise the model with respect to test accuracy, which outperformed all previously mention models, with a test accuracy of **0.860, meaning the model predicted churn correctly for 86% of the test data**. There appears to be Potential for this Model to be used in production by Bank and provide real-time data through a data pipeline, to further refine model over time for improved prediction of Customer churn. This could be used for reporting to observe shifts in the predictors that predominantly contribute customer churn rate. Ultimately the Bank could adjust their strategies and interventions to combat customer churn and provide value through increased customer retention.

Feature importance was lastly analysed using the best performing RF model to gain understanding into what features of the dataset are most influential with respect to churn and were as follows: 
<br>

![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/7b1203b3-3aea-4592-b8e1-3705b122f075)


# Actionable Recommendations 
1. Focus on High-Impact Customer Segments:
Based on the model's feature importance analysis, age, products number, balance, and credit score are the most influential factors contributing to customer churn. The bank should prioritize retaining older customers who hold credit cards, especially during their retirement years when churn rates tend to increase. Implementing targeted incentivized reward packages such as travel or health and wellness benefits could effectively retain this demographic.It should be noted that some of the statistical important can be explained by accounts being closed due to the customer becoming deceased. Despite this it should still be prioritised as an area of focus fo the Bank.

2. Leverage Product Offerings for Upselling:
The Random Forest model highlights products as a significant driver of customer responsiveness. To capitalise on this finding, the bank should actively promote its product offerings to increase upselling opportunities and enhance customer retention. Tailoring these products through further segmentation and demographic analysis can amplify their appeal and impact on the bank's customer base.

3. Implement Data-Driven Customer Retention Strategies:
Utilise the insights gained from the model to develop data-driven customer retention strategies. This includes leveraging predictive analytics to proactively identify at-risk customers and personalize retention initiatives. By deploying targeted campaigns and personalized offers based on customer behaviors and preferences, the bank can mitigate churn effectively.

4. Monitor and Adapt Strategies Over Time:
Continuously monitor the effectiveness of implemented strategies using real-time data through a robust data pipeline. This allows the bank to refine its approaches dynamically and respond promptly to shifts in customer behaviors or market conditions. Regularly updating the predictive models with new data ensures ongoing accuracy and relevance in customer churn prediction.

# Appendix 
### **Sample of dataset Used:**

![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/b388d08c-ce77-4485-a3e0-c3ee9c0bb3c8)
Source - https://www.kaggle.com/datasets/gauravtopre/bank-customer-churn-dataset/data
---

**Dataset shape:**
<br></br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/140aa6b8-79b0-4af9-8310-744f24fdd4d1)
---

**Multivariate Linear Regression r2 output:**
<br></br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/44c6ac81-e5e9-479d-b542-23e78bc3939c)
---

**Multivariate Linear Regression accuracy score and confusion matrix:**
<br></br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/140aa6b8-79b0-4af9-8310-744f24fdd4d1)
---

