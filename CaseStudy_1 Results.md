# **Case Study 1: DannysDiner**
Get codes here

---

### **Question 1:**
* What is the total amount each customer spent at the restaurant?

``` SQL
SELECT 
    s.customer_id, SUM(m.price) AS TotalAmt
FROM
    sales s
        JOIN
    menu m ON s.product_id = m.product_id
GROUP BY s.customer_id;
```
