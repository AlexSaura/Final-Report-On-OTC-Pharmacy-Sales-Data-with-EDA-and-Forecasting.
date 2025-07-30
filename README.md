# OTC Sales Forecasting Capstone

## Project Overview
This capstone project forecasts weekly over-the-counter (OTC) pharmaceutical shipments using historical sales data. The goal is to support inventory planning and decision-making during seasonal or unpredictable demand surges.

## Objectives
- Analyze historical sales patterns across products and countries
- Build regression models to predict future shipment volumes
- Evaluate model performance using multiple error metrics
- Translate model results into actionable business insights

## Data Preparation
- Aggregated daily transactions into weekly sales
- Added lag features (previous week sales), rolling averages, and calendar variables (week, month)
- Checked and confirmed there were no missing values
- Created a `Time_Index` column for sequential modeling

## Exploratory Data Analysis (EDA)

### Weekly & Monthly Trends
- Line plots show fluctuations and seasonality in sales
- Detected outliers using IQR method, which may signal spikes tied to seasonal demand or emerging public health trends

### Country and Product Insights
- Top Countries by Revenue: USA, UK, and Canada
- Top Products by Volume: Digestive Enzyme and Antiseptic Cream

### Salesperson Performance
- Visualized shipment totals by salesperson. Rajesh Patel and Nikhil Batra were the top performers

### Distribution Analysis
- Weekly shipment distribution was slightly right-skewed
- Shapiro-Wilk test showed approximate normality (p > 0.05)

## Model Building

Two regression models were developed:
- **Random Forest Regressor**: A baseline model using only time index and an enhanced version using lag and calendar features
- **Support Vector Regressor (SVR)**: A base model and a tuned version using `GridSearchCV`

## Model Evaluation

The following metrics were used to evaluate model performance:

| Metric   | Description                                                                 |
|----------|-----------------------------------------------------------------------------|
| R² Score | Measures how well the model explains variance. Higher values are better.    |
| MSE      | Mean Squared Error. Emphasizes larger errors and is commonly used in model training. |
| RMSE     | Root Mean Squared Error. Same unit as the target variable and easier to interpret for business impact. |

### Final Model Results

| Model                     | R² Score | MSE       | RMSE    |
|---------------------------|----------|-----------|---------|
| Random Forest (Baseline)  | -0.0395  | 1845.8181 | 42.9630 |
| Random Forest (Enhanced)  | 0.1691   | 1474.9401 | 38.4049 |
| SVR (Baseline)            | 0.2992   | 1244.0200 | 35.2700 |
| SVR (Tuned)               | 0.3355   | 1179.6200 | 34.3500 |

### Interpretation:
- **Enhanced Random Forest** best explained variance in the data and captured short-term fluctuations
- **Tuned SVR** achieved the lowest RMSE and MSE, suggesting better error minimization
- Baseline models confirmed the necessity of feature engineering and tuning

## Forecasting

Both models were used to forecast the next 10 weeks:
- **Random Forest** generated more responsive forecasts that reflected spikes and dips, potentially useful for detecting real-time anomalies like public health events.
- **SVR** produced a smoother, flatter projection — helpful for establishing a stable expected baseline in planning scenarios.

## Key Findings
- Lag and calendar-based features significantly improved performance
- Random Forest better captured complexity and volatility in the data
- SVR minimized overall prediction error
- Outliers and extreme values may indicate early warning signs of health-related demand shifts
- Insights into top products, regions, and salespeople offer actionable operational value

## Recommendations
- Incorporate seasonal or exogenous features (e.g. holidays, weather, public health bulletins)
- Explore time series models such as ARIMA, Prophet, or LSTM
- Use hybrid models to combine interpretability and performance
- Apply anomaly detection on forecast residuals to flag abnormal patterns linked to public health changes

## Business Value
This forecasting pipeline provides stakeholders with a practical and interpretable tool for weekly shipment planning, offering:

- Smarter inventory allocation  
- Better preparedness for demand surges  
- Early detection of unusual sales behavior that may indicate public health events
