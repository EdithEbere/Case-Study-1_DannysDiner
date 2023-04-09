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

Customer with id "A" spent the most out of all three.

![Image](https://github.com/EdithEbere/Case-Study-1_DannysDiner/blob/main/Images/Q1.PNG)

Commentary: 

Two tables, sales and menu were joined and grouped by customer_id to get the total amount spent by each customer.

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

Customer with id "B" visited the most.

![Image](https://github.com/EdithEbere/Case-Study-1_DannysDiner/blob/main/Images/Q2.PNG)



Commentary: 

* GROUP BY was used to group customers 
* COUNT(DISTINCT order_date) will return number of the days each customer visited the Danny's Diner to order

---

3. What was the first item from the menu purchased by each customer?
```SQL
WITH FirstOrder AS
(SELECT 
    customer_id, order_date, product_name, DENSE_RANK() OVER (PARTITION BY customer_id ORDER BY order_date) AS OrderRank
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

* Using CTE, a subquery was created to pull out the each customer's orders and order date. It is advised to run subquery to be sure it works independently. 
```SQL
SELECT 
    customer_id, order_date, product_name, DENSE_RANK() OVER (PARTITION BY customer_id ORDER BY order_date) AS OrderRank
FROM
    sales s
        JOIN
    menu m ON s.product_id = m.product_id
```
* DENSERANK() was used to rank the order from each customer according to their order date, that is the first order is ranked 1 followed by 2 etc.
* PARTITION BY acts like the GROUP BY function, here the result is grouped by customer A , B, C
* ORDER BY helps to order result by order date within each partition(remember we partitioned by customers A B C)

---
Q4. What is the most purchased item on the menu and how many times was it purchased by all customers?


```SQL
SELECT 
    product_name, MAX(MenuCount) TopOrder
FROM
    (SELECT 
        m.product_id, product_name, COUNT(*) MenuCount
    FROM
        sales s
    JOIN menu m ON m.product_id = s.product_id
    GROUP BY product_id
    ORDER BY 3 DESC) t1
```

### Output 4:
![Image](https://github.com/EdithEbere/Case-Study-1_DannysDiner/blob/main/Images/Q4.PNG)

Commentary:

* A subquery was used to get the count of number of times product on the menu was ordered
*
        * The subquery must be enclosed in parentheses
        * It must run indenpendently and named.
        
* The main query extracted the product with the highest count( ordered most)
