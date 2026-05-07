# Airport Taxi Demand Prediction Model

Machine learning project for forecasting airport taxi demand for the next hour using historical order data from Sweet Lift Taxi.

The goal is to help anticipate peak demand periods so the company can attract more drivers when they are needed most.

## Live Dashboard

View the interactive dashboard here:

[Airport Taxi Demand Dashboard](https://lorena885.github.io/Airport-Taxi-Demand-Prediction-Model/)

The dashboard compares actual taxi orders against CatBoost predictions and includes a simple next-hour demand simulator.

## Project Objective

Sweet Lift Taxi collected historical taxi order data at airports. The task is to build a model that predicts the number of taxi orders for the next hour.

The required performance target was:

- Test RMSE must be less than or equal to 48.

## Dataset

The dataset is stored in:

```text
datasets/taxi.csv
```

Main column:

- `datetime`: timestamp of taxi orders.
- `num_orders`: number of taxi orders.

The original data was resampled into hourly intervals to create a time series forecasting dataset.

## Methodology

The project follows a time series machine learning workflow:

1. Load and inspect the taxi order dataset.
2. Convert the date column into a `DatetimeIndex`.
3. Sort the dataset chronologically.
4. Resample taxi orders into hourly totals.
5. Create time-based features:
   - year
   - month
   - day
   - day of week
   - lag features
   - rolling mean
6. Split the data chronologically, using the final 10% as the test set.
7. Train and compare several regression models.
8. Select the best model based on test RMSE.

## Models Tested

The following models were trained and evaluated:

- Linear Regression
- Random Forest Regressor
- Gradient Boosting Regressor
- CatBoost Regressor
- LightGBM Regressor

## Results

CatBoost achieved the best performance on the test set.

| Model | Test RMSE |
| --- | ---: |
| Linear Regression | 45.53 |
| Random Forest | 43.39 |
| Gradient Boosting | 44.55 |
| CatBoost | 40.90 |
| LightGBM | 42.75 |

Final selected model:

```text
CatBoostRegressor(
    iterations=500,
    learning_rate=0.05,
    depth=6,
    loss_function='RMSE',
    random_state=42
)
```

Final RMSE:

```text
40.90
```

This result is below the required threshold of 48, so the model meets the project objective.

## Key Insights

- Taxi demand shows strong hourly variability.
- Demand increases toward the end of the observed period.
- Lag features and rolling averages help capture recent demand patterns.
- CatBoost provided the strongest balance between predictive accuracy and generalization.
- The model can support operational planning by identifying likely high-demand hours.

## Repository Structure

```text
.
|-- catboost_info/
|-- dashboard/
|   |-- taxi_dashboard_summary.csv
|   |-- taxi_hourly_history.csv
|   `-- taxi_model_predictions.csv
|-- datasets/
|   `-- taxi.csv
|-- index.html
|-- notebook taxi demand.ipynb
|-- notebook taxi demand english.ipynb
|-- README.md
`-- requirements.txt
```

## Notebooks

- `notebook taxi demand.ipynb`: original project notebook in Spanish.
- `notebook taxi demand english.ipynb`: English version of the notebook.

## How to Run Locally

Clone the repository:

```bash
git clone https://github.com/Lorena885/Airport-Taxi-Demand-Prediction-Model.git
cd Airport-Taxi-Demand-Prediction-Model
```

Create and activate a virtual environment:

```bash
python -m venv .venv
.venv\Scripts\activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Open the notebook:

```bash
jupyter notebook "notebook taxi demand english.ipynb"
```

To view the dashboard locally, open:

```text
index.html
```

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- CatBoost
- LightGBM
- Jupyter Notebook
- HTML, CSS, and JavaScript

## Author

Created by [Lorena885](https://github.com/Lorena885).
