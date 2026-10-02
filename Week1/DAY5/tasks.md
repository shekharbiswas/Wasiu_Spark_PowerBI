# Week 1 — Day 5: Tasks
## Guided Independent Repeat — Full Pipeline Stage 1 on a New Dataset

**Estimated Time: 6 hours**
*(includes brief warm-up, independent work with light instructor guidance, and a short wrap-up presentation — pace stays slow and unrushed)*

**Dataset used today:** `elektronik_shop_sales.csv` — a **new** dataset (360 rows), different domain (electronics/appliances/books retailer) from `superstore_sales_sample.csv` used on Days 1-4. The student has not seen this exact file before.

### New Dataset Columns (Same Structure as Week's Dataset, for Familiarity)
| Column | Type | Description |
|--------|------|--------------|
| Order_ID | Text | Unique identifier for each order (e.g. `ELS-2001`) |
| Order_Date | Date | Date the order was placed |
| Customer_Name | Text | Name of the customer |
| Segment | Text | Consumer, Corporate, or Home Office |
| Region | Text | German federal state — Sachsen, Hessen, Berlin, or Schleswig-Holstein |
| Category | Text | Electronics, Home Appliances, or Books & Media |
| Sub_Category | Text | More specific product grouping |
| Product_Name | Text | Specific product sold |
| Sales | Number | Sale amount |
| Quantity | Number | Units sold |
| Discount | Number | Discount applied (0 to 0.25) |
| Profit | Number | Profit or loss on the order |

**Built-in data quality issues (for the student to discover themselves, not told in advance):** some missing `Customer_Name`, some missing `Region`, some missing `Discount`, and a handful of duplicate rows.

---

## Instructor Role Today
Today, the instructor's job shifts from *teaching* to *observing and prompting*. Instead of giving the SQL directly, ask guiding questions like:
- "What's the first thing we always do with new data?"
- "How do we check if this data has any problems?"
- "How would you write that as a query?"

Only give the direct answer if the student is stuck for more than a few minutes.

---

### Step 1: Warm-Up Discussion (15-20 min, no coding yet)
Ask the student to explain out loud, from memory:
1. What are the 4 stages of a data pipeline?
2. What did we do each day this week (Days 1-4)?
3. What order do we always do things in, and why?

---

### Step 2: Set Up (Guided, Light Touch)
1. Log in to Databricks Community Edition
2. Confirm the cluster is running (restart if needed)
3. Upload `elektronik_shop_sales.csv` as a new table (student does this themselves, instructor watches)
4. Create a new notebook named `Week1_Day5_FullPipeline`, language set to SQL, attached to the cluster

---

### Step 3: Stage 1 — Ingest (Student-Led)
Ask: "What's the very first query you'd run to check the data loaded correctly?"

Expected (guide only if stuck):
```sql
SELECT * FROM workspace.default.elektronik_shop_sales LIMIT 10;
```
<img width="1605" height="802" alt="image" src="https://github.com/user-attachments/assets/0c168651-1ec6-4650-bf51-b49f2544cf0b" />

---

### Step 4: Stage 2 — Profile (Student-Led)
Ask the student to independently run and interpret:
```sql
DESCRIBE workspace.default.elektronik_shop_sales;
```
<img width="1582" height="706" alt="image" src="https://github.com/user-attachments/assets/6c2b9536-785d-42e8-8e31-b1de5eac5098" />

```sql
SELECT COUNT(*) AS total_rows FROM workspace.default.elektronik_shop_sales;
```
<img width="1527" height="597" alt="image" src="https://github.com/user-attachments/assets/c7102245-9906-47e5-8216-209cab6cb9d9" />

Then have them pick **two columns themselves** and check for missing values, e.g.:
```sql
SELECT COUNT(*) AS missing_values
FROM workspace.default.elektronik_shop_sales
WHERE Customer_Name IS NULL;
```
<img width="1557" height="633" alt="image" src="https://github.com/user-attachments/assets/2d32b2b5-9144-4bbf-834b-724ca0cda124" />

And check for duplicates using an ID column:
```sql
SELECT Order_ID, COUNT(*) AS occurrences
FROM workspace.default.elektronik_shop_sales
GROUP BY Order_ID
HAVING COUNT(*) > 1;
```
<img width="1483" height="713" alt="image" src="https://github.com/user-attachments/assets/be53d4d8-ec8a-4c33-b9cf-f577d46f0e57" />

**Ask the student to write down their findings** before moving on.

---

### Step 5: Stage 3 — Filter & Select (Instructor Poses a Business Question)
Instructor asks: *"Show me only the Customer Name, Category, and Sales for all orders from Berlin over 500."*

Student should independently write something close to:
```sql
SELECT Customer_Name, Category, Sales
FROM workspace.default.elektronik_shop_sales
WHERE Region = 'Berlin' AND Sales > 500
ORDER BY Sales DESC;
```
<img width="1517" height="717" alt="image" src="https://github.com/user-attachments/assets/0f2f3dc0-9174-4599-8bf8-658171cbf7c3" />

---

### Step 6: Stage 4 — Aggregate (Instructor Poses a Second Business Question)
Instructor asks: *"What are the total sales per category, sorted from highest to lowest?"*

Student should independently write something close to:
```sql
SELECT Category, SUM(Sales) AS total_sales
FROM workspace.default.elektronik_shop_sales
GROUP BY Category
ORDER BY total_sales DESC;
```
<img width="1491" height="615" alt="image" src="https://github.com/user-attachments/assets/58cf6eaa-6679-432c-aab4-9bc145e39da3" />


Instructor can pose 1-2 more business questions if time allows, e.g.:
- "What's the average sale per region?"
  
  <img width="1507" height="617" alt="image" src="https://github.com/user-attachments/assets/2f5c7f67-19c6-422d-9585-8656784af6a1" />


- "How many orders came from each segment?"

  <img width="1497" height="687" alt="image" src="https://github.com/user-attachments/assets/63fbe4ba-14d3-4eac-9bac-ea3bdc180925" />


---

### Step 7: Wrap-Up Presentation (15-20 min)
Have the student walk through their notebook from top to bottom, explaining out loud:
1. What each query does
2. Why they wrote it that way
3. What they found (row count, data quality issues, business answers)

This is not graded formally — it's a confidence-building exercise to reinforce that they can explain their own work.

---

## Day 5 Task Checklist
- [ ] Explained the 4 pipeline stages and Days 1-4 recap from memory
- [ ] Uploaded new dataset (`elektronik_shop_sales.csv`) independently
- [ ] Ran an ingestion check query independently
- [ ] Ran schema and row count checks independently
- [ ] Found at least 2 data quality issues (nulls or duplicates) independently
- [ ] Answered a filter/select business question independently
- [ ] Answered an aggregation (GROUP BY) business question independently
- [ ] Presented/walked through their notebook out loud
