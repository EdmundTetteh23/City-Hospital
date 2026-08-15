# City Hospital — Financial & Operations Analytics
An end-to-end financial and operational intelligence solution built for City Hospital, transforming raw transactional data into an interactive, 2-page PowerBI dashboard. This project replaces intuition-based decision-making with evidence based facts for hospital leadership to gain insights into financial performance, specialty profitability, workforce efficiency, and patient demographics.

## Table of Contents
- Overview
- Project Brief & Problem Statement
- Data Pipeline & Architecture
- Data Model & Relationships
- Dashboards & Visualizations
- Core DAX Measures & Formulas
- Key Business Insights
- Business Questions Answered
- Strategic Recommendations
- Tech Stack
- Author

## Overview
City Hospital has historically lacked a centralized, data-driven system to track operational and financial performance across departments.
This project establishes a robust business intelligence framework by structuring flat operational files into an optimized relational Star Schema, applying ETL transformations in Power Query, and building intuitive visuals that enable hospital administrators to track high-level KPIs, procedure economics, doctor capacity, and volume trends.

## Project Brief & Problem Statement
### Problem Statement
City Hospital lacked a centralized view of its financial and operational performance. Decisions were traditionally made based on intuition and historical trends, making it difficult to identify revenue trends, evaluate procedure margins, optimize resource allocation, and address capacity bottlenecks.

### Project Objectives
- Centralize Financial Visibility: Consolidate hospital transaction logs to track cumulative revenue, expenses, profit, and net profit margins over time.
- Specialty & Procedure Intelligence: Isolate top revenue-generating medical specialties and evaluate the exact financial return and transaction volume per procedure.
- Workforce & Operational Capacity: Analyze provider capacity by mapping doctor headcount against patient volume across specialties.
- Demographic & Volume Tracking: Profile physician and patient populations by gender and evaluate monthly patient visit trends to support staffing strategies.

## Data Pipeline & Architecture
[ Raw Flat File ] ➔ [ Power Query ETL ] ➔ [ Star Schema Data Model ] ➔ [ Interactive Power BI Report ]

## Power Query ETL Steps
The raw transactional dataset was normalized into 1 Fact Table and 4 Dimension Tables using Power Query to enforce data integrity and improve query performance:

fact_table
<img width="1366" height="768" alt="fact_table" src="https://github.com/user-attachments/assets/f69b3779-b5a2-4c64-8443-e8d8ef26b1bb" />

doctor_dim
<img width="1366" height="768" alt="doctor_dim" src="https://github.com/user-attachments/assets/1a3fd4f6-3fb3-4db2-ad89-2c911a69a919" />

patient_dim
<img width="1366" height="768" alt="patient_dim" src="https://github.com/user-attachments/assets/dfe5251a-4eb9-40ec-83b2-b314b1c21e82" />

location_dim
<img width="1366" height="768" alt="location_dim" src="https://github.com/user-attachments/assets/4977bf39-bea1-4def-81d5-3cff9c9e4600" />

procedure_dim
<img width="1366" height="768" alt="procedure_dim" src="https://github.com/user-attachments/assets/b3513bca-4489-4139-8880-0ba3b0b703a9" />

1.	Data Hygiene: Removed blank rows, invalid entries, and redundant header instances.
2.	Type Corrections: Applied localized data typing for proper date parsing and numeric/currency formatting (Changed Type with Locale).
3.	Primary Key Enforcement: Removed duplicate rows in dimension tables.
4.	Column Merging: Concatenated separate first and last name fields into unified Doctors_Name and Patients Name attributes.


