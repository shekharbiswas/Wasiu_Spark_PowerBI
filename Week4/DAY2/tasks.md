# Week 4, Day 2 — Tasks (6 Hrs)

Read today's Concepts doc first, then answer the questions below in your own words (a sentence or two each).

---

## Part 1 — Relationships
1. What goes wrong if two related tables are loaded into Power BI but no relationship is created between them?
  - If there is no relationship, Power BI cannot correctly connect the data between the tables. This can lead to wrong numbers, filters not working properly, and      misleading reports.
    
2. In the `Orders` / `Products` example, which column would you use to connect the two tables?
  - You would use the Product ID column to connect the Orders and Products tables
---

## Part 2 — Star Schema
3. In your own words, what is a fact table?
  - A fact table stores the main events or transactions in a business, such as orders or sales, along with the numbers you want to analyse.
    
4. In your own words, what is a dimension table?
  - A dimension table stores descriptive information about things like customers, products, or locations, which helps you understand and filter the data in a fact table.

5. For our `Orders`, `Products`, `Customers` setup — which one is the fact table, and which are the dimension tables?
  - **Fact table:** `Orders`
    **Dimension tables:** `Products` and `Customers`

---

## Part 3 — Putting It Together
6. Fill in the blank from memory:
   *"A star schema is a ___fact_ table in the middle with __dimension__ tables around it."*

7. How does building a relationship in Power BI relate to writing a `JOIN` in Spark SQL back in Week 2?
  - Both **connect related tables using a common column**, such as `ProductID`. A Power BI relationship is similar to a Spark SQL `JOIN` because it tells the          system how the tables are connected so the data can be analysed together.

---

## End-of-Day Checklist
- [ ] I've answered all 7 questions in my own words
- [ ] I can explain, without looking, what a relationship and a star schema are
