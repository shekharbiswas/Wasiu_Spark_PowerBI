# Week 1 — Spark SQL: Ingestion & Exploration

## Week Goal
The student understands and can perform **Stage 1 of a data pipeline**: getting raw data into a system, inspecting it, isolating what's needed, and summarizing it — using Spark SQL as the tool, framed entirely as data engineering work, not "learning SQL."

## Format (every day)
- **Concept (10-15 min):** framed as "which pipeline stage are we in today"
- **Hands-on (45+ min):** guided, same small dataset reused across the week for consistency
- **Repetition warm-up (first 5-10 min):** quickly repeat prior day's steps before introducing anything new

---

## Day 1 — What Does a Data Engineer Do? + First Ingestion
**Concept:** The data pipeline at a glance — ingest → clean → transform → load. Where today's work fits (Step 1: Ingestion).

**Hands-on:**
- Set up environment (Databricks Community Edition / local Spark, whichever is available)
- Fixed 2-3 line Python setup boilerplate (explicitly labeled "just plumbing — not something to learn yet")
- Ingest a CSV into Spark, register it as a table (`createOrReplaceTempView`)
- Run first query: `SELECT * FROM table_name`

**Framing line:** "You just did what every data engineer's day starts with — getting raw data into the system."

**Dataset:** one small, simple CSV (e.g. a sales or student-records dataset, <500 rows)

---

## Day 2 — Data Profiling
**Concept:** "A data engineer never trusts data blindly — you inspect it first."

**Hands-on:**
- Check schema (`DESCRIBE table_name`)
- Row counts (`SELECT COUNT(*) FROM table_name`)
- Spot-check column types and obvious issues (nulls, wrong types, blank values)
- Compare to how they'd eyeball this in Excel (familiar anchor point)

**Framing line:** "This is the equivalent of scrolling through an Excel sheet checking for weird values — just at scale."

---

## Day 3 — Filtering & Selecting
**Concept:** "Isolating only the data your pipeline or business actually needs."

**Hands-on:**
- `SELECT` specific columns
- `WHERE` clause filtering (single and multiple conditions)
- Column aliasing (`AS`)
- `ORDER BY`

**Framing line:** "This is like applying filters in Excel — but now it's repeatable and automatable."

---

## Day 4 — Aggregating Data
**Concept:** "Turning raw rows into business metrics — this is what stakeholders actually look at."

**Hands-on:**
- `GROUP BY` with `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`
- Simple two-level grouping (e.g. group by category, then by sub-category)

**Framing line:** "This is exactly a pivot table — same idea, same output, just written as a query."

---

## Day 5 — Recap + Guided Mini Exercise
**Concept:** "You've now completed Stage 1 of a pipeline — ingest, explore, filter, summarize."

**Hands-on:**
- New small dataset (different from Days 1-4)
- Student repeats, with light guidance: ingest → profile → filter/select → aggregate
- Instructor observes and corrects live, no formal test

**Wrap-up talking point:** "Next week, we take this raw-but-understood data and start actually cleaning and reshaping it — that's Stage 2 of the pipeline."

---

## Week 1 Checklist (Student Should Be Able To)
- [ ] Explain the 4 stages of a data pipeline in plain language
- [ ] Ingest a CSV into Spark and register it as a table
- [ ] Check schema and row counts of a table
- [ ] Write a `SELECT ... WHERE ... ORDER BY` query
- [ ] Write a `GROUP BY` query with at least one aggregate function
- [ ] Explain what they did today in terms of "pipeline stage," not "SQL commands used"