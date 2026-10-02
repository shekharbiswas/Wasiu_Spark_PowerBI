# Week 1 — Day 1: Concepts
## What Does a Data Engineer Do? + Intro to Ingestion

## Tool We're Using: Databricks Community Edition (FREE)
Databricks Community Edition is a free version of Databricks that gives us a real Spark environment in the browser — no installation needed. This is what we'll use for all of Week 1 and Week 2.



## What is a Data Engineer?
A Data Engineer's job has 4 basic stages — think of it like a factory assembly line for data:

| Stage | What Happens | Excel Equivalent |
|-------|---------------|-------------------|
| 1. Ingest | Bring raw data into the system | Opening a CSV file in Excel |
| 2. Clean | Fix messy/incorrect data | Removing blank rows, fixing typos |
| 3. Transform | Reshape data into useful form | Pivot tables, formulas |
| 4. Load | Save the final data somewhere usable | Saving a finished report |

**Today we only do Stage 1: Ingest.** Everything else comes later.

**Key line to repeat to student:** *"Today you are not learning a programming language. You are learning how a Data Engineer gets raw data into a system. SQL is just the tool we use to talk to Spark."*


## Why Databricks?
- It's free (Community Edition)
- It runs real Spark in the browser — nothing to install
- It lets us write SQL directly, no Python required at this stage
- It's used by real companies, so what the student learns here transfers directly to a job setting



## Key Terms Introduced Today
| Term | Plain-Language Meaning |
|------|--------------------------|
| Cluster | The "engine" that powers Spark — must be running before anything else works |
| Table | Where our uploaded data lives inside Databricks, like a sheet in Excel |
| Notebook | The place where we write and run our SQL queries, step by step |
| Query | An instruction we give Spark to look at or filter the data |
| `SELECT * FROM table` | "Show me everything in this table" |
| `LIMIT` | "Only show me the first few rows" (good habit for big datasets) |



## What Success Looks Like Today
By the end of today, the student should be able to say, in their own words:
1. What a data pipeline is (the 4 stages)
2. What stage we worked on today (Ingest)
3. What a cluster, table, and notebook are, in plain language

**Closing line for the day:** *"Today, you completed Step 1 of a real data pipeline — the exact same first step a professional Data Engineer does on day one of any project."*
