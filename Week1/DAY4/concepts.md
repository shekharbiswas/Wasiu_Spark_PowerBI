# Week 1 — Day 4: Concepts
## Aggregating Data — "Turning Raw Rows into Business Metrics"



## Recap of Day 1, 2 & 3 (5-10 min)
Before starting anything new, quickly repeat out loud:
1. What are the 4 stages of a data pipeline?
2. What's the difference between selecting and filtering?
3. Write (out loud) a simple `SELECT ... WHERE ...` query from memory



## Today's Stage: Still Ingestion — Now We Summarize
On Day 3 we learned how to isolate exactly the rows and columns we need. Today we go one step further: we take many rows and **turn them into a single meaningful number** — the kind of number a manager actually wants to see in a meeting.

**Key line to repeat to student:** *"Nobody in a business meeting wants to see 400 rows of raw orders. They want to know: What were our total sales? What's our average order value? How many orders did we get per region? Today, we learn to answer exactly those questions."*

This is called **aggregating data**.



## Why Aggregating Matters
Raw data is not a business metric by itself. A single row (one order) tells you almost nothing about the business. But when you combine hundreds of rows together — sum them, count them, average them — you get **insights**:
- "Total sales this quarter were €45,230"
- "Bayern had the most orders"
- "Average discount given was 12%"

This is the exact output that ends up in dashboards, reports, and presentations.

**Excel comparison:** This is exactly what a **Pivot Table** does in Excel — grouping data by a category and summarizing it. Spark SQL does the same thing, just written as a query instead of dragging fields into boxes.



## The Core Ideas Today

### 1. Aggregate Functions — Turning Many Values into One
| Function | What It Does | Business Example |
|----------|----------------|-------------------|
| `COUNT()` | Counts how many rows | "How many orders were placed?" |
| `SUM()` | Adds up all values in a column | "What were total sales?" |
| `AVG()` | Calculates the average | "What's the average order value?" |
| `MIN()` | Finds the smallest value | "What was our smallest sale?" |
| `MAX()` | Finds the largest value | "What was our biggest sale?" |

### 2. GROUP BY — Summarizing "Per Category" Instead of Overall
Often we don't want just one overall number — we want it **broken down by group**. For example: "total sales *per region*" instead of one single total.

**Plain-language translation:** `GROUP BY Region` means *"do the calculation separately for each region, instead of lumping everything together."*

**Excel comparison:** This is precisely what happens when you drag a field into the "Rows" box of a Pivot Table — Spark SQL's `GROUP BY` is doing the same grouping.



## Key Terms Introduced Today
| Term | Plain-Language Meaning |
|------|--------------------------|
| Aggregate function | A function that turns many rows into one summary number |
| `COUNT()` | Counts rows |
| `SUM()` | Adds values together |
| `AVG()` | Calculates the average |
| `GROUP BY` | Groups rows by a category before aggregating |
| Business metric | A summarized number used for decision-making (e.g. total sales) |



## What Success Looks Like Today
By the end of today, the student should be able to say, in their own words:
1. What an aggregate function is, and name at least 3
2. What `GROUP BY` does, using the Pivot Table comparison
3. How to write a simple query combining `GROUP BY` with `SUM` or `COUNT`

**Closing line for the day:** *"You just turned raw data into the kind of numbers a manager would put in a report. This completes Stage 1 of the pipeline — tomorrow, we recap everything and you'll repeat these steps on a brand-new dataset by yourself."*


## YouTube References (Optional Watching)
*Note: I don't have live web browsing in this session, so I can't confirm these exact links are currently live — please verify before sharing with the student.*

1. [Databricks — Introduction to Spark SQL](https://www.youtube.com/results?search_query=Databricks+Spark+SQL+tutorial) (official Databricks content on Spark SQL basics)
