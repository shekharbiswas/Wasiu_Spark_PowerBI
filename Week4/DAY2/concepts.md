# Week 4, Day 2 — Concepts
## Data Modeling in Power BI: Relationships & Star Schema Basics

---

## Start Here: The Question of the Day
**"I've loaded two tables into Power BI — why won't they just work together?"**

Loading data isn't enough. Power BI needs to be told how tables relate to each other, or it treats them as two unconnected islands. Today is about that one missing piece.

---

## 1. Recap
Yesterday we learned the three-stage model: **Get Data → Model → Report**. Today is entirely about the **Model** stage — the part that should feel familiar from the joins you wrote in Spark SQL back in Week 2.

---

## 2. Why Relationships Matter
Say you have two tables:
- `Orders` (order_id, product_id, quantity, order_date)
- `Products` (product_id, product_name, category)

Without a relationship, Power BI has no idea `product_id` in one table means the same thing as `product_id` in the other. You'd never be able to build a chart like "sales by category" — the two tables just sit there, disconnected.

A **relationship** tells Power BI: "these two tables connect on this column." Once that's set, you can pull fields from both tables into the same chart as if they were one.

> **Analogy:** Two tables without a relationship are like two people in a room who don't speak the same language. A relationship is the interpreter that lets them work together.

---

## 3. Star Schema — The Basic Shape
Most Power BI models follow a simple pattern called a **star schema**:

- One **fact table** in the middle — the thing that happened. In our case, `Orders` (each row = one sale event).
- Several **dimension tables** around it — the things that describe the event. In our case, `Products`, `Customers`, `Dates`.

The fact table is usually big and numeric (quantities, amounts). Dimension tables are usually small and descriptive (names, categories, regions). Drawn out, the fact table sits in the middle with lines going out to each dimension table — hence "star."

This is the same relationship thinking behind the joins in Week 2 — just drawn as a picture instead of written as `JOIN ... ON`.

---

## 4. One Sentence
> **A relationship connects two tables on a shared column, and a star schema is just a fact table in the middle with dimension tables around it.**

---

## 5. Quick Self-Check
1. What problem does a relationship solve?
2. In a star schema, what's the difference between a fact table and a dimension table?
3. Which Week 2 skill does this remind you of?