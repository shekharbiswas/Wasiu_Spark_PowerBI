# Week 1 — Day 1: Tasks
## Hands-On Step-by-Step (Databricks Community Edition)

**Estimated Time: 6 hours**
*(includes account setup, waiting for cluster to start, guided steps, and repetition/practice time — pace is intentionally slow, no rushing)*



### Step 1: Create a Free Databricks Account
1. Go to **https://www.databricks.com/try-databricks**
2. Click **"Get started"**
3. Choose the **Community Edition** option (look for a small link like "Get started with Community Edition" — it's usually below the main paid sign-up form)
4. Fill in name, email, company (student can write "Student" or "Dataskools")
5. Verify email (check inbox, click verification link)
6. Log in to Databricks Community Edition

> **Note for instructor:** Databricks sometimes changes where the Community Edition link is placed. If it's not visible, search "Databricks Community Edition sign up" directly.



### Step 2: Create a Cluster (the "engine" that runs Spark)
1. On the left sidebar, click **Compute**
2. Click **Create Compute** (or "Create Cluster")
3. Give it a name, e.g. `week1-cluster`
4. Leave all default settings as-is
5. Click **Create Compute**
6. Wait 3-5 minutes — status will change from grey/orange to **green (Running)**

**Explain to student:** "This is like turning on the engine of a car before driving. Spark needs this 'cluster' running before it can process any data."
<img width="1650" height="357" alt="image" src="https://github.com/user-attachments/assets/d5109fc4-3b37-47ad-8db5-de06e1ea19a5" />



### Step 3: Upload the Dataset
1. On the left sidebar, click **Catalog** (or **Data**, depending on version)
2. Click **Create Table** / **Add Data** / **Upload File**
3. Upload the provided CSV file: `superstore_sales_sample.csv` (Superstore-style sales dataset, 412 rows)
4. Databricks will show a preview of the data — let the student look at it and describe what they see (columns, rows, any obvious issues)
5. Note the table name Databricks gives it (e.g. `workspace.default.superstore_sales_sample`) — write it down, we'll need it

**Explain to student:** "This is the same as opening a CSV in Excel — except now it's stored in a system that can handle way more data than Excel ever could."



### Step 4: Create a Notebook
1. On the left sidebar, click **Workspace**
2. Click **Create** → **Notebook**
3. Name it `Week1_Day1_Ingestion`
4. Set the default language to **SQL** (important — avoids Python for now)
5. Attach it to the cluster created in Step 2 (dropdown at top of notebook)



### Step 5: Confirm the Table is Ready
In a new notebook cell, type and run:

```sql
-- This just checks that Spark can see the table we uploaded
SELECT * FROM workspace.default.superstore_sales_sample;
```

> If using the upload-to-table flow in Step 3, the table already exists — no Python needed at all. This is why Databricks + SQL notebooks are ideal for this stage: zero Python required.

Press **Shift + Enter** to run the cell.



### Step 6: First Query — See the Raw Data
In a new notebook cell, type and run:

```sql
SELECT * FROM workspace.default.superstore_sales_sample;
```

**Ask the student:**
- How many columns do you see?
- Do any column names look unclear?
- Do you see any blank/missing values already?



### Step 7: Limit Results (Good Habit)
Real datasets can be huge — good practice to preview only a few rows:

```sql
SELECT * FROM workspace.default.superstore_sales_sample LIMIT 10;
```

**Explain to student:** "This is like only scrolling the first 10 rows in Excel instead of loading the whole sheet — same idea, saves time."
<img width="1910" height="878" alt="image" src="https://github.com/user-attachments/assets/2fb1b7ed-4838-4fc2-ae8b-5a640ecae133" />


---

### Step 8: Repeat for Practice
Have the student close the notebook, reopen it, and repeat Steps 5-7 from memory with light guidance only where they get stuck. Repetition matters more than speed today.



## Day 1 Task Checklist
- [ ] Databricks Community Edition account created
- [ ] Cluster created and running (green status)
- [ ] Dataset uploaded and visible as a table
- [ ] Notebook created, set to SQL
- [ ] Ran `SELECT * FROM table_name` successfully
- [ ] Ran `SELECT * FROM table_name LIMIT 10`
- [ ] Repeated the steps once more independently
