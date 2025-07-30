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
- Detected outliers using IQR method, potentially tied to seasonal demand

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
- Random Forest Regressor: A baseline model using only time index and an enhanced version using lag and calendar features
- Support Vector Regressor (SVR): A base model and a tuned version using GridSearchCV

## Model Evaluation

The following metrics were used to evaluate model performance:

| Metric | Description |
|--------|-------------|
| R² Score | Measures how well the model explains variance. Higher values are better. |
| MSE | Mean Squared Error. Emphasizes larger errors and is commonly used in model training. |
| RMSE | Root Mean Squared Error. Same unit as the target variable and easier to interpret for business impact. |

### Final Model Results

| Model                     | R² Score | MSE       | RMSE    |
|---------------------------|----------|-----------|---------|
| Random Forest (Baseline)  | -3.1522  | 5601.6022 | 74.8260 |
| Random Forest (Enhanced)  | 0.6109   | 1474.9481 | 38.4049 |
| SVR (Baseline)            | 0.2092   | 1244.6000 | 35.2700 |
| SVR (Tuned)               | 0.2355   | 1179.5200 | 34.3500 |

Interpretation:
- Enhanced Random Forest best explained variance in the data
- Tuned SVR achieved the lowest RMSE and MSE, indicating smaller average prediction errors
- Baseline models confirmed the necessity of feature engineering and tuning

## Forecasting

Both models were used to forecast the next 10 weeks:
- Random Forest captured short-term variation but was more volatile
- SVR delivered smoother forecasts, useful for high-level planning

## Key Findings
- Lag and calendar-based features significantly improved performance
- Random Forest was better at capturing spikes and complex patterns
- Tuned SVR minimized prediction error
- Insights into top products, regions, and salespeople offer operational value

## Recommendations
- Incorporate seasonal or exogenous features such as holidays and public health events
- Explore time series models such as ARIMA, Prophet, or LSTM
- Consider hybrid models for more robust predictions
- Apply anomaly detection on model residuals

## Business Value
This model provides stakeholders with actionable forecasts for weekly box shipments, allowing for:
- Smarter inventory allocation
- Improved planning for demand surges
- Identification of unusual sales behavior
