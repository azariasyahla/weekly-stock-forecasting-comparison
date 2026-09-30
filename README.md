# Weekly Stock Price Forecasting: ARIMA vs Neural Network vs Naive

A time series coursework project using the **2023 weekly mean adjusted closing price** of `005380.KS` and a January 2024 one-step evaluation. It compares **ARIMA(1,1,1)**, a small neural network using two lagged values, and a **naive previous-week baseline** on the same four-week test window. This is an educational experiment, not an investment recommendation.

## Why the notebook was revised

The original notebook included ADF tests, differencing, ACF/PACF plots, ARIMA walk-forward predictions, a small neural network, and a naive model. It also contained an undefined `fit_model`, an incorrect “AAPL” chart title for the `005380.KS` ticker, and evaluations on different periods. This version uses actual dated weekly indices, trains models without test-period leakage, and reports comparable MAE/RMSE on one January 2024 window.

Historical outputs from the **original notebook**: ARIMA walk-forward RMSE **5,089.875** over four January weeks; neural-network R² **0.380** on a different 2023 holdout. These numbers are not directly comparable and **are not claimed as rerun results**. The cleaned notebook calculates new scores when executed.

## Run

```bash
python -m venv .venv
# Activate your virtual environment
pip install -r requirements.txt
jupyter notebook weekly_stock_forecasting.ipynb
```

Run cells from top to bottom. The first run downloads historical daily data through `yfinance` and stores a local CSV at `data/005380_KS_2023_2024.csv`. Subsequent runs use that CSV. If the provider is unavailable, supply a CSV with a date index and an `Adj Close` column for January 2023 through January 2024 at that path. `data/` is excluded from Git. See the [yfinance download documentation](https://ranaroussi.github.io/yfinance/reference/api/yfinance.download.html) for API details.

## Evaluation notes

- Weekly values are means of daily adjusted closing prices for weeks ending Friday.
- ARIMA refits after each observed January week. The neural network trains on 2023 and uses only prior observed values for each one-step January prediction.
- January has only four evaluation points. Provider price revisions and software versions can change reproduced values.
- Stock prices are difficult to predict reliably. This coursework is not financial advice or a trading strategy.
