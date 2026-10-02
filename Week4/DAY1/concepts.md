# Week 4, Day 1 — Concepts
## What Is Power BI, and Where Does It Fit After Data Engineering?

---

## Start Here: The Question of the Day
**"I already have clean data sitting in a table — why isn't that enough? Why do I need another tool on top of it?"**

Clean data is necessary, but it's not the same as *understandable* data. A perfectly cleaned table of 412 rows still means nothing to someone glancing at it for three seconds in a meeting. By the end of today, you'll see what Power BI actually adds on top of the data engineering work you've already done — and why that layer is what most people in a company actually see.

---

## 1. Recap: What You Already Have Going Into This Week
By the end of Weeks 1–3, you've built:
- A cleaned, joined, transformed version of `superstore_sales_sample` (Week 2's output)
- Optionally, a live streaming aggregation of the same data (Week 3's output)

Both of these are **correct** — but both are still sitting in tables, notebooks, or code. Nobody outside a data role is going to open a Databricks notebook to find out how sales are trending. That gap — between "the data is right" and "someone can act on it" — is exactly what Power BI closes.

---

## 2. Why Not Just Send Someone a Spreadsheet?
You could export the cleaned table to a CSV and email it. Here's why that usually fails in practice:

- A raw table of numbers doesn't answer a question — it just holds the answer somewhere inside it, buried.
- Every person receiving it has to do their own filtering, sorting, and mental math to find what matters to them.
- If the data changes tomorrow, you're emailing a new file, and everyone's already-open copy is now wrong.

**Power BI flips this.** Instead of handing someone raw numbers and hoping they find the story, you build the story once — a chart, a filter, a KPI card — and everyone who opens the report sees the same decision-ready view, refreshed from the source automatically.

> **Analogy:** A spreadsheet is like handing someone a box of ingredients and a recipe book and saying "figure out dinner." A Power BI report is like handing them the finished, plated meal.

---

## 3. Meet the Power BI Mental Model
There are three stages to learn today. Everything else this week is detail layered on top of these three.

### a) Get Data
This is the connection step — telling Power BI where the data lives (a CSV, a database, a Databricks table) and pulling it in. This is the direct handoff point from data engineering: Power BI doesn't care *how* the data got clean, only that it connects to something that already is.

### b) Model
Once data is in, it needs structure — which tables relate to which, and how. If you have an `orders` table and a `products` table, the model is where you tell Power BI "these connect on `product_id`." This should feel familiar: it's the same relationship thinking behind the joins you wrote in Spark SQL in Week 2 — just represented visually instead of in code.

### c) Report
This is the visible layer — charts, tables, filters, KPI cards, arranged on a canvas. This is the only stage most people in a company will ever see. Everything in Get Data and Model exists purely to make this stage possible and correct.

> **Analogy:** Get Data is grocery shopping. Model is organizing the kitchen so ingredients that go together are stored together. Report is the plated dish someone actually eats.

---

## 4. Putting It Together — One Sentence
> **Power BI connects to already-engineered data, models the relationships between its tables, and reports the result as something a decision-maker can read in seconds.**

Say that sentence out loud once. That's the entire mental model for this week.

---

## 5. Where Does Data Engineering Fit In?
Power BI trusts whatever it's given completely — it has no idea whether the upstream data engineering was done carefully or sloppily. If a join was wrong in Week 2, or a schema drifted, Power BI will still render a clean-looking, confident-looking chart on top of wrong numbers. Today is just about understanding the three stages — no building yet.

---

## 6. Quick Self-Check
Before moving to today's tasks, make sure you can answer these out loud, in your own words:

1. What's the difference between a raw spreadsheet and a Power BI report, using the ingredients/plated-meal analogy?
2. What are the three stages of the Power BI mental model, in order?
3. Which stage is closest to the join logic you already learned in Spark SQL?
4. Why can a Power BI report look confident and still be wrong?

If any of these feel shaky, re-read the matching section above before starting today's tasks — everything this week builds on these three words: **Get Data, Model, Report.**