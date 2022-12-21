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

## DATASET
Downloaded from arXivLabs [Chicken Cases Estimation in Hungary](https://doi.org/10.48550/arXiv.2209.14129).<br>
Time-Series Forecasting is a powerful data modeling discipline that analyzes historical observations to predict future values of a time-series. It has been utilized in numerous applications, including but not limited to economics, meteorology, and health. In this paper, we use time-series forecasting techniques to model and predict the future incidence of chickenpox.
 
## DESCRIPTION OF THE PROJECT:
In the presence of the growing need to manage increasingly huge amounts of data, and at ever increasing speeds, we find ourselves with the paradigm that Traditional AI is not useful. Traditional AI has a very specific way of proceeding. It is based on access to large volumes of data, and on having the time necessary to train and learn. It assumes that all the information will be available and accessible at all times.
The solution involves real-time data analytics, and the development of algorithms and architectures that allow the AI to learn incrementally each time information is available. Here is where the concept of Time Series Data Analysis would fit. But in addition, the data has a bad habit of changing, this effect is called Concept Drift, and consists of a sudden change in the distribution of the data, for which it is necessary to "readjust the model", so that it keeps on working correctly. In this work we are going to address the real-time prediction of chickenpox in Hungary in the long term, which will allow us to establish several time horizons. These predictions, needs to be considered under conditions of eventual changing drifts and also having into considerations the outliers.<br>
Also, the best model in forecasting has been used to **estimate uncertainty on predictions**.<br>

In this study **Nowcasting** with several models like Linear Regression Model,Hoeffding Tree Regressor,a Dummy Model just giving the value in (t-1), and also Stochastic Gradient Tree for Regression, have been used, considering or not Concept Drift and Outliers to check wether the perfomance of the models improved or not.

And for **Forecasting**, SNARIMAX model with three horizons (1,2 and 3 months) against a dummy model Holtwinter, has been stutied.
