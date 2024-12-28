## Experiments with the Informer Architecture 

In this fork of the Informe architecture we are experimenting with predicting AAPL closing price, AAPL 70 moving average, and CSX moving average.

## Data

data is stored in the data folder. The data is stored in the following format:

```csv
date,open,low,high,close,volume,70_ave
```

## Model

We train the model with both `train_informerAAPL.py` and `train_informerCSX.py`. The model CHECKPOINTS are saved in the `checkpoints` folder.
We also do a prediction with both in the results folder.


## Custom Data

I written a class in `inference_custom_data.py` that allows you to input custom data to the model after training. The `InformerPredictor` class takes in the model's args, the data, and checkpoint path and provides the `predict_future` method to predict future values from the data.

