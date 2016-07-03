# Newyork Subway Ridership Prediction

###Introduction
This project is done as a part of completion of Udacity's Introduction to Data Science course. In this project Newyork Subway data is taken and analyzed and a Linear Regression model is used to predict ridership in Newyork Subway. As a part of course completion following questions needs to be answered.

####Section 1: Statsitical Test
*1.1 Which statistical test did you use to analyse the NYC subway data? Did you use a one-tail or a two-tail P value? What is the null hypothesis? What is your p-critical value?*  
The statistical test used was mann-whitney U test. As the features were not normally distributed and t-test assumes data to be normally distributed. Two-tail P values were used since it is not know which data set has higher or lower values.  
```javascript
Null Hypothesis H0 : The rain or fog does not affect the ridrship in NYC Subway.  
Significance Level : .05 
```
*1.2 Why is this statistical test applicable to the dataset? In particular, consider the assumptions that the test is making about the distribution of ridership in the two samples.*
![Image of Yaktocat](https://github.com/am064/New-york-Subway-Ridership-Prediction/blob/master/rain_hist.png)  
![Image of Fog](https://github.com/am064/New-york-Subway-Ridership-Prediction/blob/master/fog_hist.png)  

As can be seen from the figure,Mann-Whitney test is applicable beacause it does not assumes data to be normally distirbuted. Furthermore, this test is less susceptible to outliers in the data and even in case of normally distributed data it performs equivalent to welch's t-test. 

*1.3 What results did you get from this statistical test? These should include the following numerical values: p-values, as well as the means for each of the two samples under test.*
```javascript
Without rain mean:  1090.27878015
With rain mean:  1105.44637675
Mann-Whitney Test Parameter: 1924409167.0
p-value : .0386192688276
```
```javascript
Without fog mean:  1083.44928209
With fog mean:  1154.65934963
Mann-Whitney Test Parameter: 1189034717.5 
p-value : .39141234191e-05
```
*1.4 What is the significance and interpretation of these results?*
From the above data, at significance level of .05 and U-value which is not equal to half of product of number of values in data sets
we can conclude that rain and fog does affect ridership. Hence, We can reject our null hypothesis.

#### Section 2: Linear Regression
*2.1 What approach did you use to compute the coefficients theta and produce prediction for ENTRIESn_hourly in your regression model?*
An unregularised linear regression model was used to predict ENTRIESn_hourly which is basically ridership in NYC subway. For computing parameter theta of the model gradient descent was used with alpha value of 0.1 and 200 iteratons.
*2.2 What features (input variables) did you use in your model? Did you use any dummy variables as part of your features?*
The choice of features available from the dataset are as follows :
* UNIT
* Time of the day
* Weekday
* Rain
* Fog
* Min/Max Pressure
* Min/Max Dew
* Min/Max Temperature
* Mean Temperature
* Precipitation
* Thunder
Some of the features like Pressure details, Dew Details, Min/Max temperature can be intuitively discarded from the aforementioned list because these features are very less likely to cause someone to take subway. While mean outside temperature, time of the day, weekday, rain, fog and unit (can be treated as station) does affect ridership. In this case UNIT feature was treated as dummy variable. 
