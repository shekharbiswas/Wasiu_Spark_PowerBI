# Week 2 — Day 1: Tasks
## Hands-On Step-by-Step (Databricks Community Edition)

**Estimated Time: 6 hours**
*(includes warm-up repetition, guided steps, exploration time, and independent repeat practice — pace is intentionally slow, no rushing)*

**Dataset used:** `superstore_sales_sample.csv` (same dataset as Week 1, table: `workspace.default.superstore_sales_sample`)

---

### Step 1: Warm-Up — Recap Week 1 (30-45 min)
1. Log in to Databricks Community Edition
2. Go to **Compute** and confirm the cluster is running (start it again if it shows stopped)
3. Open any Week 1 notebook and re-run this from memory, with light guidance only if stuck:
```sql
SELECT Region, SUM(Sales) AS total_sales
FROM workspace.default.superstore_sales_sample
GROUP BY Region
ORDER BY total_sales DESC;
```
<img width="1612" height="783" alt="image" src="https://github.com/user-attachments/assets/cf1871f2-43ec-498c-a74e-81a475f76cea" />

**Explain to student:** "We always start by repeating what we did before — this is how it becomes second nature."

---

### Step 2: Create Today's Notebook
1. On the left sidebar, click **Workspace**
2. Click **Create** → **Notebook**
3. Name it `Week2_Day1_DataCleaning`
4. Set the default language to **SQL**
5. Attach it to the cluster from Week 1

---

### Step 3: Re-Confirm the Problems (Quick Recap of Profiling)
In a new notebook cell, type and run:

```sql
SELECT COUNT(*) AS missing_customer_name
FROM workspace.default.superstore_sales_sample
WHERE Customer_Name IS NULL;
```
<img width="1612" height="743" alt="image" src="https://github.com/user-attachments/assets/e8772254-ec1a-4747-9226-ef92f4551b1c" />

```sql
SELECT COUNT(*) AS missing_discount
FROM workspace.default.superstore_sales_sample
WHERE Discount IS NULL;
```
<img width="1602" height="737" alt="image" src="https://github.com/user-attachments/assets/9492156f-53f8-40b1-8889-59b88dbd3235" />

**Explain to student:** "Before fixing anything, we confirm exactly what we're fixing and how many rows are affected."

---

### Step 4: Remove Rows with Missing Customer Name
Since `Customer_Name` is essential for a business report, we'll remove rows where it's missing:

```sql
SELECT *
FROM workspace.default.superstore_sales_sample
WHERE Customer_Name IS NOT NULL;
```
<img width="1547" height="805" alt="image" src="https://github.com/user-attachments/assets/05571685-4f41-4924-a6a2-c60b4f65d2b9" />

**Ask the student:** "How many rows does this return compared to the full dataset? How many rows did we lose?"

---

### Step 5: Fill In Missing Discount with a Default Value
Since a missing `Discount` likely just means "no discount was given," we'll fill it with `0` instead of removing the row:

```sql
SELECT Order_ID, Customer_Name, Discount,
       COALESCE(Discount, 0) AS Discount_Cleaned
FROM workspace.default.superstore_sales_sample;
```
<img width="1553" height="701" alt="image" src="https://github.com/user-attachments/assets/e0d2946f-f2a1-4ad9-bfb6-66c7c238e149" />

**Explain to student:** "`COALESCE` says: if this value is missing, use this other value instead. Here, we're saying 'if Discount is missing, treat it as 0.'"

**Ask the student:** "Scroll through the results — can you find a row where Discount and Discount_Cleaned are different?"

---

### Step 6: Combine Both Fixes Together
In a new cell, type and run:

```sql
SELECT Order_ID, Customer_Name, Region,
       COALESCE(Discount, 0) AS Discount_Cleaned,
       Sales
FROM workspace.default.superstore_sales_sample
WHERE Customer_Name IS NOT NULL;
```
<img width="1598" height="771" alt="image" src="https://github.com/user-attachments/assets/a60ba9ba-e805-44b4-ada0-6bdc4f49bf15" />

---

### Step 7: Remove Duplicate Rows
In a new cell, type and run:

```sql
SELECT DISTINCT *
FROM workspace.default.superstore_sales_sample;
```
<img width="1606" height="805" alt="image" src="https://github.com/user-attachments/assets/978e9415-def3-453b-a9ea-49cf113056ba" />


**Explain to student:** "`DISTINCT` keeps only one copy of each identical row — this removes the duplicate orders we found back in Week 1, Day 2."

**Ask the student:** "How many rows does this return compared to the original 412?"

---

### Step 8: Save the Cleaned Data as a New Table
Now we combine everything — removing missing customer names, filling missing discounts, and removing duplicates — and save it as a brand-new, clean table:

```sql
CREATE OR REPLACE TABLE workspace.default.superstore_sales_cleaned AS
SELECT DISTINCT
       Order_ID, Order_Date, Customer_Name, Segment, Region,
       Category, Sub_Category, Product_Name, Sales, Quantity,
       COALESCE(Discount, 0) AS Discount,
       Profit
FROM workspace.default.superstore_sales_sample
WHERE Customer_Name IS NOT NULL;
```
<img width="1542" height="788" alt="image" src="https://github.com/user-attachments/assets/e00a9e49-41bd-4664-bef2-a4f1b284d875" />

**Explain to student:** "This is a huge moment — we just created a brand-new, clean table. Every query from tomorrow onward can use this instead of the messy original."

---

### Step 9: Confirm the Clean Table
In a new cell, type and run:

```sql
SELECT COUNT(*) AS clean_row_count
FROM workspace.default.superstore_sales_cleaned;
```
<img width="1547" height="717" alt="image" src="https://github.com/user-attachments/assets/f3ac59a8-9735-4454-bb95-33ac4bc09943" />

```sql
SELECT COUNT(*) AS remaining_missing_discount
FROM workspace.default.superstore_sales_cleaned
WHERE Discount IS NULL;
```
<img width="1578" height="632" alt="image" src="https://github.com/user-attachments/assets/6dae0c27-16d5-484d-99f3-e7ef97233567" />

**Ask the student:** "What do you expect this second query to return, before you run it?" (Should be 0.)

---

### Step 10: Repeat for Practice
Close and reopen the notebook. Have the student redo Steps 5, 7, and 8 from memory with minimal guidance.

---

## Day 1 Task Checklist
- [ ] Repeated Week 1 steps as warm-up
- [ ] New notebook created for Week 2 Day 1
- [ ] Re-confirmed missing value counts
- [ ] Removed rows with missing `Customer_Name`
- [ ] Filled missing `Discount` values using `COALESCE`
- [ ] Removed duplicate rows using `DISTINCT`
- [ ] Created a new clean table using `CREATE OR REPLACE TABLE ... AS SELECT`
- [ ] Confirmed the clean table's row count and that no missing discounts remain
- [ ] Repeated key steps once more independently
