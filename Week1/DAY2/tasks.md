# Week 1 — Day 2: Tasks
## Hands-On Step-by-Step (Databricks Community Edition)

**Estimated Time: 6 hours**
*(includes warm-up repetition, guided steps, exploration time, and independent repeat practice — pace is intentionally slow, no rushing)*

---

## Dataset Used: `superstore_sales_sample.csv`

This is a trimmed, Superstore-style retail sales dataset built specifically for this module — **412 rows**, small enough to load instantly and easy to eyeball manually, but realistic enough to mirror what a Data Engineer actually works with on the job.

### Columns
| Column | Type | Description |
|--------|------|--------------|
| Order_ID | Text | Unique identifier for each order (e.g. `ORD-1001`) |
| Order_Date | Date | Date the order was placed (`YYYY-MM-DD`) |
| Customer_Name | Text | Name of the customer who placed the order |
| Segment | Text | Customer segment — Consumer, Corporate, or Home Office |
| Region | Text | German federal state — Bayern, Nordrhein-Westfalen, Baden-Württemberg, or Niedersachsen |
| Category | Text | Product category — Furniture, Office Supplies, or Technology |
| Sub_Category | Text | More specific product grouping (e.g. Chairs, Binders, Phones) |
| Product_Name | Text | Specific product sold |
| Sales | Number | Sale amount in currency units |
| Quantity | Number | Number of units sold in the order |
| Discount | Number | Discount applied (0 to 0.3, i.e. 0% to 30%) |
| Profit | Number | Profit or loss on the order (can be negative) |

<img width="1896" height="812" alt="image" src="https://github.com/user-attachments/assets/4365efe2-7177-46a6-ab2f-e77be0e882ef" />

### Data Quality Issues

This dataset is "imperfect,"— so today's profiling exercises have real things to discover:

- **15 rows** have a missing `Customer_Name`
- **10 rows** have a missing `Region`
- **8 rows** have a missing `Discount`
- **12 duplicate rows** exist (same values repeated) — a realistic scenario of an order being logged twice by mistake

**Explain to student:** "This is exactly what real company data looks like — never perfectly clean. Today, your job is to find these problems, not fix them yet. Fixing comes in Week 2."

### Why This Dataset (and Not a Random One)
- Same domain as a real retail business — Orders, Customers, Products, Sales, Profit — so the columns make intuitive sense
- Small enough (412 rows) to load fast and manually double-check results
- Reused across the entire module — the same file will come back in Week 2 (cleaning/transforming) and Week 4 (Power BI dashboard), so the student builds familiarity with one dataset instead of relearning a new one every week

---

### Step 1: Warm-Up — Repeat Day 1 (30-45 min)
1. Log in to Databricks Community Edition
2. Go to **Compute** and confirm the cluster is running (start it again if it shows stopped — clusters auto-stop after inactivity)
3. Open the notebook from Day 1 (`Week1_Day1_Ingestion`)
4. Re-run the earlier query from memory, with light guidance only if stuck:
```sql
SELECT * FROM workspace.default.superstore_sales_sample LIMIT 10;
```

**Explain to student:** "We always start by repeating what we did before — this is how it becomes second nature."

---

### Step 2: Create Today's Notebook
1. On the left sidebar, click **Workspace**
2. Click **Create** → **Notebook**
3. Name it `Week1_Day2_Profiling`
4. Set the default language to **SQL**
5. Attach it to the cluster from Day 1

---

### Step 3: Check the Table's Schema
In a new notebook cell, type and run:

```sql
DESCRIBE workspace.default.superstore_sales_sample;
```

Press **Shift + Enter** to run the cell.

**Ask the student:**
- What are the column names?
- What data type is each column (string, int, double, date, etc.)?
- Does any column's data type look wrong for what it should contain? (e.g. a "price" column showing as text)

<img width="1436" height="703" alt="image" src="https://github.com/user-attachments/assets/d1ebb94c-bc41-4c77-950f-137e667e95d4" />

---

### Step 4: Check Total Row Count
In a new cell, type and run:

```sql
SELECT COUNT(*) AS total_rows FROM workspace.default.superstore_sales_sample;
```
<img width="1605" height="671" alt="image" src="https://github.com/user-attachments/assets/a4e6b52b-cf1f-4545-b6f0-1be624ab0957" />


**Explain to student:** "This tells us exactly how big our dataset is — the first number a Data Engineer usually checks."

---

### Step 5: Check for Missing Values in a Column
Pick one important column from the dataset (e.g. `Customer_Name` or `amount`) and run:

```sql
SELECT COUNT(*) AS missing_values
FROM workspace.default.superstore_sales_sample
WHERE Customer_Name IS NULL;
```

*(Replace `Customer_Name` with the actual column name from the dataset.)*

<img width="1537" height="653" alt="image" src="https://github.com/user-attachments/assets/0fadfcd8-57cc-4ce4-8ba5-d14d469811c2" />

**Ask the student:** "If this number is greater than 0, what does that tell us?"

---

### Step 6: Repeat Step 5 for a Second Column
Have the student pick a different column themselves and write the same type of query independently, with guidance only if stuck.

---

### Step 7: Check for Obvious Duplicates
In a new cell, type and run:

```sql
SELECT Order_ID, COUNT(*) AS occurrences
FROM workspace.default.superstore_sales_sample
GROUP BY Order_ID
HAVING COUNT(*) > 1;
```
<img width="1852" height="805" alt="image" src="https://github.com/user-attachments/assets/0ecacac6-a3af-431a-9cf3-4dc692fb5391" />

*(Replace `Customer_Name` with `Order_ID` — since order IDs should never repeat.)*

**Explain to student:** "This shows us if the same value appears more than once when it maybe shouldn't — a common data quality issue."

> Note: `GROUP BY` and `HAVING` are previewed here just as a profiling tool — full explanation comes formally on Day 4 (Aggregating Data). Keep this light, don't over-explain today.

---

### Step 8: Write Down Findings
Have the student write (in the notebook, as a markdown cell or comment) 2-3 sentences summarizing what they found:
- Number of rows
- Any missing values found
- Any duplicates found
- Anything else that looked "off"

---

### Step 9: Repeat for Practice
Close and reopen the notebook. Have the student redo Steps 3, 4, and 5 from memory with minimal guidance.

---

## Day 2 Task Checklist
- [ ] Repeated Day 1 steps as warm-up
- [ ] New notebook created for Day 2
- [ ] Ran `DESCRIBE` on the table
- [ ] Ran `COUNT(*)` for total row count
- [ ] Checked at least 2 columns for missing values
- [ ] Ran a query to check for duplicates
- [ ] Wrote a short summary of findings
- [ ] Repeated key steps once more independently
