# Week 1 — Day 3: Tasks
## Hands-On Step-by-Step (Databricks Community Edition)

**Estimated Time: 6 hours**
*(includes warm-up repetition, guided steps, exploration time, and independent repeat practice — pace is intentionally slow, no rushing)*

**Dataset used:** `superstore_sales_sample.csv` (same dataset as Day 1 and Day 2, table: `workspace.default.superstore_sales_sample`)

---

### Step 1: Warm-Up — Repeat Day 1 & Day 2 (30-45 min)
1. Log in to Databricks Community Edition
2. Go to **Compute** and confirm the cluster is running (start it again if it shows stopped)
3. Open the notebook from Day 2 (`Week1_Day2_Profiling`)
4. Re-run these from memory, with light guidance only if stuck:
```sql
DESCRIBE workspace.default.superstore_sales_sample;
```
```sql
SELECT COUNT(*) AS total_rows FROM workspace.default.superstore_sales_sample;
```

**Explain to student:** "We always start by repeating what we did before — this is how it becomes second nature."

---

### Step 2: Create Today's Notebook
1. On the left sidebar, click **Workspace**
2. Click **Create** → **Notebook**
3. Name it `Week1_Day3_FilterSelect`
4. Set the default language to **SQL**
5. Attach it to the cluster from Day 1

---

### Step 3: Select Specific Columns
In a new notebook cell, type and run:

```sql
SELECT Customer_Name, Region, Sales
FROM workspace.default.superstore_sales_sample;
```

Press **Shift + Enter** to run the cell.

**Ask the student:**
- How is this different from `SELECT *`?
- Why might a manager prefer this view over seeing all 12 columns?

---

### Step 4: Rename a Column in the Output (Alias)
In a new cell, type and run:

```sql
SELECT Customer_Name AS Customer, Sales AS Sale_Amount
FROM workspace.default.superstore_sales_sample;
```

**Explain to student:** "This doesn't change the actual table — it just makes the output easier to read, like renaming a column header in Excel temporarily."

---

### Step 5: Filter Rows with a Single Condition
In a new cell, type and run:

```sql
SELECT Customer_Name, Region, Sales
FROM workspace.default.superstore_sales_sample
WHERE Region = 'Bayern';
```
<img width="1616" height="762" alt="image" src="https://github.com/user-attachments/assets/544630dd-cd44-4dfa-93e6-f95d70a0591d" />

**Ask the student:**
- How many rows came back?
  - Based on the city Bayern 77 rows was returned
- Try changing `'Bayern'` to `'Niedersachsen'` — how does the result change?
  - Based on the city Niedersachen 118 rows was returned 
---

### Step 6: Filter with a Number Condition
In a new cell, type and run:

```sql
SELECT Customer_Name, Sales
FROM workspace.default.superstore_sales_sample
WHERE Sales > 1000;
```
<img width="1512" height="702" alt="image" src="https://github.com/user-attachments/assets/54c2e7a0-17b5-48df-bba8-a964a8d40de2" />

**Explain to student:** "This is the same as filtering a column in Excel to only show values above a certain number."

---

### Step 7: Combine Two Conditions (AND)
In a new cell, type and run:

```sql
SELECT Customer_Name, Region, Sales
FROM workspace.default.superstore_sales_sample
WHERE Region = 'Bayern' AND Sales > 500;
```
<img width="1513" height="631" alt="image" src="https://github.com/user-attachments/assets/38c795f6-ad4a-46bc-ae6b-bed49b9af01b" />

**Ask the student:** "What do you think would happen if we used `OR` instead of `AND` here?" (Let them guess before trying it.)

---

### Step 8: Sort the Results (ORDER BY)
In a new cell, type and run:

```sql
SELECT Customer_Name, Sales
FROM workspace.default.superstore_sales_sample
ORDER BY Sales DESC;
```
<img width="1572" height="707" alt="image" src="https://github.com/user-attachments/assets/54e0093b-ce57-4a48-8495-c7d32ebea9a2" />

**Explain to student:** "`DESC` means highest to lowest. If we used `ASC` instead, it would go lowest to highest — same as sorting a column in Excel."

---

### Step 9: Put It All Together
In a new cell, have the student write one query independently (guide only if stuck) that:
- Selects `Customer_Name`, `Category`, and `Sales`
- Filters for `Category = 'Technology'`
- Sorts by `Sales` from highest to lowest

**Expected query:**
```sql
SELECT Customer_Name, Category, Sales
FROM workspace.default.superstore_sales_sample
WHERE Category = 'Technology'
ORDER BY Sales DESC;
```
<img width="1498" height="663" alt="image" src="https://github.com/user-attachments/assets/b333b402-9a5e-45cc-9a7b-231348cc952f" />

---

### Step 10: Repeat for Practice
Close and reopen the notebook. Have the student redo Steps 5, 6, and 8 from memory with minimal guidance.

---

## Day 3 Task Checklist
- [ ] Repeated Day 1 & Day 2 steps as warm-up
- [ ] New notebook created for Day 3
- [ ] Selected specific columns using `SELECT`
- [ ] Used an alias (`AS`) to rename a column in output
- [ ] Filtered rows using `WHERE` with a text condition
- [ ] Filtered rows using `WHERE` with a number condition
- [ ] Combined two conditions using `AND`
- [ ] Sorted results using `ORDER BY`
- [ ] Wrote one independent query combining SELECT + WHERE + ORDER BY
- [ ] Repeated key steps once more independently
