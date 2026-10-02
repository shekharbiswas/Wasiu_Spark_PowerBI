# Week 2 — Day 1: Concepts
## Data Quality — "Making Messy Data Trustworthy"

---

## Recap of Week 1 (10 min)
Before starting anything new, quickly repeat out loud:
1. What are the 4 stages of a data pipeline?
2. What did we do in Week 1? (ingest → profile → filter/select → aggregate)
3. On Day 2 of Week 1, we found nulls and duplicates in our dataset — do you remember what those are?

---

## Today's Stage: Cleaning — Stage 2 of the Pipeline
Last week, we only *found* problems in the data (profiling). We never touched or changed anything. Today, for the first time, **we actually fix the data**.

**Key line to repeat to student:** *"Finding a problem and fixing a problem are two different skills. Last week you learned to find issues. Today you learn to fix them — this is called data cleaning, and it's one of the biggest parts of a Data Engineer's job."*

---

## Why Data Cleaning Matters
If messy data flows into a report or dashboard without being cleaned first:
- A missing `Customer_Name` might show up as a blank row in a customer report
- A missing `Discount` might cause an incorrect total in a financial calculation
- Duplicate rows might make total sales look higher than they actually are

**Excel comparison:** This is the same as using "Remove Duplicates" or filling in blank cells in Excel — except now we do it in a repeatable, automatable way that works even on much larger datasets.

---

## The Two Core Cleaning Tasks Today

### 1. Handling Missing Values (NULLs)
There are two common ways to handle a NULL:
- **Remove the row** — if the missing value makes the row unusable
- **Fill it in with a default/placeholder value** — if we can reasonably guess or substitute something (e.g. replacing a missing `Discount` with `0`)

**Which one to use depends on the business context** — there's no single "correct" answer, and this is an important judgment call a Data Engineer has to make, not just a technical step.

### 2. Handling Duplicates
A duplicate is a row that appears more than once when it shouldn't (e.g. the same order logged twice by accident). The usual fix is simply to **keep only one copy** of each duplicate row.

---

## Key Terms Introduced Today
| Term | Plain-Language Meaning |
|------|--------------------------|
| Data cleaning | The process of fixing or removing problems found during profiling |
| `COALESCE()` | Replaces a NULL with a fallback value you choose |
| `DISTINCT` | Returns only unique rows, removing exact duplicates |
| `IS NOT NULL` | A condition that keeps only rows where a column has a value |
| `CREATE TABLE ... AS SELECT` (CTAS) | Saves the result of a query as a brand-new, clean table |

---

## What Success Looks Like Today
By the end of today, the student should be able to say, in their own words:
1. The difference between profiling (finding issues) and cleaning (fixing issues)
2. Two different strategies for handling a missing value, and when you'd choose each
3. How to remove duplicate rows using `DISTINCT`
4. How to save a cleaned version of the data as a new table

**Closing line for the day:** *"You just did something every professional Data Engineer does constantly — turning messy, unreliable data into something trustworthy enough to build a report on. Tomorrow, we go further: combining this data with a second table, because real business data almost never lives in just one place."*