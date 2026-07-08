## Bank database layer - testing
### Database schema overviews
- customers: Stores personal profiles of bank clients.
- accounts: Tracks financial holdings, account classifications, and current statuses.
- branches: Logs bank branch information and regional management.

## Database test
### 1. Data Integrity & Constraint Tests (Expected Failures)
- These test assertions ensure that table level constraints strictly prevent corrupt data entry.

|Test ID |	Test Objective |	SQL Action / Scenario |	Expected Database Behavior |
|:---|:---|:---|:---|
|TC-01|	Primary Key Uniqueness (customers)|	Explicitly insert a duplicate customer_id.|	Fail / Error: Duplicate key value violates unique constraint.|
|TC-02|Primary Key Uniqueness (accounts)|	Explicitly insert a duplicate account_id.|	Fail / Error: Duplicate key value violates unique constraint.|
|TC-03|Primary Key Auto-Increment (SERIAL)|	Insert a customer without providing a customer_id.	|Pass: PostgreSQL automatically assigns the next sequential integer.|
|TC-04|Data Boundary Limits (VARCHAR)	|Insert a first_name exceeding 50 characters.	|Fail / Error: Value too long for type character varying(50).|
|TC-05|Numeric Scale Adjustments| Insert an account with a scale of 3 decimals (100.555).|Pass / Auto-round: System truncates/rounds value to 100.56 per DECIMAL(10,2).

### 2. Referential Integrity Tests (Orphaned Data Tracking)
|Test ID|	Test Objective	|SQL Action / Scenario|	Current Schema Result|	Production Target Standard|
|:---|:---|:---|:---|:---|
|TC-06|Null Value Processing|Insert an account containing a customer_id of NULL.|Pass (Record is added cleanly).|Pass (Standard behavior unless restricted).|
|TC-07|Orphaned Data Validation|Insert an account pointing to a non-existent customer_id (e.g., 99).|Pass (Current system allows orphaned rows).|Fail / Error: Violates explicit foreign key rules.|

### 3. Functional Queries & Aggregations (Expected Success)
- Run these queries against your active database instance to test the logic of data extractions.

#### TC-08: Active Customer to Account Relationship Match (Inner Join)
- Objective: Verify matched accounts and display customer names.
```
SELECT c.first_name, c.last_name, a.account_type, a.balance 
FROM customers c
INNER JOIN accounts a ON c.customer_id = a.customer_id
WHERE a.status = 'Active';
```
- Expected Output: 6 rows returned. All records matching orphaned IDs (99, 100, NULL) must be completely filtered out.

#### TC-09: Unlinked Account Discoveries (Left Join Isolation)
- Objective: Find all accounts without a matching customer profile.
```
SELECT a.account_id, a.customer_id, a.balance 
FROM accounts a
LEFT JOIN customers c ON a.customer_id = c.customer_id
WHERE c.customer_id IS NULL;
```
- Expected Output: 3 rows returned (Identifies the rows with IDs: NULL, 99, and 100).

- #### TC-10: Fiscal Data Aggregation (Grouped Summary)
- Objective: Calculate total balances across account category pools.
```
SELECT account_type, SUM(balance) AS total_balance 
FROM accounts 
GROUP BY account_type;
```
##### Expected Output:
- Savings: 25000.50
- Checking: 9000.50

### 4. Edge Cases & Boundary Conditions
|Test ID|	Test Objective	|SQL Action / Scenario|	Expected database Behavior|
|:---|:---|:---|:---|
|TC-11|Zero/Negative Parameters|Input financial balances of exactly 0.00 or negative values like -500.00.|Pass (Allowed unless a CHECK constraint rule is added).|
|TC-12|Redundant Text Entries|Insert a new branch matching an existing name and location details.|Pass (Allowed unless a UNIQUE identifier is bound to the column).|
|TC-13|Date Boundaries|Add a customer record with a future date placeholder (e.g., 2030-01-01).|Pass (Allowed unless time rules are validated via logic validation).|


