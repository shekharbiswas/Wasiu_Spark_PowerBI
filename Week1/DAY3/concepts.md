# Week 1 — Day 3: Concepts
## Filtering & Selecting — "Isolating the Data You Actually Need"


## Recap of Day 1 & Day 2 (5-10 min)
Before starting anything new, quickly repeat out loud:
1. What are the 4 stages of a data pipeline?
2. What is data profiling, and why do we do it before anything else?
3. Name one data quality issue we found in our dataset on Day 2 (missing values? duplicates?)


## Today's Stage: Still Ingestion — Now We Narrow Down What We Look At
On Day 1 we brought data in. On Day 2 we inspected it and found problems. Today we still don't fix anything — we just learn how to **look at only the part of the data we care about**.

**Key line to repeat to student:** *"A business almost never needs the entire dataset at once. A manager might only want to see sales from one region, or only orders above a certain amount. Today we learn how to isolate exactly that — nothing more, nothing less."*

This is called **filtering and selecting**.


## Why Filtering & Selecting Matters
Imagine a table with 400+ rows and 12 columns. If someone asks:
- "Show me only orders from Bayern"
- "Show me only the Customer Name and Sales columns, not everything"
- "Show me only orders where Sales was above 1000"

...you don't want to scroll through everything manually. Filtering and selecting let us answer these questions precisely and instantly.

**Excel comparison:** This is exactly what the **Filter** button and **hiding/selecting columns** does in Excel — except now it's written as a repeatable instruction instead of a manual click.


## The Two Core Ideas Today

### 1. Selecting — Choosing Which Columns to See
Not every column matters for every question. If we only care about customer and sales amount, we don't need to see Discount, Profit, Region, etc. **Selecting** means choosing exactly the columns we want to look at.

### 2. Filtering — Choosing Which Rows to See
Even within the columns we've selected, we usually only want certain rows — e.g. only orders from a certain region, or only orders above a certain sales value. **Filtering** means applying a condition so only matching rows show up.

**Together:** Selecting narrows the columns (the "what"), filtering narrows the rows (the "which ones"). A Data Engineer combines both constantly.


## Key Terms Introduced Today
| Term | Plain-Language Meaning |
|------|--------------------------|
| SELECT | Choosing which columns to display |
| WHERE | A condition that filters which rows are shown |
| Alias (`AS`) | Giving a column a friendlier temporary name in the output |
| ORDER BY | Sorting the results (e.g. highest sales first) |
| Comparison operators (`=`, `>`, `<`, `>=`, `<=`) | Used inside `WHERE` to define a condition |
| AND / OR | Combining more than one filter condition |


## What Success Looks Like Today
By the end of today, the student should be able to say, in their own words:
1. The difference between "selecting" (columns) and "filtering" (rows)
2. Why a business would want only part of a dataset, not all of it
3. How to write a simple `SELECT ... WHERE ... ORDER BY` query

**Closing line for the day:** *"You just gave the business exactly what it asked for — not everything, just what matters. Tomorrow we go one step further: summarizing this data into real numbers a manager could use in a meeting."*
