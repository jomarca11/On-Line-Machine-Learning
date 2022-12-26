# On-Line-Machine-Learning (Nowcasting and Forecasting with several horizons)
This repository is intended for On Line Machine Learning
## Technical Requirements.
* Python 3.9
* [RiverML Library version 0.14](https://riverml.xyz/0.14.0/)
* Numpy Version 1.24.3 for PAC and PACF plotting. (Autocorrelation and Parcial Autocorrelation Plots)
* [SHAP library for Model Explanation] (https://shap-lrjball.readthedocs.io/en/latest/index.html)
## Project Structure (Source Code): 
The project is divided into two notebooks:
> TFM_Largo_Plazo <br>
> TFM_Nowcasting <br>

Both notebooks are joint in this notebook TFM_Nowcasting_y_Largo_Plazo.ipynb, you can check whatever you prefer,BUT the latter is very long.<br>

## Language.
Comments in code and Thesis for the master in Spanish<br>

## Dataset.
Downloaded from arXivLabs [Chicken Cases Estimation in Hungary](https://doi.org/10.48550/arXiv.2209.14129).<br>
Time-Series Forecasting is a powerful data modeling discipline that analyzes historical observations to predict future values of a time-series. It has been utilized in numerous applications, including but not limited to economics, meteorology, and health. In this paper, we use time-series forecasting techniques to model and predict the future incidence of chickenpox.
 
## Description of the project.
In the presence of the growing need to manage increasingly huge amounts of data, and at ever increasing speeds, we find ourselves with the paradigm that Traditional AI is not useful. Traditional AI has a very specific way of proceeding. It is based on access to large volumes of data, and on having the time necessary to train and learn. It assumes that all the information will be available and accessible at all times.
The solution involves real-time data analytics, and the development of algorithms and architectures that allow the AI to learn incrementally each time information is available. Here is where the concept of Time Series Data Analysis would fit. But in addition, the data has a bad habit of changing, this effect is called Concept Drift, and consists of a sudden change in the distribution of the data, for which it is necessary to "readjust the model", so that it keeps on working correctly. In this work we are going to address the real-time prediction of chickenpox in Hungary in the long term, which will allow us to establish several time horizons. These predictions, needs to be considered under conditions of eventual changing drifts and also having into considerations the outliers.<br>
Also, the best model in forecasting has been used to **estimate uncertainty on predictions**.<br>

In this study **Nowcasting** with several models like **Linear Regression Model,Hoeffding Tree Regressor,a Statistic Dummy Model (base line) just giving the value in (t-1), and also Stochastic Gradient Tree for Regression**, have been used, considering or not Concept Drift and Outliers to check wether the perfomance of the models improved or not.

And for **Long Term Forecasting**, SNARIMAX model with three horizons (1,2 and 3 months) against a dummy model Holtwinter, has been studied.

Once all the investigations have been done. A bit of light explaining the best model, Linear Regression,have been carried out with SHAP Library, although there is also another library called LIME for the same purpose.
**Estimation of uncertainity and the explanation** of the model are in TFM_Nowcasting and in the global notebook TFM_Nowcasting_y_Largo_Plazo.ipynb <br>

## Results.
### For Nowcasting
Looking at the table containing the measurements of MAE metric gathered across the whole process
![image](https://user-images.githubusercontent.com/66425146/209072982-c3f90426-8824-45b6-9e71-c3efe25c25e7.png)
We can say that 
* For each county:
>It can be seen that the model that best predicts, presents the least MAE, is the linear regression model, which we have called the **Linear Regressor Model**, although the Hoefding Tree Regressor Model , has very similar behaviour since in its leaves  has a linear regression model equal to that of the Linear Regressor Model. The figures of the table have been obtained by comparing the models against the **Statistic Regressor base model**, which simply returns the value at the previous instant (t-1).
Measurements have been made first without handling the outliers, afterward handling outliers by simply not learning from them when they were detected, giving better performance to modes. In addition to treating the outliers, an artificial drift was introduced into the data to see how  different models behaved and the answer was that they behaved better than if the models adapt to the drift than if they don't. They adapt earlier and more smoothly to the drift. In order to detect possible Concept Drifts, an ADWIN drift detector has been used. Every time a drift is detected, the model is restarted so that it learns from the most recent data and ignores the oldest ones.
* Comparing counties:
>Comparing the measurements between counties, the counties that present the lowest MAE regardless of the model used, although of course there are differences between models and the lowest MAE is still with those models treating  outliers and drift, they are those that present less dispersion, less standard deviation and lower mean, in the data. These cities are those that have a lower population or have a lower number of cases of chickenpox. The greater the spread in the data, the greater the error.

### For Long Term Forecasting:
![image](https://user-images.githubusercontent.com/66425146/209214675-39efb656-694b-49d5-9633-cb893ad63ef6.png)

* For each county:
 >In this case we have two models with several horizons. The **SNARIMAX** model that has been configured with its parameters from the Autocorrelation (ACF) and Partial Autocorrelation (PACF) plots, and **another model taken as Baseline, the Holtwinter**, in which its parameters have also been adjusted for good performance. The first thing to note is that the longer the horizon the models predict worse. Obviously, as in the case of Nowcasting, if the outliers are treated, better performance is obtained than if it is not done. The same is valid for drift. An artificial drift has been introduced to make these checks with the ADWIN drift detector. Every time a drift is detected, both the model and the detector are reset.

* Comparing counties:
>Comparing the measurements between counties, the countie swith the lowest MAE regardless of the model used, although of course there are differences between models,  are still those that handles outliers and drift. Aagain the best model is SNARIMAX. As with Nowcating, the best provinces are those that present a lower dispersion, lower standard deviation and lower mean, in the data. These provinces are those that have a smaller population or have contracted a smaller number of cases of chickenpox. The greater the spread in the data, the greater the error.

### Uncertainity Estimation:
![image](https://user-images.githubusercontent.com/66425146/209218190-dcaa5818-09a0-461a-b411-4f64a2fd341b.png)
For this section, the model with the best metrics obtained during all the previous sections has been chosen. Linear Regression has been chosen, although it has been modified a little by introducing the parameter intercept_lr=0, so that it does not take any default value. This default value is set to 0.01.

* Outliers: It has been clearly seen in the results table that handling outliers, the *trust region*,range between upper bound and lower bound, parameterized with the following parameters models = { 'lower': make_model(alpha=0.05), 'center': make_model(alpha= 0.5), 'upper': make_model(alpha=0.95) } has been reduced, moreover the model produces better MAE metrics. S ohandling outliers does improve both the accuracy of the Model and the confidence zone.trust region, for individual predictions.<br>
* Concept Drift: For Concept Drift, the improvement is not so clear, although it does exist, although it is less noticeable than handling outliers because at first glance the ranges of the confidence zone, Max upper limit and Min lower limit, are the same, however an improved MAE metric and the mean measurements  of both the lower and upper bounds also improve, although not as much as in the treatment of outliers.

These results are so because the Prediction Interval (trust region) predicts the distribution of future values **individually**. While the Confidence Interval, relative to the metrics in this case, MAE, estimates the population mean based on previous values. This is why the metric improves when handling the concept drift, it makes the model produce better metrics, but not so much in the trust region. However, when dealing with outliers, extreme values are eliminated, thus reducing the confidence zone and the values of the MAE metric.

### Model Explainability:
In  this case 5 artificial features have been introduced to check the explainability of the Linear Regressor Model.
![image](https://user-images.githubusercontent.com/66425146/209220927-a755a1dd-1fb7-4e54-80cd-79e30075dc36.png)<br>

We have drawn two summary plots with SHAP Library
![image](https://user-images.githubusercontent.com/66425146/209221102-2dab39bc-74c3-4dcf-9cfd-ab83f077d0a9.png)

As we can see in the first plot features are ordered in term os influence in the model, Firstly lag_1, then month and so on. In the second plot Feature importance: Variables are ranked in descending order, as in the first plot. The horizontal location shows whether the effect of that value is associated with a higher or lower prediction And color shows whether that variable is high (in red) or low (in blue) for that observation.



