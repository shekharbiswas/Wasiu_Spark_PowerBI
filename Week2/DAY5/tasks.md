# Week 2 — Day 5: Tasks
## Mini ETL Project — Light Guided Build

**Estimated Time: 3-4 hours**
*(a lighter day on purpose — no new concepts, just connecting what you already know)*

**Dataset used:** `superstore_sales_sample` (the original raw table from Week 1)

---

### Step 1: Warm-Up (10-15 min)
Open a fresh notebook, name it `Week2_Day5_MiniETL`, set language to SQL, attach it to the cluster.

Run one quick check to confirm you're starting from the raw data:
```sql
SELECT COUNT(*) AS raw_row_count
FROM workspace.default.superstore_sales_sample;
```
<img width="1096" height="406" alt="image" src="https://github.com/user-attachments/assets/f9d29d3c-515d-47e8-814e-0cff1c6f4d0c" />

---

### Step 2: Extract + Clean (Day 1 Skills)
Using what you learned on Day 1, write one query that removes rows with a missing `Customer_Name` and fills missing `Discount` with `0`. Save it as a new table called `mini_etl_cleaned`.

*(If you get stuck, look back at your Week2_Day1 notebook — it's completely fine to reference it.)*
```sql
CREATE OR REPLACE TABLE  dataskool.dataskool_schema.mini_etl_cleaned AS
SELECT Order_ID, Order_Date, Customer_Name, Segment, Region, 
    Category, Sub_Category, Product_Name, Sales, Quantity,
    Profit, COALESCE(Discount, 0) AS Discount
FROM dataskool.dataskool_schema.superstore_sales_sample
WHERE Customer_Name IS NOT NULL;
````
<img width="1517" height="630" alt="image" src="https://github.com/user-attachments/assets/77905b6d-46ee-4265-8b40-a28e69fb4fdc" />

---

### Step 3: Join (Day 2 Skills)
Join `mini_etl_cleaned` with `category_details` using `Category`, and save the result as `mini_etl_joined`.

*(Reference your Week2_Day2 notebook if needed.)*
```sql
CREATE OR REPLACE TABLE dataskool.dataskool_schema.mini_etl_joined AS
SELECT m.Order_ID, m.Order_Date, m.Segment, m.Region, m.Category,
 m.Sub_Category, m.Product_Name, m.Sales, m.Quantity, m.Profit, 
 m.Discount, c.Category_Manager, c.Warehouse_Location 
 FROM dataskool.dataskool_schema.mini_etl_cleaned m 
 JOIN dataskool.dataskool_schema.category_details c 
 ON m.Category = c.Category
```
<img width="1435" height="687" alt="image" src="https://github.com/user-attachments/assets/06a05ebd-4cfa-4c0e-9a55-232647168a6b" />

---

### Step 4: Transform (Day 3 Skills)
Add a `CASE WHEN` column labeling each order as "High Value," "Standard," or "Low Value" based on `Sales`, and save the result as `mini_etl_transformed`.

*(Reference your Week2_Day3 notebook if needed.)*
```sql
CREATE OR REPLACE TABLE dataskool.dataskool_schema.mini_etl_transformed
AS
SELECT *,
CASE 
    WHEN Sales > 700 THEN "High_Value"
    WHEN Sales BETWEEN 700 AND 300 THEN "Medium_Value"
    ELSE "Low_Value"
END AS Value_Bucket FROM dataskool.dataskool_schema.superstore_sales_sample
```
<img width="1490" height="682" alt="image" src="https://github.com/user-attachments/assets/a356a9fe-7415-4043-801a-a70f2dd1798f" />


---

### Step 5: Load (Day 4 Skills)
Save `mini_etl_transformed` as a Parquet table called `mini_etl_final`.

*(Reference your Week2_Day4 notebook if needed.)*

---

### Step 6: Confirm the Full Pipeline Worked
Run this to check your final output:
```sql
SELECT COUNT(*) AS final_row_count
FROM dataskool.dataskool_schema.mini_etl_final;
```
<img width="1011" height="322" alt="image" src="https://github.com/user-attachments/assets/9f00c32f-9508-43be-8dd0-7dc23731f16a" />

```sql
SELECT * FROM dataskool.dataskool_schema.mini_etl_final LIMIT 10;
```
<img width="1496" height="482" alt="image" src="https://github.com/user-attachments/assets/8915976d-7ebf-4105-9af9-e4196e63bbe4" />


---

## Day 5 Task Checklist
- [ ] Confirmed the raw row count
- [ ] Cleaned the data (removed missing names, filled missing discounts)
- [ ] Joined in the category lookup table
- [ ] Added a `CASE WHEN` label column
- [ ] Saved the final result as a Parquet table
- [ ] Confirmed the final row count and content
- [ ] Wrote one summary business question query
- [ ] Explained the full pipeline out loud, table by table
