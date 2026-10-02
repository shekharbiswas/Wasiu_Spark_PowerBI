# Week 1 — Day 4: Tasks
## Hands-On Step-by-Step (Databricks Community Edition)

**Estimated Time: 6 hours**
*(includes warm-up repetition, guided steps, exploration time, and independent repeat practice — pace is intentionally slow, no rushing)*

**Dataset used:** `superstore_sales_sample.csv` (same dataset as Day 1, Day 2, and Day 3, table: `workspace.default.superstore_sales_sample`)

---

### Step 1: Warm-Up — Repeat Day 3 (30-45 min)
1. Log in to Databricks Community Edition
2. Go to **Compute** and confirm the cluster is running (start it again if it shows stopped)
3. Open the notebook from Day 3 (`Week1_Day3_FilterSelect`)
4. Re-run this from memory, with light guidance only if stuck:
```sql
SELECT Customer_Name, Category, Sales
FROM workspace.default.superstore_sales_sample
WHERE Category = 'Technology'
ORDER BY Sales DESC;
```
<img width="1606" height="757" alt="image" src="https://github.com/user-attachments/assets/38ea8b01-c7a9-45fb-92c4-96cea2daf280" />

**Explain to student:** "We always start by repeating what we did before — this is how it becomes second nature."

---

### Step 2: Create Today's Notebook
1. On the left sidebar, click **Workspace**
2. Click **Create** → **Notebook**
3. Name it `Week1_Day4_Aggregation`
4. Set the default language to **SQL**
5. Attach it to the cluster from Day 1

<img width="1517" height="623" alt="image" src="https://github.com/user-attachments/assets/f969f62c-8c6d-436c-8fa0-0acc8e9c0990" />

---

### Step 3: Count Total Orders
In a new notebook cell, type and run:

```sql
SELECT COUNT(*) AS total_orders
FROM workspace.default.superstore_sales_sample;
```
<img width="1563" height="673" alt="image" src="https://github.com/user-attachments/assets/62800d28-0456-4972-b565-ee07958cb68d" />

Press **Shift + Enter** to run the cell.

**Ask the student:** "Does this number match the row count we found on Day 2?"

---

### Step 4: Sum Total Sales
In a new cell, type and run:

```sql
SELECT SUM(Sales) AS total_sales
FROM workspace.default.superstore_sales_sample;
```
<img width="1472" height="513" alt="image" src="https://github.com/user-attachments/assets/f5a90ffc-1631-4a01-a1c4-305d1736637d" />

**Explain to student:** "This single number is exacly what a manager would want in a report — total revenue from all orders."

---

### Step 5: Average Order Value
In a new cell, type and run:

```sql
SELECT AVG(Sales) AS average_sale
FROM workspace.default.superstore_sales_sample;
```
<img width="1502" height="576" alt="image" src="https://github.com/user-attachments/assets/37ffdb6e-1b46-4bc2-b738-309327d268d5" />

---

### Step 6: Find Smallest and Largest Sale
In a new cell, type and run:

```sql
SELECT MIN(Sales) AS smallest_sale, MAX(Sales) AS largest_sale
FROM workspace.default.superstore_sales_sample;
```
<img width="1612" height="715" alt="image" src="https://github.com/user-attachments/assets/fa61ace1-bebc-47c3-9d36-c6a5c3663418" />

**Ask the student:** "Do these numbers seem reasonable, or does anything look surprising?"

---

### Step 7: Total Sales PER Region (Introduce GROUP BY)
In a new cell, type and run:

```sql
SELECT Region, SUM(Sales) AS total_sales
FROM workspace.default.superstore_sales_sample
GROUP BY Region;
```
<img width="1513" height="628" alt="image" src="https://github.com/user-attachments/assets/2137cd46-fedc-4d48-ac3e-35d29e2a8b18" />

**Explain to student:** "This is the same as building a Pivot Table in Excel with Region in the Rows box and Sales in the Values box (Sum)."

---

### Step 8: Order Count PER Category
In a new cell, type and run:

```sql
SELECT Category, COUNT(*) AS order_count
FROM workspace.default.superstore_sales_sample
GROUP BY Category;
```
<img width="1516" height="612" alt="image" src="https://github.com/user-attachments/assets/205f3a15-2684-4b05-b795-4f1c9f4dbb28" />

**Ask the student:** "Which category has the most orders? Which has the fewest?"

---

### Step 9: Combine GROUP BY with ORDER BY
In a new cell, type and run:

```sql
SELECT Region, SUM(Sales) AS total_sales
FROM workspace.default.superstore_sales_sample
GROUP BY Region
ORDER BY total_sales DESC;
```
<img width="1493" height="642" alt="image" src="https://github.com/user-attachments/assets/6c8ed9fb-0d2b-462a-b10a-fc097dd4a05d" />

**Explain to student:** "Now we can immediately see which region generated the most sales — sorted highest to lowest."

---

### Step 10: Put It All Together
Have the student write one query independently (guide only if stuck) that:
- Groups by `Sub_Category`
- Shows the average `Sales` per sub-category
- Sorts from highest to lowest average

**Expected query:**
```sql
SELECT Sub_Category, AVG(Sales) AS average_sales
FROM workspace.default.superstore_sales_sample
GROUP BY Sub_Category
ORDER BY average_sales DESC;
```
<img width="1597" height="788" alt="image" src="https://github.com/user-attachments/assets/577096d4-717b-4ec4-94cd-dfa649c30987" />

---

### Step 11: Repeat for Practice
Close and reopen the notebook. Have the student redo Steps 4, 7, and 9 from memory with minimal guidance.

---

## Day 4 Task Checklist
- [ ] Repeated Day 3 steps as warm-up
- [ ] New notebook created for Day 4
- [ ] Used `COUNT(*)` to count total orders
- [ ] Used `SUM()` to calculate total sales
- [ ] Used `AVG()` to calculate average sale
- [ ] Used `MIN()` and `MAX()` to find smallest/largest sale
- [ ] Used `GROUP BY` to get totals per region
- [ ] Used `GROUP BY` to get counts per category
- [ ] Combined `GROUP BY` with `ORDER BY`
- [ ] Wrote one independent query combining GROUP BY + AVG + ORDER BY
- [ ] Repeated key steps once more independently
