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
