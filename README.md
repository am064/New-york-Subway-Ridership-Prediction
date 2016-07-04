# Newyork Subway Ridership Prediction

###Introduction
This project is done as a part of completion of Udacity's Introduction to Data Science course. In this project Newyork Subway data is taken and analyzed and a Linear Regression model is used to predict ridership in Newyork Subway. As a part of course completion following questions needs to be answered.

####Section 1: Statsitical Test
*_1.1_ Which statistical test did you use to analyse the NYC subway data? Did you use a one-tail or a two-tail P value? What is the null hypothesis? What is your p-critical value?* 

The statistical test used was mann-whitney U test. As the features were not normally distributed and t-test assumes data to be normally distributed. Two-tail P values were used since it is not know which data set has higher or lower values.  
```javascript
Null Hypothesis H0 : The rain or fog does not affect the ridrship in NYC Subway.  
Significance Level : .05 
```
*_1.2_ Why is this statistical test applicable to the dataset? In particular, consider the assumptions that the test is making about the distribution of ridership in the two samples.*  

![Image of Yaktocat](https://github.com/am064/New-york-Subway-Ridership-Prediction/blob/master/rain_hist.png)  
![Image of Fog](https://github.com/am064/New-york-Subway-Ridership-Prediction/blob/master/fog_hist.png)  

As can be seen from the figure,Mann-Whitney test is applicable beacause it does not assumes data to be normally distirbuted. Furthermore, this test is less susceptible to outliers in the data and even in case of normally distributed data it performs equivalent to welch's t-test. 

*_1.3_ What results did you get from this statistical test? These should include the following numerical values: p-values, as well as the means for each of the two samples under test.*  

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
*_1.4_ What is the significance and interpretation of these results?*  

From the above data, at significance level of .05 and U-value which is not equal to half of product of number of values in data sets
we can conclude that rain and fog does affect ridership. Hence, We can reject our null hypothesis.

#### Section 2: Linear Regression
*_2.1_ What approach did you use to compute the coefficients theta and produce prediction for ENTRIESn_hourly in your regression model?*  

An unregularised linear regression model was used to predict ENTRIESn_hourly which is basically ridership in NYC subway. For computing parameter theta of the model gradient descent was used with alpha value of 0.1 and 70 iteratons.
*_2.2_ What features (input variables) did you use in your model? Did you use any dummy variables as part of your features?*  

The features selected were UNIT, Hour and weekday. All the 3 features selected were used as dummy variables.

*_2.3_ Why did you select these features in your model? We are looking for specific reasons that lead you to believe that the selected features will contribute to the predictive power of your model.*  

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
Some of the features like Pressure details, Dew Details, Min/Max temperature can be intuitively discarded from the aforementioned list because these features are very less likely to cause someone to take subway. While mean outside temperature, time of the day, weekday, rain, fog and unit (can be treated as station) does affect ridership. In this case UNIT, time of the day and weekday are treated as dummy variable. Also, feautre rain tell us whether it rained that or not that day. So even if it rained in the night it would have a value of '1' whereas precipitation value gives us the precipitation in inches at that time and location which is a more refined feature. Now to select best feature each feature was added sequentially and there performance was measured by R-squared value.

| Features | R-squared values |
| --- | --- |
| UNIT | 0.418339891299  |
| UNIT,Hour| 0.500865986392 |
| UNIT,Hour,weekday | 0.513811132529 |
| UNIT,Hour,weekday,fog | 0.513838196845 |
| UNIT,Hour,weekday,fog,precipi| 0.513899738594 |
| UNIT,Hour,weekday,fog,precipi,meantempi| 0.514371255759 |


From the above table we can see that most of the data can be described by first three variable and rest variable does not contribute significantly to r-squared value. Hence the features selected are UNIT,HOUR and weekday.

*_2.4_ What are the coefficients (or weights) of the non-dummy features in your linear regression model?*  

No non-dummy feature was used in the model.

*_2.5_ What is your model’s R2 (coefficients of determination) value?*  

  ```javascript
R-squared value :  0.513811132529
```
*_2.6_ What does this R2 value mean for the goodness of fit for your regression model? Do you think this linear model to predict ridership is appropriate for this dataset, given this R2 value?*  

In general 2 basic components of any valid regression model are : 
* Deterministic Component
* Stochastic Error Component  
And we want our model to be good enough to explain deterministic component of the response and none of the predictive information to be present in error term or simply put, error term should be unpredictable. Just by lookin at thr R-squred value we cant tell whether the error term is unpredictable or it is biased. So we plot the residuals.
![Image of Residual](https://github.com/am064/New-york-Subway-Ridership-Prediction/blob/master/residual_histo.png)
![Image of Residual](https://github.com/am064/New-york-Subway-Ridership-Prediction/blob/master/scatter_residual.png)  
From the plot we can see that our residual are normally distributed and centered at zero. Since our error term is random it tells us that our model is good enough to describe deterministic portion of the response. Although the model wont give the exact values but it can give an approximate idea of ENTRIESn_hourly. Also, we know from the statsitical test that rain and fog does affect ridership but this adding them to features does not explain significant variance in the data. So for such case we might need bigger dataset so that model can properly incorporate effect of rain and fog on ridership. Also a non-linear model can be a good choice for such dataset.

#### Section 3: Visualizations

*3.1 Include and describe a visualization containing two histograms: one of ENTRIESn_hourly for rainy days and one of ENTRIESn_hourly for non-rainy days.*  

Please Refer to Section 1.1.

*3.2 Include and describe a freeform visualization.*  

![Image of plot1](https://github.com/am064/New-york-Subway-Ridership-Prediction/blob/master/mean_entries_by_time_day.png)

The plot has three prominent peaks showing maximum mean Entries in subway. Which tells us that peak hours are from 11-12 am and in the evening from 4pm-5pm and in the night from 8pm-9pm. Interestingly, for the time between 8am-10am which are generally considered as morning peak hours the rush is less then it is between 11am-12am. And also for evening rush hours have less rush compared to night rush hours.IT would be hard to comment on from the given data as it is just for one month or alternatively it can also tell us the changing working hours and lifestyle of poeple in NYC. Since, an era of flexible working hours have begun most people would prefer to go office late. To comment on above statement with more surity more data is required.

![Image of plot2](https://github.com/am064/New-york-Subway-Ridership-Prediction/blob/master/mean_hourly_per_day.png)

![Image of plot3](https://github.com/am064/New-york-Subway-Ridership-Prediction/blob/master/conditions_entries.png)

####Section 4: Conclusion

*4.1 From your analysis and interpretation of the data, do more people ride the NYC subway when it is raining or when it is not raining?*

Only the means for Entries when its raining and for when its not raining are not enough to tell us because of the variance in the data. From mann-whitney U-test we can tell with much certainity that the data sets were statistically significant but at the same time rain as a feature does a little bit in improving performance of our linear regression model. So we cant tell yet whether rain affects ridership or not.

*4.2 What analyses lead you to this conclusion? You should use results from both your statistical tests and your linear regression to support your analysis.*
Since, the linear regression model did not use rain as feature. And even after including rain as feature model's performance did not increase much. Both the statistical test and linear regression contradict each other. Also, from the plot of condition and entries in NYC subway(from section 4) we can see that light rain witnesses more mean entries then heavy rain and light drizzle witnessess more mean entries then rain.The data highly depends on demographics of NYC population as well as location of each station. It may happen so, that in certain areas with heavy rainfall subway needs to be closed. In any case we need a more robust prediciting model to incorporate such complexities using information from rain and precipitation to tell wether rain affects ridership or not.
