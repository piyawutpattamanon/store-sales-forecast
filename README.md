# Store Sales Forecasting

Predicting unit sales for thousands of items sold at Ecuadorian stores.

---

## Solution Overview

**Main notebook:** [`candidate.2.ipynb`](candidate.2.ipynb)

### Approach

Due to compute constraints, the solution focuses on a single representative item-store time series as a proof of concept.

**EDA findings:**
- Strong weekly seasonality in unit sales
- Promotion status and day-of-week are the most influential features
- No meaningful monthly or yearly seasonality detected
- The late-2016 sales spike is driven by promotion activity, not seasonality or oil price

**Feature engineering:**
- Day-of-week, day-of-month, month-of-year (one-hot encoded)
- Daily oil price (forward-filled for gaps)
- Promotion status
- 7-day and 30-day lagged moving averages

**Models trained:**
- **SARIMAX** — captures time series structure and weekly seasonality; hyperparameters tuned with `auto_arima`
- **XGBoost** — captures non-linear relationships across all engineered features; tuned with `GridSearchCV`
- **Ensemble** — simple average of tuned SARIMAX and tuned XGBoost
- **Baseline** — 30-day moving average

### Results (3-fold cross-validation RMSE)

| Model | RMSE |
|---|---|
| **Ensemble** | **7.01** |
| Tuned XGBoost | 7.32 |
| Tuned SARIMAX | 7.33 |
| Untuned XGBoost | 8.14 |
| MA30 Baseline | 8.43 |

All models outperform the baseline. Hyperparameter tuning significantly improves XGBoost. Ensembling reduces RMSE further beyond individual models.

---

## Getting Started

### 1. Get the data

The CSV input files are large and not stored in this repo. Download the compressed data files (.7z) from the link below and place them in the `7z/` folder:

> **Data download link:** _(to be added)_

### 2. Extract the CSVs

Install [7-Zip](https://www.7-zip.org/) (or `p7zip` on macOS/Linux), then extract all archives into the project root:

```bash
# macOS
brew install p7zip

# Extract all
cd 7z/
for f in *.7z; do 7z e "$f" -o../; done
```

After extraction, the root directory should contain:
```
train.csv
transactions.csv
items.csv
stores.csv
oil.csv
holidays_events.csv
```

### 3. Install dependencies

```bash
pip install pandas seaborn matplotlib scikit-learn statsmodels pmdarima xgboost
```

### 4. Run the notebook

Open `candidate.2.ipynb` in Jupyter and run all cells.

```bash
jupyter notebook candidate.2.ipynb
```

---

## Dataset Description

Predict `unit_sales` for thousands of items sold at different stores in Ecuador. Training data includes dates, store and item information, promotion status, and unit sales. Additional files provide supplementary information for feature engineering.

### File Descriptions

#### `train.csv`
- Target column: `unit_sales` by `date`, `store_nbr`, and `item_nbr`
- `unit_sales` can be integer or float (e.g., 1.5 kg of cheese)
- Negative values represent returns
- `onpromotion` indicates whether an item was on promotion (~16% are NaN)

#### `stores.csv`
- Store metadata: `city`, `state`, `type`, `cluster`
- `cluster` is a grouping of similar stores

#### `items.csv`
- Item metadata: `family`, `class`, `perishable`
- Perishable items have a score weight of 1.25; others are 1.0

#### `transactions.csv`
- Count of sales transactions per `date` and `store_nbr` (training period only)

#### `oil.csv`
- Daily oil price (Ecuador's economy is oil-dependent)

#### `holidays_events.csv`
- Holidays and events with metadata
- **Transferred** holidays officially fall on a date but were moved by the government — treat as normal days
- **Bridge** days extend holidays across long weekends, offset by **Work Day** entries

### Additional Notes
- Public sector wages are paid on the 15th and last day of each month — expect sales spikes
- A magnitude 7.8 earthquake hit Ecuador on April 16, 2016, causing unusual sales patterns for several weeks
