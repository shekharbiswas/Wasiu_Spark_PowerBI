# Week 1 — Day 5: Concepts
## Recap — "You Just Built Stage 1 of a Real Data Pipeline"



## Why Today Is Different
There's no new syntax today. Today is about **proving to yourself** that what you learned this week isn't four separate tricks — it's one connected skill: taking raw data and turning it into something a business can use, step by step, on your own.

**Key line to repeat to student:** *"Today, I'm not going to teach you anything new. You already know everything you need. Today, you show me you can do it yourself, from start to finish, on data you've never seen before."*



## The Full Picture — What We Actually Did This Week

| Day | What We Did | The Real-World Question It Answers |
|-----|--------------|--------------------------------------|
| 1 | Ingested raw data into Spark | "How do I get data into the system?" |
| 2 | Profiled the data (schema, nulls, duplicates) | "Can I trust this data before I use it?" |
| 3 | Filtered and selected relevant data | "How do I isolate only what the business needs?" |
| 4 | Aggregated data into summary metrics | "How do I turn rows into numbers a manager can use?" |

Put together, Days 1-4 form **Stage 1 of the data engineering pipeline**: getting raw data in, understanding it, narrowing it down, and summarizing it. This is real, professional work — not a classroom exercise. Every data engineer does exactly this sequence, on every new dataset they encounter, in every job.



## Why This Sequence Always Matters
Notice the *order* was never random:
1. You can't filter or aggregate data you haven't ingested (Day 1 first)
2. You shouldn't trust or use data you haven't checked for problems (Day 2 before anything else)
3. You should narrow down to what's relevant before you summarize it (Day 3 before Day 4)
4. Only then do you summarize into business metrics (Day 4 last)

**This order is not just "how we taught it" — it's how professionals actually approach any new dataset, every time.**



## What's Different Today
- **New dataset** (`elektronik_shop_sales.csv`) — a different business (electronics/appliances/books retailer), different regions, different product categories. The student has never seen this exact data before.
- **Less guidance** — the instructor observes and only steps in when truly stuck, rather than walking through each line
- **The student explains out loud** what they're doing and why, at each stage — not just typing commands


## Key Ideas to Reinforce Today
| Concept | What the Student Should Be Able to Explain |
|---------|-----------------------------------------------|
| Ingestion | "I'm bringing raw data into Spark so I can work with it" |
| Profiling | "I'm checking the schema, row count, nulls, and duplicates before trusting this data" |
| Filtering/Selecting | "I'm narrowing down to only the columns and rows that matter for this question" |
| Aggregating | "I'm turning many rows into one meaningful business number" |



## What Success Looks Like Today
By the end of today, the student should be able to, **with minimal help**:
1. Ingest a brand-new CSV into Spark and register it as a table
2. Profile it — check schema, row count, and find at least 2 data quality issues on their own
3. Write a filtered/selected query answering a business question the instructor poses
4. Write an aggregated (GROUP BY) query answering a second business question

**Closing line for the day:** *"This week, you didn't just learn SQL commands — you learned how to think like a Data Engineer: bring data in, question it before trusting it, narrow it to what matters, and summarize it into something useful. Next week, we go further — cleaning and transforming this data into a real pipeline output."*
