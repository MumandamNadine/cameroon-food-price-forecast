# Cameroon Food Price Forecast

A time-series analysis and forecasting project using monthly food-price estimates for Cameroon.

The project focuses on predicting the prices of beans and maize in the Bamenda market using historical prices from January 2007 to June 2026.

## Research Question

Can historical monthly prices help estimate the next month’s prices of beans and maize in Bamenda, Cameroon?

## Data Source

World Bank Cameroon Monthly Food Price Estimates:

* 83 Cameroon markets
* Monthly data from 2007 to 2026
* Currency: XAF
* Products include beans, cassava, and maize
* Prices are market-price estimates based on publicly available WFP, FAO, and national data

Source: [World Bank Cameroon Food Prices](https://microdata.worldbank.org/catalog/4487)

## Data Preparation

The analysis:

* loaded the CSV file with pandas;
* handled the file’s Latin-1 encoding;
* converted price dates into monthly datetime values;
* filtered the data to the Bamenda market;
* selected beans and maize price columns;
* checked missing months;
* created lag and rolling-average features;
* used chronological train/test splitting.

## Forecasting Methods

The following methods were compared:

1. Seasonal naïve forecasting
2. Previous-month forecasting
3. Three-month moving average
4. Random Forest regression
5. Exponential Smoothing

The final 12 months of known observations were used as the test period. The data was not randomly shuffled because future observations must not be used to predict the past.

## Model Results

| Product | Selected method         |          MAE |  MAPE |
| ------- | ----------------------- | -----------: | ----: |
| Beans   | Random Forest           | 34.11 XAF/kg | 5.59% |
| Maize   | Previous-month forecast | 11.66 XAF/kg | 4.41% |

Random Forest performed best for beans. For maize, the simpler previous-month method performed slightly better than Random Forest.

## Example Forecast

The latest actual observations ended in June 2026.

The first forecast after the last known observation was:

| Product | Forecast price |
| ------- | -------------: |
| Beans   |  599.38 XAF/kg |
| Maize   |  233.55 XAF/kg |

The 12-month forecast is saved in:

```text
bamenda_price_forecast.csv
```

The model comparison is saved in:

```text
model_evaluation.csv
```

## Limitations

* The price dataset contains estimates and modeled values, not only direct measurements.
* Bamenda-Nkwen has too few observations for a reliable forecast.
* Cassava has no usable observations for the selected markets.
* The forecast does not include rainfall, inflation, exchange rates, transport costs, or harvest information.
* The evaluation uses one 12-month test period, so future validation would improve confidence.
* Long-term forecasts should be treated as estimates rather than guaranteed prices.

## Project Structure

```text
cameroon-food-price-forecast/
├── price_analysis.py
├── market_prices.csv
├── bamenda_price_forecast.csv
├── model_evaluation.csv
├── requirements.txt
└── README.md
```

## Technologies

* Python
* pandas
* NumPy
* Matplotlib
* scikit-learn
* statsmodels

## Installation

```bash
python -m pip install -r requirements.txt
```

## Author

Ntsang Nadine Mumandam Che
