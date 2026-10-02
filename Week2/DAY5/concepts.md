# Week 2 — Day 5: Concepts
## Mini ETL Project — "Putting It All Together"

---

## Quick Recap
Before we start, think back over the whole week:
1. Day 1: What did you do to the data? (cleaned it — nulls and duplicates)
2. Day 2: What did you combine? (joined a second table using `Category`)
3. Day 3: What did you create that didn't exist before? (labels and a calculated field, using `CASE WHEN`)
4. Day 4: What did you do at the very end? (saved the data as CSV and Parquet)

---

## Today Is Different — Today You Build the Whole Thing Yourself
No new concepts today. Today, you take everything from this week — cleaning, joining, transforming, saving — and put it together as **one complete pipeline**, from raw data to final output, mostly on your own.

This is exactly what a real ETL (Extract, Transform, Load) pipeline looks like in a real job — the only difference is scale.

---

## What ETL Actually Stands For
| Letter | Stage | What You Did This Week |
|--------|-------|---------------------------|
| **E** — Extract | Getting raw data into the system | Ingesting the CSV (Week 1) |
| **T** — Transform | Cleaning, joining, and reshaping the data | Days 1-3 this week |
| **L** — Load | Saving the final result somewhere usable | Day 4 this week |

Today, you run E → T → L yourself, start to finish, without being told each individual step.

---

## Today's Pace
This is a lighter day on purpose. You already know every piece — today is about **connecting the pieces**, not learning anything new. Go at your own pace, and if you get stuck, that's completely normal — it means you're thinking, not failing.

---

## What Success Looks Like Today
By the end of today, you should be able to say, in your own words:
1. What ETL stands for, and what happens in each stage
2. How the tables you built this week connect to each other (raw → cleaned → joined → enriched → final)
3. That you can rebuild this entire pipeline yourself, on a new dataset, if asked

**Closing line for the week:** *You didn't just learn SQL commands this week — you built a real, working data pipeline, the same shape every professional Data Engineer builds every day. Next week, we move into Kafka, and start learning how data moves between systems in real time.*