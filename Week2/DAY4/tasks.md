# Week 2 — Day 4: Tasks 

## Hands-On Step-by-Step (Databricks Community Edition)
**Estimated Time: 6 hours**
*(includes warm-up repetition, guided steps, exploration time, independent repeat practice, and now troubleshooting/optimization work — pace stays slow, no rushing)*

**Dataset used:** `superstore_sales_enriched` (the table you created yesterday, Week 2 Day 3)

**Note:** No SQL is provided in this version. You must write every query yourself from the descriptions given. Use Day 3's notebook and Databricks documentation as your only references.


### Step 1: Warm-Up — Recap Day 3 (30-45 min)
1. Log in to Databricks Community Edition
2. Go to **Compute** and confirm the cluster is running (start it again if it shows stopped)
3. Open yesterday's notebook (`Week2_Day3_DerivedColumns`) and, entirely from memory, write and run a query that counts the rows in `superstore_sales_enriched`
4. Also write a second query from memory that counts *distinct* customers in the table — you did something similar on Day 3, but write it fresh without looking


### Step 2: Create Today's Notebook
1. On the left sidebar, click **Workspace**
2. Click **Create** → **Notebook**
3. Name it `Week2_Day4_WritingOutput`
4. Set the default language to **SQL**
5. Attach it to the cluster

### Step 3: Confirm What You're About to Save
Write and run your own queries to:
1. Preview the first 10 rows of `superstore_sales_enriched`
```sql
SELECT * FROM dataskool.dataskool_schema.superstore_sales_cleaned LIMIT 10;
```
2. Get the full schema of the table
```sql
DESCRIBE dataskool.dataskool_schema.superstore_sales_cleaned
```
3. Additionally, write a query that reports, for every column, how many NULL values it contains — you'll need to construct this yourself (there is no single built-in command that does this for a whole table at once)
```sql
SELECT
    SUM(CASE WHEN Order_ID IS NULL THEN 1 ELSE 0 END) AS Oder_ID_Nulls,
    SUM(CASE WHEN Sales IS NULL THEN 1 ELSE 0 END) AS Sales_Nulls,
    SUM(CASE WHEN Region IS NULL THEN 1 ELSE 0 END) AS Region_Nulls
FROM  dataskool.dataskool_schema.superstore_sales_cleaned
```
```sql
SELECT COUNT(Order_ID) AS Counts_Of_Order_ID,
       COUNT(Sales) AS Counts_Of_Sales,
       COUNT(Region) AS Counts_Of_Region
FROM dataskool.dataskool_schema.superstore_sales_cleaned
```
4. Record the total row count and the null-count results somewhere in the notebook as markdown notes — you'll need them later to verify nothing was lost or corrupted
- The total record counts for Region is 385, but there was a missing values of 10, which made it 375 rows
- The total record count of Oder_ID is 385 and has no missing Values
- The total record count of Sales is 385 and has no missing Values
 

### Step 4: Save as a New Managed Table — With a Twist
Instead of a straight copy, create a new managed table called `superstore_sales_final` that contains only the following, and you must figure out the correct clauses yourself:
1. All original columns from `superstore_sales_enriched`
2. Rows filtered to exclude any order with a negative or zero sales amount
3. A new column that buckets each order into `"Low"`, `"Medium"`, or `"High"` based on sales amount, using thresholds you choose and justify in a markdown note
4. Results ordered by order date, most recent first
```sql
CREATE OR REPLACE TABLE dataskool.dataskool_schema.superstore_sales_final AS
SELECT *,
CASE WHEN Sales < 50 THEN "Low"
WHEN Sales BETWEEN 50 AND 300 THEN "Medium"
ELSE "High"
END AS Sales_Bucket
FROM dataskool.dataskool_schema.superstore_sales_cleaned
WHERE Sales > 0
```
```sql
SELECT * FROM dataskool.dataskool_schema.superstore_sales_final
```
Confirm the table now has fewer rows than the original and explain why in a markdown cell.
-

### Step 5: Save as CSV — Two Ways
1. Using the **Catalog** UI, export `superstore_sales_final` as CSV and download it. Open it in Excel to confirm it looks correct.
2. Separately, write a query that produces a *summary* CSV instead of a raw export: total sales and total order count grouped by region and by your new bucket column from Step 4. Export this summary table as its own CSV using the same UI method. You now have two CSVs — a full detail file and a small summary file — and you should be able to explain when each would be useful in a real pipeline.
```sql
CREATE OR REPLACE TABLE dataskool.dataskool_schema.superstore_sales_summary AS
SELECT region, sales_bucket,
       SUM(sales) AS total_sales,
       COUNT(*) AS order_count
FROM dataskool.dataskool_schema.superstore_sales_final
GROUP BY region, sales_bucket;
```

### Step 6: Save as Parquet — Partitioned
Create a Parquet-format table called `superstore_sales_parquet` from `superstore_sales_final`, but this time:
1. Partition the underlying storage by region (research how to do this in Databricks SQL — it is not identical to a plain `CREATE TABLE ... AS SELECT`)
2. After creating it, find a way to confirm the partitioning actually took effect (not just that the table exists) — describe what you checked and what you saw in a markdown note

<img width="1488" height="455" alt="image" src="https://github.com/user-attachments/assets/80da71ca-db6a-4911-9366-c8240b6db419" />



