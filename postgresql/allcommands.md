# all pg admin commands 
```
-- create table for customers
CREATE TABLE customers (
    customer_id SERIAL PRIMARY KEY,
    first_name VARCHAR(50), 
    last_name VARCHAR(50),
    city VARCHAR(50), 
    email VARCHAR(100), 
    join_date DATE
);

-- create tables for accounts
CREATE TABLE accounts (
    account_id SERIAL PRIMARY KEY,
    customer_id INT, 
    balance DECIMAL(10, 2),
    account_type VARCHAR(20), 
    status VARCHAR(20)
);

-- create tables for branches
CREATE TABLE branches (
    branch_id SERIAL PRIMARY KEY,
    branch_name VARCHAR(50), 
    location VARCHAR(50), 
    manager_name VARCHAR(50)
);

-- insert values on customers table/relation
INSERT INTO customers (first_name, last_name, city, email, join_date) VALUES  
('vishal', 'singh', 'delhi', 'vishal@example.com', '2025-01-10'),
('rohit', 'bisht', 'bhopal', 'rohit@example.com', '2025-02-15'),
('kaustav', 'sahu', 'kolkata', 'kaustav@example.com', '2025-03-20'),
('nitin', 'yadav', 'surat', 'nitin@example.com', '2025-04-05'),
('rishabh', 'singh', 'lucknow', 'rishabh@example.com', '2025-05-12'),
('abhisekh', 'thakur', 'kathmandu', 'abhisekh@example.com', '2025-06-01'),
('aagman', 'verma', 'kathmandu', 'aagman@example.com', '2025-07-18'),
('ansh', 'gupta', 'meerut', 'ansh@example.com', '2025-08-22'),
('jatin', 'kumar', 'delhi', 'jatin@example.com', '2025-09-30'),
('raghav', 'rajoria', 'delhi', 'raghav@example.com', '2025-10-11');

-- insert values on accounts table/relation
INSERT INTO accounts (customer_id, balance, account_type, status) VALUES  
(1, 5000.00, 'Savings', 'Active'), 
(2, 3000.00, 'Checking', 'Active'),
(1, 1500.50, 'Checking', 'Active'), 
(3, 7500.00, 'Savings', 'Active'),
(5, 2000.00, 'Savings', 'Frozen'), 
(6, 4000.00, 'Checking', 'Active'),
(8, 9000.00, 'Savings', 'Active'), 
(NULL, 1200.00, 'Savings', 'Closed'),
(99, 500.00, 'Checking', 'Active'), 
(100, 300.00, 'Savings', 'Closed');

-- insert values on branches table/relation
INSERT INTO branches (branch_name, location, manager_name) VALUES  
('delhi', 'INDIA', 'Aarav Sharma'), 
('bhopal', 'MP, INDIA, UK', 'Vikram Singh'),
('kolkata', 'WB, INDIA', 'Amit Patel'), 
('surat', 'GUJARAT, INDIA', 'Priya Sharma'),
('lucknow', 'UP, INDIAUP, INDIA', 'Rajesh Kumar'), 
('noida', 'UP, INDIAUP, INDIA', 'Sanjay Gupta'),
('noida', 'UP, INDIA, UK', 'Deepak Verma'), 
('meerut', 'UP, INDIA', 'Anjali Desai'),
('delhi', 'INDIA', 'Rohan Mehta'), 
('delhi', 'INDIA', 'Neha Joshi');

-- display/show tables
SELECT * FROM accounts;
SELECT * FROM branches;
SELECT * FROM customers;

-- EXPLAIN/EXPLAIN ANALYZE
EXPLAIN ANALYZE
SELECT * FROM customers;

-- test case 08 (verify matched accounts and display customer names)
SELECT c.first_name, c.last_name, a.account_type, a.balance 
FROM customers c
INNER JOIN accounts a ON c.customer_id = a.customer_id
WHERE a.status = 'Active';

-- test case 09 (find all accounts without a matching customer profile)
SELECT a.account_id, a.customer_id, a.balance 
FROM accounts a
LEFT JOIN customers c ON a.customer_id = c.customer_id
WHERE c.customer_id IS NULL;

-- test case 09 (calculate total balances across account category pools)
SELECT account_type, SUM(balance) AS total_balance 
FROM accounts 
GROUP BY account_type;

-- test case like 09 (calculate total balances across account status)
SELECT status, SUM(balance) AS total_balance 
FROM accounts 
GROUP BY status;

-- inner join
SELECT 
    c.customer_id, 
    c.first_name, 
    c.city, 
    a.account_id, 
    a.balance, 
    a.account_type
FROM customers c
INNER JOIN accounts a ON c.customer_id = a.customer_id;

-- left outer join aka left join
SELECT 
    c.customer_id, 
    c.first_name, 
    c.city, 
    a.account_id, 
    a.balance
FROM customers c
LEFT JOIN accounts a ON c.customer_id = a.customer_id;

-- right outer join aka right join
SELECT 
    c.customer_id, 
    c.first_name, 
    a.account_id, 
    a.balance, 
    a.status
FROM customers c
RIGHT JOIN accounts a ON c.customer_id = a.customer_id;

-- full outer join
SELECT 
    c.customer_id AS cust_table_id, 
    c.first_name, 
    a.customer_id AS acct_table_id, 
    a.account_id, 
    a.balance
FROM customers c
FULL OUTER JOIN accounts a ON c.customer_id = a.customer_id;

-- cross join
SELECT 
    c.first_name, 
    c.city AS customer_city, 
    b.branch_name, 
    b.manager_name
FROM customers c
CROSS JOIN branches b;

-- self join complex
SELECT 
    c1.first_name AS customer_1, 
    c2.first_name AS customer_2, 
    c1.city
FROM customers c1
INNER JOIN customers c2 ON c1.city = c2.city AND c1.customer_id < c2.customer_id;
```
