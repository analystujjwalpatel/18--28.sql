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

-- Day 20/30 days sql challenge 

CREATE TABLE zomato_orders(
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    price FLOAT,
    city VARCHAR(25)
);

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

SELECT city, COUNT(customers) AS total_customers
FROM (
    SELECT city,
           customer_id AS customers,
           COUNT(order_id) AS total_orders
    FROM public.zomato_orders
    WHERE order_date BETWEEN '2023-11-01' AND '2023-11-30'
    GROUP BY city, customer_id
    HAVING COUNT(order_id) > 3
) subquery
GROUP BY city;

----------------------------------------------------------------------------------------------------

-- 21/30 days sql challenge 

CREATE TABLE hotel_revenue (
    hotel_id INT,
    month VARCHAR(10),
    year INT,
    revenue DECIMAL(10, 2)
);

WITH table1 AS (
    SELECT month,
           year,
           hotel_id,
           revenue,
           DENSE_RANK() OVER (PARTITION BY hotel_id, year ORDER BY revenue DESC) drn
    FROM public.hotel_revenue
)
SELECT month,
       year,
       hotel_id,
       revenue
FROM table1
WHERE drn <= 2;

----------------------------------------------------------------------------------------------------

-- 22 to 28 code continues exactly same pattern as above


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
		
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
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


--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------

-- 25/30 SQL Challenge

-- ----------------------------------------------------------------------------------
-- Question 1
-- ----------------------------------------------------------------------------------

-- Dropping the table if it exists and then recreating it
DROP TABLE IF EXISTS orders;

-- Creating the orders table
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    amount DECIMAL(10,2)
);

-- Inserting sample data into the orders table
INSERT INTO orders (order_id, customer_id, order_date, amount) VALUES
(1, 101, '2024-01-01', 500),
(2, 102, '2024-01-03', 300),
(3, 101, '2024-01-05', 700),
(4, 103, '2024-01-07', 200),
(5, 102, '2024-01-10', 900),
(6, 101, '2024-01-12', 400),
(7, 104, '2024-01-15', 600),
(8, 103, '2024-01-18', 1000),
(9, 104, '2024-01-20', 750),
(10, 102, '2024-01-25', 650);

select * from public.orders

/*
Write a SQL query to find the total order amount for each customer.
Return customer_id and total_amount.
*/

select 
    customer_id,
    sum(amount) as total_amount
from public.orders
group by 1


--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------

-- 26/30 SQL Challenge

-- ----------------------------------------------------------------------------------
-- Question 1
-- ----------------------------------------------------------------------------------

-- Dropping the table if it exists and then recreating it
DROP TABLE IF EXISTS products;

-- Creating the products table
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    price DECIMAL(10,2)
);

-- Inserting sample data into the products table
INSERT INTO products (product_id, product_name, price) VALUES
(1, 'Laptop', 60000),
(2, 'Mobile', 25000),
(3, 'Tablet', 30000),
(4, 'Headphones', 2000),
(5, 'Keyboard', 1500),
(6, 'Mouse', 800),
(7, 'Monitor', 12000),
(8, 'Printer', 10000),
(9, 'Camera', 45000),
(10, 'Speaker', 5000);

select * from public.products

/*
Write a SQL query to find the second highest price from the products table.
*/

select 
    max(price) as second_highest_price
from public.products
where price < (select max(price) from public.products)


--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------

-- 27/30 SQL Challenge

-- ----------------------------------------------------------------------------------
-- Question 1
-- ----------------------------------------------------------------------------------

-- Dropping the table if it exists and then recreating it
DROP TABLE IF EXISTS sales;

-- Creating the sales table
CREATE TABLE sales (
    sale_id INT PRIMARY KEY,
    product_id INT,
    quantity INT,
    sale_date DATE
);

-- Inserting sample data into the sales table
INSERT INTO sales (sale_id, product_id, quantity, sale_date) VALUES
(1, 1, 2, '2024-01-01'),
(2, 2, 5, '2024-01-02'),
(3, 1, 3, '2024-01-05'),
(4, 3, 4, '2024-01-07'),
(5, 2, 1, '2024-01-10'),
(6, 4, 6, '2024-01-12'),
(7, 5, 2, '2024-01-15'),
(8, 3, 7, '2024-01-18'),
(9, 1, 1, '2024-01-20'),
(10, 2, 3, '2024-01-25');

select * from public.sales

/*
Write a SQL query to find the total quantity sold for each product.
Return product_id and total_quantity.
*/

select 
    product_id,
    sum(quantity) as total_quantity
from public.sales
group by 1

--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------

-- 28/30 SQL Challenge

-- ----------------------------------------------------------------------------------
-- Question 1
-- ----------------------------------------------------------------------------------

-- Dropping the table if it exists and then recreating it
DROP TABLE IF EXISTS students;

-- Creating the students table
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(100),
    marks INT
);

-- Inserting sample data into the students table
INSERT INTO students (student_id, student_name, marks) VALUES
(1, 'Aman', 85),
(2, 'Riya', 92),
(3, 'Karan', 76),
(4, 'Sneha', 89),
(5, 'Rahul', 95),
(6, 'Priya', 67),
(7, 'Vikas', 73),
(8, 'Neha', 88),
(9, 'Arjun', 90),
(10, 'Pooja', 81);

select * from public.students

/*
Write a SQL query to find the student with the highest marks.
Return student_name and marks.
*/

select 
    student_name,
    marks
from public.students
where marks = (select max(marks) from public.students)

