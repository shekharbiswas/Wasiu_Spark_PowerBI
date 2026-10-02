# Week 4, Day 3 — Tasks (6 Hrs)
## Hands-On: Your First DAX Formulas

Open Power BI Desktop with `superstore_sales_sample` loaded (from Day 1–2). Work through these in order — each one builds on the last.

---

## Part 1 — Calculated Column
1. Create a calculated column called `Total Line Value`:
   ```
   Total Line Value = Orders[quantity] * Orders[unit_price]
   ```
2. Add it to a Table visual alongside `product_name` and confirm the values look correct for a few rows you can check by hand.

---

## Part 2 — Basic Measures
3. Create a measure for total sales:
   ```
   Total Sales = SUM(Orders[Total Line Value])
   ```
4. Create a measure for order count:
   ```
   Order Count = COUNTROWS(Orders)
   ```
5. Create a measure for average order value, using `DIVIDE`:
   ```
   Average Order Value = DIVIDE([Total Sales], [Order Count])
   ```
6. Drop all three measures onto Card visuals on a blank report page. Confirm the numbers change when you click a filter (e.g., filter by one `category`).

---

## Part 3 — One More on Your Own
7. Using the same pattern, write one more measure of your choosing (e.g., `Total Profit` if a profit column exists, or `Max Order Value` using `MAX()`). Write down the DAX formula you used.
   
<img width="1887" height="797" alt="image" src="https://github.com/user-attachments/assets/c878eff4-32e7-40d4-a92c-5ab196e9a44b" />

---

## Part 4 — Write It Down
8. In one or two sentences: why did the Card visual numbers change when you applied a filter, even though you didn't edit the measure formula?

---

## Part 5 — Challenge: Apply It to a New Dataset

Time to prove you can do this without a walkthrough. Download the **Sample Sales Data** dataset from Kaggle:

🔗 https://www.kaggle.com/datasets/kyanyoga/sample-sales-data

This is a medium-difficulty dataset — not tough, but different enough from `superstore_sales_sample` that you'll have to think, not just copy-paste. It has order-level sales data with quantity, price, product line, deal size, territory, and order dates.

Load it into Power BI Desktop and, on your own, redo the full exercise against this new data:

9. Create a calculated column that computes a line-level total (equivalent of `Total Line Value`), using whatever the quantity and price columns are called here (`QUANTITYORDERED`, `PRICEEACH`).
10. Create the same three core measures — a total sales measure, a count measure, and an average using `DIVIDE` — renamed to fit this dataset (e.g., `Total Sales`, `Order Count`, `Average Order Value`).
11. Build a Card visual page and confirm the numbers respond to a filter — this time filter by `PRODUCTLINE` or `DEALSIZE` instead of `category`.
12. Write **two new measures** that didn't exist in Part 3, exploring columns unique to this dataset — for example:
    - Total sales by `TERRITORY` or `COUNTRY`
    - A measure using `QTR_ID` or `MONTH_ID` (e.g., average sales per quarter)
    - A `DISTINCTCOUNT` of `CUSTOMERNAME` (unique customers)
13. In two or three sentences: what was different about working with this dataset compared to `superstore_sales_sample` (column names, structure, anything that tripped you up)?

---

## End-of-Day Checklist
- [ ] I created one calculated column
- [ ] I created three measures (`Total Sales`, `Order Count`, `Average Order Value`)
- [ ] I confirmed the measures respond to filters
- [ ] I wrote one measure of my own and can explain what it does
- [ ] I loaded the Kaggle Sample Sales Data dataset and rebuilt the calculated column + three measures on it
- [ ] I wrote two new measures exploring columns unique to the new dataset
- [ ] I noted what was different about working with the new dataset
