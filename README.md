## 📌 Day 18/30 SQL Challenge

```sql
-- SWIGGY Interview Question

-- Create Table
CREATE TABLE restaurant_orders (
    city VARCHAR(50),
    restaurant_id INT,
    order_id INT,
    order_date DATE
);

-- Insert Records
INSERT INTO restaurant_orders (city, restaurant_id, order_id, order_date)
VALUES
('Delhi', 101, 1, '2021-09-05'),
('Bangalore', 102, 12, '2021-09-08'),
('Bangalore', 102, 13, '2021-09-08'),
('Bangalore', 102, 14, '2021-09-08'),
('Mumbai', 103, 3, '2021-09-10'),
('Mumbai', 103, 30, '2021-09-10'),
('Chennai', 104, 4, '2021-09-15'),
('Delhi', 105, 5, '2021-09-20'),
('Bangalore', 106, 6, '2021-09-25'),
('Mumbai', 107, 7, '2021-09-28'),
('Chennai', 108, 8, '2021-09-30'),
('Delhi', 109, 9, '2021-10-05'),
('Bangalore', 110, 10, '2021-10-08'),
('Mumbai', 111, 11, '2021-10-10'),
('Chennai', 112, 12, '2021-10-15'),
('Kolkata', 113, 13, '2021-10-20'),
('Hyderabad', 114, 14, '2021-10-25'),
('Pune', 115, 15, '2021-10-28'),
('Jaipur', 116, 16, '2021-10-30');

-- Question:
-- Which metro city had the highest number of restaurant orders in September 2021?

SELECT city,
       COUNT(order_id) AS total_orders
FROM restaurant_orders
WHERE city IN ('Delhi', 'Mumbai', 'Bangalore', 'Hyderabad')
  AND order_date BETWEEN '2021-09-01' AND '2021-09-30'
GROUP BY city
ORDER BY total_orders DESC
LIMIT 1;
```
----------------------------------------------------------------------------------------------------

