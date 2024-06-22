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
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/5fdfa64d-ac2b-47ca-9497-ee3880e49bdc)

Very Even distribution of a estimated salary count for customers, This could indicate wide target audience. 
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/d51f07c6-a48f-46ca-8b02-120ddfe26b0f)

Mean balance of $76,485, could be interpreted both positively or negatively. The Bank does on one hand have increased Liquidity for investing and lending and potential high customer retention. However, this could also mean higher interest expenses and idle funds. 
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/58e9f0d0-e23f-49bb-82de-ad0f9b261d7a)

When also considering that a higher number of customers are inactive then active, this could point towards the more negative implications of high average customer balance being true (though the figures are not too dissimilar). 
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/33300922-e845-496a-8035-11de3679368b)

The credit scores of customers displays a mean of 650.5. Given the capital within the current dataset is in USD, the credit scores will be interpreted using the United States FICO Scoring System.
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
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/aba91140-b2b6-4c1a-99e8-9355f874e6b7)

The number of products utilised by customers sits on average at around 1 (with up to 4 products being on offer). 
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/d43b8e0c-3d06-4d6e-af19-e9d5ceed8bfe)

When coupled with the fact a significantly greater number of customers have a credit card with the bank than do not, this would suggest that that credit cards is the primary product of interest for customers. This is of use given the Bank being analysed wants particular focus towards customers who use credit cards. 

![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/4477aa62-4c14-42ed-846e-4473210d1229)

When looking at the boxplots of certain metrics (age,  credit score and product number) there may be some need to outlier detection and removal.
Further, there is clearly a much higher number of customers within the dataset who have a credit card, and so indicates that it is a popular product with the current bank being analysed and could provide opportunity to upsell other products given that customers appear receptive to such products. Thus, this predictor may be an area which I focus on more heavily, despite the aforementioned negligible negative Pearson correlation score. 

Possible anomolous data was only observed for the age variable and porducts number of the customer. Anomolous data was determined as follows: 
<br></br>
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/9475936b-60cd-4060-8a02-bf7cab508b3f)

After further consideration, the anomolous data for both fields was included in all subsequent analysis techniques, given the outliers from the each filed were explained by a lower count of elderly customers or customers utilising the maximum number of products provided from the Bank.

### In summary when examining the correlation heatmap, it seems of benefit to isolate variables such as age, balance, and customer activity status concerning customer churn. This focused analysis aims to gain insight into any underlying trends or patterns that may exist within these specific predictors in relation to churn propensity. Whether the customer has a credit card should also be explored further to help solve the proposed problem statement (possibly in tandem with the higher correlators mentioned). 

# Refined Exploration - Age 
When taking a more focused approach to the predictor of age, there is a clear negative skew for the 'likelihood' of churn, as customers approach 'older age' (with a median age of 56 for the highest likelihood of customer churn). Further, the increase of customer churn appears to begin around the age of 39 and tapers off around 71 (although the later may be due to a lack of data points for these ages resulting in misleading insights).
![image](https://github.com/LiamBatiste/Bank-Customer-Churn/assets/68031898/c804a14d-72c1-4b5b-b7cd-d34de744e273)


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


