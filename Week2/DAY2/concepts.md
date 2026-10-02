# Week 2 — Day 2: Concepts
## Joins — "Combining Data That Lives in Different Places"

---

## Recap of Week 2 Day 1 (10 min)
Before starting anything new, quickly repeat out loud:
1. What's the difference between profiling and cleaning?
2. What does `COALESCE()` do?
3. What does `DISTINCT` do?
4. What table did we save yesterday? (`superstore_sales_cleaned`)

---

## Today's Stage: Still Cleaning/Transformation — Now We Combine Sources
So far, everything we've done lives in **one table**. But real businesses never keep all their data in a single table. Customer info, product info, sales, region info — these usually live in **separate tables**, sometimes even in separate systems entirely.

**Key line to repeat to student:** *"In the real world, no business keeps everything in one giant spreadsheet. Sales data lives in one place, manager info lives somewhere else, warehouse info lives somewhere else again. A Data Engineer's job is to bring these pieces together — that's called a join."*

---

## Why Joins Matter
Imagine your manager asks: *"Who is the Category Manager responsible for our top-selling category, and which warehouse handles it?"*

Our sales table has `Category`, but it doesn't have `Category_Manager` or `Warehouse_Location` — that information lives in a **separate, small lookup table** (`category_details.csv`). To answer the question, we need to **join** the two tables together, matching rows where the `Category` column is the same in both.

**Excel comparison:** This is exactly what `VLOOKUP` (or `XLOOKUP`) does in Excel — looking up a matching value in another table and pulling back extra information. A SQL `JOIN` does the same thing, but can pull back many columns at once and match many rows at once, not just one lookup at a time.

---

## The Two Tables We'll Use Today

**Main table:** `superstore_sales_cleaned` (the clean table we created yesterday) — has `Order_ID`, `Customer_Name`, `Category`, `Sales`, etc.

**Lookup table:** `category_details` — has `Category`, `Category_Manager`, `Warehouse_Location`

Both tables share one column in common: **`Category`**. This shared column is what we "join on."

---

## The Core Idea Today: INNER JOIN and LEFT JOIN

### INNER JOIN
Returns only the rows where a match is found in **both** tables. If a category in the sales table has no matching row in the lookup table, that row disappears from the result.

### LEFT JOIN
Returns **all rows from the main (left) table**, and fills in matching info from the second table where it exists — or shows blank/NULL if no match is found. Nothing from the main table gets dropped.

**Plain-language rule of thumb:** *"If you don't want to lose any of your original data, use LEFT JOIN. If you only want rows that have a match in both tables, use INNER JOIN."* In most real Data Engineering work, LEFT JOIN is the safer default.

---

## Key Terms Introduced Today
| Term | Plain-Language Meaning |
|------|--------------------------|
| Join | Combining two tables based on a shared column |
| Join key | The column used to match rows between two tables (e.g. `Category`) |
| `INNER JOIN` | Keeps only matching rows from both tables |
| `LEFT JOIN` | Keeps all rows from the main table, fills in matches where found |
| Lookup table | A small reference table used to add extra information via a join |

---

## What Success Looks Like Today
By the end of today, the student should be able to say, in their own words:
1. Why business data usually lives in more than one table
2. The difference between INNER JOIN and LEFT JOIN
3. How to write a simple join between two tables using a shared column

**Closing line for the day:** *"You just combined data from two different sources into one answer — this is one of the single most common tasks in real Data Engineering work. Tomorrow, we go further: creating brand-new columns from the data we already have."*