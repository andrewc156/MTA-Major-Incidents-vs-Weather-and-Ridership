# 🚇 Modeling Subway Major Incidents Using Weather and Ridership

> **Key Insight:** Both ridership and snowfall drive NYC subway major incidents, and a **log-log model** best captures the multiplicative relationship — outperforming the linear and log-response specifications by AIC.

---

## 📊 Overview
This project analyzes **monthly major incidents in the New York City subway system (2015–2024)** and evaluates how well **weather conditions and subway ridership** explain disruption frequency.

A *major incident* is defined as a delay affecting **50 or more trains**.

---

## 🎯 Objectives
- Quantify the impact of **weather variables** on subway disruptions  
- Evaluate whether **ridership explains variation more effectively**  
- Compare **linear, log, and log-log** specifications to identify the best-fitting model  
- Build and validate **statistical models**  

---

## 📁 Data Sources
- **MTA Incident Data (2015–2024)**  
- **NOAA Weather Data (NYC)**  
- **MTA Subway Ridership Data (2020 onward)**  

---

## ⚙️ Methodology

### Data Engineering
- Aggregated incidents to **monthly totals**
- Processed NOAA weather data (temperature, precipitation, snowfall)
- Engineered features:
  - Heavy precipitation days
  - Hot days (≥ 90°F)
- Aggregated subway ridership to monthly totals
- Merged all datasets into a unified modeling dataset

---

### Statistical Modeling
- Correlation analysis  
- Linear regression models:
  - Weather-only  
  - Snow-only  
  - Log-transformed snow-only  
  - Linear model with snow and ridership  
- Logarithmic transformation comparison:
  - Linear response
  - Log response
  - Log-log specification  
- Model validation:
  - AIC comparison  
  - Residual diagnostics (both linear and log-log)  
  - VIF  

---

## 📈 Results

### 🔹 Relationship Between Ridership and Incidents
![Ridership vs Incidents](images/ridership_regression.png)

- Strong positive relationship  
- Higher ridership → more incidents  

---

### 🔹 Correlation Analysis
![Correlation Heatmap](images/heatmap.png)

- Snowfall shows strongest relationship among weather variables  
- Most weather variables have weak correlations  

---

### 🔹 Time Series Trends
![Time Series](images/timeseries.png)

- Incidents and ridership move together over time  
- Confirms ridership as a key driver  

---

### 🔹 Linear Model Diagnostics

#### Residuals vs Fitted
![Residuals vs Fitted](images/residuals_fitted.png)

#### Q-Q Plot
![Q-Q Plot](images/qq_plot.png)

#### Scale-Location
![Scale Location](images/scale_location.png)

#### Residuals vs Leverage
![Leverage Plot](images/leverage.png)

- Residuals are approximately normal  
- No major influential points  
- Slight heteroscedasticity but acceptable  

---

### 🔹 Log-Log Model Visualizations

#### Log-Log Relationship: Snowfall vs Incidents
![Log-Log Snowfall vs Incidents](images/loglog_snow.png)

#### Log-Log Relationship: Ridership vs Incidents
![Log-Log Ridership vs Incidents](images/loglog_ridership.png)

#### Actual vs Predicted Monthly Incidents
![Actual vs Predicted](images/actual_vs_predicted.png)

#### Actual vs Predicted Over Time
![Actual vs Predicted Over Time](images/actual_vs_predicted_timeseries.png)

- Log transformation produces more linear relationships  
- Predicted values track observed incidents closely  

---

### 🔹 Log-Log Model Diagnostics

#### Residuals vs Fitted
![Log-Log Residuals vs Fitted](images/loglog_residuals_fitted.png)

#### Normal Q-Q
![Log-Log Q-Q Plot](images/loglog_qq_plot.png)

#### Scale-Location
![Log-Log Scale Location](images/loglog_scale_location.png)

#### Residuals vs Leverage
![Log-Log Leverage Plot](images/loglog_leverage.png)

- Improved residual behavior over the linear specification  
- More stable variance across fitted values  

---

## 📊 Key Findings
- 🚆 **Ridership and snowfall both significantly predict incidents**
- ❄️ Snowfall retains an independent effect even after controlling for system usage
- 📉 Weather alone has low explanatory power
- 🔁 The **log-log model** had the lowest AIC, indicating a multiplicative relationship fits better than a purely linear one
- 📈 Diagnostics for the log-log specification show improved residual behavior compared with the linear model

### 🔢 AIC Model Comparison

| Model         | df | AIC     |
|---------------|----|---------|
| Linear        | 4  | 392.13  |
| Log response  | 4  |  12.52  |
| **Log-log**   | 4  |   **5.40**  |

The log-log specification wins by a wide margin (ΔAIC > 10 is considered decisive evidence).

### 🔢 Log-Log Regression Coefficients

| Term                              | Estimate | Std. Error | t      | p-value     |
|-----------------------------------|---------:|-----------:|-------:|------------:|
| (Intercept)                       |   0.751  |    0.297   |  2.53  | 0.014 *     |
| log(total_snow + 1)               |   0.135  |    0.045   |  3.03  | 0.004 **    |
| log(ridership_millions)           |   0.626  |    0.069   |  9.12  | < 1e-11 *** |

Residual SE = 0.243 on 55 df. A 1% increase in ridership is associated with a ≈ 0.63% increase in monthly major incidents; a 1% increase in (snow + 1) is associated with a ≈ 0.13% increase.

---

## 🧰 Tech Stack
- **R**
- `dplyr`, `ggplot2`, `readr`, `lubridate`, `tidyr`, `httr`, `car`
- Quarto

---

## 🚀 How to Run
```r
install.packages(c("dplyr", "ggplot2", "readr", "lubridate", "tidyr", "httr", "car"))
quarto render FinalVizProject.qmd
```