----------------------------------------------------------------------------------------------------
```
-- Day 20/30 days sql challenge 

-- Schemas 


CREATE TABLE zomato_orders(
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    price FLOAT,
    city VARCHAR(25)
);


-- Insert sample records into the zomato_orders table
INSERT INTO zomato_orders (order_id, customer_id, order_date, price, city) VALUES
(1, 101, '2023-11-01', 150.50, 'Mumbai'),
(2, 102, '2023-11-05', 200.75, 'Delhi'),
(3, 103, '2023-11-10', 180.25, 'Mumbai'),
(4, 104, '2023-11-15', 120.90, 'Delhi'),
(5, 105, '2023-11-20', 250.00, 'Mumbai'),
(6, 108, '2023-11-25', 180.75, 'Gurgoan'),
(7, 107, '2023-12-30', 300.25, 'Delhi'),
(8, 108, '2023-12-02', 220.50, 'Gurgoan'),
(9, 109, '2023-11-08', 170.00, 'Mumbai'),
(10, 110, '2023-10-12', 190.75, 'Delhi'),
(11, 108, '2023-10-18', 210.25, 'Gurgoan'),
(12, 112, '2023-11-24', 280.50, 'Mumbai'),
(13, 113, '2023-10-29', 150.00, 'Mumbai'),
(14, 103, '2023-11-03', 200.75, 'Mumbai'),
(15, 115, '2023-10-07', 230.90, 'Delhi'),
(16, 116, '2023-11-11', 260.00, 'Mumbai'),
(17, 117, '2023-11-16', 180.75, 'Mumbai'),
(18, 102, '2023-11-22', 320.25, 'Delhi'),
(19, 103, '2023-11-27', 170.50, 'Mumbai'),
(20, 102, '2023-11-05', 220.75, 'Delhi'),
(21, 103, '2023-11-09', 300.25, 'Mumbai'), 
(22, 101, '2023-11-15', 180.50, 'Mumbai'), 
(23, 104, '2023-11-18', 250.75, 'Delhi'), 
(24, 102, '2023-11-20', 280.25, 'Delhi'),
(25, 117, '2023-11-16', 180.75, 'Mumbai'),
(26, 117, '2023-11-16', 180.75, 'Mumbai'),
(27, 117, '2023-11-16', 180.75, 'Mumbai'),
(28, 117, '2023-11-16', 180.75, 'Mumbai');

select * from public.zomato_orders

/*
 zomato business analyst interview question

 Find city wise customers count who have placed 
 more than three orders in November 2023.
*/

select city, count(customers) as total_customers from
(
select 
     city, 
	 customer_id as customers,
	count(order_id)  as total_orders
	 from public.zomato_orders
	 where order_date between '2023-11-01' and '2023-11-30'
group by 1,2
having count(order_id) > 3 -- using fir filter function 
) subquery
group by 1
```
----------------------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------------------
--------------------------------------------------------
```
-- 21/30 days sql challenge 

-- SCHEMA

-- Create the hotel_revenue table
CREATE TABLE hotel_revenue (
    hotel_id INT,
    month VARCHAR(10),
    year INT,
    revenue DECIMAL(10, 2)
);


-- Insert sample records
INSERT INTO hotel_revenue (hotel_id, month, year, revenue) VALUES
(101, 'January', 2022, 15000.50),
(101, 'February', 2022, 18000.75),
(101, 'March', 2022, 20000.00),
(101, 'April', 2022, 20000.00),
(101, 'May', 2022, 20000.00),
(101, 'June', 2022, 20000.00),
(101, 'July', 2022, 26000.00),
(101, 'August', 2022, 28000.00),
(102, 'January', 2022, 12000.25),
(102, 'February', 2022, 14000.50),
(102, 'March', 2022, 16000.75),
(101, 'January', 2023, 17000.25),
(101, 'February', 2023, 19000.50),
(101, 'March', 2023, 21000.75),
(102, 'January', 2023, 13000.50),
(102, 'February', 2023, 15000.75),
(102, 'March', 2023, 17000.25),
(103, 'January', 2022, 11000.25),
(103, 'February', 2022, 13000.50),
(103, 'March', 2022, 15000.75),
(104, 'January', 2022, 14000.50),
(108, 'May', 2022, 31000.75),
(108, 'April', 2022, 28000.75),
(108, 'June', 2022, 16000.75),
(108, 'August', 2022, 16000.75),	
(104, 'March', 2022, 18000.25),
(103, 'January', 2023, 12000.50),
(103, 'February', 2023, 14000.75),
(103, 'March', 2023, 16000.25),
(104, 'January', 2023, 15000.75),
(107, 'February', 2023, 17000.25),
(106, 'March', 2023, 19000.50);

select * from public.hotel_revenue
-- Booking.com Data Analyst interview question

/*
Find the top-performing two months 
by revenue for each hotel for each year.
return hotel_id, year, month, revenue
*/

with table1
as
(
select 
	  month,
	  year,
	  hotel_id,
	  revenue,
dense_rank() over(partition by hotel_id, year order by revenue desc) drn
from public.hotel_revenue
)
select   month,
	  year,
	  hotel_id,
	  revenue
	  from table1
	  where drn <= 2
```

--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------

