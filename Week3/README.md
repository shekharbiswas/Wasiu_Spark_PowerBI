# Week 3 — Kafka: Streaming Basics

## Week Goal
Weeks 1–2 covered data **at rest**: a file sitting still, ready to be queried, cleaned, joined, and summarized whenever you feel like it. This week introduces data **in motion** — records that arrive continuously and don't wait for you to run a query. The student learns how systems move data to each other in real time, and how Databricks plugs into that flow.

**Key line to repeat to student throughout the week:** *"Every week so far, the data was already sitting there waiting for you. This week, the data is moving — your job is to catch it as it goes by."*

---

## Setup Note: Kafka on Databricks
Databricks does not run a Kafka broker itself — there's no "create a Kafka cluster" button in the workspace. What Databricks *does* natively is speak Kafka fluently through **Structured Streaming**, using `readStream`/`writeStream` against an external Kafka-compatible cluster.

For this week, the student connects their Databricks notebook to a **free-tier Confluent Cloud** Kafka cluster (no infra to install, generous free quota, and it's the same connection pattern used against a real production Kafka). This is the identical shape of what happens in industry: Kafka is almost always a separate managed service, and Databricks is the consumer/producer client — so this is a realistic setup, not a simplified toy version.

---

## Dataset Used
We turn the now-familiar **`superstore_sales_sample.csv`** into a live stream. Instead of loading all 412 rows at once, a small Python producer script sends the rows to a Kafka topic one at a time (or in small batches), simulating orders arriving live. The student then consumes that same topic inside Databricks. Same data, new shape — nothing new to learn about the domain, only about how it arrives.

---

## Week Structure

| Day | Focus | Real-World Question It Answers |
|-----|-------|----------------------------------|
| 1 | Streaming concepts — topics, producers, consumers, brokers | "Why can't I just query a database every 5 seconds instead?" |
| 2 | Producing events — writing rows to a Kafka topic | "How does data get into the stream in the first place?" |
| 3 | Consuming with Structured Streaming — `readStream` into a DataFrame | "How does Databricks read a stream that never stops?" |
| 4 | Windowed aggregation — summarizing data over time windows | "How do I summarize something that's still arriving?" |
| 5 | Mini streaming pipeline — producer → Kafka → Databricks → live output, guided | "Can I build a real-time pipeline, start to finish?" |

---

## Teaching Principles (Same as Weeks 1–2, plus one addition)
1. Every new command is introduced through the business problem it solves, not the syntax itself
2. Bridge from what the student already knows (batch pipeline from Week 2 → "same steps, but the data keeps coming")
3. Repeat prior day's syntax at the start of every session
4. One core new idea per day
5. **New this week:** streaming requires PySpark (`readStream`/`writeStream`), not pure Spark SQL — flag this shift explicitly on Day 1 so it isn't a surprise
6. Week ends with a real mini project the student can point to and say "I built this"

---

## Deliverable by End of Week 3
A working mini streaming pipeline that:
1. Produces order events into a Kafka topic (via the provided producer script)
2. Reads that topic as a live stream in Databricks using Structured Streaming
3. Applies a windowed aggregation (e.g., rolling sales total per time window)
4. Writes the streaming result to an output sink (console or a live table)

This mirrors, in miniature, exactly what a real production real-time pipeline does — the same pattern behind live dashboards and alerting systems.

---
*See `Week3_Day1_Concepts.md` / `Week3_Day1_Tasks.md` and `Week3_Day2_Concepts.md` / `Week3_Day2_Tasks.md` for detailed daily breakdowns.*