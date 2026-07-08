# Bank Database

### Create Database
- CREATE DATABASE bankdata

### Tables (RELATIONS)
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

<img width="504" height="541" alt="Screenshot 2026-07-08 at 12 05 16 PM" src="https://github.com/user-attachments/assets/9525889b-632b-486d-9904-3177b35a7fe6" />

### Insertion of values in table command
```
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
```
<img width="1000" height="758" alt="Screenshot 2026-07-08 at 12 16 04 PM" src="https://github.com/user-attachments/assets/5a4ea35a-35b0-48a5-961e-4d7fe276a247" />

### All tables (Relations)
```
- SELECT * FROM accounts;
- SELECT * FROM branches;
- SELECT * FROM customers;
```

#### Accounts Table
<img width="696" height="419" alt="Screenshot 2026-07-08 at 12 19 10 PM" src="https://github.com/user-attachments/assets/463879b5-5274-4a84-af0e-dc8ae077e786" />

#### Branches Table
<img width="713" height="467" alt="Screenshot 2026-07-08 at 12 19 27 PM" src="https://github.com/user-attachments/assets/8130ccea-ebad-45bd-a90a-713bfe9d9005" />

#### Customers Table
<img width="884" height="435" alt="Screenshot 2026-07-08 at 12 19 44 PM" src="https://github.com/user-attachments/assets/0e6e746e-0697-4f02-a4e7-f2b7729f33ec" />

### List all tables in the current schema
```
\dt
```

### List all tables in all schemas
```
\dt *.*
```

### To see the table structure  (Columns and data type)
```
\d <table name>
```



