# Retail Sales Forecasting for Walmart’s Hobbies Category

# 🌟 Overview  

## **Problem Statement and Objective**  
Accurate forecasting is critical for Walmart to maintain optimal inventory, enhance financial planning, and support strategic investments. Without reliable forecasts, businesses risk overstocking, revenue loss, and missed strategic opportunities.

For this project, we forecast unit sales for items in Walmart's “Hobbies_1” department using a hierarchical dataset that includes daily sales, pricing, promotions, and event calendars.

**Objective:**  
Generate accurate 28-day point forecasts (April 25, 2016 to May 22, 2016) to support inventory and supply chain decisions.

**Target Audiences:**  
- Inventory Planners  
- Supply Chain Operators  
- Operations Managers

## **Methodology**  
Our approach integrates traditional time series models such as ARIMA and SARIMAX with advanced machine learning techniques, Long Short-Term Memory (LSTM) networks, Prophet, and LightGBM. This hybrid modeling approach allows us to effectively capture both linear trends and intricate seasonal patterns within the dataset, resulting in highly accurate and actionable forecasts. The resulting predictions will be critical for strategic inventory management and resource allocation. By anticipating demand fluctuations accurately, Walmart can improve its operational efficiency and reduce waste.

## **Dataset**  
- **Data Description**: This dataset contains historical sales records from 45 Walmart stores across regions. It includes detailed information on sales performance at the department and item levels, along with factors influencing demand. 
- **Key Features**  
  - Time-Series Data: Daily sales records for multiple products over several years  
  - Store & Product Details: Information on different Walmart stores and product categories  
  - Price Data: Historical pricing information for various products
  - Calendar Data: Includes events, holidays, and other factors influencing sales trends  
- **Source**: https://www.kaggle.com/competitions/m5-forecasting-accuracy

---


# 💡 Key EDA Insights

EDA insights guide our feature engineering and model selection, ensuring models align closely with business objectives and deliver improved forecasting accuracy.
Here is the sample of EDA: [https://github.com/katarinaa19/Walmart-Store-Sales-Forecasting/blob/main/eda-insights.md](https://github.com/katarinaa19/Walmart-Store-Sales-Forecasting/blob/main/EDA/eda-insight.md)

- Model Selection
  - Prophet: Automatically models weekly and yearly seasonality; ideal for strong weekly cycles and holiday effects.
  - SARIMA/SARIMAX: Effective for one or two dominant seasonalities (e.g., weekly, yearly) but may struggle with overlapping cycles.
  - Tree-Based Models (LightGBM/XGBoost): Powerful for non-linear relationships; require engineered features (e.g., sine/cosine transformations) to capture cyclicality.
  - Decomposition Approaches: Choose additive vs. multiplicative models based on whether seasonal effects remain constant or grow with the trend.

- Feature Engineering
  - Lagged & Rolling Features: Use lags (e.g., lag_7) and rolling averages/stds to capture recurring weekly patterns and volatility.
  - Cyclical Transformations: Create sine and cosine features to represent 6–7 day cycles.
  - Event-Based Features: Add binary flags or dummy variables for holidays and promotions to capture event-driven effects.
  - Distribution Transformations: Apply log transformation to stabilize variance in right-skewed sales data.
  - Weekday Patterns: Include day-of-week as a categorical variable to capture differences between weekdays and weekends.

---

# 🔍 Model Performance Summary

| Model       | RMSE   | MAE    | MAPE  |
|-------------|--------|--------|-------|
| ETS+ARIMA   | 265.53 | 187.57 | 4.80% |
| SARIMAX     | 246.07 | 187.22 | 4.91% |
| Prophet     | 248.14 | 178.69 | 4.86% |
| LightGBM    | 248.05 | 181.68 | 4.90% |

### Prophet
**Overview:**  
Developed by Facebook (Meta), Prophet decomposes time series into trend, seasonality, and holiday effects. Robust to missing data, outliers, and strong seasonalities.

**Modeling Strategy:**  
Optimized via grid search and time-series cross-validation.  
Used Tweedie deviance loss to handle skewed, positive sales data.  
Final model favors many changepoints (50), low changepoint flexibility, and strong multiplicative seasonality.

![image](https://github.com/user-attachments/assets/8a6dc530-ebe1-463f-983f-091acf4a9c3f)

### LightGBM
**Overview:**  
A tree-based model using histogram-based learning for fast training. Captures nonlinear interactions among promotions, prices, holidays, and past sales — ideal for large, item-level sales datasets.

**Modeling Strategy:**  
Engineered lag features, rolling stats, price normalization, and calendar effects.  
Optimized hyperparameters via Bayesian Optimization.  
Adopted recursive forecasting with dynamic feature updating to adapt to new trends.

![image](https://github.com/user-attachments/assets/86fb80c6-89b3-438e-ac86-fc54b70f8a0e)

### SARIMAX
**Overview:**  
Extends ARIMA by modeling seasonality and incorporating exogenous factors like weekends, lagged sales (`Sales_lag7`), and rolling means (`Sales_rolling_mean_7`). Especially effective for datasets with weekly seasonality (`S=7`).

**Modeling Strategy:**  
Trained with seasonal orders and external regressors to improve predictive accuracy and capture recurring sales fluctuations.

![image](https://github.com/user-attachments/assets/65d8d0b5-1e72-4131-ac77-e26878562254)

### ETS + ARIMA
**Overview:**  
A two-stage approach where ETS captures level, trend, and seasonality, while ARIMA models residual autocorrelation for finer adjustments. Suitable for series with both systematic seasonal patterns and subtle dependencies.

**Modeling Strategy:**  
First fit ETS to remove primary structure, then fit ARIMA on residuals to capture remaining patterns.

![Uploading image.png…]()




 
