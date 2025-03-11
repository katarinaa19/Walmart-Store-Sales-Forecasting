# Key EDA Insights

Below are the major findings from our exploratory data analysis. These insights are drawn from various visualizations including time-series trends, moving averages, FFT analysis, distribution plots, and correlation heatmaps.

---

## 1. Time-Series Trends & Moving Averages

- **Overall Sales Trend (2011–2016):**  
  Daily sales data show a general upward trend with noticeable fluctuations over time.
  
- **7-Day & 30-Day Moving Averages:**  
  - The 7-day moving average highlights weekly seasonality.
  - The 30-day moving average captures broader, monthly variations.

**Key Takeaway:**  
Walmart’s sales display both short-term (weekly) and long-term (monthly/seasonal) patterns.

![image](https://github.com/user-attachments/assets/d46108e3-8060-4ab8-b177-d3a4da8d8f3a)

---

## 2. Power Spectrum Analysis (FFT)

- **Dominant Cycles Identified:**  
  - The graph reveals a distinct 6-7 day cycle, highlighting a strong weekly pattern.
  - This cycle is very common in retail, e-commerce, and other business scenarios, often reflecting differences in weekend versus weekday behavior or recurring weekly purchasing patterns.

**Takeaways on Model Choice:**
- **Prophet:** Automatically models both yearly and weekly seasonality, making it a strong candidate.
- **SARIMA / SARIMAX:** These models can handle one or two major seasonalities (such as weekly or yearly), but managing multiple overlapping cycles might be challenging.
- **Tree Models (LightGBM / XGBoost):** Typically require feature engineering, such as creating sine/cosine transformations to capture each dominant period.

![image](https://github.com/user-attachments/assets/f798ec41-3bf3-44ab-b0af-c83a9d05020b)

---

## 3. Rolling Standard Deviation & Distribution

- **Rolling Standard Deviation:**  
  - Variability in daily sales changes over different windows (e.g., 3-day vs. 30-day).
  - Periodic spikes hint at effects from promotions or holidays.
  
- **Sales Distribution:**  
  - The data is right-skewed, with most days showing moderate sales and some days showing spikes.
  - A log-transformed distribution appears more symmetric.

**Key Takeaway:**  
Sales volatility is not constant. A log transformation might stabilize variance and improve predictive modeling.

![image](https://github.com/user-attachments/assets/a8a77e48-74b9-426a-a0ea-76c676e300a1)

---

## 4. Weekday Patterns (Example: Store TX_3)

- **Weekly Sales Patterns:**  
  - Higher sales are observed on weekends (e.g., Saturday) with lower sales on some weekdays (e.g., Monday).
  - A trendline shows a gradual upward trend over the week.
  
**Key Takeaway:**  
Weekday feature is needed to capture the variability.

![image](https://github.com/user-attachments/assets/13455a61-dd30-4114-9fb2-cef1176c9c38)


---

## 5. Correlation Heatmap (Example: Store CA_1)

- **Lag & Rolling Feature Correlations:**  
  - Strong correlations exist between certain lagged features (e.g., lag_7) and rolling means (e.g., rolling_mean_7).
  - Some rolling standard deviations (e.g., rolling_std_14 vs. rolling_std_30) indicate overlapping information. PCA might required if creating too much of the rolling/lagged features.

**Key Takeaway:**  
Lagged features and rolling statistics effectively capture the recurring weekly patterns, though some may be redundant.

![image](https://github.com/user-attachments/assets/794800e3-d5c5-4338-af12-38c69c13a4d0)

---

## 6. Impact of Events on Sales

- **Event vs. Non-Event Days:**  
  - Sales differ on days with special events or promotions.
  - The effect of events is store-dependent, reflecting localized factors.

**Key Takeaway:**  
Incorporating event-based features is essential to accurately forecast sales, as holidays and promotions can significantly affect performance.

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

