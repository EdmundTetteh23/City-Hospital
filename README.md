# City Hospital — Financial & Operations Analytics
An end-to-end financial and operational intelligence solution built for City Hospital, transforming raw transactional data into an interactive, 2-page PowerBI dashboard. This project replaces intuition-based decision-making with evidence based facts for hospital leadership to gain insights into financial performance, specialty profitability, workforce efficiency, and patient demographics.

## Table of Contents
- [Overview](#overview)
- [Project Brief and Problem Statement](#Project-Brief-and-Problem-Statement)
- [Data Pipeline and Architecture](#Data-Pipeline-and-Architecture)
- [Data Model and Relationships](#Data-Model-and-Relationships)
- [Core DAX Measures and Formulas](#Core-DAX-Measures-and-Formulas)
- [Dashboards and Visualizations](#Dashboards-and-Visualizations)
- [Key Business Insights](#Key-Business-Insights)
- [Strategic Recommendations](#Strategic-Recommendations)
- [Tech Stack](#Tech-Stack)
- Author

## Overview
City Hospital has historically lacked a centralized, data-driven system to track operational and financial performance across departments.
This project establishes a robust business intelligence framework by structuring flat operational files into an optimized relational Star Schema, applying ETL transformations in Power Query, and building intuitive visuals that enable hospital administrators to track high-level KPIs, procedure economics, doctor capacity, and volume trends.

## Project Brief and Problem Statement
### Problem Statement
City Hospital lacked a centralized view of its financial and operational performance. Decisions were traditionally made based on intuition and historical trends, making it difficult to identify revenue trends, evaluate procedure margins, optimize resource allocation, and address capacity bottlenecks.

### Project Objectives
- Centralize Financial Visibility: Consolidate hospital transaction logs to track cumulative revenue, expenses, profit, and net profit margins over time.
- Specialty & Procedure Intelligence: Isolate top revenue-generating medical specialties and evaluate the exact financial return and transaction volume per procedure.
- Workforce & Operational Capacity: Analyze provider capacity by mapping doctor headcount against patient volume across specialties.
- Demographic & Volume Tracking: Profile physician and patient populations by gender and evaluate monthly patient visit trends to support staffing strategies.

## Data Pipeline and Architecture
[Raw Flat File] ➔ [Power Query ETL] ➔ [Star Schema Data Model] ➔ [Interactive Power BI Report]

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

## Data Model and Relationships
The model follows a classic Star Schema centered around the transactional fact table, configured with one-to-many (1:*) single-direction filter relationships:

<img width="1009" height="491" alt="CH Data Model" src="https://github.com/user-attachments/assets/f7fcd82f-8618-442c-b045-95150f7289fe" />

- Facts_table: Stores central transactional metrics (RevenueAmount, ExpensesAmount) linked via foreign keys (Date, DoctorID, PatientID, ProcedureID, LocationID).
- Doctor_dim: Contains physician profiles, merged full names, gender, and medical specialties.
- Patient_dim: Tracks patient identity, merged full names, gender, and date of birth.
- Location_dim: Geographic lookup (City, State, Country, PostalCode).
- Procedure_dim: Detail lookup for medical procedure names, categories, and descriptions.
- Selected Metric: Disconnected parameter table implemented for dynamic parameter selection across visual metrics.

## Core DAX Measures and Formulas
- Total Revenue = SUM(RevenueAmount)
- Total Expense = SUM(ExpensesAmount)
- Total Profit = Total Revenue − Total Expense
- Profit Margin (%) = Total Profit ÷ Total Revenue × 100
- Total Doctors = DISTINCTCOUNT(DoctorID)
- Total Patients = DISTINCTCOUNT(PatientID)

## Dashboards and Visualizations
### Dashboard 1 — Financial Performance & Specialty Analysis
Tailored to provide leadership with executive visibility into financial trends, category performance, and procedure economics.

<img width="605" height="452" alt="Page 1" src="https://github.com/user-attachments/assets/9a1e58a7-d446-4b6d-8dd3-d2b91a5ae2d5" />

- KPI Strip: Total Revenue ($273.6K), Total Expenses ($189.4K), Total Profit ($84.1K), Profit Margin (30.8%), Total Doctors (81), and Total Patients (86).
- Revenue Trend: Line visual tracking monthly revenue performance across the full reporting period.
- Category & Specialty Breakdown: Horizontal bar charts comparing revenue generation across medical specialties and procedure categories.
- Financial Metrics Matrix: Comprehensive breakdown detailing Revenue, Expenses, Profit Margin %, and Transaction Count for every individual procedure.
- Slicer Panel: Interactive filtering pane for Year, State, Gender of Doctor, and Gender of Patient.

### Dashboard 2 — Workforce & Patient Demographics
Focused on operational flow, physician workloads, top revenue contributors, and patient demographics.

<img width="606" height="452" alt="Page 2" src="https://github.com/user-attachments/assets/080ee091-d217-4109-9235-3e8874ef4249" />

•	Top Contributors: Ranked visual metrics highlighting top revenue-generating doctors (led by Ava Adams at $24.8K) and top 5 revenue-impacting patients (led by Harper Young at $16.7K).
•	Specialty Staffing vs. Patient Load: Comparative bar charts mapping doctor headcount against patient volume per specialty.
•	Demographics: Column chart breakdowns showing full gender distribution across providers, (42 Male / 39 Female) doctors and (47 Female / 39 Male) patients.
•	Patient Visit Trend: Line chart tracking patient visit volume over time.

## Key Business Insights
### Financial Performance
- Overall Profitability: City Hospital generated $273.6K in total revenue against $189.4K in expenses, yielding $84.1K profit at a 30.8% net profit margin.
- Revenue Seasonality: Revenue exhibits a seasonal wave. The first half (Jan–Jun) averages approximately $24.0K/month compared to $21.6K/month in the second half (Jul–Dec). September represents the seasonal low point ($20.2K), approximately 20% below the March peak ($25.2K).
- Margin Consistency: Margins across all 10 procedures remain tightly bounded between 29.65% (X-Ray) and 31.87% (Heart Bypass Surgery), showing consistent pricing discipline across services.
- Specialty Concentration: Dermatology leads all specialties in revenue generation at $68K (~25% of total specialty revenue).

### Operational & Workforce Intelligence
- Primary Volume Driver: Cardiology is the busiest specialty overall, maintaining both the largest physician staff (15 doctors) and highest patient volume (21 patients).
- Capacity Strain in Neurology: Neurology doctors carry a high workload density (18 patients / 13 doctors ≈ 1.38 ratio), nearly identical to Cardiology (1.38 vs 1.40) despite having two fewer physicians on staff.
- Demographic Inversion: The physician workforce skews male (52% Male / 48% Female), whereas the patient base skews female (55% Female / 45% Male).
- Volume-Driven Revenue Drop: Patient visits decline steadily over the year (from 19 visits per month in Q1 to 15 visits per month in Q4), confirming the second-half revenue drop is driven by lower patient volume rather than margin compression.

## Strategic Recommendations
1. Proactively Plan for the September Dip
Launch targeted patient outreach campaigns—such as preventative health screenings and routine checkup reminders—in August, ahead of the seasonal trough, rather than reacting after revenue has already fallen.

2. Investigate Heart Bypass Surgery Capacity
Heart Bypass Surgery yields the highest profit margin per case ($519/case, 31.87% margin). Investigate if surgeon or OR availability is capping volume at 23 cases.

3. Diversify Specialty Revenue
Continue investing in Cardiology and Neurology to expand their pipelines and reduce financial concentration risk, ensuring the hospital does not remain overly dependent on Dermatology, which currently drives approximately 25% of revenue.

4. Operationalize the Dashboard as a Living Tool
Establish a daily data refresh cycle and integrate the report into recurring leadership reviews so executive management can track whether seasonal, specialty, and staffing interventions are actively moving the numbers.

## Tech Stack
- Data Source: Hospital transaction dataset (CSV/Excel)
- Transformation: Power Query (data cleaning, type correction, relationship modeling)
- Modeling & Metrics: DAX (KPI measures, profit margin, ratios)
- Visualization: Microsoft PowerBI


