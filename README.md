# IoT System Performance & Data Visualization Dashboard

## 📌 Project Overview
This repository showcases a public-facing **IoT Data Visualization Dashboard** deployed to monitor critical system performance metrics. The project translates raw, high-frequency streams from network infrastructures and sensor endpoints into interactive, actionable business intelligence KPIs to support automated system health evaluation and rapid operational monitoring.

## 🛠️ Tech Stack & Analytical Capabilities
- **Visualization Tool:** Power BI Desktop / Microsoft Portal Deployment 
- **Data Engineering:** Power Query (ETL, Data Transformation, Cleaning) 
- **Data Modeling:** Star Schema Design, Relationship Mapping (1:Many), Cross-filtering Optimization
- **Languages:** DAX (Data Analysis Expressions) for custom calculated measures

---

## 🏗️ Data Architecture & Modeling Workflow

### 1. Extraction and Transformation (Power Query ETL)
- Cleaned and shaped raw historical IoT datasets by removing missing metrics, normalizing timestamp shapes, and casting explicit numeric datatypes.
- Engineered structured date/time dim-tables to optimize processing performance and cross-filtering stability across real-time feeds.

### 2. Analytical Data Modeling (Star Schema)
- Engineered a robust **Star Schema** within Power BI's Model View to map explicit relationships between fact logging tables and dimension tables.
- [cite_start]Leveraged single-directional and bi-directional cross-filtering parameters to build an intuitive, one-page responsive interface[cite: 58].

---

## 📊 Dashboard Visualizations & Interactive Controls

### Primary Analytical Dashboard View
![Dashboard Main View](images/dashboard_main.png)
*Description: High-fidelity interactive layout illustrating key system performance indicators, operational telemetry curves, and real-time alerts.*

### Star Schema Relationships Layout (Model View)
![Data Model Schema](images/data_model.png)
*Description: Power BI schema model demonstrating relationships, indexing, and data modeling best practices applied to support data-driven decisions.*

---

## 📈 Implemented KPIs & Business Logic (DAX Expressions)

To drive advanced evaluation metrics, the dashboard implements custom **DAX** logic:

```dax
// 1. Dynamic System Efficiency Indicator
System_Efficiency_Score = 
DIVIDE(
    CALCULATE(COUNT(sensor_logs[status]), sensor_logs[status] = "Active"),
    COUNT(sensor_logs[status]),
    0
)

// 2. Rolling Average Network Load
Rolling_Avg_Network_Load = 
AVERAGEX(
    DATESINPERIOD('Dim_Date'[Date], LASTDATE('Dim_Date'[Date]), -7, DAY),
    [Total_Network_Traffic]
)
