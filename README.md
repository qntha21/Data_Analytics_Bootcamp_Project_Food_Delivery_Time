# Data_Analytics_Bootcamp_Project_Food_Delivery_Time

# Food Delivery Time Analysis & Prediction

## Overview
Built 2 interactive Tableau dashboards analyzing food delivery performance and the drivers of delivery time, covering order distribution across operational conditions, a validated regression model comparison, and a business-ready ranking of what actually moves delivery time and by how much.

## Problem Statement
Delivery time is the single metric that most directly shapes customer satisfaction on a food delivery platform, yet the factors behind it are a mix of things a business can control (kitchen prep speed, courier assignment) and things it can't (traffic, weather). Treating every factor as equally actionable wastes operational effort on levers that don't move the number. This project asks: which conditions actually drive delivery time, how much time (in minutes) does each one realistically cost, and can that time be predicted reliably enough to set honest customer expectations and guide where operations should focus first?

## Dataset
- Source: Bootcamp-provided food delivery operations dataset
- Size: 1,000 orders
- Includes: Order_ID, Distance_km, Weather, Traffic_Level, Time_of_Day, Vehicle_Type, Preparation_Time_min, Courier_Experience_yrs, Delivery_Time_min

## Key Findings
- **Model selection**: Linear Regression (MAE 5.90 min, RMSE 8.83, R² 0.826) outperformed Random Forest (MAE 7.02, RMSE 10.22, R² 0.767) and comfortably beat a mean-only baseline (MAE 17.50) chosen as the primary model for both accuracy and interpretability, since its coefficients translate directly into minutes, unlike Random Forest's importance scores
- **Driver ranking (impact in minutes across each factor's observed range)**: Distance 58.2 min, Prep time 23.3 min, Traffic 11.1 min, Weather 9.2 min, Courier experience 6.1 min, Time of day 2.4 min, Vehicle type 1.5 min
- **Statistical significance**: An OLS regression confirms Distance, Prep time, Courier experience, most Weather categories, and Traffic are all statistically significant (p < 0.05); Time_of_Day and Vehicle_Type are not (p 0.26–0.82), backing up their low ranking in practical impact
- **Correlation check**: Distance_km correlates strongly with delivery time (r = 0.78); Prep time moderately (r = 0.31); Courier experience is nearly uncorrelated (r = -0.09) despite showing up higher in naive feature-importance rankings, a reminder that impurity-based importance (e.g., Random Forest) can overstate continuous variables relative to one-hot encoded categorical ones
- **Secondary factors**: Traffic and weather add real but situational delay; they matter less than distance and prep time but more than courier experience or vehicle choice

## Recommendations
- **Prioritize delivery zone optimization**: distance is the single largest driver of delivery time (a 58-minute swing across the observed range) — tightening delivery radius or assigning couriers by proximity has the highest expected payoff
- **Tighten kitchen prep workflows**: prep time is the second-largest controllable factor (23-minute swing), standardizing kitchen processes, especially during peak volume, is a direct and actionable lever
- **Treat traffic and weather as ETA buffers, not restructuring targets**: they add secondary, situational delay (11 and 9 minutes respectively) — worth building into customer-facing time estimates, but not worth redesigning operations around
- **Don't over-invest in courier experience or vehicle upgrades**: despite intuitive appeal, both are statistically weak and practically negligible (6 and 1.5 minutes respectively) — training or fleet programs aimed at cutting delivery time specifically are unlikely to move the number

## Tools Used
Tableau Public (2 dashboards) · Python (Pandas, NumPy, Scikit-learn, Statsmodels, Matplotlib, Seaborn) · Linear Regression / Random Forest · Sensitivity-Based Driver Impact Analysis

Part of the Data Analytics Bootcamp portfolio (2026)
