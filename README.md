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
The predictor of age within the dataset has a median of 38.9 years, with 50% of data points between 32 (Q1) and 44 years (Q3), however there may be many outliers for customer age within the dataset. 
<br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/fc28ebc1-825c-428e-801b-84df906ddba8)

Very Even distribution of a estimated salary count for customers, This could indicate wide target audience. 
<br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/d51f07c6-a48f-46ca-8b02-120ddfe26b0f)

Mean balance of $76,485, could be interpreted both positively or negatively. The Bank does on one hand have increased Liquidity for investing and lending and potential high customer retention. However, this could also mean higher interest expenses and idle funds. 
<br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/58e9f0d0-e23f-49bb-82de-ad0f9b261d7a)

When also considering that a higher number of customers are inactive then active, this could point towards the more negative implications of high average customer balance being true (though the figures are not too dissimilar). 
<br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/33300922-e845-496a-8035-11de3679368b)

The credit scores of customers displays a mean of 650.5. Given the capital within the current dataset is in USD, the credit scores will be interpreted using the United States FICO Scoring System.
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

Customer tenure appears normally distributed, with a mean of 5.01 years. 
<br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/ab416614-b46c-491e-875a-91229c4a2710)

The number of products utilised by customers sits on average at around 1 (with up to 4 products being on offer). 
<br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/d43b8e0c-3d06-4d6e-af19-e9d5ceed8bfe)

When coupled with the fact a significantly greater number of customers have a credit card with the bank than do not, this would suggest that that credit cards is the primary product of interest for customers. This is of use given the Bank being analysed wants particular focus towards customers who use credit cards. 
<br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/4477aa62-4c14-42ed-846e-4473210d1229)

When looking at the boxplots of certain metrics (age,  credit score and product number) there may be some need to outlier detection and removal.
Further, there is clearly a much higher number of customers within the dataset who have a credit card, and so indicates that it is a popular product with the current bank being analysed and could provide opportunity to upsell other products given that customers appear receptive to such products. Thus, this predictor may be an area which I focus on more heavily, despite the aforementioned negligible negative Pearson correlation score. 

Possible anomolous data was only observed for the age variable and porducts number of the customer. Anomolous data was determined as follows: 
<br></br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/9475936b-60cd-4060-8a02-bf7cab508b3f)

After further consideration, the anomolous data for both fields was included in all subsequent analysis techniques, given the outliers from the each filed were explained by a lower count of elderly customers or customers utilising the maximum number of products provided from the Bank.

### In summary when examining the correlation heatmap, it seems of benefit to isolate variables such as age, balance, and customer activity status concerning customer churn. This focused analysis aims to gain insight into any underlying trends or patterns that may exist within these specific predictors in relation to churn propensity. Whether the customer has a credit card should also be explored further to help solve the proposed problem statement (possibly in tandem with the higher correlators mentioned). 

## Refined Exploration - Age 
When taking a more focused approach to the predictor of age, there is a clear negative skew for the 'likelihood' of churn, as customers approach 'older age' (with a median age of 56 for the highest likelihood of customer churn). Further, the increase of customer churn appears to begin around the age of 39 and tapers off around 71 (although the later may be due to a lack of data points for these ages resulting in misleading insights).
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/c804a14d-72c1-4b5b-b7cd-d34de744e273)

## Refined Exploration - Balance 
After further analysis, there appears to be a higher number of customers who have been retained by the bank who would be deemed 'small depositors'/'debtor Customers' than those who have churned. The opposite can be observed for the 'large depositors', whereby more have churned than have been retained. This could be due to many factors, such as customer behaviour/needs as a result of their standings as a depositor, the banks customer retention strategies, the bank's perceived risk of customers given their financial standing or Economic factors related to current market conditions such as interest rates or overall economic uncertainty.
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/6eda79dd-c7f1-478a-8d8b-8a5880757d62)

## Refined Exploration - Active/Inactive Members
A higher chance of churn can be observed for active members of the bank. This in fact is common amongst different industries, given that the inactive members are sometime treated by businesses as 'idle' and so simply do not engage with their bank, obviously this is not always the case. Rather the banks active customers may have higher expectations and therefore if their expectations as a customer are not met, they may look elsewhere for investment/lending opportunities. Other factors may also be at play, such as service fatigue or simply the changing needs of the customer as their financial situation changes over time. It should be in the banks interest to adapt policy and targeted strategies to retain more active customers however, to increase opportunities to upsell products to said customer base. 
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/cbcd8f3d-9faf-4f7f-a57e-1e3c89c88b60)

### After 'drilling down' more deeply into key predictors (based off correlation coefficients). Greater insight into these proposed key predictors with respect to customer churn has been obtained. It has therefore been deemed appropriate to perform some final exploration into these predictors, with a focus on customer who do/do not own a credit card with the bank: 

### - Exploration of Age and Churn by Credit Card Status
### - Exploration of Balance and Churn by Credit Card Status
### - Exploration of Active Member Status and Churn by Credit Card Status
<br>

## Concluding Examinations of Churn Rate- Age and Credit Cards:
There can be an observed set of spikes in churn rate for non-holders for the ages of 47, 57 and 68. An irregular rise in churn was observed ages 65 and 70 for credit card holders. These changes given the sample size (2495 records) may be due to chance and so it would be of use to perform a significance test to determine as such. We will presume that these age groups display true higher churn and as a result these ages for non-credit and credit card holders should be targeted by the bank, to improve general customer retention and increase retained credit card customers. Further, Given that the churn of credit card holders occurs in their 'retirement period', there is opportunity for the bank to incorporate incentivised reward packages such as travel or health and wellness benefits to preserve more of said demographic. 

![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/441a6591-e6a1-4d8e-9c0c-f7f4d70dcd51)

# Predictive Modeling
Approach
Describe the modeling approach taken, including the types of models tested (e.g., linear regression, logistic regression, random forest), and preprocessing steps (e.g., scaling, feature engineering).

## Model Performance
Discuss the performance of each model tested, including accuracy metrics (e.g., accuracy, precision, recall, F1-score) and any challenges encountered.

## Refinement
Explain how the model was refined using techniques like GridSearchCV or hyperparameter tuning to optimize performance.

## Best Model
Detail the best-performing model selected based on evaluation metrics, such as test accuracy and other relevant metrics.

# Actionable Recommendations
Summarize the actionable recommendations derived from the predictive modeling results, emphasizing strategies to reduce customer churn based on the insights gained.

# Conclusion
Wrap up with a brief conclusion highlighting the main findings, the impact of the best model, and potential next steps for further improvement or application.

# Appendix
Include any additional details, code snippets, or visualizations that support your findings but weren't included in the main sections.


