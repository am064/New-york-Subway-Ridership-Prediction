# Newyork Subway Ridership Prediction

###Introduction
This project is done as a part of completion of Udacity's Introduction to Data Science course. In this project Newyork Subway data is taken and analyzed and a Linear Regression model is used to predict ridership in Newyork Subway. As a part of course completion following questions needs to be answered.

####Section 1: Statsitical Test
*1.1 Which statistical test did you use to analyse the NYC subway data? Did you use a one-tail or a two-tail P value? What is the null hypothesis? What is your p-critical value?*  
The statistical test used was mann-whitney U test. As the features were not normally distributed and t-test assumes data to be normally distributed. Two-tail P values were used since it is not know which data set has higher or lower values.  
```javascript
Null Hypothesis H0 : The rain does not affect the ridrship in NYC Subway.  
Significance Level : .05 
```
*1.2 Why is this statistical test applicable to the dataset? In particular, consider the assumptions that the test is making about the distribution of ridership in the two samples.*
Mann-Whitney test is applicable beacause it does not assumes data to be normally distirbuted. Furthermore, this test is less susceptible to outliers in the data and even in case of normally distributed data it performs equivalent to welch's t-test. 
