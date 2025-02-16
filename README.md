Start-Up Funding Analysis (1995-2015)
Introduction
This project provides a descriptive and predictive analysis of start-up funding from 1995 to 2015. The goal is to analyze how start-ups have evolved, identify trends, and determine which markets have been the most dominant. The project involves both descriptive analysis and predictive modeling to forecast future trends in start-up funding.

Table of Contents
Imports
Data Description
Data Pre-processing
Data Exploration
Predictive Model
Summary
Bibliography
Data Description
The dataset used in this project includes several key attributes such as:

permalink: Unique identifier for each organization.
name: The name of the organization.
homepage_url: URL of the organization's website.
category_list: List of categories the organization belongs to.
market: Market in which the organization operates.
funding_total_usd: Total funding amount received (in USD).
status: Current status of the organization (e.g., acquired).
country_code: Country code of the organization's headquarters.
state_code: State code of the organization's headquarters (US only).
region: Region within the country of the headquarters.
city: City of the organization's headquarters.
funding_rounds: Number of funding rounds the organization has participated in.
founded_at: Date the organization was founded.
first_funding_at: Date the organization received its first funding.
last_funding_at: Date the organization received its last funding.
Data Pre-processing
For the descriptive analysis, we pre-processed the dataset to handle missing values, categorical data, and various other issues. As we move into predictive modeling, further pre-processing steps are taken:

Date Conversion: Since machine learning algorithms do not support date/time variables directly, all date fields (e.g., founded_at, first_funding_at, last_funding_at) are converted to integers representing the number of years. This simplification removes the day and month details, which are not relevant for the predictive model.

Feature Engineering: The category_list column is split so each category receives its own row. This transformation enables the model to compute and incorporate each category as a feature for analysis.

One-hot Encoding: For the categorical variables (such as status, market, etc.), we use one-hot encoding to convert them into numerical data suitable for regression analysis. Columns that are not useful for the predictive model (such as permalink, name, homepage_url) are removed from the dataset.

Data Exploration
In this section, we explore key insights derived from the dataset:

Geographical Insights: The USA leads in start-up funding, receiving 76.6% of the total funding, with other countries such as China, Great Britain, India, and Canada receiving much smaller portions.
Market Insights: The most heavily funded industries are Biotechnology, Software, Clean Technology, Health Care, and E-Commerce. Differences across countries show preferences for different sectors, with the USA most interested in Biotechnology, China focusing on E-Commerce, and other countries prioritizing mobile technologies and clean tech.
Trends Over Time: Start-up funding saw slow growth until 2005, but expanded rapidly thereafter. The economic crisis of 2008 saw funding peaks, particularly in Biotechnology.
Predictive Model
The goal of the predictive model is to forecast future trends in start-up funding. The model is built using the cleaned dataset (processed_dataset.csv) created in the descriptive analysis section.

Data Preprocessing for Predictive Modeling
Date Conversion: Dates are converted into years to make them usable for machine learning models.
Feature Engineering: We split the category_list column into separate rows, with each category assigned its own value.
One-hot Encoding: Categorical variables are encoded into numerical data, enabling them to be used in regression models.
Column Removal: Columns such as permalink, name, and homepage_url are dropped as they don't significantly affect the model’s predictive power.
Modeling Process
We developed several models using a training/test dataset split at a 70/30 ratio (70% training and 30% testing). The models are trained using the following steps:

Training: The model is trained on the pre-processed dataset excluding the target variable (funding_total_usd).
Validation: Hyperparameters are tuned, and model performance is validated.
Testing: The model is tested on the holdout test data to evaluate its performance.
Parameter Tuning
During the modeling process, we tuned the following parameters:

Learning Rate: After using grid search, we found that a learning rate of 0.5 gave the best results. However, to avoid overfitting, we lowered the learning rate to improve the model’s generalization.
Max Depth: To control tree complexity and avoid overfitting, we set max_depth to 5.
Number of Estimators (n_estimators): The number of decision trees created in the Gradient Boosting Regressor was set to 1000, providing the best results for the test data. However, the 5-fold cross-validation showed that performance starts to plateau after a certain threshold.
Model Evaluation
To evaluate model performance, we used the following metrics:

R2-Score: Measures how well the independent variables explain the variance in the target variable.
Mean Squared Error (MSE): Measures the average squared difference between predicted and actual values.
Root Mean Squared Error (RMSE): Converts MSE into the same unit as the target variable (USD).
Mean Absolute Error (MAE): Measures the average absolute difference between predicted and actual values.
Conclusion
Based on the evaluation metrics, the best-performing model was the Gradient Boosting Regressor, which achieved an R2 score of 0.84 and the lowest RMSE (25,800,852 USD). This model provided the most accurate predictions and the best performance among the regression models tested.

Summary
Geographical Insights: The USA leads in start-up funding, with 76.6% of the total funding received. Other countries like China and Great Britain receive smaller shares.
Market Insights: Biotechnology, Software, Clean Technology, and Health Care dominate funding, with slight variations by country.
Trends: Funding for start-ups has grown exponentially after 2005, peaking around 2009-2010, particularly in Biotechnology.
Best Model: The Gradient Boosting Regressor achieved the highest R2 score of 0.84, making it the best model for predicting start-up funding trends.