```
-- 22/30 days sql challenge 


CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(255),
    manager_id INT,
    FOREIGN KEY (manager_id) REFERENCES employees(emp_id)
);


-- Inserting records into the employees table
INSERT INTO employees (emp_id, emp_name, manager_id) VALUES
(1, 'John Doe', NULL),           -- John Doe is the manager
(2, 'Jane Smith', 1),            -- Jane Smith reports to John Doe
(3, 'Alice Johnson', 1),         -- Alice Johnson reports to John Doe
(4, 'Bob Williams', 2),          -- Bob Williams reports to Jane Smith
(5, 'Charlie Brown', 2),         -- Charlie Brown reports to Jane Smith
(6, 'David Lee', 3),             -- David Lee reports to Alice Johnson
(7, 'Emily Davis', 3),           -- Emily Davis reports to Alice Johnson
(8, 'Fiona Clark', 4),           -- Fiona Clark reports to Bob Williams
(9, 'George Turner', 4),         -- George Turner reports to Bob Williams
(10, 'Hannah Baker', 5),         -- Hannah Baker reports to Charlie Brown
(11, 'Isaac White', 5),          -- Isaac White reports to Charlie Brown
(12, 'Jessica Adams', 6),        -- Jessica Adams reports to David Lee
(13, 'Kevin Harris', 6);         -- Kevin Harris reports to David Lee

select * from public.employees
-- 
/*

-- TCS Data Analyst Interview question

Question
Write a SQL query to retrieve the emp_id, emp_name, and manager_name 
from the given employee table. 
It's important to note that managers are also employees in the table.

Employees table has 3 COLUMNS
-- emp_id, emp_name, maneger_id
*/

select e1.emp_id,
        e1. emp_name,
		e1. manager_id, 
		 e2.emp_name as manager_name
		 from employees as e1
cross join 
employees as e2
where 
e1.manager_id = e2.emp_id

		---------- aproch 1 

select e1.emp_id,
        e1. emp_name,
		e1. manager_id, 
		 e2.emp_name as manager_name
		 from employees as e1
left join 
employees as e2
on
e1.manager_id = e2.emp_id

---------------- aproch 2

select e1.emp_id,
        e1. emp_name,
		e1. manager_id, 
		 e2.emp_name as manager_name
		 from employees as e1
inner join 
employees as e2
on
e1.manager_id = e2.emp_id

		---------------- aproch 3
```		
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
```
-- 23/30 Days SQL Challenge

-- Dropping the table if it exists and then recreating it
DROP TABLE IF EXISTS employee;

-- Creating the employee table
CREATE TABLE employee (
    EMP_ID INT PRIMARY KEY,
    SALARY DECIMAL(10, 2)
);

-- Inserting sample data into the employee table
INSERT INTO employee (EMP_ID, SALARY) VALUES
(1, 50000),
(2, 60000),
(3, 70000),
(4, 45000),
(5, 80000),
(6, 55000),
(7, 75000),
(8, 62000),
(9, 48000),
(10, 85000);

select * from public.employee
/*
Question 1

Given the employee table with columns EMP_ID and SALARY, 
write an SQL query to find all salaries greater than the average salary.
return emp_id and salary
*/

select emp_ID,
        salary
      from employee
where salary > (select avg(salary) from employee)


--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------

-- 24/30 SQL Challenge

--  ----------------------------------------------------------------------------------
-- Questions 1
--  ----------------------------------------------------------------------------------	

-- SCHEMA 

-- Dropping the table if it exists and then recreating it
DROP TABLE IF EXISTS customers;

-- Creating the customers table
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100)
);

-- Inserting sample data into the customers table
INSERT INTO customers (customer_id, first_name, last_name, email) VALUES
(1, 'John', 'Doe', 'john.doe@example.com'),
(2, 'Jane', 'Smith', 'jane.smith@example.com'),
(3, 'Alice', 'Johnson', 'alice.johnson@example.com'),
(4, 'Bob', 'Brown', 'bob.brown@example.com'),
(5, 'Emily', 'Davis', 'john.doe@example.com'),
(6, 'Michael', 'Williams', 'michael.w@example.com'),
(7, 'David', 'Wilson', 'jane.smith@example.com'),
(8, 'Sarah', 'Taylor', 'sarah.t@example.com'),
(9, 'James', 'Anderson', 'james.a@example.com'),
(10, 'Laura', 'Martinez', 'laura.m@example.com');

select * from public.customers

/*
Consider a table named customers with the following columns: 
customer_id, first_name, last_name, and email. 
Write an SQL query to find all the duplicate email addresses 
in the customers table.

*/

select 
    email , 
	count(email) as email_cnt
from public.customers
group by 1
having count(email) > 1

```
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
```
-- 25/30

-- Drop the orders table if it exists
DROP TABLE IF EXISTS orders;

-- Create the orders table with columns: date, product_id, product_name, and revenue
CREATE TABLE orders (
    date DATE,
    product_id INT,
    product_name VARCHAR(255),
    revenue DECIMAL(10, 2)
);

-- Insert sample data into the orders table representing orders of iPhones
INSERT INTO orders (date, product_id, product_name, revenue) VALUES
('2024-01-01', 101, 'iPhone 13 Pro', 1000.00),
('2024-01-01', 102, 'iPhone 13 Pro Max', 1200.00),
('2024-01-02', 101, 'iPhone 13 Pro', 950.00),
('2024-01-02', 103, 'iPhone 12 Pro', 1100.00),
('2024-01-03', 102, 'iPhone 13 Pro Max', 1250.00),
('2024-01-03', 104, 'iPhone 11', 1400.00),
('2024-01-04', 101, 'iPhone 13 Pro', 800.00),
('2024-01-04', 102, 'iPhone 13 Pro Max', 1350.00),
('2024-01-05', 103, 'iPhone 12 Pro', 1000.00),
('2024-01-05', 104, 'iPhone 11', 700.00),
('2024-01-06', 101, 'iPhone 13 Pro', 600.00),
('2024-01-06', 102, 'iPhone 13 Pro Max', 550.00),
('2024-01-07', 101, 'iPhone 13 Pro', 400.00),
('2024-01-07', 103, 'iPhone 12 Pro', 250.00),
('2024-01-08', 102, 'iPhone 13 Pro Max', 200.00),
('2024-01-08', 104, 'iPhone 11', 150.00),
('2024-01-09', 101, 'iPhone 13 Pro', 100.00),
('2024-01-09', 102, 'iPhone 13 Pro Max', 50.00),
('2024-01-10', 101, 'iPhone 13 Pro', 1000.00),
('2024-01-10', 102, 'iPhone 13 Pro Max', 1200.00),
('2024-01-11', 101, 'iPhone 13 Pro', 950.00),
('2024-01-11', 103, 'iPhone 12 Pro', 1100.00),
('2024-01-12', 102, 'iPhone 13 Pro Max', 1250.00),
('2024-01-12', 104, 'iPhone 11', 1400.00);

select * from public.orders

/*
-- Flipkart Business Analyst Interview Question

Question: 
	Write a SQL query to calculate the running 
	total revenue for each combination of date and product ID.

Expected Output Columns: 
	date, product_id, product_name, revenue, running_total
	ORDER BY product_id, date ascending

*/

-- date, prod_id, prod_name, revenue, running_total

select 
      date,
	  product_id,
      	  product_name,
			revenue,
          sum(revenue)
 over( partition by product_id order by date)as running_total
	   from public.orders
order by product_id , date asc
```
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
```
-- 26/30 Days SQL Challenge

-- SCHEMA

DROP TABLE IF EXISTS orders;

CREATE TABLE orderss (
    order_id INT,
    customer_id INT,
    order_date DATE,
    total_items_ordered INT
);

INSERT INTO orderss VALUES
(1, 101, '2022-01-01', 5),
(2, 102, '2022-01-02', 10),
(3, 103, '2022-01-03', 8),
(4, 104, '2022-01-04', 12),
(5, 105, '2022-01-05', 15),
(6, 106, '2022-01-06', 20),
(7, 107, '2022-01-07', 25),
(8, 108, '2022-01-08', 30),
(9, 109, '2022-01-09', 35),
(10, 110, '2022-01-10', 40),
(11, 111, '2022-01-11', 45),
(12, 112, '2022-01-12', 50),
(13, 113, '2022-01-13', 55),
(14, 114, '2022-01-14', 60),
(15, 115, '2022-01-15', 65);


DROP TABLE IF EXISTS returns;

CREATE TABLE returns (
    return_id INT,
    order_id INT,
    return_date DATE,
    returned_items INT
);

INSERT INTO returns VALUES
(1, 1, '2022-01-03', 2),
(2, 2, '2022-01-05', 3),
(3, 3, '2022-01-07', 1),
(4, 5, '2022-01-08', 4),
(5, 6, '2022-01-08', 6),
(6, 7, '2022-01-09', 7),
(7, 8, '2022-01-10', 8),
(8, 9, '2022-01-11', 9),
(9, 10, '2022-01-12', 10),
(10, 11, '2022-01-13', 11),
(11, 12, '2022-01-14', 12),
(12, 13, '2022-01-15', 13),
(13, 14, '2022-01-16', 14),
(14, 15, '2022-01-17', 15);


select * from public.orderss
select * from public.returns
/*
-- Amazon Data Analyst Interview 
Hard Category Questions Time 15min

Question:

Suppose you are given two tables - Orderss and Returns. 
The Orders table contains information about orders placed by customers, 
and the Returns table contains information about returned items. 

Design a SQL query to 
find the top 5 customer with the highest percentage 
of returned items out of their total orders. 
	
Return the customer ID 
and the percentage of returned items rounded to two decimal places.

percentage of return item = sum(r.returned_items) * 100.0 / sum(o.total_items_ordered),

*/

-- customer_id,
-- total_items_ordered by each cx
-- total_items_returned by each cx
-- 2/4*100 50% total_items_returned/total_items_ordered*100

select 
        customer_id,
		total_items_ordered,
		returned_items,
		round(sum(returned_items)*100 / sum(total_items_ordered ), 2) as return_percentage
from orderss as o
join returns as r
on 
o.order_id = r.order_id
group by 1,2,3
order by return_percentage desc
limit 5
```
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------

