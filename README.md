# Rainfall Forecasting

Forecasts the next 12 months of rainfall using ARIMA (SARIMAX), SimpleRNN and LSTM. The best model is picked automatically for each target using RMSE.

## What it predicts
- Total monthly rainfall (mm)
- Highest rainfall in a single day for each month (mm)

## Project structure
```
rainfall-forecast/
|-- notebook 
|   |-- rainfall_forecast.ipynb
|-- README.md
|-- data/
|   |-- rainfall-monthly-total.csv
|   |-- rainfall-monthly-number-of-rain-days.csv
|   |-- rainfall-monthly-highest-daily-total.csv
|-- next_year_forecast.csv      (created after running the notebook)
```

## Data
The `data/` folder contains the three monthly CSV files used by the notebook:

| File | Description |
|------|-------------|
| `rainfall-monthly-total.csv` | Total rainfall per month |
| `rainfall-monthly-number-of-rain-days.csv` | Number of rainy days per month |
| `rainfall-monthly-highest-daily-total.csv` | Highest daily rainfall per month |

All files are joined using the `month` column.

## How it works
1. Load and merge the three CSV files
2. Check for missing values and duplicates
3. Convert `month` to a date index
4. Explore the data (histogram, pairplot, boxplot, heatmap)
5. Train ARIMA, RNN and LSTM on all data except the last 12 months
6. Compare the models with RMSE and choose the best one
7. Retrain the best model on all data and forecast the next 12 months
8. Save the forecast to `next_year_forecast.csv`

## Setup
```bash
pip install numpy pandas matplotlib seaborn scikit-learn statsmodels tensorflow jupytergit
```

## How to run
1. Keep the CSV files inside the `data/` folder.
2. In the notebook, make sure the file paths point to the `data/` folder:
   ```python
   total_rainfall = pd.read_csv("data/rainfall-monthly-total.csv")
   no_of_rainy_days = pd.read_csv("data/rainfall-monthly-number-of-rain-days.csv")
   maximum_rainfall_in_day = pd.read_csv("data/rainfall-monthly-highest-daily-total.csv")
   ```
3. Open the notebook:
   ```bash
   jupyter notebook rainfall_forecast.ipynb
   ```
4. Run all cells (Kernel > Restart and Run All).

Google Colab: upload the `data` folder to the Colab files panel, then run all cells.

## Output
`next_year_forecast.csv` with the columns:
- Month
- Total Rainfall (mm)
- Highest Rainfall In A Day (mm)

## Notes
- Neural network results can change slightly on every run.
- Forecasts are clipped at 0 because rainfall cannot be negative.
- Later months are less reliable because the RNN and LSTM predict one month at a time.
