# Retail Sales Forecasting for Walmart’s Hobbies Category

# 🌟 Overview  

## **🎯Problem Statement and Objective**  
- Sales patterns fluctuate seasonally, directly affecting profitability. Accurate forecasting helps businesses anticipate demand, manage inventory, and make strategic financial decisions. Without reliable forecasts, companies risk overstocking, revenue loss, and missed strategic opportunities. For Walmart, precise forecasting is essential to maintain optimal inventory, enhance financial planning, and support data-driven pricing and investments.

- For the project, we aim to forecast unit sales for items in Walmart's “Hobbies_1” department using a hierarchical dataset that includes daily sales, pricing, promotions, and other key features. Our primary goal is to generate accurate 28-day point forecasts (April 25, 2016, to May 22, 2016) to enhance inventory management and support strategic business decisions. The target audiences are the inventory planners, supply chain operators, and operations managers. These people rely on reliable predictions to optimize inventory levels and avoid costly stock outs or overstock situations.

## **🛠️ Methodology**  
Our approach integrates traditional time series models such as ARIMA and SARIMAX with advanced machine learning techniques, Long Short-Term Memory (LSTM) networks, Prophet, and LightGBM. This hybrid modeling approach allows us to effectively capture both linear trends and intricate seasonal patterns within the dataset, resulting in highly accurate and actionable forecasts. The resulting predictions will be critical for strategic inventory management and resource allocation. By anticipating demand fluctuations accurately, Walmart can improve its operational efficiency and reduce waste.

## **📂Dataset**  
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

## 🔍 Implementation Steps  
1️⃣ **Data Collection & Preprocessing** – Cleaning and structuring the dataset for analysis.  
2️⃣ **Exploratory Data Analysis (EDA)** – Identifying seasonal patterns and trends.  
3️⃣ **Feature Engineering** – Creating meaningful variables to improve model accuracy.  
4️⃣ **Model Selection & Training** – Testing various forecasting models.  
5️⃣ **Evaluation & Optimization** – Measuring accuracy and fine-tuning the best-performing model.  
6️⃣ **Deployment & Insights** – Providing actionable insights for Walmart’s decision-makers.  

---

## 🎯 Expected Outcomes  
✅ **Accurate sales predictions** to enhance decision-making.  
✅ **Optimized stock levels** to minimize excess inventory costs.  
✅ **Improved revenue forecasting** for financial planning.  
✅ **Strategic business insights** for Walmart’s leadership team.  

---

## 🚀 Future Enhancements  
🚀 Expand the model to include **other product categories**.  
📊 Integrate **macroeconomic factors and competitor pricing** into predictions.  
⚡ Automate the forecasting process with **real-time data updates**.  

---

