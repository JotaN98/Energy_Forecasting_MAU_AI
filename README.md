# Wind Turbine Power Output Prediction

**Authors:** João Domingos & Wilmer H. Jacobsson 

**Course:** Artificial Intelligence for Data Science

## 📌 Project Overview

This project focuses on predicting the power output of wind turbines using supervised machine learning algorithms.
Wind energy, while a promising renewable resource, is inherently chaotic and inconsistent, making grid integration challenging.
Accurate forecasting is essential to mitigate these issues, reduce reliance on fossil-fuel-based spinning reserves, and minimize financial risks for energy providers.

This repository contains the implementation of a machine learning pipeline that preprocesses SCADA data and compares the performance of **Linear Regression** and **Random Forest Regression** models in forecasting energy generation.

## 📂 Dataset

The project utilizes the **"Wind Turbine SCADA Dataset"** obtained from Kaggle. The data was collected from a wind turbine in Turkey throughout 2018.

* **Source:** [Wind Turbine SCADA Dataset on Kaggle](https://www.kaggle.com/datasets/berkerisen/wind-turbine-scada-dataset/data) 


* **Resolution:** 10-minute intervals
* **Features:**
  * `Date/Time`: Timestamp of the measurement 
  * `LV ActivePower (kW)`: Actual power generated (Target Variable) 
  * `Wind Speed (m/s)`: Average wind speed 
  * `Theoretical_Power_Curve (KWh)`: Theoretical power generation based on manufacturer specifications 
  * `Wind Direction (°)`: Automatic turbine direction 

## 🛠️ Methodology

### 1. Data Preprocessing & Cleaning

* **Outlier Handling:** Negative `ActivePower` values were analyzed. Measurements with negative power at low wind speeds (< 3.5 m/s) were identified as non-generating phases (consumption) rather than sensor faults and set to zero.

* **Time Series Split:** To prevent data leakage, a Time Series Split was used instead of random shuffling, ensuring the model trains on past data to predict future events.



### 2. Feature Engineering 

* **Temporal Extraction:** Extracted Month, Day, Hour, and Minutes from timestamps.

* **Cyclical Encoding:**
 * **Seasons:** Mapped from months and One-Hot Encoded.
 * **Day/Night:** Binary encoded based on a static 6 AM – 6 PM window appropriate for the latitude.
 * **Wind Direction:** Transformed into two 2D coordinate features (Sine and Cosine) to preserve the circular nature of directional data ().
 * **Scaling:** Applied Standard Scaler () to numerical features like Wind Speed and Theoretical Power Curve.

### 3. Models

Two supervised learning models were implemented and compared:

1. **Linear Regression:** Serves as a baseline, assuming a linear relationship between features and output.
2. **Random Forest Regression:** An ensemble method capable of capturing non-linear relationships, such as the cubic dependence of power on wind speed.

## 📊 Results

The Random Forest model demonstrated slightly superior performance, effectively capturing the non-linear operational regimes of the turbine (cut-in, ramp-up, and saturation plateau).

| Model |  Score | RMSE (kW) |
| --- | --- | --- |
| **Linear Regression** | 0.9065 | 367.1876 |
| **Random Forest Regression** | **0.9106** | **366.4178** |

Table Data Source: 

While both models performed well due to the strong correlation of the theoretical power curve, the RMSE (~370 kW) suggests that further error reduction is needed for commercial grid dispatch.

## 📚 References

1. V. S. Rao, et al. "Prediction of Power Generation in Wind Turbines." IJSREM Journal, 2023.
2. S. Preethi, et al. "Predicting the Wind Turbine Power Generation based on Weather Conditions." IEEE, 2021.
3. Braeschke, M. & Müller, S. "Leveraging Shapley Values for Temperature Contributions..." 2025.
4. Berk Erisen. "Wind Turbine SCADA Dataset." Kaggle, 2018.
5. Magesh, T., et al. "Machine Learning-Driven Wind Energy Forecasting..." 2026.
6. N. M. Nasab, et al. "Comparative Critique on Power Generation in Wind Turbines." 2019.
7. G. Liu, & K. Tomsovic. "Quantifying spinning reserve in systems with significant wind power penetration." 2012.
8. Ela, E., et al. "Operating reserves and variable generation." 2011.
