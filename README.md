# 📊 SQL for Data Analysis – Task 4 Submission

## ✅ Objective:
Use SQL queries to extract and analyze data from the Superstore dataset.

---

## 📁 Dataset Used:
- Dataset Name: Raw - Superstore.csv
- Total Rows: ~10,000
- Imported into: MySQL

---

## 🔧 Tools:
- MySQL Workbench
- MySQL Server
- VS Code / Notepad for .sql file
- Excel (for pre-cleaning)
- (Optional) Tableau for visualization

---

## 🔍 Query Results and Screenshots

### a. SELECT, WHERE, ORDER BY, GROUP BY

**Query 1: All orders from California**
```sql
SELECT * FROM superstore_orders WHERE state = 'California';
```
![image](https://github.com/user-attachments/assets/3c7ccf60-b4f5-4b7c-b463-bb6606f910be)




---

**Query 2: Top 10 highest selling orders**
```sql
SELECT * FROM superstore_orders ORDER BY sales DESC LIMIT 10;
```
![image](https://github.com/user-attachments/assets/087d0d83-649d-4e51-8306-9f9836edb770)



---

**Query 3: Total sales by Region**
```sql
SELECT region, SUM(sales) AS total_sales FROM superstore_orders GROUP BY region ORDER BY total_sales DESC;
```
![image](https://github.com/user-attachments/assets/a5585741-8c7e-4fb0-93ed-5566ddf4e537)




---

### b. JOINS (INNER, LEFT, RIGHT)

**INNER JOIN: Sales by Region and Manager**
```sql
SELECT o.region, r.manager, SUM(o.sales) AS total_sales
FROM superstore_orders o
INNER JOIN region_manager r ON TRIM(o.region) = TRIM(r.region)
GROUP BY o.region, r.manager;
```
![image](https://github.com/user-attachments/assets/8784af30-a142-46d8-a77f-3d18f277fe01)




---

**LEFT JOIN: Show all managers even if no orders**
```sql
SELECT r.region, r.manager, COUNT(o.order_id) AS total_orders
FROM region_manager r
LEFT JOIN superstore_orders o ON TRIM(r.region) = TRIM(o.region)
GROUP BY r.region, r.manager;
```
![image](https://github.com/user-attachments/assets/3d6bd2eb-d743-4038-9b5d-a17675f99894)





---

**RIGHT JOIN: Similar to LEFT JOIN with reversed roles**
```sql
SELECT r.region, r.manager, SUM(o.sales) AS total_sales
FROM superstore_orders o
RIGHT JOIN region_manager r ON TRIM(o.region) = TRIM(r.region)
GROUP BY r.region, r.manager;
```
![image](https://github.com/user-attachments/assets/8cb20143-ee13-4bbd-926b-30f7443672a2)




---

### c. Subqueries

**Top customer by sales**
```sql
SELECT customer_name, total_sales
FROM (
  SELECT customer_name, SUM(sales) AS total_sales
  FROM superstore_orders
  GROUP BY customer_name
) AS customer_sales
ORDER BY total_sales DESC
LIMIT 1;
```
![image](https://github.com/user-attachments/assets/f094d88b-d89c-4f22-ae8c-42842c0eaf33)



---

### d. Aggregate Functions

```sql
SELECT 
  SUM(sales) AS total_sales,
  AVG(profit) AS avg_profit,
  MAX(discount) AS max_discount,
  MIN(sales) AS min_sale
FROM superstore_orders;
```
![image](https://github.com/user-attachments/assets/e0d5f18a-e48a-46de-bd6e-04ae1f0aa684)




---

### e. Views

**Create monthly sales view**
```sql
CREATE VIEW monthly_sales AS
SELECT DATE_FORMAT(order_date, '%Y-%m') AS month,
       SUM(sales) AS total_sales, SUM(profit) AS total_profit
FROM superstore_orders
GROUP BY month
ORDER BY month;
SELECT * FROM monthly_sales;
```
![image](https://github.com/user-attachments/assets/6e5ddccd-1ca3-4c2c-b508-c8afeaf3ca8f)



---

### f. Index Optimization

```sql
CREATE INDEX idx_state ON superstore_orders(state);
CREATE INDEX idx_region ON superstore_orders(region);
CREATE INDEX idx_order_date ON superstore_orders(order_date);
CREATE INDEX idx_customer_id ON superstore_orders(customer_id);
CREATE INDEX idx_product_name ON superstore_orders(product_name);
```
![image](https://github.com/user-attachments/assets/de257291-9c51-49e6-9f77-3c50fd322b9a)



---

## ✅ Submission Checklist:
- [ ] SQL file included (`Superstore_Analysis.sql`)
- [ ] Screenshots of all outputs
- [ ] This README filled with screenshots or output
