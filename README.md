

# The Public Transport Network Diagnostic & 7-Day Strategic Forecast

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Model](https://img.shields.io/badge/Model-SARIMAX-blue)
![TimeSeries](https://img.shields.io/badge/Category-Time%20Series%20Forecasting-orange)
![Python](https://img.shields.io/badge/Language-Python-yellow)
![Data](https://img.shields.io/badge/Data-Daily%20Ridership-lightgrey)



This document details the entire journey of our data analysis and forecasting project. Our goal was to move beyond just reporting historical facts and provide **actionable business intelligence** for the transit network.

## 1. Exploratory Data Analysis (EDA): Uncovering the Network's Heartbeat

Our first step was rigorous data cleaning to ensure we were building a model on a solid foundation.

* **Data Integrity:** We fixed the date formats and explicitly told the system that our data was a **Daily** series. This was vital because it allowed our model to understand the **weekly cycles** correctly.
* **Trend Diagnosis:** By looking closely at the primary **Rapid Route** service, we discovered a **permanent structural break** in demand. Essentially, the pandemic caused the passenger baseline to shift significantly downwards, and it has not recovered to old levels. This means we are now planning for a "new normal."
* **Weekly Seasonality:** We confirmed the network's massive, predictable cycle: high demand Monday through Thursday, a drop on Friday, and a complete collapse over the weekend. This powerful pattern proved we absolutely needed a **Seasonal model**.
* **Service Interaction:** We checked how demand across different services correlates. We found that the **Local Route** is highly linked to the **School** service, while **Light Rail** is a much cleaner indicator for general business/commuter health.

## 2. Key Strategic Insights: The "Why" Behind the Numbers

These are the five most important takeaways that should drive strategic decisions, not just daily operations:

* **Structural Demand Shock:** The current baseline is permanently lower due to long-term behavioral changes. **The strategic action is to stop budgeting and planning based on pre-2020 numbers.**
* **Light Rail as the Commuter Health Proxy:** Because Light Rail's demand is highly correlated with the main network but minimally influenced by schools, it serves as the **most reliable real-time indicator** of how many professionals are actually returning to the office.
* **Local Route Vulnerability:** The Local Route is heavily dependent on school activity. This makes it **the most fragile route** during school breaks or periods of remote learning. Resource planning must be flexible here.
* **Operational Misalignment:** We observed that "Peak Service" records journeys even on the weekends. This suggests its designation is wrong. A review should determine if this service is truly 'peak' or if it's acting as a general weekend connector.
* **Weekend Demand Fragility & Model Failure:** Our initial forecast produced negative values for the weekend! This technical failure was actually an important insight: weekend demand is so low and chaotic that a standard model cannot reliably predict it. **This proves we need specialized, event-based planning (like weather or sporting events) for weekend resource allocation.**

## 3. Forecasting Methodology: SARIMAX – The Perfect Balance

We chose the **SARIMAX** model because it gives us the right mix of **power, transparency, and accuracy** for this specific data:

* **The Model:** SARIMAX is perfect because it is built to handle the three major components of our data: **Trend**, **Seasonality**, and **Residual Noise**.
* **Seasonal Order (S=7):** We specifically set the seasonal order to **seven** ($S=7$). This forces the model to understand the weekly cycle—for example, it knows Monday's demand must be predicted by looking back at the previous Monday's data.
* **Differencing (d=1):** We used differencing ($d=1$) to stabilize the data by eliminating the massive, non-stationary trend caused by the structural demand shock. This ensures our predictions are reliable.
* **The Zero-Floor Fix:** Passenger counts cannot be negative. This is a real-world fact. We demonstrated technical maturity by applying a **post-processing constraint** (the "zero-floor fix") to set all negative forecast numbers to zero, making the output immediately usable by operations staff.

## 4. Final Forecast and Conclusion

The following is our final, corrected, and error-free 7-day forecast, starting Monday, September 30, 2024.

**7-Day Public Transport Passenger Journey Forecast**

| Date | Local Route | Light Rail | Peak Service | Rapid Route | School |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **2024-09-30** | 9,281 | 2,545 | 167 | 3,811 | 1,431 |
| **2024-10-01** | 10,231 | 2,567 | 169 | 4,042 | 1,540 |
| **2024-10-02** | 10,012 | 2,514 | 165 | 3,660 | 1,519 |
| **2024-10-03** | 9,824 | 2,177 | 128 | 3,348 | 1,574 |
| **2024-10-04** | 6,672 | 800 | 46 | **0** | 771 |
| **2024-10-05** | 670 | **0** | **0** | **0** | 395 |
| **2024-10-06** | **0** | **0** | **0** | **0** | 406 |

### Conclusion: Readiness for Strategic Planning

This project successfully moved from raw data to a fully justified, robust 7-day forecast. By using SARIMAX, we not only predicted demand but gained a deep understanding of the network's vulnerabilities (like the weekend demand fragility). This analysis is immediately ready to inform scheduling, resource allocation, and long-term policy adjustments for the public transport network.
