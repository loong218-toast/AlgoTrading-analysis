# Trading-analysis
[Notebook_v2](https://github.com/loong218-toast/AlgoTrading-analysis/blob/main/Trading_Analysis-v2.ipynb)  <br />
Original version is too large to view on Github, v2 version removed all Plotly plots. <br />

(Trading with time series forecasting using LSTM and some other calculations.) <br />

First, we have the gold market with 12 years of historical data (2010-2022) :


<img src="https://user-images.githubusercontent.com/77558802/166462259-e973e7f6-9fc3-4664-a148-c2d33a4ba3b1.png" width=80%>



Blue line = Market price <br />
Red line = Daily moving average (DMA) <br />
Green line = Weekly moving average (WMA) <br />

10 years for training model and 2 years for testing model. <br />
  
We take the first 10 years data and calculate the overall results : 

<img src="https://user-images.githubusercontent.com/77558802/166701104-2a42aab8-7574-442d-a7b9-3296b22f3b97.png" width=80%>


Within 10 years of historical data, we get total valid 5829 positions. <br />
Yellow points are winning trades and dark blue points are losing trades. <br />

Calculation is done by filtering positions that are either above all MA or below all MA. <br />
The whole approach is that we only buy when the price goes upward, and vice versa.

In 5829 positions, we get 29% winning trades (1683/5829). <br />

Then we find to best value for TP (Take profit) and SL (Stop loss) to increase profit :

<img src="https://user-images.githubusercontent.com/77558802/166470256-ec7a1280-6c09-4b10-9d6b-00fb146ca4c4.png" width=50%>

(Lighter data points mean better results) <br />

For buy, Best TP and SL are 9.0 and 1.5 (21644 scores), and worst TP and SL are 20.0 and 1.0 (-44861 scores) <br />
For sell, Best TP and SL are 8.0 and 1.5 (16153 scores), and worst TP and SL are 20.0 and 1.0 (-47281 scores) <br />
1 TP is +1 score, and 1 SL is -1 score (depends on the result of each position) <br />
Basically, High TP and low SL is the best approach to the gold market. <br />

Even we have a low chance of winning, but we have a good risk/reward ratio.

To improve the performance, I classify all positions that are closed to each other (24 hours), as I noticed cluster patterns in those positions.

<img src="https://user-images.githubusercontent.com/77558802/166701292-622aab04-5a79-4361-af95-94fe83e6ac54.png" width=80%>

Our winning chance increases from 29% (1683/2944) to 54.4% (816/1499). <br />
We get only 3216 scores, but I find it very consistent and it also loses less scores.

We then do logistic regression from different data of each positions, but I find most data are too uncorrelated to make a good model.

Our last approach is LSTM time series forecasting model, which performed very well.

<img src="https://user-images.githubusercontent.com/77558802/166491304-72456de7-70fc-4e3b-8e87-3f911bf4913e.png" width=80%>

<img src="https://user-images.githubusercontent.com/77558802/166491309-3a7ffbe3-620e-469a-bcf8-e8a0c4447495.png" width=50%>

Our winning chance for test data increases from 50.7% to 58.33%.

# Algo-Trading

[Algo-Notebook](https://github.com/loong218-toast/AlgoTrading-analysis/blob/main/Algorithmic_Trading.ipynb)  <br />

The program automatically opens and closes position depending on the market condition.

It handles everything for you, and the only thing you need to do is drinking Mai Tai on the beach.

# Other

If you want to view the market and do the trading at the same time, use [Live-Notebook](https://github.com/loong218-toast/AlgoTrading-analysis/blob/main/LiveTrading.ipynb) and [Live-Plot-Notebook](https://github.com/loong218-toast/AlgoTrading-analysis/blob/main/LiveTrading_plot.ipynb)

The [Live-Notebook](https://github.com/loong218-toast/AlgoTrading-analysis/blob/main/LiveTrading.ipynb) runs [Algo-Notebook](https://github.com/loong218-toast/AlgoTrading-analysis/blob/main/Algorithmic_Trading.ipynb)

# Limitations

The LSTM model works with sklearn MinMaxScaler which transform features scaling each feature to a given range. Since financial markets have not acutal "Min" and "Max" values, the model accuracy can lose over time. Market prices may keep going up or down and may exceed the Min and Max values.

# Resources
Python packages : Pandas, Numpy, Tensorflow, Scikit-learn, Plotly, Matplotlib, MetaTrader5, Datetime, Talib, Schedule, Pytz, Isoweek


