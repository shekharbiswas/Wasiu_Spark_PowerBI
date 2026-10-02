# Week 2 — Day 2: Tasks
## Hands-On Step-by-Step (Databricks Community Edition)

**Estimated Time: 6 hours**
*(includes warm-up repetition, guided steps, exploration time, and independent repeat practice — pace is intentionally slow, no rushing)*

**Datasets used today:**
- `superstore_sales_cleaned` (the clean table created yesterday, Week 2 Day 1)
- `category_details.csv` (new small lookup table — upload this today)

---

### Step 1: Warm-Up — Recap Day 1 (30-45 min)
1. Log in to Databricks Community Edition
2. Go to **Compute** and confirm the cluster is running (start it again if it shows stopped)
3. Open yesterday's notebook (`Week2_Day1_DataCleaning`) and re-run this from memory, with light guidance only if stuck:
```sql
SELECT COUNT(*) AS clean_row_count
FROM workspace.default.superstore_sales_cleaned;
```

**Explain to student:** "We always start by repeating what we did before — this is how it becomes second nature."

---

### Step 2: Upload the New Lookup Table
1. On the left sidebar, click **Catalog** (or **Data**)
2. Click **Create Table** / **Add Data** / **Upload File**
3. Upload `category_details.csv`
4. Note the table name Databricks gives it (e.g. `workspace.default.category_details`) — write it down

**Explain to student:** "This is a small reference table — only 3 rows, one for each product category. Small lookup tables like this are extremely common in real business data."

---

### Step 3: Look at Both Tables First
In a new notebook cell (create it named `Week2_Day2_Joins`, language SQL, attached to the cluster), run:

```sql
SELECT * FROM workspace.default.category_details;
```
<img width="1516" height="615" alt="image" src="https://github.com/user-attachments/assets/c3088584-ed19-4939-8b95-ce10ba278cbe" />

```sql
SELECT Order_ID, Customer_Name, Category, Sales
FROM workspace.default.superstore_sales_cleaned
LIMIT 10;
```
<img width="1502" height="687" alt="image" src="https://github.com/user-attachments/assets/a94a5e82-77c4-4312-9abc-e1c1276b7902" />

**Ask the student:** "What column do both tables have in common?" (Answer: `Category`)

---

### Step 4: Your First JOIN (INNER JOIN)
In a new cell, type and run:

```sql
SELECT s.Order_ID, s.Customer_Name, s.Category, s.Sales,
       c.Category_Manager, c.Warehouse_Location
FROM workspace.default.superstore_sales_cleaned s
INNER JOIN workspace.default.category_details c
  ON s.Category = c.Category
LIMIT 10;
```
<img width="1503" height="696" alt="image" src="https://github.com/user-attachments/assets/cff59783-b53a-4b18-afec-744566cb510f" />

**Explain to student:**
- `s` and `c` are short nicknames (aliases) for the two tables, so we don't have to type the full table name every time
- `ON s.Category = c.Category` tells Spark exactly how to match rows between the two tables

**Ask the student:** "Do you see the new columns `Category_Manager` and `Warehouse_Location` now attached to each sales row?"

---

### Step 5: Confirm No Rows Were Lost (or Were They?)
In a new cell, type and run:

```sql
SELECT COUNT(*) AS joined_row_count
FROM workspace.default.superstore_sales_cleaned s
INNER JOIN workspace.default.category_details c
  ON s.Category = c.Category;
```
<img width="1506" height="660" alt="image" src="https://github.com/user-attachments/assets/0159ed30-6a89-4a42-8f09-aa64d85193ba" />

Compare this to yesterday's clean row count.

**Ask the student:** "Is this number the same, smaller, or bigger than yesterday's clean row count? Why do you think that is?" *(Should be the same, since every Category in the sales table has a match in the lookup table.)*

---

### Step 6: Try a LEFT JOIN and Compare
In a new cell, type and run:

```sql
SELECT s.Order_ID, s.Customer_Name, s.Category, s.Sales,
       c.Category_Manager, c.Warehouse_Location
FROM workspace.default.superstore_sales_cleaned s
LEFT JOIN workspace.default.category_details c
  ON s.Category = c.Category
LIMIT 10;
```
<img width="1517" height="712" alt="image" src="https://github.com/user-attachments/assets/30a6b5eb-c0ed-46ce-a70b-1f828e26488d" />

**Explain to student:** "In this case, the result looks the same as INNER JOIN, because every category has a match. LEFT JOIN really shows its value when a match is *missing* — it keeps the row anyway and just leaves the new columns blank."

---

### Step 7: See LEFT JOIN's Real Value (Simulate a Missing Match)
In a new cell, type and run this query, which filters the lookup table down before joining, to simulate a missing category on purpose:

```sql
SELECT s.Order_ID, s.Category, s.Sales,
       c.Category_Manager
FROM workspace.default.superstore_sales_cleaned s
LEFT JOIN (
    SELECT * FROM workspace.default.category_details
    WHERE Category != 'Technology'
) c
  ON s.Category = c.Category
WHERE s.Category = 'Technology'
LIMIT 5;
```

**Ask the student:** "What shows up in the `Category_Manager` column for these rows? Why?" *(Should be NULL/blank — because we removed Technology from the lookup table on purpose, but LEFT JOIN still kept the sales rows.)*

**Explain to student:** "This is exactly why LEFT JOIN is usually the safer choice — it never silently drops your main data, even if a match is missing."

---

### Step 8: Save the Joined Result as a New Table
In a new cell, type and run:

```sql
CREATE OR REPLACE TABLE workspace.default.superstore_sales_joined AS
SELECT s.Order_ID, s.Order_Date, s.Customer_Name, s.Segment, s.Region,
       s.Category, s.Sub_Category, s.Product_Name, s.Sales, s.Quantity,
       s.Discount, s.Profit,
       c.Category_Manager, c.Warehouse_Location
FROM workspace.default.superstore_sales_cleaned s
LEFT JOIN workspace.default.category_details c
  ON s.Category = c.Category;
```
<img width="1502" height="563" alt="image" src="https://github.com/user-attachments/assets/d0ef3449-e8ed-4683-b1fe-cd6050a848d6" />

**Explain to student:** "This is now our most complete table yet — cleaned, and enriched with extra information from a second source."

---

### Step 9: Confirm the New Table
In a new cell, type and run:

```sql
SELECT COUNT(*) AS joined_table_row_count
FROM workspace.default.superstore_sales_joined;
```
<img width="1485" height="587" alt="image" src="https://github.com/user-attachments/assets/52604d73-d137-4053-8efb-1d664864acf3" />

```sql
SELECT * FROM workspace.default.superstore_sales_joined LIMIT 10;
```
<img width="1495" height="635" alt="image" src="https://github.com/user-attachments/assets/841d4505-abd8-49b1-b968-aec944261c02" />

---

### Step 10: Repeat for Practice
Close and reopen the notebook. Have the student redo Steps 4, 6, and 8 from memory with minimal guidance.

---

## Day 2 Task Checklist
- [ ] Repeated Day 1 steps as warm-up
- [ ] Uploaded `category_details.csv` as a new table
- [ ] Ran an `INNER JOIN` between the sales table and the lookup table
- [ ] Compared row counts before and after the join
- [ ] Ran a `LEFT JOIN` and understood how it differs from `INNER JOIN`
- [ ] Saw a real example of LEFT JOIN keeping rows even without a match
- [ ] Created a new joined table using `CREATE OR REPLACE TABLE ... AS`
- [ ] Confirmed the new joined table's row count and contents
- [ ] Repeated key steps once more independently
