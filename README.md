# On-Line-Machine-Learning (Nowcasting and Forecasting with several horizons)
This repository is intended for On Line Machine Learning
## Technical Requirements:
* Python 3.9
* [RiverML Library version 0.14](https://riverml.xyz/0.14.0/)
* Numpy Version 1.24.3 for PAC and PACF plotting. (Autocorrelation and Parcial Autocorrelation Plots)
## Project Structure (Source Code): 
The project is divided into two notebooks:
> TFM_Largo_Plazo <br>
> TFM_Nowcasting <br>

Both notebooks are joint in this notebook TFM_Nowcasting_y_Largo_Plazo.ipynb, you can check whatever you prefer,BUT the latter is very long.<br>

## Language:
Comments in code and Thesis for the master in Spanish<br>

## Dataset:
Downloaded from arXivLabs [Chicken Cases Estimation in Hungary](https://doi.org/10.48550/arXiv.2209.14129).<br>
Time-Series Forecasting is a powerful data modeling discipline that analyzes historical observations to predict future values of a time-series. It has been utilized in numerous applications, including but not limited to economics, meteorology, and health. In this paper, we use time-series forecasting techniques to model and predict the future incidence of chickenpox.
 
## Description of the project:
In the presence of the growing need to manage increasingly huge amounts of data, and at ever increasing speeds, we find ourselves with the paradigm that Traditional AI is not useful. Traditional AI has a very specific way of proceeding. It is based on access to large volumes of data, and on having the time necessary to train and learn. It assumes that all the information will be available and accessible at all times.
The solution involves real-time data analytics, and the development of algorithms and architectures that allow the AI to learn incrementally each time information is available. Here is where the concept of Time Series Data Analysis would fit. But in addition, the data has a bad habit of changing, this effect is called Concept Drift, and consists of a sudden change in the distribution of the data, for which it is necessary to "readjust the model", so that it keeps on working correctly. In this work we are going to address the real-time prediction of chickenpox in Hungary in the long term, which will allow us to establish several time horizons. These predictions, needs to be considered under conditions of eventual changing drifts and also having into considerations the outliers.<br>
Also, the best model in forecasting has been used to **estimate uncertainty on predictions**.<br>

In this study **Nowcasting** with several models like **Linear Regression Model,Hoeffding Tree Regressor,a Statistic Dummy Model (base line) just giving the value in (t-1), and also Stochastic Gradient Tree for Regression**, have been used, considering or not Concept Drift and Outliers to check wether the perfomance of the models improved or not.

And for **Forecasting**, SNARIMAX model with three horizons (1,2 and 3 months) against a dummy model Holtwinter, has been studied.

Once all the investigations have been done. A bit of light explaining the best model, Linear Regression,have been carried out with SHAP Library, although there is also another library called LIME for the same purpose.
**Estimation of uncertainity and the explanation** of the model are in TFM_Nowcasting and in the global notebook TFM_Nowcasting_y_Largo_Plazo.ipynb <br>

## Results:
Looking at the table containing the measurements of MAE metric gathered across the whole process
![image](https://user-images.githubusercontent.com/66425146/209072982-c3f90426-8824-45b6-9e71-c3efe25c25e7.png)
We can say that 
* For each county:
>It can be seen that the model that best predicts, presents the least MAE, is the linear regression model, which we have called the **Linear Regressor Model**, although the Hoefding Tree Regressor Model , has very similar behaviour since in its leaves  has a linear regression model equal to that of the Linear Regressor Model. The figures of the table have been obtained by comparing the models against the **Statistic Regressor base model**, which simply returns the value at the previous instant (t-1).
Measurements have been made first without handling the outliers, afterward handling outliers by simply not learning from them when they were detected, giving better performance to modes. In addition to treating the outliers, an artificial drift was introduced into the data to see how  different models behaved and the answer was that they behaved better than if the models adapt to the drift than if they don't. They adapt earlier and more smoothly to the drift. In order to detect possible Concept Drifts, an ADWIN drift detector has been used. Every time a drift is detected, the model is restarted so that it learns from the most recent data and ignores the oldest ones.
* Comparing counties:
>Comparing the measurements between counties, the counties that present the lowest MAE regardless of the model used, although of course there are differences between models and the lowest MAE is still with those models treating  outliers and drift, they are those that present less dispersion, less standard deviation and lower mean, in the data. These cities are those that have a lower population or have a lower number of cases of chickenpox. The greater the spread in the data, the greater the error.

