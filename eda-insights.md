# Key EDA Insights

Below are the major findings from our exploratory data analysis. These insights come from time-series plots, moving averages, FFT analysis, decomposition, rolling statistics, and correlation heatmaps.

---

## 1. Time-Series Trends & Moving Averages

- **Overall Sales Trend (2011–2016):**  
  Daily sales show a general upward trajectory, with some notable fluctuations over time.

- **7-Day & 30-Day Moving Averages:**  
  - **7-day MA** highlights weekly seasonality.  
  - **30-day MA** captures broader, monthly variations.

**Key Takeaway:**
Walmart’s sales exhibit both short-term (weekly) and longer-term (monthly or seasonal) patterns. These moving averages confirm recurring demand cycles, as well as an overall growth trend.

![image](https://github.com/user-attachments/assets/d46108e3-8060-4ab8-b177-d3a4da8d8f3a)

---

## 2. Time-Series Decomposition Analysis

1. **Original Series (Blue)**  
   - Raw daily sales from 2011 to 2016.  
   - Noticeable spikes often coincide with holidays, promotions, or other anomalies.

2. **Trend Component (Red)**  
   - Reflects the long-term movement in sales.  
   - Overall upward slope indicates steady growth, with occasional dips or rebounds.

3. **Seasonal Component (Green)**  
   - Captures repeating cycles (e.g., weekly, annual).  
   - Consistent peaks/troughs often align with weekends, holidays, or monthly shopping habits.

4. **Residual Component (Black)**  
   - What remains after removing trend and seasonality.  
   - Ideally appears random; large spikes may suggest unmodeled events or outliers.

**Key Takeaway:**
- **Strong Weekly/Monthly Seasonality:** Repeating cycles confirm a regular pattern in sales volumes.  
- **Overall Growth Trend:** A steady upward slope, though some periods show slower growth.  
- **Residual Spikes:** Indicate events or promotions that aren’t captured by simple trend/seasonality modeling.

- **7-day**  
  ![image](https://github.com/user-attachments/assets/4c510fcd-8f4a-47b0-8b8e-69b8c2466506)  
- **30-day**  
  ![image](https://github.com/user-attachments/assets/a0e78e4d-6a05-4936-8cf5-0e7d39bcf80f)  
- **90-day**  
  ![image](https://github.com/user-attachments/assets/e8cb2676-bb52-4e16-aca2-4c81c54b60e6)

---

## 3. Power Spectrum Analysis (FFT)

- **Dominant Cycles Identified:**  
  - A **6–7 day** cycle highlights a strong weekly pattern.  
  - Weekly seasonality is common in retail and e-commerce (weekend vs. weekday shopping).

### Practical Implications
- **Prophet:** Automatically handles yearly and weekly seasonality.  
- **SARIMA / SARIMAX:** Manages one or two major seasonalities (weekly, yearly), but multiple overlapping cycles can be complex.  
- **Tree Models (LightGBM / XGBoost):** Require feature engineering (e.g., sine/cosine transformations) to capture dominant periods.

![image](https://github.com/user-attachments/assets/e30ec9c9-70ef-46f2-afda-751bf827a9ee)


---

## 4. Variance Analysis

- **Rolling Standard Deviation:**  
  - Reveals how sales volatility changes over different windows (3-day vs. 30-day).  
  - Periodic spikes may reflect promotions or holiday effects.

- **Sales Distribution:**  
  - Right-skewed distribution with moderate daily sales and occasional spikes.  
  - Log-Transformed distribution is more symmetric, often aiding modeling.

**Key Takeaway:**
Sales volatility is not constant. A log transform can help stabilize variance, and capturing volatility patterns (via rolling std) may improve forecast accuracy.

![image](https://github.com/user-attachments/assets/a8a77e48-74b9-426a-a0ea-76c676e300a1)

---

## 5. Weekday Patterns (Store TX_3, WI_1)

- **Weekly Sales Patterns:**  
  - Typically higher sales on weekends (e.g., Saturday) vs. certain weekdays (e.g., Monday).  
  - Trendlines show a gradual rise over the week.

**Key Takeaway:**
Including weekday features is essential to capture these intra-week fluctuations and plan inventory or staffing accordingly.

![image](https://github.com/user-attachments/assets/13455a61-dd30-4114-9fb2-cef1176c9c38)
![image](https://github.com/user-attachments/assets/88828fb6-1a4b-4eda-a61f-09e4f9fc5815)

---

## 6. Correlation Heatmap (Store CA_1, TX_1)

- **Lag & Rolling Feature Correlations:**  
  - Certain lags (e.g., lag_7) and rolling means (e.g., rolling_mean_7) are strongly correlated.  
  - Some rolling std features (e.g., rolling_std_14 vs. rolling_std_30) overlap.

**Key Takeaway:**
While lagged and rolling features capture weekly patterns, too many similar features can introduce redundancy. **PCA** or careful feature selection may be necessary to avoid overfitting.

![image](https://github.com/user-attachments/assets/794800e3-d5c5-4338-af12-38c69c13a4d0)
![image](https://github.com/user-attachments/assets/e39ed5ce-f089-452c-a541-991d140127e2)

---

## 7. Impact of Events on Sales

- **Event vs. Non-Event Days:**  
  - Special events or promotions can significantly shift sales.  
  - The effect varies by store, highlighting regional or demographic factors.

**Key Takeaway:**
Incorporating holiday or event-based features is crucial for accurate forecasting. Such days often create sales spikes or dips beyond normal trends.

![image](https://github.com/user-attachments/assets/54836e67-1b48-42b5-a281-e82931004bfb)

---

## Overall Conclusions

1. **Strong Weekly Seasonality:**  
   Both moving averages and FFT confirm a 7-day cycle.
2. **Event & Holiday Effects:**  
   Special events have a marked impact on sales.
3. **Feature Redundancy:**  
   Lagged and rolling features are useful but may overlap, so careful feature selection is required.

These insights guide our feature engineering and model selection to improve forecasting accuracy.

---

