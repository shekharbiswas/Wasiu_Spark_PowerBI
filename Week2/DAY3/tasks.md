# Week 2 — Day 3: Tasks
## Hands-On Step-by-Step (Databricks Community Edition)
**Estimated Time: 10-12 hours**
*(includes warm-up repetition, guided steps, exploration time, and independent repeat practice — pace stays slow, no rushing)*

**Dataset used:** `superstore_sales_joined` (the joined table created yesterday, Week 2 Day 2)

**Note:** No SQL is provided in this version. Write every query yourself from the descriptions given, using Day 2's notebook and Databricks documentation as your only references.

---

### Step 1: Warm-Up — Recap Day 2 (30-45 min)
1. Log in to Databricks Community Edition
2. Go to **Compute** and confirm the cluster is running (start it again if it shows stopped)
3. Open yesterday's notebook (`Week2_Day2_Joins`) and, entirely from memory, write and run a query that counts the rows in `superstore_sales_joined`
4. Also write a second query from memory that returns the total `Sales` across the whole table — you'll use this number later to sanity-check a later step

---

### Step 2: Create Today's Notebook
1. On the left sidebar, click **Workspace**
2. Click **Create** → **Notebook**
3. Name it `Week2_Day3_DerivedColumns`
4. Set the default language to **SQL**
5. Attach it to the cluster

---

### Step 3: Your First CASE WHEN — Three Tiers Plus an Edge Case
Write a query that labels every order using `Sales` with these rules:
- `"High Value Order"` for Sales at or above 1000
- `"Standard Order"` for Sales at or above 300 but under 1000
- `"Low Value Order"` for everything else
- `"Unusable Record"` for any row where `Sales` is NULL — think about where this condition needs to go in your `CASE WHEN` so it's actually reachable

Select `Order_ID`, `Customer_Name`, `Sales`, and your new label column. Run it and confirm all rows got a label, including any with missing Sales values.



Answer:

```sql
select Order_ID, Customer_Name, Sales,
  CASE
   WHEN Sales IS NULL THEN 'Unusable Record'
   WHEN Sales >= 1000 THEN 'High Value Order'
   WHEN Sales >= 300  THEN 'Standard Order'
   ELSE 'Low Value Order'
  END AS Order_Value_Label

FROM superstore_sales_joined
```


---

### Step 4: Count and Cross-Tabulate
1. Write a query that counts how many orders fall into each label from Step 3.
```sql
SELECT
    CASE
        WHEN Sales IS NULL THEN 'Unusable Record'
        WHEN Sales >= 1000 THEN 'High Value Order'
        WHEN Sales >= 300 THEN 'Standard Order'
        ELSE 'Low Value Order'
    END AS Order_Value_Label,
    ROUND(SUM(Sales),2) AS Total_Sales,
    COUNT(*) AS Order_Count
FROM dataskool.dataskool_schema.superstore_sales_cleaned
GROUP BY 1
ORDER BY Total_Sales DESC;
```

3. Go further: write a second query that counts orders by label **and** by `Category` at the same time, so you can see, for example, how many "High Value Order" rows came from each category. You'll need to group by more than one column.
```sql
SELECT Category,
    CASE
        WHEN Sales IS NULL THEN 'Unusable Record'
        WHEN Sales >= 1000 THEN 'High Value Order'
        WHEN Sales >= 300 THEN 'Standard Order'
        ELSE 'Low Value Order'
    END AS Order_Value_Label,
    ROUND(SUM(Sales),2) AS Total_Sales,
    COUNT(*) AS Order_Count
FROM dataskool.dataskool_schema.superstore_sales_cleaned
GROUP BY 1,2
ORDER BY Category, Total_Sales DESC;
```
5. In a markdown note, state which category contributes the most "High Value Order" rows and whether that surprises you.
 - Furniture Category has the highest value Orders
---

### Step 5: A Second CASE WHEN — Profit Health, Three-Way
Write a query that classifies each order's `Profit` as `"Loss"`, `"Break Even"`, or `"Profitable"`. Then, in the same query, add a second derived column showing the `Discount` for that order. Order the results so the biggest losses appear first.
```sql
SELECT Order_ID, Customer_Name,Profit,Discount,
    CASE 
        WHEN Profit < 0 THEN "Loss"
        WHEN Profit = 0 THEN "Break_Even"
        ELSE "Profitable"
    END AS Profit_Status
FROM dataskool.dataskool_schema.superstore_sales_cleaned
ORDER BY Profit ASC;
```

In a markdown note, look at the rows with the largest losses and describe what their `Discount` values have in common.

---

### Step 6: Calculated Field — Profit Margin, Handled Safely
Write a query that calculates `Profit_Margin` as `Profit` divided by `Sales`, rounded to 2 decimal places. This time, you must prevent the query from failing or returning nonsense on rows where `Sales` is 0 or NULL — research how to guard a division safely in SQL rather than letting it error or return infinity.
```sql
SELECT Product_Name, Customer_Name, Profit, Sales, ROUND(Profit/nullif(Sales,0),2) AS Profit_Margin
FROM dataskool.dataskool_schema.superstore_sales_cleaned
```
Confirm your fix worked by finding at least one row in the source table where `Sales` is 0 or NULL and checking what your query returned for that row instead of an error.
```sql
SELECT Order_ID, Sales, Profit
FROM dataskool.dataskool_schema.superstore_sales_cleaned
WHERE Sales is null or Sales = 0
```

## Day 3 Task Checklist
- [ ] Repeated Day 2 steps as warm-up, including a total-Sales check for later comparison
- [ ] New notebook created for Day 3
- [ ] Built a four-tier order-value label that correctly handles NULL Sales
- [ ] Counted orders per label, and cross-tabulated labels by category
- [ ] Built a profit-status label alongside the Discount column, sorted to surface the worst losses
- [ ] Built a safely-guarded Profit_Margin calculation and verified it against a zero/NULL Sales row
- [ ] Combined labels, calculation, and filtering into one query, sorted by margin
- [ ] Saved the enriched result as a new table with duplicates removed
- [ ] Verified row count and total Sales against Step 1's recorded baseline
- [ ] Independently invented two separate labeling rules, one multi-column, without referring to earlier work
