# Parallelize Logistic Regression - BIG DATA
## Dataset
- Name: Health Insurance Cross Sell Prediction.
- Link: https://www.kaggle.com/anmolkumar/health-insurance-cross-sell-prediction?select=train.csv 
- Description: The dataset provides information to predict whether health insurance customers are interested in Vehicle Insurance.
- Method: Using the Logistic Regression Algorithm.
- Dataset contains 381,109 rows and 12 columns.

|Property|Description|Data type|
| --- | --- | --- |
|id|Unique ID for the customer| integer|
|Gender|Gender of the customer and contains 2 values: Male and Female.| varchar(50)|
|Age|Age of the customer| interger|
|Driving_License| Did Customer have driving license? And contains 2 values: <br />&emsp;0 : Customer does not have DL.<br />&emsp;1 : Customer already has DL.|integer|
|Region Code| Unique code for the region of the customer| integer|
|Previously_Insured| Did Customer have vehicle insurance? And contains 2 values: <br />&emsp;1 : Customer already has Vehicle Insurance.<br />&emsp;0 : Customer doesn't have Vehicle Insurance.|integer|
|Vehicle Age| Age of the Vehicle| varchar(50)|
|Vehicle Damaged| Did customer got his/her vehicle damage in the past? Contains 2 values: <br />&emsp;1 : Customer got his/her vehicle damaged in the past.<br />&emsp;0 : Customer didn't get his/her vehicle damaged in the past.| varchar(50)|
|Annual_Premium| The amount customer needs to pay as premium in the year.| interger|
|PolicySalesChannel|Anonymized Code for the channel of outreaching to the customer ie. Different Agents, Over Mail, Over Phone, In Person, etc.|integer|
|Vintage|Number of Days, Customer has been associated with the company.|interger|
|Response|Reponse of Customer. Contains 2 values:<br />&emsp;1 : Customer is interested,<br />&emsp;0 : Customer is not interested.|integer|
