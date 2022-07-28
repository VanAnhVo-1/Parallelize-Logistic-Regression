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
## Enviroment 
- Apache Spark
## Processing
  Data is split to 80% train and 20% test.
  1. Preprocessing
      - Create schema for train data and test data and assign data to the appropriate data types. Import train data and test to Spark SQL DataFrame by using spark.read.csv.
      - Check missing data and drop duplicates data.
      - Consider the correlation relationship between the attributes.
      - Convert data from string type to number type.
      - Standardize data.
  2. Re-simulate the algorithm 
      - Defines the sigmoid function to convert the input data (a number) into a certain small range – which will have a value in the range [0,1]. In other words, the Sigmoid function converts a real value into a probabilistic value.
      - Defines the weights_gradient function. The input data consists of an RDD row(rdd_row) and a weight matrix w. 
        - Multiply 2 matrices x, w:
          - x: data of 1 RDD row containing values from index 1 --> last index – 1 (except id value – index 0 and label – last index).
          - w: weight matrix.
        - Calculate the residual free coefficient by converting the result of multiplying x, w matrices into the value in the range [0,1] and subtract y (the decision attribute).
        - Multiply the result by the value in x to return the weighted gradients.
      - Defines the function cum_sum_gradients bt Multipling 2 arrays with shape (1,n).
      - Define function distributed_gradient_descent:
        - Initialize the weight matrix with shape (1, n), with n = length of a data line – 2 (because id at index 0 and label at index -1). Then convert the weight matrix to a list (list)
