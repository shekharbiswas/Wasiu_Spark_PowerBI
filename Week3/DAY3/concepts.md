# Week 3, Day 3 — Concepts
## Reading the Stream Into Databricks

---

## Question of the Day
**"How does Databricks read a stream that never stops?"**

For two days now, data has been flowing into your Kafka topic. Today, Databricks finally joins in — as the **consumer**. You'll connect to the same topic you built yesterday and watch rows land inside a Databricks notebook, live.

---

## 1. Recap in One Line
*"A producer sends events into a topic, sitting on a broker, and a consumer reads those events out — in real time, as they happen."*

Yesterday you were the producer. Today, **Databricks is the consumer**.

---

## 2. A Normal DataFrame vs. a Streaming DataFrame
In Weeks 1–2, every DataFrame you touched was **static** — it held a fixed set of rows the moment you loaded it. Run a query, get an answer, done.

A **streaming DataFrame** is different: it doesn't hold a fixed set of rows. Instead, it represents an ongoing table that keeps growing as new events arrive. Think of it less like a spreadsheet and more like a live scoreboard — every time you glance at it, there might be new rows that weren't there a second ago.

> **Analogy:** A static DataFrame is a photograph. A streaming DataFrame is a live camera feed — same subject, but one is frozen and one keeps updating.

---

## 3. The Command That Makes This Happen: `readStream`
So far you've always loaded data with something like `spark.read.csv(...)` — that's a **one-time** load.

Today you'll use `spark.readStream` instead of `spark.read`. That one word change tells Spark: *"Don't just load what's there right now — keep watching this source and hand me new rows as they arrive."*

Everything else about working with the resulting DataFrame feels similar to what you already know — you can still select columns, filter, and so on. The difference is *when* the data shows up: continuously, not all at once.

---

## 4. Messages Arrive as Raw Bytes — You Have to Unpack Them
When Databricks reads from Kafka, each message initially looks like a `value` column full of raw bytes — Databricks doesn't automatically know it's JSON with columns like Order ID, Product Name, and Sales. You have to tell it:

1. **Convert** the raw bytes into a string
2. **Parse** that string as JSON, using a **schema** you define (a list of column names and types — very similar to describing a table's structure)

This is the same idea as Week 1's CSV loading, where you told Spark what the columns were — just applied to each streaming message instead of a whole file at once.

---

## 5. Watching It Work: `display()`
In a Databricks notebook, calling `display()` on a streaming DataFrame starts continuously showing new rows as they arrive, refreshing live — this is how you'll "watch" your stream today, similar to how you watched messages in the Confluent Cloud console on Day 1 and 2.

---

## 6. What Success Looks Like Today
By the end of Day 3, you should be able to:
- Connect a Databricks notebook to your own Kafka topic from Day 2
- Turn the raw Kafka messages into a proper structured DataFrame (real column names, not just raw bytes)
- Watch new rows appear live inside Databricks, without re-running anything

Tomorrow (Day 4), we stop just watching the stream and start **summarizing** it — using time windows to answer questions like "how much have we sold in the last minute?"