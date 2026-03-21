# 🚇 Modeling Subway Major Incidents Using Weather and Ridership

## 📊 Project Overview
This project analyzes **monthly major incidents in the New York City subway system (2015–2024)** and evaluates the extent to which **weather conditions and subway ridership** explain variation in incident frequency.

Major incidents are defined as disruptions delaying **50 or more trains**. The analysis progresses from baseline weather-only models to an improved predictive framework incorporating **system usage (ridership)**.

---

## 🎯 Objective
To determine whether environmental factors (weather) or operational factors (ridership) are the primary drivers of large-scale subway disruptions.

---

## 📁 Data Sources
- **MTA Incident Data (2015–2024)**
- **NOAA Weather Data (NYC station USW00094728)**
- **MTA Subway Ridership Data (2020 onward)**

---

## ⚙️ Methodology

### Data Engineering
- Merged multi-year incident datasets and aggregated to **monthly totals**
- Retrieved and processed NOAA daily weather data:
  - Temperature (TMAX, TMIN)
  - Precipitation (PRCP)
  - Snowfall (SNOW)
- Engineered features:
  - Heavy precipitation days
  - Hot days (≥ 90°F)
- Aggregated subway ridership to monthly totals and scaled to millions
- Joined datasets into a unified modeling table

### Statistical Analysis
- Correlation analysis across weather and incident variables
- Linear regression modeling:
  - Weather-only models
  - Feature-reduced models (snowfall)
  - Log-transformed models
  - Final multivariate model including ridership
- Model evaluation:
  - R² and Adjusted R²
  - AIC comparison
  - Residual diagnostics (Q-Q, leverage, heteroscedasticity)
  - Variance Inflation Factor (VIF)

---

## 📈 Results

### Weather-Only Models
- Snowfall was the only statistically significant predictor
- Limited explanatory power:
  - **R² ≈ 0.08–0.10**
- Temperature and precipitation showed minimal impact

### Final Model (Snowfall + Ridership)
- Significant improvement in predictive performance:
  - **R² ≈ 0.54**
  - **AIC reduced from 434 → 392**
- Key findings:
  - **Ridership is the strongest predictor of incidents**
  - **Snowfall remains independently significant**
- Interpretation:
  - +1 million riders → ~0.29 additional incidents
  - +1 inch snowfall → ~0.70 additional incidents

---

## 📊 Key Insights
- Weather alone is insufficient to explain disruption patterns
- System demand (ridership) is the dominant factor driving incidents
- Snowfall contributes meaningfully but plays a secondary role
- Combining operational and environmental data significantly improves model performance

---

## 🧰 Tech Stack
- **Language:** R
- **Libraries:**  
  `dplyr`, `ggplot2`, `readr`, `lubridate`, `tidyr`, `httr`, `car`
- **Tools:** Quarto, GitHub

---

## 📉 Visualizations
- Correlation heatmap of weather vs. incidents
- Time series of incidents and ridership
- Regression fit plots
- Residual diagnostics (Q-Q, leverage, scale-location)

---

## 🚀 How to Run
```r
# Install dependencies
install.packages(c("dplyr", "ggplot2", "readr", "lubridate", "tidyr", "httr", "car"))

# Render analysis
quarto render FinalVizProject.qmd
```
