# **Case Study 1: DannysDiner**
Get codes here

---

### **Question 1:**
_What is the total amount each customer spent at the restaurant?_

``` SQL
SELECT 
    s.customer_id, SUM(m.price) AS TotalAmt
FROM
    sales s
        JOIN
    menu m ON s.product_id = m.product_id
GROUP BY s.customer_id;
```
#### Explanation of SQL Query: Two tables, sales and menu were joined, grouped by customer_id to get the SUM of amount spent.
### Output:
![Image](https://github.com/EdithEbere/Case-Study-1_DannysDiner/blob/main/Images/Q1.PNG)
#### Customer with id "A" spent the most out of all three.

---
### **Question 2:**
_How many days has each customer visited the restaurant?_
```SQL
SELECT 
    customer_id, COUNT(DISTINCT order_date) AS NumberOfDays
FROM
    sales
GROUP BY customer_id;
```
#### Explanation of SQL Query: COUNT(DISTINCT order_date) will return unique count of the days each customer visited the DannysDiner to order
# ![Image](https://github.com/EdithEbere/Case-Study-1_DannysDiner/blob/main/Images/Q2.PNG)
#### Customer with id "B" visited the most.

---

