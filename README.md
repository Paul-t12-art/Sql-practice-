SELECT setval('orders_order_id_seq', (SELECT MAX(order_id) FROM orders));
SELECT COUNT(*) FROM orders;

SELECT
    customer.customer_name,
    SUM(orders.amount) AS total_spent
FROM orders
JOIN customer ON orders.customer_id = customer.customer_id
GROUP BY customer.customer_name
ORDER BY total_spent DESC;

SELECT
    product,
    COUNT(*) AS times_ordered,
    SUM(amount) AS total_revenue
FROM orders
GROUP BY product
ORDER BY total_revenue DESC;

SELECT
    customer.customer_name,
    SUM(orders.amount) AS total_spent
FROM orders
JOIN customer ON orders.customer_id = customer.customer_id
GROUP BY customer.customer_name
HAVING SUM(orders.amount) > 1000
ORDER BY total_spent DESC;


SELECT
    EXTRACT(YEAR FROM order_date) AS order_year,
    SUM(amount) AS total_revenue
FROM orders
GROUP BY order_year
ORDER BY order_year;

SELECT
    DATE_TRUNC('month', order_date) AS order_month,
    SUM(amount) AS total_revenue
FROM orders
GROUP BY order_month
ORDER BY order_month;

SELECT
    orders.order_id,
    customer.customer_name,
    customer.city,
    orders.product,
    orders.amount,
    TO_CHAR(orders.order_date, 'YYYY-MM-DD') AS order_date,
    EXTRACT(YEAR FROM orders.order_date) AS order_year,
    TO_CHAR(DATE_TRUNC('month', orders.order_date), 'YYYY-MM') AS order_month
FROM orders
JOIN customer ON orders.customer_id = customer.customer_id
ORDER BY orders.order_date;
