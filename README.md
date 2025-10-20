# 🚗 Used Car Price Prediction

This project identifies the key drivers of used car prices using a dataset of approximately **426,000 used cars**.  
The analysis follows the **CRISP-DM framework**, covering business understanding, data understanding, data preparation, modeling, and evaluation.  
The goal is to provide insights to a used car dealership to help fine-tune inventory and pricing strategies.

---

## 📑 Table of Contents

1. [Project Overview](#1-project-overview)
2. [CRISP-DM Framework](#2-crisp-dm-framework)
3. [Data Understanding](#3-data-understanding)
4. [Data Preparation](#4-data-preparation)
5. [Modeling](#5-modeling)
6. [Evaluation](#6-evaluation)
7. [Deployment (Recommendations)](#7-deployment-recommendations)
8. [Repository Structure](#8-repository-structure)

---

## 1️⃣ Project Overview

The primary objective is to understand which factors significantly influence used car prices.  
This understanding will enable the dealership to make informed decisions on purchasing, pricing, and marketing — ultimately improving profitability.

---

## 2️⃣ CRISP-DM Framework

The project follows the standard **CRISP-DM** methodology:

- **Business Understanding:** Reframe the dealership’s business question (“what drives car prices?”) as a regression task.  
- **Data Understanding:** Explore data types, missing values, outliers, and relationships between predictors and price.  
- **Data Preparation:** Clean, transform, and encode features for modeling.  
- **Modeling:** Train multiple regression models (Linear, Ridge, Lasso, SVR) to predict car prices.  
- **Evaluation:** Compare performance, interpret results, and identify key features influencing price.  
- **Deployment:** Translate findings into clear, actionable recommendations.

---

## 3️⃣ Data Understanding

Initial exploration included:

- Inspecting dataset shape and data types  
- Summarizing numerical & categorical features  
- Identifying missing values  
- Visualizing key distributions (`price`, `year`, `odometer`)  
- Analyzing relationships (e.g., year vs. price, odometer vs. price)

**Key Findings:**
- Significant missing values in `size`, `cylinders`, `condition`, `VIN`, `drive`, `paint_color`, and `type`  
- `price` was highly skewed → required transformation  
- Outliers existed in `price` and `odometer`

---

## 4️⃣ Data Preparation

**Main Steps:**

- **Data Cleaning:** Removed invalid prices (≤0 or >500,000) and unrealistic years (<1990 or >2025).  
- **Handling Missing Values:**  
  - Imputed missing categorical features with `"unknown"`  
  - Imputed odometer using median by year  
- **Feature Engineering:**  
  - Created `age`, `age_group`, `mileage_group`, `is_luxury`, `is_efficient`  
- **Transformation & Scaling:**  
  - Log-transformed `price` and `odometer`  
  - Scaled numerical features with `StandardScaler`  
  - Encoded categorical features (One-Hot + Target Encoding)  
- **Feature Selection:**  
  - Dropped irrelevant columns (`id`, `region`, `VIN`, `state`)

---

## 5️⃣ Modeling

Trained and compared:

- **Linear Regression**  
- **Ridge Regression**  
- **Lasso Regression**  
- **Support Vector Regression (SVR)** — on a smaller subset for efficiency  

**Evaluation Metrics:**
- R² (Coefficient of Determination)  
- RMSE (Root Mean Squared Error)  
- MAE (Mean Absolute Error)  
- Overfitting Gap (Train R² − Test R²)

Cross-validation confirmed **Ridge Regression** as the most stable and interpretable model.

---

## 6️⃣ Evaluation

The **Ridge Regression** model offered the best balance between performance and interpretability.

| Metric | Value |
|--------|-------|
| **Model Used** | Ridge Regression |
| **R² (Test Data)** | ~0.37 |
| **RMSE (Test Data)** | ~0.97 |
| **MAE (Test Data)** | ~0.48 |

**Interpretation:**  
Ridge Regression explains roughly **37%** of the variation in log-transformed prices — reasonable for real-world market data with many unrecorded factors (e.g., vehicle condition, location, negotiation).  
Low overfitting indicates the model generalizes well.

---

## 7️⃣ Deployment (Recommendations)

### 🔑 Key Drivers of Used Car Prices

1. **Model (Target Encoded):** Most influential — certain models hold value better.  
2. **Year / Age:** Newer cars → higher value; older cars depreciate faster.  
3. **Type (SUV, Sedan, etc.):** SUVs/trucks retain value better than small sedans.  
4. **Odometer / Log Odometer / Mileage Group:** Lower mileage → higher price; depreciation slows at higher mileage.  
5. **Paint Color:** Popular colors (white, black, silver) slightly improve price.  
6. **Manufacturer:** Premium brands (BMW, Lexus, Mercedes) yield higher resale prices.

### 💡 Actionable Insights

- **Inventory:** Focus on newer, low-mileage vehicles and popular models/body types.  
- **Pricing:** Use age and mileage as main pricing levers; adjust for brand and model desirability.  
- **Marketing:** Emphasize model, year, and mileage in listings; mention manufacturer and body type to reinforce value.

### 🔄 Next Steps

- Add more data sources (condition, location, maintenance history) to improve accuracy.  
- Retrain the model periodically with updated listings to track market trends.  
- Integrate the model into an **automated pricing tool** for real-time dealer use.

---

## 8️⃣ Repository Structure


