# Week 4, Day 3 — Concepts
## DAX Fundamentals: Calculated Columns and Measures

---

## Start Here: The Question of the Day
**"I have raw columns like `quantity` and `unit_price` — how do I turn them into real business numbers like Total Sales or Profit Margin?"**

That's exactly what DAX (Data Analysis Expressions) is for. Today you write your first DAX formulas against the same `superstore_sales_sample` data you've used all course.

---

## 1. Recap
Day 2 built the model — tables connected by relationships. Today we start writing formulas on top of that model. DAX is Power BI's formula language, and it's used in two places: **calculated columns** and **measures**.

---

## 2. Calculated Column vs Measure
This is the one distinction to really understand today.

### Calculated Column
- Computed **row by row**, stored in the table, one value per row.
- Example: `Total Line Value = Orders[quantity] * Orders[unit_price]`
- Use when you need a per-row value (e.g., to filter or group by it later).

### Measure
- Computed **on the fly**, based on whatever is currently filtered/grouped in a report (a chart, a card, a table).
- Example: `Total Sales = SUM(Orders[Total Line Value])`
- Use for anything that should summarize a set of rows — totals, averages, ratios.

> **Analogy:** A calculated column is like writing a note on every single receipt. A measure is like the total your calculator shows once you've added up whichever receipts are currently in your hand.

Most of the numbers you'll want on a dashboard (Total Sales, Total Profit, Average Order Value) are **measures**, not calculated columns — because they need to change depending on what's filtered (a region, a date range, a category).

---

## 3. Basic DAX Syntax
DAX formulas look like this:

```
Total Sales = SUM(Orders[Total Line Value])
Order Count = COUNTROWS(Orders)
Average Order Value = DIVIDE([Total Sales], [Order Count])
```

Notice: a measure can reference another measure (`[Total Sales]`), which keeps formulas simple and reusable instead of repeating logic everywhere.

---

## 4. One Sentence
> **A calculated column adds a value to every row; a measure calculates a summary value based on whatever's currently filtered on the report.**

---

## 5. Quick Self-Check
1. What's the core difference between a calculated column and a measure?
2. Why are most dashboard KPIs built as measures rather than calculated columns?
3. What does `DIVIDE()` do that a plain `/` might not handle safely?