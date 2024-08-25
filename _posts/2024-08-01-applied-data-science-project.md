---
layout: post
author: PARTHIBAN SETHURAMAN
title: "Applied Data Science Project Documentation"
categories: ITD214
---
## Project Background

The dataset, obtained from Kaggle, related to conversion record of inquirers for enrolling course in X Education, an institution offering a diverse range of courses including financial management, e-commerce, business administration, healthcare, IT project managements, service excellence and other courses. 

The dataset encompasses a comprehensive overview of inquirers, including their demographics, online behavior, lead sources, asymmetrical information, and most crucially, their conversion status - whether they ultimately enrolled in a course.  

## Work Accomplished
Analyzed the behaviors of candidates landing on various online platforms, an institution that markets courses on multiple websites examines the factors influencing potential candidate conversion success.
Dependent / Target Variable: Converted (0/1): Indicates whether the lead was successfully converted (1) or not (0).
Tasks Breakdown
Determine the contribution of final independent variables to the likelihood of conversion.
Compare the coefficients of these variables to understand their relative impact.
Provide a summary of findings with recommendations for improvement in generation and conversion strategies.

### Data Preparation
Following are the steps involved in cleaning data as part of data preparation:

Determine and handle missing values for numeric columns and Imputation:

Many Categorical column has the value ‘select’ (as the candidate did not select any option) which needs to  be handled as its treated as a null value. - Specialization, How did you hear about X Education, Lead Profile, City
Numerical columns that has missing values:  total visits has been imputed using mode.
Page views per visit: Imputed using mode
Columns with more than 40% missing values are dropped. 

Analyse Categorical columns for missing values and skewness:

City” has 39.71 % missing values. Imputing missing values with Mumbai will make the data more skewed. Skewness will later cause bias in the model. Hence City column can be dropped.
“Specialization” has 36.58 % missing values. The specialization selected is evenly distributed. Hence imputation or dropping is not a good choice. We need to create additional category called 'Others'.
”Tags” has 36.29 % missing values. Tags are assigned to customers indicating the current status of the lead. Since this is current status, this column will not be useful for modeling. Hence it can be dropped.
“What matters most to you in choosing a course” This variable has 29.32 % missing values. 99.95% customers have selected 'better career prospects'. This is massively skewed and will not provide any insight.
“What is your current occupation”: We can impute the missing values with 'Unemployed' as it has the most values. This seems to be a important variable from business context, since X Education sells online courses and unemployed people might take this course to increase their chances of getting employed.
“Country”: X Education sells online courses and appx 96% of the customers are from India. Does not make business sense right now to impute missing values with India. Hence `Country column can be dropped.
“Last Activity”: "Email Opened" is having highest number of values and overall missing values in this column is just 1.11%, hence we will impute the missing values with label 'Email Opened'.
“Lead Source”: "Google" is having highest number of occurences and overall nulls in this column is just 0.39%, hence we will impute the missing values with label 'Google'

Removing unwanted columns or columns that does not contribute to the model:

Following columns has only 1 value and does not add any value to the model and these will be dropped.

'I agree to pay the amount through cheque',
'Get updates on DM Content',
'Update me on Supply Chain Content',
'Receive More Updates About Our Courses',
'Magazine'
'Prospect ID',
'Lead Number',
'Last Notable Activity'
Analyse Outliers:


Univariate Analysis:

Lead Origin: Around 52% of all leads originated from "Landing Page Submission" with a lead conversion rate (LCR) of 36%.The "API" identified approximately 39% of customers with a lead conversion rate (LCR) of 31%.
Current_occupation: Around 90% of the customers are Unemployed with lead conversion rate (LCR) of 34%. While Working Professional contribute only 7.6% of total customers with almost 92% lead conversion rate.

Creating dummy variables for categorical variables and dropping the first category is a common practice to avoid multicollinearity, especially when using linear models. This process involves converting each category of a categorical variable into a separate binary column (dummy variable) and then removing one of these columns to serve as a baseline.

### Modelling
Feature Selection is done using RFE (Recursive Feature Elimination). 
This is the estimator/model used by RFE to evaluate the importance of features. In this case, it's the LogisticRegression model.
No of features to select is 15 and the final list of features is as below after the RFE method.

The selected features from RFE method is fitted into Logistic regression and the model parameters are considered to drop certain variables which has high p-value
The following variables are dropped as they have a high p-value. After 3 models the final list of attributes with stable p value <0.05 and VIF


### Evaluation

Logistic Regression:

The evaluation matrics are pretty close to each other so it indicates that the model is performing consistently across different evaluation metrics in both test and train dataset.
The model achieved a sensitivity of 80.05% in the train set and 79.82% in the test set, using a cut-off value of 0.345.
Sensitivity in this case indicates how many leads the model identify correctly out of all potential leads which are converting.

Ensemble Method:

Weak Learners - Random forest, logistic regression, Gradient boosting classifier. Individual models are trained on the shortlisted features and finally a voting classifier is used with a soft voting which averages the probabilities of each class predicted by the models.

Benefits:
The ensemble model combines a Random Forest, Logistic Regression, and Gradient Boosting model using soft voting. Each model contributes to the final prediction based on its confidence in its predictions. This approach often results in a more accurate and robust model, leveraging the strengths of each base learner.

Comparison:

The ROC curve comparison shows that while each model has its strengths, the ensemble method outperforms both Logistic Regression and Random Forest individually. This highlights the power of ensemble methods in machine learning, where the combination of different models often leads to better generalization and more robust performance on unseen data. The higher AUC of the ensemble method indicates its superior ability to distinguish between the classes, making it the preferred choice for this particular classification task.

## Recommendation and Analysis

Enhance Website Engagement
Optimize Content: Ensure that website content is engaging, relevant, and valuable to encourage longer visits. Use interactive elements, videos, and high-quality information.
Improve User Experience: Simplify navigation, reduce page load times, and ensure that the website is mobile-friendly to increase time spent on the site.
Leverage Referrals
Referral Programs: Develop or enhance referral programs to incentivize existing customers to refer new leads. Offer rewards or discounts for successful referrals.
Build Partnerships: Collaborate with partners or influencers who can refer high-quality leads.
Optimize SMS Communication
Targeted SMS Campaigns: Use SMS for timely and personalized follow-ups. Ensure that messages are relevant and provide value to the recipient.
Automate SMS Notifications: Set up automated SMS notifications for key actions, such as abandoned carts or special offers.
Tailor Offers for Working Professionals
Customize Messaging: Create targeted marketing campaigns specifically for working professionals, highlighting features and benefits that cater to their needs.
Offer Flexible Solutions: Provide flexible payment plans or options that cater to the schedules and needs of working professionals.
Enhance Landing Pages
Optimize Forms: Simplify and optimize landing page forms to reduce friction and improve conversion rates. Use A/B testing to find the most effective form designs.
Personalize Content: Ensure that landing page content is relevant to the source of the lead and aligns with their interests or needs.

## AI Ethics

Followed some of the secure measures such as masking user personal informations.
In the dataset their are important data  like websites accessed by users which is followed secure data usage. 

## Source Codes and Datasets
