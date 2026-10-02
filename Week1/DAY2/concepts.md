# Week 1 — Day 2: Concepts
## Data Profiling — "Never Trust Data Blindly"

---

## Recap of Day 1 (5 min)
Before starting anything new, quickly repeat out loud:
1. What are the 4 stages of a data pipeline?
2. What stage did we do yesterday? (Ingest)
3. What does `LIMIT` do?

---

## Today's Stage: Still Part of Ingestion — Now We Inspect What We Ingested
Yesterday we brought raw data into Databricks. Today we don't touch or change anything yet — we just **look closely** at what we have.

**Key line to repeat to student:** *"A Data Engineer never trusts data just because it loaded successfully. Before doing anything else, we check: what columns exist, what type of data is in them, and whether anything looks wrong."*

This is called **data profiling**.

---

## Why Profiling Matters
If you skip this step and jump straight to building reports or pipelines, you risk:
- Treating a text column as a number (and getting wrong calculations)
- Missing that half the rows have blank values in an important column
- Not noticing duplicate records that would inflate totals

**Excel comparison:** This is the same instinct as scrolling through a spreadsheet checking for weird values, blank cells, or a column that "looks off" — except now we do it properly and at scale.

---

## What Exactly Is "Data Profiling"?
Data profiling means asking a fixed set of questions about a dataset **before** using it for anything else. Think of it like a doctor doing a check-up before treatment — you gather basic vitals first. For a dataset, the "vitals" are:

1. **Structure** — What columns exist, and in what order?
2. **Types** — Is each column storing the kind of data it should (text, number, date)?
3. **Volume** — How many rows are there in total?
4. **Completeness** — Are there missing (NULL) values, and in which columns?
5. **Uniqueness** — Are there duplicate rows or duplicate key values that shouldn't repeat?
6. **Validity** — Do values make sense (e.g. no negative ages, no dates in the future)?

We won't cover all six deeply today — Day 2 focuses on Structure, Types, Volume, and Completeness. Uniqueness gets a light preview today and returns properly in Week 2. Validity checks come later once the student is comfortable with the basics.

---

## The Four Profiling Checks We Do Today

### 1. Structure & Types (Schema Check)
Every table has a **schema** — a blueprint listing each column's name and the type of data it holds.

| Data Type | What It Stores | Example |
|-----------|------------------|---------|
| STRING | Text | "Jen Starke" |
| INT / DOUBLE | Numbers | 245, 19.99 |
| DATE / TIMESTAMP | Dates and times | 2024-05-01 |
| BOOLEAN | True/False values | true, false |

**Why it matters:** If a column like "price" is accidentally stored as STRING instead of a number, you cannot do math on it (SUM, AVG) until it's fixed. Catching this on Day 2 saves confusion later.

### 2. Volume (Row Count Check)
Knowing the total number of rows tells us the scale we're working with, and gives us a baseline to compare against later (e.g. "we started with 500 rows — did we lose any after cleaning?").

### 3. Completeness (Missing Values / NULLs)
A **NULL** is a blank/missing value in a column — not zero, not an empty string, but literally "no value was recorded."

**Why it matters:** If 30% of a "customer_email" column is NULL, any process depending on emailing customers is already broken for a third of the data. A Data Engineer needs to know this *before* building anything downstream.

### 4. Uniqueness (Light Preview — Duplicates)
Sometimes the same record appears more than once by mistake (e.g. the same sale entered twice). Today we only peek at this using `GROUP BY` + `HAVING` as a profiling tool — the full explanation of how `GROUP BY` works comes formally on Day 4.

---

## Key Terms Introduced Today
| Term | Plain-Language Meaning |
|------|--------------------------|
| Data profiling | The practice of inspecting a dataset's structure and quality before using it |
| Schema | The structure of a table — column names and their data types |
| Data type | Whether a column holds text, numbers, dates, etc. |
| Row count | How many total records/rows are in the table |
| NULL | A missing/blank value in a column |
| Duplicate | A record that appears more than once when it shouldn't |
| `DESCRIBE` | A command that shows you a table's schema |
| `COUNT(*)` | Counts the total number of rows in a table |
| `IS NULL` | A condition used to find rows where a column is missing a value |

---

## What Success Looks Like Today
By the end of today, the student should be able to say, in their own words:
1. What "data profiling" means and why it comes before any other pipeline step
2. How to check a table's schema and row count
3. At least one thing they noticed about the dataset (a data type, a missing value, anything unusual)

**Closing line for the day:** *"You just did what every Data Engineer does before touching a dataset — you inspected it first. Tomorrow we start actually working with it: filtering and selecting only what we need."*