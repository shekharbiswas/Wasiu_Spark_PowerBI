# Data Engineering Foundations — Spark Power BI

## Student Profile
- Strong in Excel, ETL logic, and data cleaning (manual/Excel-based)
- Basic Canva design familiarity
- Theory-only exposure to Spark and Kafka concepts (no hands-on practice yet)
- No Python knowledge yet (introduced in a later module)
- Learning pace: slow, needs heavy repetition, concept-first before syntax

## Module Goal
By the end of 4 weeks, the student should be able to say **"I can build a basic data pipeline"** — not "I learned some SQL commands." Every session is framed around the *data engineering task* (ingest, clean, transform, load, stream, visualize), with tools (Spark SQL, Kafka, Power BI) positioned as the means to do that task, not the subject itself.

## Module Structure

| Week | Focus | Core Question Answered |
|------|-------|--------------------------|
| 1 | Spark SQL — Ingestion & Exploration | "How do I get raw data into a system and understand it?" |
| 2 | Spark SQL — Transformation & Pipeline | "How do I clean, join, and shape data into something usable?" |
| 3 | Kafka — Streaming Basics | "How does data move between systems in real time?" |
| 4 | Power BI — Visualization & Reporting | "How do I turn processed data into a decision-ready dashboard?" |

## Teaching Principles Used Throughout
1. **No new tool without a "why"** — every concept is introduced by the business/pipeline problem it solves, not the command itself.
2. **Bridge from what the student already knows** — Excel pivot tables → GROUP BY, VLOOKUP → JOIN, Excel data cleaning → NULL/duplicate handling.
3. **Repetition over coverage** — prior day's syntax/concepts are repeated at the start of every session before adding anything new.
4. **Minimal new syntax per day** — one core idea per day, not a syntax dump.
5. **SQL only, no Python yet** — Spark is taught via Spark SQL; the only Python touched is 2-3 lines of fixed setup boilerplate, explicitly labeled as "just plumbing, not something to learn yet."
6. **End each week with a mini project** — small, guided, end-to-end, so the student always finishes the week having "built something," not just learned commands.

## Weekly Breakdown (High Level)

### Week 1 — Spark SQL: Ingestion & Exploration
Set up environment, load data into Spark, profile it, filter/select, and aggregate — framed as the first stage of a data pipeline.

### Week 2 — Spark SQL: Transformation & Pipeline
Data quality (nulls/duplicates), joins, derived columns, writing output, and a full mini ETL pipeline project.

### Week 3 — Kafka: Streaming Basics
Recap theory quickly, then hands-on: create a topic, produce messages, consume messages, simulate a simple event stream.

### Week 4 — Power BI: Visualization & Reporting
Import data, build visuals, apply Power Query cleaning (mirroring Excel), light DAX, and a final dashboard presentation.

## Deliverables by End of Module
- A working mini Spark SQL ETL pipeline (ingest → clean → transform → aggregate → save)
- A basic Kafka producer/consumer demo with simulated events
- A Power BI dashboard built from a cleaned dataset
- Student can explain, in plain language, what a data engineer does at each pipeline stage

## Assessment Approach
Each week ends with a **guided mini exercise/project** rather than a test — the student repeats the week's steps independently on a new small dataset, with the instructor observing and correcting live rather than grading after the fact.

---
*See `Week_1_Spark_SQL_Ingestion.md` for the detailed daily breakdown of Week 1.*
