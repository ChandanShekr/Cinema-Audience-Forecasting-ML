# Cinema Audience Forecasting

## Problem Statement
In this project, we tackle a time-series forecasting problem to predict cinema audience attendance. The goal is to optimize operations and marketing by accurately forecasting how many people will visit theaters.

The data is sourced from two separate booking platforms:
*   **BookNow**: An online booking and aggregation platform for advance ticket booking.
*   **CinePOS**: A Point-of-Sale (POS) system installed at theaters tracking on-site ticket sales.

## Dataset
The project utilizes the following datasets:
*   `cinePOS_theaters.csv`: Information about theaters using CinePOS.
*   `booknow_theaters.csv`: Information about theaters on BookNow.
*   `movie_theater_id_relation.csv`: Mapping table to link BookNow and CinePOS theaters.
*   `cinePOS_booking.csv`: Transactional data for CinePOS bookings.
*   `booknow_booking.csv`: Transactional data for BookNow bookings.
*   `booknow_visits.csv`: Daily audience counts (target variable).
*   `date_info.csv`: Calendar information (holidays, weekends, etc.).
*   `sample_submission.csv`: Format for the final submission.

## Solution Approach

### 1. Exploratory Data Analysis (EDA)
*   **Data Quality**: Checked for missing values and data consistency.
*   **Trend Analysis**: Analyzed daily audience traffic variations.
*   **Feature Engineering**: Created rolling statistics (e.g., 7-day and 14-day moving averages) to capture temporal trends and seasonality.

### 2. Modeling
A robust machine learning pipeline was developed using a mix of linear and non-linear models to capture different data patterns:
*   **Linear Model**: `Ridge Regression` (L2 regularization) to capture linear potential trends.
*   **Tree Ensembles**: 
    *   `RandomForestRegressor`: For capturing non-linear relationships and interactions.
    *   `XGBoost` & `LightGBM`: Gradient boosting machines for high-performance forecasting.

### 3. Model Tuning & Evaluation
*   **Cross-Validation**: Used `GridSearchCV` to find optimal hyperparameters (e.g., tree depth, learning rates).
*   **Metrics**: Models are evaluated using **R2 Score** and **Root Mean Squared Error (RMSE)**.

## Getting Started

### Prerequisites
Ensure you have Python installed with the following libraries:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost lightgbm
```

### Usage
1.  Clone this repository.
2.  Ensure the dataset files are located in the `dataset/` directory.
3.  Open `cinema audience forecasting ml.ipynb`.
4.  Update the data path variable if necessary:
    ```python
    BASE = "./dataset/"
    ```
5.  Run all cells to execute the training pipeline and generate forecasts.
