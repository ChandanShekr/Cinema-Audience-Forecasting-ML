# Cinema Audience Forecasting

## Problem Statement
This project tackles a **Time-Series Forecasting** problem to predict daily audience counts for various theaters. By leveraging historical booking data from two distinct platforms, we aim to build a robust predictive model.

The dataset consists of:
*   **BookNow**: An online aggregator for browsing and booking tickets in advance.
*   **CinePOS**: An on-premise Point-of-Sale system used at box offices for walk-in tickets.

## Dataset Overview

| File Name | Description | Key Features |
| :--- | :--- | :--- |
| `booknow_visits.csv` | **Target Variable**. Daily footfall per theater. | `book_theater_id`, `show_date`, `audience_count` |
| `booknow_bookings.csv` | Transactional logs from the online platform. | `booking_datetime`, `tickets_booked` |
| `cinePOS_booking.csv` | Transactional logs from the POS system. | `booking_datetime`, `tickets_booked` |
| `date_info.csv` | Contextual calendar data. | `holiday_flag`, `weekend_flag` |
| `*_theaters.csv` | Metadata for theaters on both platforms. | Location, screens, capacity details. |
| `movie_theater_id_relation.csv` | Bridge table linking the two platforms. | Maps `BookNow_ID` to `CinePOS_ID`. |

## Solution Architecture

### 1. Data Preprocessing & Validation
*   **Data Integration**: Merged online (BookNow) and offline (CinePOS) data streams using the relation mapping file.
*   **Cleaning**: Handled missing values and standardized datetime formats.
*   **Outlier Detection**: Identified and treated anomalies in daily booking counts to prevent model skew.

### 2. Exploratory Data Analysis (EDA)
*   **Seasonality Analysis**: Decomposed the time series to observe weekly and monthly attendance patterns.
*   **Correlation Heatmaps**: Analyzed the relationship between advance bookings (BookNow) and walk-ins (CinePOS).
*   **Rolling Statistics**: Visualized 7-day and 14-day moving averages to understand short-term trends.

### 3. Feature Engineering
To capture the temporal dynamics of the data, the following features were generated:
*   **Lag Features**: Values from previous days (t-1, t-7, t-30) to capture autocorrelation.
*   **Rolling Window Statistics**: Mean and standard deviation over 7, 14, and 28-day windows.
*   **Calendar Features**: Day of week, month, quarter, and holiday flags to capture weekend spikes and festive trends.

### 4. modeling Strategy
Employed a diverse set of regression algorithms to minimize the error:
*   **Baseline - Ridge Regression**: A regularized linear model to establish a baseline and capture linear dependencies.
*   **Ensemble Methods**:
    *   **RandomForest Regressor**: Bagging technique to reduce variance and handle non-linear interactions.
    *   **Gradient Boosting (XGBoost & LightGBM)**: Sequential boosting algorithms optimized for performance and speed, highly effective for tabular time-series data.

### 5. Evaluation & Tuning
*   **Hyperparameter Tuning**: Utilized `GridSearchCV` to optimize estimators, learning rates, and tree depths.
*   **Metric**: The primary evaluation metric is **R2 Score**

## Project Structure
```
├── dataset/                   # CSV Data files (Not managed by git)
├── cinema audience...ipynb    # Main analysis and modeling notebook
├── README.md                  # Project documentation
└── .gitignore                 # Files to exclude from version control
```
