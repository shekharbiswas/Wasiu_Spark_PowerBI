# Week 2 — Day 4: Concepts
## Writing Output — "Handing Off Your Work to the Next Stage"

---

## Quick Recap
Before we start, think back:
1. What are the 4 stages of a data pipeline?
2. What did you build yesterday? (a table with labels and a calculated field: `superstore_sales_enriched`)
3. What does `CASE WHEN` do?

---

## Today's Stage: Load — The Final Step of a Pipeline
So far, everything you've built has lived inside Databricks, inside tables you can query. But a real pipeline doesn't stop there — the whole point of doing all this work is to **hand the finished data off** to something else: a dashboard, a report, another team, another system.

That handoff step is called **Load**, and it completes the classic pipeline: **Ingest → Clean → Transform → Load**.

Today, you learn how to save your work as an actual output file — something that could be opened in Excel, loaded into Power BI, or picked up by another pipeline entirely.

---

## Why This Step Matters
Imagine spending days cleaning and enriching a dataset, and then... it just stays locked inside your notebook. Nobody else can use it. All that work goes nowhere.

Writing output solves this. Once your table is saved as a file, it becomes portable — anyone, or anything, can pick it up next.

**Excel comparison:** This is exactly like clicking "Save As" in Excel and choosing a file format. Except here, you're deciding both where the data goes and how it's structured, which matters a lot more at scale.

---

## Two File Formats You'll Use Today

### CSV (Comma-Separated Values)
- Simple, readable text format
- Opens directly in Excel or Power BI
- Best for smaller datasets or final reports meant for humans to open

### Parquet
- A format designed for big data and pipelines, not for opening manually
- Stores data more efficiently and keeps track of column types automatically
- The standard format real Data Engineering pipelines use to pass data between stages

**Plain-language rule of thumb:** *CSV is for humans. Parquet is for machines and pipelines.* A real production pipeline almost always uses Parquet internally, and only converts to CSV at the very end, if a person needs to open it.

---

## Key Terms Introduced Today
| Term | Plain-Language Meaning |
|------|--------------------------|
| Load | The final pipeline stage — saving finished data somewhere usable |
| CSV | A simple, readable file format, good for opening in Excel |
| Parquet | An efficient file format built for pipelines and big data |
| Write / Save | Taking a table's contents and storing it permanently as a file |

---

## What You Should Be Able to Do By the End of Today
1. Explain what the "Load" stage means and why it matters
2. Explain the difference between CSV and Parquet, and when to use each
3. Save a table as a CSV file
4. Save a table as a Parquet file
5. Reload a saved file back into Spark to confirm it saved correctly

By the end of today, you will have completed a full pipeline stage from start to finish — ingest, clean, transform, and now load. Tomorrow, you put all of it together into one complete mini project, on your own.