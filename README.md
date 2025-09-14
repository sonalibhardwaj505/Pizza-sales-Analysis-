Pizza Sales Data Analysis

This project analyzes pizza sales data to help a restaurant understand performance, customer preferences, and revenue patterns. Using SQL queries, the dataset was explored to uncover insights and provide actionable recommendations for business growth.

 Business Problem

The restaurant wanted to answer key business questions, such as:

How many total orders were placed?
What is the total revenue generated from pizza sales?
Which pizza is the most expensive?
Which pizza sizes are most popular?
What are the top 5 best-selling pizzas?
Which categories (Classic, Veggie, Supreme, etc.) do customers prefer?
What times of day see the most orders?
What is the average number of pizzas sold per day?
Which pizzas bring in the highest revenue?
How much does each pizza type contribute to total revenue?
How has revenue grown over time?

📊 Key Findings

Total Orders: 21,350
Total Revenue: ₹817,860.05
Most Expensive Pizza: Greek Pizza
Most Popular Pizzas: Classic Deluxe, Barbecue Chicken, Hawaiian, Pepperoni
Average Daily Sales: 138 pizzas/day
Peak Ordering Times: Lunch & Dinner
Top Revenue Pizzas: Thai Chicken, Barbecue Chicken, California Pizza
Popular Categories: Classic, Supreme, Chicken, Veggie
Revenue Trend: Steadily growing over time
Category Insights: Each category has a few “star” pizzas driving most revenue

 Tools & Techniques

SQL for data extraction and analysis

Data Visualization (presentation insights)
Business Intelligence approach for actionable recommendations
  SQL Queries
  
1. Total Orders
SELECT COUNT(order_id) AS total_orders
FROM orders;

2. Total Revenue
SELECT ROUND(SUM(order_details.quantity * pizzas.price), 2) AS total_revenue
FROM order_details
JOIN pizzas ON order_details.pizza_id = pizzas.pizza_id;

3. Most Expensive Pizza
SELECT pizza_name, price
FROM pizzas
ORDER BY price DESC
LIMIT 1;

4. Most Popular Pizza Sizes
SELECT size, COUNT(order_details.order_details_id) AS total_sold
FROM order_details
JOIN pizzas ON order_details.pizza_id = pizzas.pizza_id
GROUP BY size
ORDER BY total_sold DESC;

5. Top 5 Best-Selling Pizzas
SELECT pizza_name, SUM(order_details.quantity) AS total_sold
FROM order_details
JOIN pizzas ON order_details.pizza_id = pizzas.pizza_id
GROUP BY pizza_name
ORDER BY total_sold DESC
LIMIT 5;

6. Revenue by Pizza Category
SELECT category, ROUND(SUM(order_details.quantity * pizzas.price), 2) AS revenue
FROM order_details
JOIN pizzas ON order_details.pizza_id = pizzas.pizza_id
GROUP BY category
ORDER BY revenue DESC;

7. Average Pizzas Sold Per Day
SELECT ROUND(AVG(daily_sales), 0) AS avg_pizzas_per_day
FROM (
    SELECT orders.order_date, SUM(order_details.quantity) AS daily_sales
    FROM orders
    JOIN order_details ON orders.order_id = order_details.order_id
    GROUP BY orders.order_date
) AS subquery;

8. Revenue Trend Over Time
SELECT DATE_TRUNC('month', orders.order_date) AS month, 
       ROUND(SUM(order_details.quantity * pizzas.price), 2) AS revenue
FROM orders
JOIN order_details ON orders.order_id = order_details.order_id
JOIN pizzas ON order_details.pizza_id = pizzas.pizza_id
GROUP BY month
ORDER BY month;

  Recommendations

Focus on Best-Sellers:  Keep best-selling pizzas well stocked and promote them regularly.
Improve or Remove Weak Performers:  Adjust recipes/marketing or consider dropping low-selling pizzas.
Inventory & Staff Planning:  Stock popular sizes more, and schedule more staff during lunch/dinner rush.
Upsell Premium Pizzas:  Market Greek Pizza as a premium offering.
Category Promotions:  Bundle popular and weaker pizzas (e.g., Classic + Veggie deals).
Targeted Marketing:  Offer discounts during off-peak hours.
Track Growth Regularly:  Continue monitoring revenue trends monthly to guide strategy.

  Author

Sonali Bhardwaj
Data Analyst | SQL Enthusiast | Business Insights
