# **CaseStudy #1: Danny'sDiner**
---

1. What is the total amount each customer spent at the restaurant?

``` SQL
SELECT 
    s.customer_id, SUM(m.price) AS TotalAmt
FROM
    sales s
        JOIN
    menu m ON s.product_id = m.product_id
GROUP BY s.customer_id;
```

### Output 1: 
![Image](https://github.com/EdithEbere/Case-Study-1_DannysDiner/blob/main/Images/Q1.PNG)

Customer with id "A" spent the most out of all three.

Commentary: 

* Two tables, sales and menu were joined and grouped by customer_id to get the total amount spent by each customer.

---

2. How many days has each customer visited the restaurant?
```SQL
SELECT 
    customer_id, COUNT(DISTINCT order_date) AS NumberOfDays
FROM
    sales
GROUP BY customer_id;
```

### Output 2: 
![Image](https://github.com/EdithEbere/Case-Study-1_DannysDiner/blob/main/Images/Q2.PNG)

Customer with id "B" visited the most.

Commentary: 

* COUNT(DISTINCT order_date) will return number of the days each customer visited the Danny's Diner to order

---

3. What was the first item from the menu purchased by each customer?
```SQL
WITH FirstOrder AS
(SELECT 
    customer_id, order_date, product_name, dense_rank() OVER (partition by customer_id order by order_date) AS OrderRank
FROM
    sales s
        JOIN
    menu m ON s.product_id = m.product_id)

SELECT customer_id, order_date, product_name
FROM FirstOrder
WHERE OrderRank = 1;
```

### Output 3:
![Image](https://github.com/EdithEbere/Case-Study-1_DannysDiner/blob/main/Images/Q3.PNG)

Commentary: 

* Using CTE, a subquery was created to pull out the each customer's orders and order date. 
* DENSERANK() ranked the order from each customer according to their order date, that is the first order is ranked 1 followed by 2 etc.
* PARTITION BY acts like the GROUP BY, here the resukt is grouped by customers 
* ORDER BY helps to order result by order date within each partition. 
