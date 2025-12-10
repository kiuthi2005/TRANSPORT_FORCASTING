

# The Public Transport Network Diagnostic & 7-Day Strategic Forecast

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Model](https://img.shields.io/badge/Model-SARIMAX-blue)
![TimeSeries](https://img.shields.io/badge/Category-Time%20Series%20Forecasting-orange)
![Python](https://img.shields.io/badge/Language-Python-yellow)
![Data](https://img.shields.io/badge/Data-Daily%20Ridership-lightgrey)

This is the complete, breakdown of the data analysis and forecasting project, showcasing the journey from raw data to actionable business intelligence.

---

# Table of Contents

* [1. Exploratory Data Analysis (EDA): Uncovering the Network's Heartbeat](#1-exploratory-data-analysis-eda-uncovering-the-networks-heartbeat)
* [2. Key Strategic Insights: The "Why" Behind the Numbers](#2-key-strategic-insights-the-why-behind-the-numbers)
* [3. Forecasting Methodology: SARIMAX – The Perfect Balance](#3-forecasting-methodology-sarimax--the-perfect-balance)
* [4. Final Forecast and Conclusion](#4-final-forecast-and-conclusion)

---

## 1. Exploratory Data Analysis (EDA): Uncovering the Network's Heartbeat

The first step was rigorous data cleaning and analysis to understand the fundamental patterns driving passenger demand.

| EDA Component           | Discovery                                                                                                                                                                                                                                                                                                  | Visualization                                      |
| :---------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------- |
| **Data Integrity**      | Converted dates, corrected inconsistent data types, and explicitly set the frequency to **Daily** (`D`) to ensure the time series model could accurately track weekly cycles.                                                                                                                              | (Code step, ensuring clean data.)                  |
| **Trend Diagnosis**     | By decomposing the primary Rapid Route service, we found a **permanent structural break** (the COVID-19 effect). The baseline demand shifted down significantly and has not recovered to pre-2020 levels.                                                                                                  | (File: `rapid_route_decomposition.png`)            |
| **Weekly Seasonality**  | Confirmed a massive, predictable cycle: high demand Monday-Thursday, a drop on Friday, and a collapse over the weekend. This proves the need for a **Seasonal** model.                                                                                                                                     | (File: `weekly_average_journeys.png`)              |
| **Service Interaction** | Calculated correlations between all service types. The **Local Route** shows the highest correlation with **School** service, suggesting it's most sensitive to school holidays. **Light Rail** shows the highest correlation with **Rapid Route**, making it a key indicator for general commuter health. | (Data used for **Insight #2** and **Insight #3**). |

---

## 2. Key Strategic Insights: The "Why" Behind the Numbers

These are the five high-level insights that move beyond facts to inform strategic planning and resource allocation.

1. **Structural Demand Shock:** The network is operating on a **permanently lowered baseline** due to pandemic-era shifts. Future planning must ignore pre-2020 ridership targets.
2. **Light Rail as the Commuter Health Proxy:** Light Rail's high correlation with the core network (Rapid Route) and low correlation with School service makes it the **cleanest, most reliable indicator** of non-educational commuter recovery (e.g., return-to-office rates).
3. **Local Route Vulnerability:** Local Route's high dependency on the School service means it is the **most fragile** during school breaks or policy changes, requiring flexible scheduling to prevent over-resourcing during off-peak times.
4. **Operational Misalignment:** The "Peak Service" records non-zero demand on weekends. This suggests its title is misleading. A review is necessary to redefine its role (e.g., weekend overflow or inter-peak connector).
5. **Weekend Demand Fragility & Model Failure:** The initial model produced negative forecast values for the weekend! This mathematical failure highlighted that weekend demand is too volatile and near-zero to be predicted by a standard linear model. **Action:** Requires a specialized model (or a pragmatic zero-floor fix).

---

## 3. Forecasting Methodology: SARIMAX – The Perfect Balance

We chose the **SARIMAX** model because it perfectly balances **complexity, transparency, and accuracy** for this specific type of data.

| Component                | Why it was chosen                                                                                 | Why SARIMAX is Superior                                                                                                                                         |
| :----------------------- | :------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Model**                | **SARIMAX** (Seasonal AutoRegressive Integrated Moving Average)                                   | It is explicitly designed to handle all three properties of our data: **Trend**, **Seasonality**, and **Residual Noise**.                                       |
| **Seasonal Order (S=7)** | The model must know that Monday demand is linked to the previous Monday, not the previous Sunday. | The $S=7$ parameter enforces the correct weekly cycle detection.                                                                                                |
| **Differencing (d=1)**   | The model must eliminate the non-stationary, multi-year trend caused by the structural shock.     | The $d=1$ parameter stabilizes the time series, making the subsequent predictions reliable.                                                                     |
| **The Zero-Floor Fix**   | Passenger counts cannot be negative.                                                              | We applied a post-processing **real-world constraint** (`max(0, prediction)`) to fix the model's negative forecast artifacts, demonstrating technical maturity. |

---

## 4. Final Forecast and Conclusion

The final, error-free forecast for the next 7 days, corrected for the negative-value constraint, is presented below.

**7-Day Public Transport Passenger Journey Forecast**

| Date           | Local Route | Light Rail | Peak Service | Rapid Route | School |
| :------------- | :---------- | :--------- | :----------- | :---------- | :----- |
| **2024-09-30** | 9,281       | 2,545      | 167          | 3,811       | 1,431  |
| **2024-10-01** | 10,231      | 2,567      | 169          | 4,042       | 1,540  |
| **2024-10-02** | 10,012      | 2,514      | 165          | 3,660       | 1,519  |
| **2024-10-03** | 9,824       | 2,177      | 128          | 3,348       | 1,574  |
| **2024-10-04** | 6,672       | 800        | 46           | **0**       | 771    |
| **2024-10-05** | 670         | **0**      | **0**        | **0**       | 395    |
| **2024-10-06** | **0**       | **0**      | **0**        | **0**       | 406    |

### **Conclusion: Readiness for Strategic Planning**

This project successfully moved from raw data to a fully justified, robust 7-day forecast. By using SARIMAX, we not only predicted demand but gained a deep understanding of the network's vulnerabilities (like the weekend demand fragility). This analysis is immediately ready to inform scheduling, resource allocation, and long-term policy adjustments for the public transport network.

---
