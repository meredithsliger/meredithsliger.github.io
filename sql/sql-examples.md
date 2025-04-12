---
title: SQL Examples
description: Query and Join Examples from SQL Assignment 1 & 2 using Teradata ViewPoint (db_pvfc11_big)
---

# 🧠 SQL Query & Join Examples

These examples were written using **Teradata ViewPoint** and the **db_pvfc11_big** database. They demonstrate practical SQL skills including filtering, aggregation, joins, and set operations.

📎 **Download the full assignments and answers**:
- [SQL Assignment 1 – Question Set](../assets/sql/SQL_Assignment1-canvas.docx)
- [SQL Assignment 2 – Question Set](../assets/sql/SQL_Assignment2-canvas.docx)
- [SQL Assignment 1 – Answers](../assets/sql/SQL_Assignment1-Sliger_Meredith.docx)
- [SQL Assignment 2 – Answers](../assets/sql/SQL_Assignment2-Sliger_Meredith.docx)

---

## 🔹 Filtering & Basic WHERE Conditions

**Find all raw materials made of cherry and that have dimensions 12x12.**
```sql
SELECT *
FROM "db_pvfc11_big"."RawMaterial_T"
WHERE Material = 'Cherry' 
  AND Thickness = 12 
  AND Width = 12;
```

**Find raw materials that are not cherry or oak and have width > 10.**
```sql
SELECT MaterialName, Material, Width
FROM "db_pvfc11_big"."RawMaterial_T"
WHERE Material NOT IN ('Cherry', 'Oak') 
  AND Width > 10;
```

---

## 🔹 Aggregation & GROUP BY

**Average standard price per product line.**
```sql
SELECT ProductLineID, AVG(ProductStandardPrice) AS AvgStandardPrice
FROM "db_pvfc11_big"."Product_T"
GROUP BY ProductLineID;
```

**Product lines with average product price > $200 and overall average >= $500.**
```sql
SELECT ProductLineID, AVG(ProductStandardPrice) AS AvgStandardPrice
FROM "db_pvfc11_big"."Product_T"
WHERE ProductStandardPrice > 200
GROUP BY ProductLineID
HAVING AVG(ProductStandardPrice) >= 500;
```

---

## 🔹 Join Logic (Including Self Joins)

**Employees born before their manager.**
```sql
SELECT e1.EmployeeName, e1.EmployeeBirthDate, 
       e2.EmployeeName AS Manager, e2.EmployeeBirthDate AS ManagerBirth
FROM "db_pvfc11_big"."Employee_T" e1
JOIN "db_pvfc11_big"."Employee_T" e2 ON e1.EmployeeSupervisor = e2.EmployeeID
WHERE e1.EmployeeBirthDate < e2.EmployeeBirthDate;
```

**Order line info with total price (Order ID = 1).**
```sql
SELECT ol.ProductID, p.ProductStandardPrice, 
       (ol.OrderedQuantity * p.ProductStandardPrice) AS TotalPrice
FROM "db_pvfc11_big"."OrderLine_T" ol
JOIN "db_pvfc11_big"."Product_T" p ON ol.ProductID = p.ProductID
WHERE ol.OrderID = 1;
```

---

## 🔹 Set Operations (MINUS, UNION, INTERSECT)

**States with customers but no salespeople.**
```sql
SELECT DISTINCT CustomerState
FROM "db_pvfc11_big"."Customer_T"
MINUS
SELECT DISTINCT SalespersonState
FROM "db_pvfc11_big"."Salesperson_T";
```

---

## 🔹 Multi-Table Queries & Conditional Joins

**Customers who ordered both Product ID 3 and 4.**
```sql
SELECT c.CustomerID, c.CustomerName
FROM "db_pvfc11_big"."Customer_T" c
JOIN "db_pvfc11_big"."Order_T" o ON c.CustomerID = o.CustomerID
JOIN "db_pvfc11_big"."OrderLine_T" ol1 ON o.OrderID = ol1.OrderID AND ol1.ProductID = 3
JOIN "db_pvfc11_big"."OrderLine_T" ol2 ON o.OrderID = ol2.OrderID AND ol2.ProductID = 4;
```

**Territories with more than one salesperson.**
```sql
SELECT SalesTerritoryID, COUNT(SalespersonID) AS NumSalesPersons
FROM "db_pvfc11_big"."Salesperson_T"
GROUP BY SalesTerritoryID
HAVING COUNT(SalespersonID) > 1;
```

---

## ✅ Summary
These examples demonstrate proficiency in SQL querying, joins, and aggregation using relational databases. The queries come from practical business scenarios involving customers, employees, and product data.
