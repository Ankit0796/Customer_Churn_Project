# 📉 Customer Churn Analysis | SQL Server + Python (ML) + Power BI

This end-to-end Customer Churn Analysis project utilizes **SQL Server** for data profiling and transformation, **Python** for churn prediction and model tuning, and **Power BI** for interactive dashboard visualization.
### 🌐 Power BI Online Report

You can view the interactive churn dashboard live on Power BI Service:

🔗 [**View Power BI Dashboard**](https://app.powerbi.com/groups/9aa20a76-8582-4f9b-ac43-89baea9f0cda/reports/6693e750-76cc-47eb-86a9-0d7d8ed970ab/28983728a210d014d489?experience=power-bi)

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

SELECT Gender,
COUNT(GENDER) AS totalcount,
COUNT(GENDER) * 100.0/(SELECT COUNT(*) FROM stg_churn) AS Percentage
FROM stg_churn
GROUP BY GENDER

<img width="264" height="70" alt="Image" src="https://github.com/user-attachments/assets/3d5e04f0-fbee-4978-ad24-9cc61a8b79d3" />

SELECT Contract,
COUNT(Contract) AS totalcount,
COUNT(Contract) * 100.0/(SELECT COUNT(*) FROM stg_churn) AS Percentage
FROM stg_churn
GROUP BY Contract

<img width="302" height="96" alt="Image" src="https://github.com/user-attachments/assets/a5bdde35-f4b1-48db-8c07-262ab47affb6" />

- Revenue Distribution by Customer Status

SELECT customer_status,
COUNT(customer_status) AS totalcount,
SUM(total_revenue) AS Totalrevnue,
SUM(total_revenue) * 100.0/(SELECT SUM(total_revenue) FROM stg_churn) AS Revenuepercentage
FROM stg_churn
GROUP BY customer_status

<img width="414" height="110" alt="Image" src="https://github.com/user-attachments/assets/bd10a3d3-6518-481a-ab01-fcaa5261d12d" />

- State-wise customer count and churn %

SELECT state,
COUNT(state) AS TotalCount,
COUNT(state) * 100.0 / (SELECT COUNT(*) FROM stg_churn) AS Percentage
FROM stg_churn
GROUP BY state
ORDER BY Percentage DESC

<img width="308" height="443" alt="Image" src="https://github.com/user-attachments/assets/73fb394d-0692-4ac7-9b57-70d75c758082" />

- Null Value Audit (30+ columns)

SELECT 
    SUM(CASE WHEN Customer_ID IS NULL THEN 1 ELSE 0 END) AS Customer_ID_Null_Count,

    SUM(CASE WHEN Gender IS NULL THEN 1 ELSE 0 END) AS Gender_Null_Count,

    SUM(CASE WHEN Age IS NULL THEN 1 ELSE 0 END) AS Age_Null_Count,

    SUM(CASE WHEN Married IS NULL THEN 1 ELSE 0 END) AS Married_Null_Count,

    SUM(CASE WHEN State IS NULL THEN 1 ELSE 0 END) AS State_Null_Count,

    SUM(CASE WHEN Number_of_Referrals IS NULL THEN 1 ELSE 0 END) AS Number_of_Referrals_Null_Count,

    SUM(CASE WHEN Tenure_in_Months IS NULL THEN 1 ELSE 0 END) AS Tenure_in_Months_Null_Count,

    SUM(CASE WHEN Value_Deal IS NULL THEN 1 ELSE 0 END) AS Value_Deal_Null_Count,

    SUM(CASE WHEN Phone_Service IS NULL THEN 1 ELSE 0 END) AS Phone_Service_Null_Count,

    SUM(CASE WHEN Multiple_Lines IS NULL THEN 1 ELSE 0 END) AS Multiple_Lines_Null_Count,

    SUM(CASE WHEN Internet_Service IS NULL THEN 1 ELSE 0 END) AS Internet_Service_Null_Count,

    SUM(CASE WHEN Internet_Type IS NULL THEN 1 ELSE 0 END) AS Internet_Type_Null_Count,

    SUM(CASE WHEN Online_Security IS NULL THEN 1 ELSE 0 END) AS Online_Security_Null_Count,

    SUM(CASE WHEN Online_Backup IS NULL THEN 1 ELSE 0 END) AS Online_Backup_Null_Count,

    SUM(CASE WHEN Device_Protection_Plan IS NULL THEN 1 ELSE 0 END) AS Device_Protection_Plan_Null_Count,

    SUM(CASE WHEN Premium_Support IS NULL THEN 1 ELSE 0 END) AS Premium_Support_Null_Count,

    SUM(CASE WHEN Streaming_TV IS NULL THEN 1 ELSE 0 END) AS Streaming_TV_Null_Count,

    SUM(CASE WHEN Streaming_Movies IS NULL THEN 1 ELSE 0 END) AS Streaming_Movies_Null_Count,

    SUM(CASE WHEN Streaming_Music IS NULL THEN 1 ELSE 0 END) AS Streaming_Music_Null_Count,

    SUM(CASE WHEN Unlimited_Data IS NULL THEN 1 ELSE 0 END) AS Unlimited_Data_Null_Count,

    SUM(CASE WHEN Contract IS NULL THEN 1 ELSE 0 END) AS Contract_Null_Count,

    SUM(CASE WHEN Paperless_Billing IS NULL THEN 1 ELSE 0 END) AS Paperless_Billing_Null_Count,

    SUM(CASE WHEN Payment_Method IS NULL THEN 1 ELSE 0 END) AS Payment_Method_Null_Count,

    SUM(CASE WHEN Monthly_Charge IS NULL THEN 1 ELSE 0 END) AS Monthly_Charge_Null_Count,

    SUM(CASE WHEN Total_Charges IS NULL THEN 1 ELSE 0 END) AS Total_Charges_Null_Count,

    SUM(CASE WHEN Total_Refunds IS NULL THEN 1 ELSE 0 END) AS Total_Refunds_Null_Count,

    SUM(CASE WHEN Total_Extra_Data_Charges IS NULL THEN 1 ELSE 0 END) AS Total_Extra_Data_Charges_Null_Count,

    SUM(CASE WHEN Total_Long_Distance_Charges IS NULL THEN 1 ELSE 0 END) AS Total_Long_Distance_Charges_Null_Count,

    SUM(CASE WHEN Total_Revenue IS NULL THEN 1 ELSE 0 END) AS Total_Revenue_Null_Count,

    SUM(CASE WHEN Customer_Status IS NULL THEN 1 ELSE 0 END) AS Customer_Status_Null_Count,

    SUM(CASE WHEN Churn_Category IS NULL THEN 1 ELSE 0 END) AS Churn_Category_Null_Count,

    SUM(CASE WHEN Churn_Reason IS NULL THEN 1 ELSE 0 END) AS Churn_Reason_Null_Count

FROM stg_Churn;

<img width="1302" height="51" alt="Image" src="https://github.com/user-attachments/assets/fd207de9-cfe2-4440-b26c-511d4ee4fead" />

<img width="1235" height="51" alt="Image" src="https://github.com/user-attachments/assets/9c1567a4-0153-4137-ad2a-309293123053" />

<img width="1167" height="50" alt="Image" src="https://github.com/user-attachments/assets/22c94d37-ca88-4861-83ce-c99b8a1f9054" />

<img width="1021" height="50" alt="Image" src="https://github.com/user-attachments/assets/3c62cfb3-c49c-4357-89c2-531c6680e836" />

- Data Cleansing using `ISNULL()` for categorical columns

SELECT 
    Customer_ID,

    Gender,

    Age,

    Married,

    State,

    Number_of_Referrals,

    Tenure_in_Months,

    ISNULL(Value_Deal, 'None') AS Value_Deal,

    Phone_Service,

    ISNULL(Multiple_Lines, 'No') As Multiple_Lines,

    Internet_Service,

    ISNULL(Internet_Type, 'None') AS Internet_Type,

    ISNULL(Online_Security, 'No') AS Online_Security,

    ISNULL(Online_Backup, 'No') AS Online_Backup,

    ISNULL(Device_Protection_Plan, 'No') AS Device_Protection_Plan,

    ISNULL(Premium_Support, 'No') AS Premium_Support,

    ISNULL(Streaming_TV, 'No') AS Streaming_TV,

    ISNULL(Streaming_Movies, 'No') AS Streaming_Movies,

    ISNULL(Streaming_Music, 'No') AS Streaming_Music,

    ISNULL(Unlimited_Data, 'No') AS Unlimited_Data,

    Contract,

    Paperless_Billing,

    Payment_Method,

    Monthly_Charge,

    Total_Charges,

    Total_Refunds,

    Total_Extra_Data_Charges,

    Total_Long_Distance_Charges,

    Total_Revenue,

    Customer_Status,

    ISNULL(Churn_Category, 'Others') AS Churn_Category,

    ISNULL(Churn_Reason , 'Others') AS Churn_Reason
INTO [db_Churn].[dbo].[prod_Churn]
FROM [db_Churn].[dbo].[stg_Churn];

- Split Views Created:
  - `vw_ChurnData` (Churned & Stayed customers)

CREATE VIEW vw_ChurnData AS
	SELECT * 
	FROM prod_Churn 
	WHERE customer_status IN ('Churned', 'Stayed')

  - `vw_JoinData` (New joiners for prediction)

CREATE VIEW vw_JoinData AS
	SELECT *
	FROM prod_Churn
	WHERE customer_status = 'Joined';

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
- **Predicted Churners (Untuned Model):** 381
- Accuracy: ~0.81
- Confusion Matrix & Classification Report generated

<img width="449" height="264" alt="Image" src="https://github.com/user-attachments/assets/d984bf49-bab5-41af-a89c-f6876c5beac9" />

- Feature Importance plotted (Seaborn barplot)

importances = model.feature_importances_
indices = np.argsort(importances)[::-1]

plt.figure(figsize=(15,10))
sns.barplot(x=importances[indices], y=X.columns[indices])
plt.title('Feature Importances')
plt.xlabel('Relative Importance')
plt.ylabel('Feature Names')
plt.show()

<img width="1416" height="855" alt="Image" src="https://github.com/user-attachments/assets/d7696fe2-60bd-4eb7-b19c-1de2493a9e22" />

- This chart ranks input features by their relative contribution to the model’s decisions. Features with higher importance scores had a stronger influence on predicting whether a customer would churn.
- Features like Tenure_in_Months, Contract Type, and Monthly_Charge were found to be most influential.
- Less important features which has relative importance less than 0.01 were considered for removal during the model tuning phase to improve generalization and reduce complexity.
- The features include 'Gender', 'Married', 'Phone_Service', 'Multiple_Lines','Online_Backup', 'Device_Protection_Plan','Streaming_TV', 'Streaming_Movies', 'Streaming_Music', 'Unlimited_Data', 'Total_Refunds', 'Total_Extra_Data_Charges'

Explain the model to non-technical stakeholders
---

### 🛠️ Model Tuning: Feature Reduction & Re-training

To improve model performance and reduce overfitting, less important features (based on feature importance chart) were dropped:
- Removed: `Gender`, `Married`, `Phone_Service`, `Multiple_Lines`, `Streaming_*`, `Unlimited_Data`, `Total_Refunds`, `Total_Extra_Data_Charges`, etc.
- Relative importance of remaining features

<img width="1416" height="855" alt="Image" src="https://github.com/user-attachments/assets/2b3e1604-deed-4923-a97f-41b900d0d41a" />

#### Re-tuning Process:
- Re-trained model with remaining important features
- Re-encoded categorical variables
- Evaluated accuracy and classification report again

![image](https://github.com/user-attachments/assets/f14f3e70-7745-4628-9c54-485e078bface)


#### Results:

| Model Version     | Accuracy | Precision | Recall | F1-Score | Churn Predicted |
|------------------|----------|-----------|--------|----------|-----------------|
| All Features      | 85.3%    | 80.6%     | 64.5%  | 71.7%    | 381 customers   |
| Reduced Features  | 86.0%    | 80.0%     | 63.0%  | 71.0%    | 364 customers   |


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
- Used tooltips for reasons of churn

<img width="881" height="501" alt="Image" src="https://github.com/user-attachments/assets/1aa88e2b-dbc2-4154-829e-e6aee1593058" />

![PowerBI - Prediction ](https://github.com/user-attachments/assets/58bdb2a3-8152-49cd-bbbc-8c5cc2bd7614)


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


