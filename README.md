# linear-reg
# Linear Regression

## Introduction
Linear Regression Algorithm is a machine learning algorithm based on supervised learning.  It performs a regression task. Regression models a target prediction value based on independent variables. It is mostly used for finding out the relationship between variables and forecasting. Regression shows a line or curve that passes through all the data points on a target-predictor graph in such a way that the vertical distance between the data points and the regression line is minimum.” It is used principally for prediction, forecasting, time series modeling, and determining the causal-effect relationship between variables

### Simple Linear Regression
Linear regression performs the task to predict a dependent variable(target) based on the given independent variable(s). So, this regression technique finds out a linear relationship between a dependent variable and the other given independent variables. Hence, the name of this algorithm is Linear Regression.
![image](https://user-images.githubusercontent.com/97376928/161058951-a0632816-a306-4cec-bf47-29ea7828e6d9.png)<br>
In the figure above, on X-axis is the independent variable and on Y-axis is the output. The regression line is the best fit line for a model. And our main objective in this algorithm is to find this best fit line.

### Cost function
Cost function optimizes the regression coefficients or weights and measures how a linear regression model is performing. The cost function is used to find the accuracy of the mapping function that maps the input variable to the output variable. This mapping function is also known as the Hypothesis function.In Linear Regression, Mean Squared Error (MSE) cost function is used, which is the average of squared error that occurred between the predicted values and actual values.
By simple linear regression we can calculate MSE as:<br>
![image](https://user-images.githubusercontent.com/97376928/161059573-f70594af-946d-4e8a-b173-685aa88ee0d7.png)<br>
where y = actual values, y<sup>^</sup> = predicted values.

### Learning Rate

>Let **D={x<sup>i<sup>→</sup></sup>, y<sup>→</sup>)**  ∣ **x<sup>(i)</sup> ∈  X**,**y<sup>(i)</sup>∈ Y, i= 1,2,……N}**,<br>

Let's assume our hypothesis  h  is a linear combination of the input features (even though the graph above shows it is not), then for an input  x<sup>→</sup>  we will calculate the output  y<sup>^</sup>   as<br>
![image](https://user-images.githubusercontent.com/97376928/161063324-83b65201-7de7-496d-9662-0ef5a1c44217.png)<br>
where  w<sup>k</sup> 's are the parameters (also known as weights). We can simplify, the notation by introducing  x<sub>0</sub>=1  in the  x  vectors to form<br>
![image](https://user-images.githubusercontent.com/97376928/161063762-72065e2c-90e8-4c69-96df-0f0563429945.png)<br> where <br> ,
![image](https://user-images.githubusercontent.com/97376928/161064182-37ae1722-107f-495b-b8d3-991cd7aa961b.png)<br> 
and  x<sup>→</sup> <br> = <br>![image](https://user-images.githubusercontent.com/97376928/161064406-a6eebf16-429f-485c-b96f-d2ff4172314b.png)
###
we can use the gradient descent to find the point where the minimum of the cost function is w.r.t the weight vector.<br>

Lets find the gradient of the cost function w.r.t  w<sub>k</sub>,k=0,1,2<br>

![image](https://user-images.githubusercontent.com/97376928/161066341-0614a1cd-c23d-4339-b789-201e0b62209c.png)<br>
Lets now first find <br>
![image](https://user-images.githubusercontent.com/97376928/160916773-67b7df9c-1abe-40f5-9583-c5877ab0281a.png)<br>
<br>and then substitute that in the above equation 1.<br>
![image](https://user-images.githubusercontent.com/97376928/161067417-bfd70d83-db9a-4517-ba3c-818fed8c2119.png)<br>
Substituting in the above equation we get,<br>![image](https://user-images.githubusercontent.com/97376928/161067630-149e11dc-4cba-4270-a793-6e3d58e6cb01.png)<br>
We will find the gradient with respect to all  wk 's to form the gradient vector<br>![image](https://user-images.githubusercontent.com/97376928/161067879-6231fb31-3ff1-4aa8-9175-c74ad4665c43.png)<br>
## Implementation of Linear Regression Using Python code
In this regression task we will predict the percentage of marks that a student is expected to score based upon the number of hours they studied. This is a simple linear regression task as it involves just two variables.

### Importing Libraries
To import necessary libraries for this task, execute the following import statements:<br>
###### import pandas as pd
###### import numpy as np
###### import matplotlib.pyplot as plt
###### %matplotlib inline

### Dataset

The dataset being used for this example has been made publicly available and can be downloaded from this link:https://drive.google.com/open?id=1oakZCv7g3mlmCSdv9J8kdSaqO5_6dIOw

The following command imports the CSV dataset using pandas:

>dataset = pd.read_csv('D:\Datasets\student_scores.csv')


Now let's explore our dataset a bit. To do so, execute the following script:

> dataset.shape


After doing this, you should see the following printed out:

###### (25, 2)

This means that our dataset has 25 rows and 2 columns. Let's take a look at what our dataset actually looks like. To do this, use the head() method:

> dataset.head()


The above method retrieves the first 5 records from our dataset, which will look like this:

![fig1](https://user-images.githubusercontent.com/4158204/160814627-96ab0b1f-28c4-47b6-a9ba-aa8a20dd282f.JPG)


>dataset.describe()


![fig2](https://user-images.githubusercontent.com/4158204/160868466-b64b7b63-8d1c-4266-bab6-3c9733a9cf80.JPG)


And finally, let's plot our data points on 2-D graph to eyeball our dataset and see if we can manually find any relationship between the data. We can create the plot with the following script:

> dataset.plot(x='Hours', y='Scores', style='o')<br>
plt.title('Hours vs Percentage')<br>
plt.xlabel('Hours Studied')<br>
 plt.ylabel('Percentage Score')<br>
 plt.show()<br>

In the script above, we use plot() function of the pandas dataframe and pass it the column names for x coordinate and y coordinate, which are "Hours" and "Scores" respectively.

The resulting plot will look like this:

![fig3](https://user-images.githubusercontent.com/4158204/160868781-5cad28f4-4101-41b3-a3f7-aeadbe8e16e5.JPG)

From the graph above, we can clearly see that there is a positive linear relation between the number of hours studied and percentage of score.
### Preparing the Data
Now we have an idea about statistical details of our data. The next step is to divide the data into "attributes" and "labels". Attributes are the independent variables while labels are dependent variables whose values are to be predicted. In our dataset we only have two columns. We want to predict the percentage score depending upon the hours studied. Therefore our attribute set will consist of the "Hours" column, and the label will be the "Score" column. To extract the attributes and labels, execute the following script:

> X = dataset.iloc[:, :-1].values<br>
 y = dataset.iloc[:, 1].values

The attributes are stored in the X variable. We specified "-1" as the range for columns since we wanted our attribute set to contain all the columns except the last one, which is "Scores". Similarly the y variable contains the labels. We specified 1 for the label column since the index for "Scores" column is 1. Remember, the column indexes start with 0, with 1 being the second column. In the next section, we will see a better way to specify columns for attributes and labels.

Now that we have our attributes and labels, the next step is to split this data into training and test sets. We'll do this by using Scikit-Learn's built-in train_test_split() method:

>from sklearn.model_selection import train_test_split X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

The above script splits 80% of the data to training set while 20% of the data to test set. The test_size variable is where we actually specify the proportion of test set.




## Training the Algorithm
We have split our data into training and testing sets, and now is finally the time to train our algorithm. Execute following command:
>from sklearn.linear_model import LinearRegression<br>
regressor = LinearRegression()<br>
 regressor.fit(X_train, y_train)<br>
With Scikit-Learn it is extremely straight forward to implement linear regression models, as all you really need to do is import the LinearRegression class, instantiate it, and call the fit() method along with our training data. This is about as simple as it gets when using a machine learning library to train on your data.
In the theory section we said that linear regression model basically finds the best value for the intercept and slope, which results in a line that best fits the data. To see the value of the intercept and slop calculated by the linear regression algorithm for our dataset, execute the following code.
To retrieve the intercept:<br>
>print(regressor.intercept_)

The resulting value you see should be approximately 2.01816004143.

For retrieving the slope (coefficient of x):
>print(regressor.coef_)
The result should be approximately 9.91065648.This means that for every one unit of change in hours studied, the change in the score is about 9.91%. Or in simpler words, if a student studies one hour more than they previously studied for an exam, they can expect to achieve an increase of 9.91% in the score achieved by the student previously.
## Making Predictions
Now that we have trained our algorithm, it's time to make some predictions. To do so, we will use our test data and see how accurately our algorithm predicts the percentage score. To make pre-dictions on the test data, execute the following script:
> y_pred = regressor.predict(X_test)
The y_pred is a numpy array that contains all the predicted values for the input values in the X_test series.To compare the actual output values for X_test with the predicted values, execute the following script:
>df = pd.DataFrame({'Actual': y_test, 'Predicted': y_pred})
The output looks like this:<br>
![fig4](https://user-images.githubusercontent.com/4158204/160877632-39fa20d9-b431-44b6-9f1f-e0cbc89f1ba4.JPG)<br>Though our model is not very precise, the predicted percentages are close to the actual ones.

>Note:The values in the columns above may be different in your case because the train_test_split function randomly splits data into train and test sets, and your splits are likely different from the one shown in this article.

## Evaluating the Algorithm




The final step is to evaluate the performance of algorithm. This step is particularly important to compare how well different algorithms perform on a particular dataset. For regression algorithms, three evaluation metrics are commonly used:

>Mean Absolute Error (MAE) is the mean of the absolute value of the errors.
 It is calculated as:<br>![image](https://s3.amazonaws.com/stackabuse/media/linear-regression-python-scikit-learn-3.png)<br>






* Mean Squared Error (MSE) is the mean of the squared errors and is calculated as:

![image](https://s3.amazonaws.com/stackabuse/media/linear-regression-python-scikit-learn-4.png)


* Root Mean Squared Error (RMSE) is the square root of the mean of the squared errors:

![image](https://s3.amazonaws.com/stackabuse/media/linear-regression-python-scikit-learn-5.png)

Luckily, we don't have to perform these calculations manually. The Scikit-Learn library comes with pre-built functions that can be used to find out these values for us.

Let's find the values for these metrics using our test data. Execute the following code:

>from sklearn import metrics<br>
print('Mean Absolute Error:', metrics.mean_absolute_error(y_test, y_pred))<br>
print('Mean Squared Error:', metrics.mean_squared_error(y_test, y_pred))<br>
print('Root Mean Squared Error:', np.sqrt(metrics.mean_squared_error(y_test, y_pred)))<br>

>The output will look similar to this (but probably slightly different):<br>Mean Absolute Error: 4.183859899<br>
Mean Squared Error: 21.5987693072<br> Root Mean Squared Error: 4.6474476121<br>
The value of root mean squared error is 4.64, which is less than 10% of the mean value of the percentages of all the students i.e. 51.48. This means that our algorithm did a decent job.
