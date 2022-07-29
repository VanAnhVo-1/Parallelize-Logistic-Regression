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
        - Initialize the weight matrix with shape (1, n), with n = length of a data line – 2 (because id at index 0 and label at index -1). Then convert the weight matrix to a list (list).
        - Caculate m - total of rows
        - Optimize weight matrix by gradient_descent algorithm.
      - Define function predict.
  3. Result
      - Define accuracy funtion.
      - Train model
      - In the first times, the accuracy = 100%  and total runtime = 1098.4s = 0.305h that unconvinced because the decision attribute value is only 0.
      - In the second times, split data into train and test with 0.8:0.2. The accuracy = 87.58% and total runtime = 842s = 0.233h.
  4. Evaluate
      - Define score function and choose class 0 (not concern) is the important class.
      - Caculate score_array, precision, recall and f1_score.
      - Show results using heatmap.
![image](https://user-images.githubusercontent.com/72924182/181673238-0b3b6ccc-9688-4e48-809e-5e7fb0221245.png)
  5. Comment
      - With Logistic Regression, the accuracy is 87.39%.
      - There are 66322 surveys predicting no interest (class 0) true to reality. There are 172 surveys predicting interest (class 1) true to reality. There were 313 surveys that were misclassified (predicted as interested but in fact not interested). There were 9276 surveys missed (predicted not interested but actually interested).
      - There are precsion, recall, f1_score of 0.877, 0.995, 0.932 respectively. With this result, we can see that the accuracy of the found points is high, every postitive point is found. Both precision and recall values are close to 1, so the classification model is good. We have high f1_score so this is better classifier.
