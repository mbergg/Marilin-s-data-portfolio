# Case Study 1: Danny's Diner

## Task
Danny wants to deliver a more personalized experience to his customers to increase the loyalty. In order to do that, he needs to answer questions about customers' visiting patters, how much money they've spent and which menu items are their faovurite.

## Additional information: 
<img width="556" alt="Screenshot 2024-01-15 at 11 48 04" src="https://github.com/mbergg/Portfolio/assets/102917473/506ab7a9-7b33-43b6-8969-de12092c3c83">

## Questions and solutions

**1. What is the total amount each customer spent at the restaurant?**

```sql 
SELECT
sales.customer_id,
SUM(price) AS total_amount
FROM dannys_diner.menu
JOIN dannys_diner.sales ON sales.product_id = menu.product_id
GROUP BY sales.customer_id;
``` 

**Thought process**
* Working backwards: The end goal is to find **total amount spent per customer**. 
* To determine the amount per customer, I will **GROUP BY** `customer_id`
* Total amount consists of summarizing all the orders (use **SUM**`(price)`)
* I will **SELECT** `sales.customer_id` and `menu.price`, which are in separate tables. This means, I need to use **JOIN** to combine sales and menu tables

**Answer**

- Customer A spent 76 USD
- Customer B spent 74 USD
- Customer C spent 36 USD

**2. How many days has each customer visited the restaurant?**
```sql
SELECT
sales.customer_id,
COUNT(DISTINCT order_date) as nr_of_days
FROM dannys_diner.sales
GROUP BY sales.customer_id;
```
**Thought process**
- The end goal is to find the **total number of days per customer**.
- To determine the days per customer, I will **GROUP BY** `customer_id`
- To determine the total number of days (without duplicating multiple orders on the same day), I will **COUNT DISTINCT** `order_date`

**Answer**
- Customer A visited the restaurant 4 days.
- Customer B visited the restaurant 6 days.
- Customer C visited the restaurant 2 days. 
