# HR_PAYROLL_ANALYTICS_SNOWFLAKE_SCHEMA | Power BI Analytics

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Excel](https://img.shields.io/badge/Microsoft_Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-Data_Analysis_Expressions-blue?style=for-the-badge)

## Executive Summary
This project provides a multi-year analysis of corporate payroll expenditure across divisions, industries, and departmental units for the 2024–2026 fiscal periods. Managing a total payroll spend of **578.44M**againsta**600.00M** budget baseline, the organization achieved a favorable budget variance of **-3.59%**. 

### Key Highlights
* **Total Payroll Spend:** $578.44M (vs. $600.00M Budget)
* **Payroll Variance:** -3.59% (Favorable surplus of $21.56M)
* **Tax Deducted:** $133.08M
* **Overtime Pay Ratio:** 1.76% ($9.17M total overtime)

---

## Dashboard Preview

![Payroll Overview Dashboard](Images/Payroll_Overview_Dashboard.png)
*Figure 1: Main Payroll Overview Dashboard interface in Power BI.*

---

## Project Objectives & Scope
* **Objective:** Build an interactive executive dashboard enabling leadership to monitor monthly payroll distributions, track budget variances, and analyze department spending.
* **Scope:** 3 fiscal years (2024–2026) spanning 5 core industry sectors and specialized department units.

---

## Data Architecture & Schema
The data model follows a **Snowflake Schema** design to ensure normalized relationships and high-performance DAX evaluations.

![Data Model Schema](images/data_model_schema.png)
*Figure 2: Data Model showing Fact_Payroll linked to normalized Dimension tables.*

* **Fact Table:** `Fact_Payroll` (Transactional payroll metrics, base pay, tax, overtime)
* **Dimension Tables:** `Dim_Band`, `Dim_Calender`, `Dim_City`, `Dim_Client`, `Dim_Date`, `Dim_Department`, `Dim_Division`, `Dim_Education`, `Dim_Employee`, `Dim_Industry`, `Dim_Job_Role`, `Dim_Location`, `Dim_Project`, `Dim_Quarter`, `Dim_Year`.

---

## Key DAX Calculations

```dax
// 1. Total Payroll Spend
Total Payroll = CALCULATE(SUM(Fact_Payroll[Gross_Pay]))

// 2. Payroll Variance %
Payroll Variance % = 
DIVIDE([Total Payroll] - [Budgeted Payroll], [Budgeted Payroll]) * 100

// 3. Year-To-Date Payroll
PAYROLL_TOTALYTD = TOTALYTD([Total Payroll], Dim_Calender[Date])

// 4. Overtime Ratio
OVERTIME_RATIO = DIVIDE(SUM(Fact_Payroll[Overtime_Pay]), SUM(Fact_Payroll[Base_Salary]))
```
## Key Analytical Insights

* **Under-Budget Performance:** Total payroll came in **$21.56M below budget**, representing a **-3.59%** variance[cite: 8].
* **February Monthly Anomaly:** While average monthly payroll ranges between **55M–56M**, February records an extreme drop to **$18.6M** (~67% reduction)[cite: 8].
* **Industry Expenditure:** *Internal Corporate Ops* (23.36%), *Retail & E-Commerce* (23.08%), and *Technology & SaaS* (23.03%) account for **>69% of all payroll spending**[cite: 8].
* **Top Department Units:** *Application Modernization Unit 26* and *Unit 6* represent the largest year-over-year departmental costs (~5.3M–6.3M annually)[cite: 8].

---

## Strategic Business Recommendations

* **Audit February Accounting Operations:** Investigate whether February's $18.6M dip stems from contractor offboarding cycles, delayed bonus posts, or logging latency[cite: 8].
* **Optimize Industry Budget Allocation:** Re-assess resource allocation in lower-spend divisions like *Banking & FinTech* (13.20%) to support scaling requirements[cite: 8].
* **Reinvest Budget Surplus:** Channel the $21.56M favorable variance toward high-impact technology upskilling and strategic engineering hires[cite: 9].
