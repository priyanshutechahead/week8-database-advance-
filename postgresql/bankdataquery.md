# Bank Database

### Create Database
- CREATE DATABASE bankdata

### CREATE TABLE (RELATION)
- accounts
- branches
- customers

### Table Creation Commands
```
CREATE TABLE customers (
    customer_id SERIAL PRIMARY KEY,
    first_name VARCHAR(50), 
    last_name VARCHAR(50),
    city VARCHAR(50), 
    email VARCHAR(100), 
    join_date DATE
);

CREATE TABLE accounts (
    account_id SERIAL PRIMARY KEY,
    customer_id INT, 
    balance DECIMAL(10, 2),
    account_type VARCHAR(20), 
    status VARCHAR(20)
);

CREATE TABLE branches (
    branch_id SERIAL PRIMARY KEY,
    branch_name VARCHAR(50), 
    location VARCHAR(50), 
    manager_name VARCHAR(50)
);
```

### Insertion of values in table command
```
INSERT INTO customers (first_name, last_name, city, email, join_date) VALUES  
('Alice', 'Smith', 'New York', 'alice@example.com', '2025-01-10'),
('Bob', 'Jones', 'London', 'bob@example.com', '2025-02-15'),
('Charlie', 'Brown', 'New York', 'charlie@example.com', '2025-03-20'),
('David', 'Wilson', 'Tokyo', 'david@example.com', '2025-04-05'),
('Eve', 'Davis', 'Paris', 'eve@example.com', '2025-05-12'),
('Frank', 'Miller', 'London', 'frank@example.com', '2025-06-01'),
('Grace', 'Moore', 'New York', 'grace@example.com', '2025-07-18'),
('Heidi', 'Taylor', 'Berlin', 'heidi@example.com', '2025-08-22'),
('Ivan', 'Anderson', 'Tokyo', 'ivan@example.com', '2025-09-30'),
('Judy', 'Thomas', 'Paris', 'judy@example.com', '2025-10-11');

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

INSERT INTO branches (branch_name, location, manager_name) VALUES  
('Manhattan', 'NY, USA', 'Sarah Lane'), 
('Canary Wharf', 'London, UK', 'Tom Hardy'),
('Shinjuku', 'Tokyo, JP', 'Kenji Sato'), 
('Le Marais', 'Paris, FR', 'Marie Curie'),
('Mitte', 'Berlin, DE', 'Hans Muller'), 
('Brooklyn', 'NY, USA', 'John Doe'),
('Westminster', 'London, UK', 'Jane Eyre'), 
('Ginza', 'Tokyo, JP', 'Yuki Tanaka'),
('Montmartre', 'Paris, FR', 'Pierre Dubois'), 
('Prenzlauer', 'Berlin, DE', 'Anna Schmidt');
```
