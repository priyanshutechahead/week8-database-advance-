### 1. INNER JOIN
- only the records where there is a match in both tables. Customers without accounts and accounts without valid customers are excluded.
<img width="864" height="540" alt="Screenshot 2026-07-08 at 2 06 48 PM" src="https://github.com/user-attachments/assets/4da8ed51-8184-43b4-8d5b-559424ba209f" />

### 2. LEFT OUTER JOIN (or LEFT JOIN)
- all records from the left table (customers), and the matched records from the right table (accounts). If there is no match, NULL values are returned for the right table's columns.
<img width="695" height="522" alt="Screenshot 2026-07-08 at 2 09 18 PM" src="https://github.com/user-attachments/assets/55d11410-5de8-44ab-a3a8-405995118770" />

### 3. RIGHT OUTER JOIN (or RIGHT JOIN)
- all records from the right table (accounts), and the matched records from the left table (customers). If there is no match, NULL values are returned for the left table's columns.
<img width="637" height="488" alt="Screenshot 2026-07-08 at 2 10 05 PM" src="https://github.com/user-attachments/assets/aa965ef7-468a-4b6d-9c5a-0b1ba4f0ca45" />

### 4. FULL OUTER JOIN
- all records when there is a match in either left or right table. It combines the results of both LEFT and RIGHT joins.
<img width="662" height="588" alt="Screenshot 2026-07-08 at 2 10 31 PM" src="https://github.com/user-attachments/assets/9a2b276f-d98d-47bc-80ae-7a5d19491ed5" />

### 5. CROSS JOIN (Cartesian Product)
- Pairs every single row from the first table with every single row from the second table. It does not use an ON clause. Since you have 10 customers and 10 branches, this query will generate exactly $10 \times 10 = 100$ rows.
<img width="646" height="825" alt="Screenshot 2026-07-08 at 2 13 25 PM" src="https://github.com/user-attachments/assets/9e1e5ddd-40dd-4aeb-8e75-9d7593f7e118" />


