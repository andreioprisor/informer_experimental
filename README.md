# Informer Architecture Experiments

This project experiments with the Informer architecture, a state-of-the-art deep learning model designed for time series forecasting. The Informer uses a novel self-attention mechanism and stacked encoder-decoder layers to capture long-range dependencies in time series data.

We focus on predicting:
1. Apple Inc. (AAPL) stock closing price 
2. AAPL 70-day moving average price
3. CSX Corporation (CSX) stock moving average price

Moving averages smooth out short-term fluctuations to highlight longer-term trends. Predicting moving averages can help identify broader market patterns and make more informed investment decisions.

## Data
Input data is stored as CSV files in the `data` folder. Each file includes these columns:
- `date`: date and hour of the data point
- `open`, `high`, `low`, `close`: OHLC prices for that hour
- `volume`: number of shares traded that hour
- `70_ave`: 70-day moving average price 

This format aligns with the common OHLCV (Open, High, Low, Close, Volume) format used in finance, plus the `70_ave` column for our experiments.

## Model Training
We train the Informer model using:
- `train_informerAAPL.py` for AAPL stock data
- `train_informerCSX.py` for CSX stock data

During training, the model learns patterns and dependencies in the historical price data to make future predictions. 

Trained model weights are saved as checkpoints in the `checkpoints` folder. This allows loading the model later for predictions without retraining.

Prediction results are saved in the `results` folder for further analysis.

## Custom Data Predictions
To make predictions on new, unseen data, use the `InformerPredictor` class in `inference_custom_data.py`.

1. Create an `InformerPredictor` instance with the model config, custom data, and path to the trained checkpoint.
   
2. Call the `predict_future` method to preprocess the data, load the model, and generate predictions.

This separates the training and inference code for better modularity and reusability.

## Evaluation and Analysis
The `informer_train_evaluateAAPL_CSX.ipynb` Jupyter notebook contains code to evaluate and analyze the trained models.

We compare the predicted prices to actual prices to assess prediction accuracy. Several custom analysis functions provide additional insights:

1. `roll_close` and `roll_close_adjusted`: calculate rolling price averages over a specified window to smooth short-term noise and highlight trends.

2. Moving average calculation: compute the cumulative moving average of predicted prices up to each time point.

3. `get_coef`: fit linear and polynomial trendlines to the predicted prices. The trendline coefficients (slope, curvature) indicate the overall prediction trend.
   - For example, a positive linear slope suggests the model predicts increasing prices over time.

4. `plot_4_curves`: visualize the original predictions, rolling averages, moving average, trendlines, and actual prices together. 
   - This allows a comprehensive view of the model's performance and how well its predictions match reality.

By calculating averages, fitting trends, and visualizing results alongside real prices, these functions provide a toolkit to thoroughly evaluate the model's predictive power and make informed decisions based on its outputs.