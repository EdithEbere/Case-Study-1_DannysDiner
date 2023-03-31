# **CaseStudy #1: Danny'sDiner**
---

### **Question 1:** What is the total amount each customer spent at the restaurant?

``` SQL
SELECT 
    s.customer_id, SUM(m.price) AS TotalAmt
FROM
    sales s
        JOIN
    menu m ON s.product_id = m.product_id
GROUP BY s.customer_id;
```
#### Commentary: Two tables, sales and menu were joined and grouped by customer_id to get the total amount spent by each customer.
#### Output 1: Customer with id "A" spent the most out of all three.
![Image](https://github.com/EdithEbere/Case-Study-1_DannysDiner/blob/main/Images/Q1.PNG)

---

### **Question 2:** How many days has each customer visited the restaurant?
```SQL
SELECT 
    customer_id, COUNT(DISTINCT order_date) AS NumberOfDays
FROM
    sales
GROUP BY customer_id;
```
#### Commentary: COUNT(DISTINCT order_date) will return number of the days each customer visited the Danny's Diner to order
#### Output 2: Customer with id "B" visited the most.
![Image](https://github.com/EdithEbere/Case-Study-1_DannysDiner/blob/main/Images/Q2.PNG)

---

### **Question 3:**
_What was the first item from the menu purchased by each customer?_
```SQL
WITH CTE_FirstOrder AS 
(SELECT 
    customer_id, order_date, product_name, dense_rank() OVER (partition by customer_id order by order_date asc) AS OrderRank
FROM
    sales s
        JOIN
    menu m ON s.product_id = m.product_id
GROUP BY customer_id)
SELECT customer_id, order_date, product_name FROM CTE_FirstOrder
WHERE OrderRank = 1;
```
### Output 3:
![Image](https://github.com/EdithEbere/Case-Study-1_DannysDiner/blob/main/Images/Q3.PNG)
