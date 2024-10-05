# Credit Card Fraud Detection

## Kaggle Link
Unfortunately, GitHub does not allow viewing large files directly. You can download and test it, or click the Kaggle link:
[https://www.kaggle.com/code/emiryilmazey/aygaz-credit-card-fraud-detection](https://www.kaggle.com/code/emiryilmazey/aygaz-credit-card-fraud-detection)

## Project Objective
The aim of this project is to detect fraud in a financial dataset and optimize this detection using supervised approaches. In supervised learning, model performance is enhanced using voting methods, prioritizing the recall metric for fraud detection. The overall goal of the project is to develop a system that accurately detects fraud cases.

## Dataset
The dataset used consists of approximately 1.3 million rows. The column names are as follows:

- **Unnamed: 0**: An automatic index number assigned to each row in the dataset.
- **trans_date_trans_time**: The date and time when the transaction occurred.
- **cc_num**: The credit card number (masked or shortened).
- **merchant**: The name of the merchant or business where the transaction took place.
- **category**: The category of the merchant (e.g., grocery, restaurant).
- **amt**: The amount of the transaction.
- **first**: The first name of the cardholder.
- **last**: The last name of the cardholder.
- **gender**: The gender of the cardholder.
- **street**: The street address of the cardholder.
- **city**: The city where the cardholder resides.
- **state**: The state or region where the cardholder resides.
- **zip**: The postal code where the cardholder resides.
- **lat**: The latitude of the cardholder's location.
- **long**: The longitude of the cardholder's location.
- **city_pop**: The population of the city where the cardholder resides.
- **job**: The profession of the cardholder.
- **dob**: The birth date of the cardholder.
- **trans_num**: The unique transaction number associated with the transaction.
- **unix_time**: The UNIX timestamp (epoch time) of the transaction.
- **merch_lat**: The latitude of the merchant's location.
- **merch_long**: The longitude of the merchant's location.
- **is_fraud**: Indicates whether the transaction is fraudulent (1: fraud, 0: not fraud).
- **merch_zipcode**: The postal code of the merchant's location.

## Data Preprocessing
The following steps were followed in data preprocessing:
- **Dropping Unnecessary Features**: Removed columns that were not meaningful or effective for the model, aiding in both data cleaning and optimizing processing time.
- **Handling Null Variables**: Checked for missing (null) values in the dataset and implemented necessary actions to avoid negatively impacting the model (e.g., filling missing values or removing relevant rows).
- **Normalization**: Normalized numerical values to improve model performance by assessing different measurement units on a common scale.
- **Label Encoding**: Due to the ineffectiveness of one-hot encoding and PCA, label encoding was used to convert categorical data into numerical format, allowing for a smaller data footprint.

## Supervised Learning - Model Selection and Training
The training section can be summarized as follows:

- **Voting for Model Selection**: The voting method was employed to enhance model performance. Multiple models were combined to achieve a stronger prediction. **Decision Trees**, **Hist Gradient Boosting**, and **Naive Bayes** algorithms were used in the voting ensemble.
- **Model Evaluation with Cross-Validation**: The trained model was evaluated using the **cross_val_score** function for cross-validation, testing its generalization ability and preventing overfitting. The dataset was divided into different subsets, and the model was trained and tested on each subset.
- **Prioritizing Recall Metric and Confusion Matrix Evaluation**: The **recall** metric (sensitivity) was prioritized for performance measurement, as it indicates how well the model captures rare cases like fraud. A confusion matrix was used for performance measurement, detailing the model's correct and incorrect classifications.


## Conclusion
This project presents a comprehensive approach to detecting credit card fraud using both supervised and unsupervised learning techniques. Through data preprocessing, model selection, and evaluation, the objective of accurately identifying fraudulent transactions has been achieved.