```
-- 27/30 

-- SCHEMAS

DROP TABLE IF EXISTS ordersss;

-- Create the orders table
CREATE TABLE ordersss (
    user_id INT,
    item_ordered VARCHAR(512)
);

-- Insert sample data into the orders table
INSERT INTO ordersss VALUES 
('1', 'Pizza'),
('1', 'Burger'),
('2', 'Cold Drink'),
('2', 'Burger'),
('3', 'Burger'),
('3', 'Cold Drink'),
('4', 'Pizza'),
('4', 'Cold Drink'),
('5', 'Cold Drink'),
('6', 'Burger'),
('6', 'Cold Drink'),
('7', 'Pizza'),
('8', 'Burger');

select * from public.ordersss
-- Flipkart Data Analyst Interview Questions
-- Question: Write an SQL query to fetch user IDs that have only bought both 'Burger' and 'Cold Drink' items.

-- Expected Output Columns: user_id

select user_id
       -- item_ordered
from public.ordersss
group by 1
having count(distinct item_ordered) = 2
and sum(case when item_ordered in ('Burger', 'Cold Drink') then 1  else 0 end) = 2
```
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
```
-- 28/30 Days SQL Challenge!

DROP TABLE IF EXISTS oorders;

CREATE TABLE oorders (
    order_id INT PRIMARY KEY,
    seller_id INT,
    sale_amount DECIMAL(10, 2)
);


DROP TABLE IF EXISTS returns;

CREATE TABLE returnss (
    return_id INT PRIMARY KEY,
    seller_id INT,
    return_quantity INT
);


INSERT INTO oorders (order_id, seller_id, sale_amount) VALUES
(1, 101, 1500.00),
(2, 102, 2200.00),
(3, 103, 1800.00),
(4, 104, 2500.00),
(5, 107, 1900.00),
(6, 106, 2100.00),
(7, 107, 2400.00),
(8, 107, 1700.00),
(9, 108, 2000.00),
(10, 107, 2300.00),
(11, 103, 2600.00),
(12, 102, 2900.00),
(13, 101, 3100.00),
(14, 101, 2800.00),
(15, 101, 3300.00),
(16, 106, 2700.00),
(17, 101, 3000.00),
(18, 108, 3200.00),
(19, 107, 3400.00),
(20, 106, 3500.00),
(21, 101, 3600.00),
(22, 102, 3700.00),
(23, 103, 3800.00),
(24, 102, 3900.00),
(25, 105, 4000.00);

INSERT INTO returnss (return_id, seller_id, return_quantity) VALUES
(1, 101, 10),
(2, 102, 5),
(3, 103, 8),
(4, 104, 3),
(5, 105, 12),
(6, 106, 6),
(7, 107, 4),
(8, 108, 9);

select * from oorders
select * from returnss

/*
-- Amazon DS Interview Question?

-- Given two tables, oorders and returnss, containing sales and returns data for Amazon's 


write a SQL query to find the top 3 sellers with the highest sales amount 
but the lowest lowest return qty. 

*/

WITH orders_cte
AS
(
SELECT
	seller_id,
	SUM(sale_amount) as total_sales
FROM oorders
GROUP BY seller_id	
),

returns_cte
AS
(
SELECT
	seller_id,
	SUM(return_quantity) as total_return_qty
FROM returnss
GROUP BY seller_id
)

SELECT 
	orders_cte.seller_id as seller_id,
	orders_cte.total_sales as total_sale_amt,
	COALESCE(returns_cte.total_return_qty, 0) as total_return_qty
FROM orders_cte
LEFT JOIN
returns_cte
ON orders_cte.seller_id = returns_cte.seller_id
ORDER BY total_sale_amt DESC, total_return_qty ASC
```
LIMIT 3





