# 📉 Customer Churn Analysis | SQL Server + Python (ML) + Power BI

This end-to-end Customer Churn Analysis project utilizes **SQL Server** for data profiling and transformation, **Python** for churn prediction and model tuning, and **Power BI** for interactive dashboard visualization.

---

## 🎯 Objective

To identify factors influencing customer churn and predict at-risk customers using historical data. The project aims to:
- Understand customer behavior across services and demographics
- Quantify churn impact on business revenue
- Enable data-driven retention strategies

---

## 🗃️ 1. SQL Server: Data Profiling & Preparation

### ✅ Tasks Performed:
- Database Created: `db_Churn`
- Raw staging table: `stg_Churn`
- Final table: `prod_Churn`

### 🔍 Key SQL Operations:
- Gender & Contract Distribution
- Revenue Distribution by Customer Status
- Churned vs Retained breakdown
- State-wise customer count and churn %
- Null Value Audit (30+ columns)
- Data Cleansing using `ISNULL()` for categorical columns
- Split Views Created:
  - `vw_ChurnData` (Churned & Stayed customers)
  - `vw_JoinData` (New joiners for prediction)

---

## 🧪 2. Python: Machine Learning Model (Random Forest)

### 📊 Goal:
To predict which newly joined customers are likely to churn using a classification model.

### 🔍 Key Steps:
- **Data Source:** `Prediction Data.xlsx` (from SQL export)
- **Target Variable:** `Customer_Status` (`Churned` = 1, `Stayed` = 0)
- **Preprocessing:**
  - Dropped ID and non-informative columns
  - Label Encoding applied to categorical features
  - Handled missing values
- **Model:** `RandomForestClassifier`
- **Train-Test Split:** 80–20

### ✅ Initial Evaluation:
- Accuracy: ~0.81
- Confusion Matrix & Classification Report generated
- Feature Importance plotted (Seaborn barplot)

---

### 🛠️ Model Tuning: Feature Reduction & Re-training

To improve model performance and reduce overfitting, less important features (based on feature importance chart) were dropped:
- Removed: `Gender`, `Married`, `Phone_Service`, `Multiple_Lines`, `Streaming_*`, `Unlimited_Data`, `Total_Refunds`, `Total_Extra_Data_Charges`, etc.

#### Re-tuning Process:
- Re-trained model with remaining important features
- Re-encoded categorical variables
- Evaluated accuracy and classification report again

#### Results:
- **Predicted Churners (Tuned Model):** 364
- Exported prediction to: `Prediction Data tuned.csv`
- High-churn segments retained:
  - Customers with <6 months or >24 months tenure
  - Month-to-month contracts
  - Low engagement in value-added services

---

## 📊 3. Power BI: Dashboard & Business Insights

### 🔧 Data Source:
- Live connection to `SQL Server` (prod_Churn, vw_ChurnData, vw_JoinData)
- Power Query used for transformation and modeling

### 📁 Pages in Power BI Report:

#### 🔹 Executive Summary
- Total Customers: 6,418
- Total Churned: 1,732
- Churn Rate: 27.0%
- Total Revenue
- ARPU
- Revenue Lost to Churn

#### 🔹 Demographic & Geographic Analysis
- Churn Rate by:
  - Gender (Male churn rate ~64%)
  - Age Group (Highest: 35–50)
  - Marital Status
  - State (J&K: 57.2%, Assam: 38.1%)

#### 🔹 Churn Breakdown
- Category-wise Churn:
  - Competitor: 761
  - Attitude: 301
  - Dissatisfaction: 196
- Churn by Internet Type (Fiber Optic: 41.1%)
- Contract Type (Month-to-Month: 26.4%)

#### 🔹 Prediction Dashboard
- 364 predicted churners
- Highest churn likelihood in customers:
  - With <6 months or >24 months tenure
  - On month-to-month contracts
  - Using minimal value-added services

### 🔍 Visuals Used:
- KPI cards, Donut & Bar charts, Heatmaps, Treemaps, Histograms
- Customer Funnel: Active → Churned → Retained
- Segmentation by services, payment method, referrals

---

## 🧰 Tech Stack Used

| Tool / Language     | Purpose                            |
|---------------------|------------------------------------|
| **SQL Server**      | Data ingestion, cleaning, queries  |
| **Python (sklearn)**| ML model training and tuning       |
| **Pandas / NumPy**  | Data manipulation in Python        |
| **Matplotlib / Seaborn** | Visualizing feature importance |
| **Power BI**        | Visualization and reporting        |
| **Power Query**     | Data transformation in Power BI    |

---
### 💼 Business Value:
- 📉 Reduced Churn by identifying at-risk segments
- 💡 Informed Strategy through churn driver insights
- 📊 Predictive Targeting for retention campaigns
- 💰 Revenue Protection by focusing on profitable customers at risk


