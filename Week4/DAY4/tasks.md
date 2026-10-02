# Week 4, Day 4 — Tasks (6 Hrs)
## Practice: Apply Day 3's DAX Concepts to New Questions

Same dataset, same two building blocks (calculated column, measure) — different business questions this time. Try each one yourself first before checking any hints.

---

## Part 1 — Another Calculated Column
1. Create a calculated column called `Discounted Price` (assume a `discount_percent` column exists, or use a flat 10% for practice):
   ```
   Discounted Price = Orders[unit_price] * (1 - 0.10)
   ```

---

## Part 2 — More Measures
2. Create a measure for total quantity sold:
   ```
   Total Quantity = SUM(Orders[quantity])
   ```
3. Create a measure for the number of distinct products sold:
   ```
   Distinct Products = DISTINCTCOUNT(Orders[product_id])
   ```
4. Create a measure for average unit price:
   ```
   Average Unit Price = AVERAGE(Orders[unit_price])
   ```

---

## Part 3 — Combine and Check
5. Put `Total Sales`, `Total Quantity`, and `Distinct Products` on Card visuals on one page. Filter by a single `category` and confirm all three update together.
   <img width="1891" height="787" alt="image" src="https://github.com/user-attachments/assets/ddd2bc64-aa4c-4f35-bd25-5a8ac4c1f7aa" />
   <img width="1896" height="793" alt="image" src="https://github.com/user-attachments/assets/772d11f1-4c45-4dd8-bb43-1fb5ff438433" />

7. Write one new measure of your own choosing (different from Day 3's) using any aggregation function (`SUM`, `AVERAGE`, `MAX`, `MIN`, `COUNTROWS`, `DISTINCTCOUNT`).

---

## Part 4 — Write It Down
7. In one sentence: what's one DAX function you used today that you hadn't used on Day 3?

---

## Part 5 — Challenge: Apply It to the Kaggle Dataset

Use the same **Sample Sales Data** dataset from Day 3's challenge:

🔗 https://www.kaggle.com/datasets/kyanyoga/sample-sales-data

This is a medium-difficulty task — the building blocks are the same, but you have to figure out which columns to use yourself. On your own, rebuild today's exercise against this dataset:

8. Create a calculated column equivalent to `Discounted Price` using `PRICEEACH` — apply a flat 10% discount.
9. Create a measure for total quantity sold, using `QUANTITYORDERED` instead of `quantity`.
10. Create a measure for the number of distinct products sold, using `PRODUCTCODE` instead of `product_id`.
11. Create a measure for average unit price, using `PRICEEACH`.
12. Put all three new measures plus `Total Sales` from Day 3 on Card visuals on one page. Filter by `PRODUCTLINE` and confirm all four update together.
13. Write **two new measures** exploring angles you haven't covered yet, for example:
    - `MAX(Orders[PRICEEACH])` — highest unit price sold
    - `DISTINCTCOUNT(Orders[CUSTOMERNAME])` — unique customers
    - Total quantity sold filtered to a single `DEALSIZE`
14. In one or two sentences: did any DAX function behave differently on this dataset than you expected (e.g., because of a different column type or missing values)?

---

## End-of-Day Checklist
- [ ] I created one new calculated column
- [ ] I created three new measures
- [ ] I confirmed the measures respond correctly to a filter
- [ ] I wrote one measure entirely on my own
- [ ] I rebuilt the calculated column + three measures on the Kaggle Sample Sales Data dataset
- [ ] I wrote two new measures exploring new angles on the Kaggle dataset
- [ ] I noted anything that behaved differently on the new dataset
