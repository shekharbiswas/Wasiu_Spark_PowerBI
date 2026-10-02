# Week 2 — Spark SQL: Transformation & Pipeline

## Week Goal
Week 1 covered **Stage 1** of the pipeline: ingest, profile, filter/select, aggregate. This week covers **Stage 2 and beyond**: cleaning messy data, combining data from multiple sources, creating new business fields, and saving output — ending with a full mini ETL pipeline the student builds themselves.

**Key line to repeat to student throughout the week:** *"Last week you learned to look at data and summarize it. This week, you learn to fix it, combine it, and reshape it — this is where a Data Engineer spends most of their time."*

---

## Dataset Used
We continue using **`superstore_sales_sample.csv`** (412 rows, same dataset from Week 1) so the student stays familiar with the columns and doesn't need to relearn a new domain. New for this week: a **second, small lookup dataset** will be introduced on Day 2 to teach joins — since joining data from more than one source is a core, everyday Data Engineering task.

---

## Week Structure

| Day | Focus | Real-World Question It Answers |
|-----|-------|----------------------------------|
| 1 | Data Quality — handling nulls & duplicates | "How do I make messy data trustworthy?" |
| 2 | Joins — combining multiple data sources | "How do I bring together data that lives in different tables?" |
| 3 | Derived columns — CASE WHEN, calculated fields | "How do I create new business fields from raw data?" |
| 4 | Writing output — saving pipeline results | "How does a pipeline hand off data to the next stage?" |
| 5 | Mini ETL project — full pipeline, guided | "Can I build ingest → clean → transform → aggregate → save, start to finish?" |

---

## Teaching Principles (Same as Week 1)
1. Every new command is introduced through the business problem it solves, not the syntax itself
2. Bridge from what the student already knows (Excel cleaning, VLOOKUP, pivot tables)
3. Repeat prior day's syntax at the start of every session
4. One core new idea per day
5. Still Spark SQL only — no Python beyond fixed setup boilerplate
6. Week ends with a real mini project the student can point to and say "I built this"

---

## Deliverable by End of Week 2
A working mini ETL pipeline in Spark SQL that:
1. Loads the raw sales dataset
2. Cleans nulls and removes duplicates
3. Joins in extra information from a second table
4. Creates at least one new derived/calculated column
5. Aggregates the cleaned, joined, transformed data into a business summary
6. Saves the final result as output (CSV/Parquet)

This mirrors, in miniature, exactly what a real production data pipeline does.

---
*See `Week2_Day1_Concepts.md` / `Week2_Day1_Tasks.md` and `Week2_Day2_Concepts.md` / `Week2_Day2_Tasks.md` for detailed daily breakdowns.*