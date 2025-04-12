---
layout: default
title: Tableau Prep (ETL)
---

## 🧼 Tableau Prep + Data Cleaning (ETL)

This page highlights my work using **Tableau Prep Builder** to perform data cleansing, transformation, and integration tasks. The featured project showcases how I applied ETL (Extract, Transform, Load) techniques to prepare employee data for analysis.

---

### 📁 Featured Project: Employee Info ETL

**Overview**  
In this Tableau Prep Builder assignment, I combined data from two different sources—employee addresses and payroll records—to produce a clean and analysis-ready dataset. The key steps in the workflow included:

- Removing unnecessary columns and rows  
- Creating calculated fields:
  - `Bonus` = 1.5% of salary  
  - `New_Salary` = salary with a 2% raise  
  - `Years_Employed` based on hire date and today's date  
- Standardizing fields like gender, country, and state  
- Joining data sources on `Employee_ID`  
- Aggregating employee data by city (e.g., average salary, years employed)

---

### 🔧 Workflow Steps

**Input Datasets**:
- [`employee_info.xlsx`](../../data/employee_info%20(1).xlsx) – employee address info  
- [`employee_payroll.csv`](../../data/employee_payroll%20(1).csv) – payroll and employment details  

**Output Files**:
- [`Output_Employee_Info.hyper`](../../data/Output_Employee_Info.hyper) – final cleaned Tableau extract  
- [`Tableau Prep Assignment Instructions`](../../data/Tableau%20Prep%20Assignment%20(1).docx)

---

### 🖼️ Coming soon
- Screenshots of the Tableau Prep Flow  
- Preview of the aggregated summary table  

---

### 🧠 Skills Demonstrated
- Data wrangling and type conversion  
- Date calculations and conditional filtering  
- Field renaming and string formatting  
- Tableau Prep Join and Aggregate steps  

_This project emphasizes my understanding of practical data preparation workflows using visual tools._
