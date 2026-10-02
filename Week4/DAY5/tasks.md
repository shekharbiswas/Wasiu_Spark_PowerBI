# Week 4, Day 5 — Tasks (6 Hrs)
## Mini Project: Berlin Sales Dashboard

Build one finished report page using everything from this week. Keep it simple — this is a wrap-up, not new material.

---

## Build Checklist
1. Load `superstore_sales_sample.csv` (or your Day 2 tables) into Power BI.
2. Confirm your relationships/model from Day 2 are still working.
3. Add these measures if you don't already have them:
   - `Total Sales`
   - `Total Profit`
   - `Order Count`
4. Build one report page with:
   - A **map or filled map** visual using `city` / `region` (Berlin districts)
   - A **line chart** of `Total Sales` by `order_date` (month)
   - A **bar chart** of `Total Sales` by `category`
   - **Card** visuals for `Total Sales`, `Total Profit`, `Order Count`
5. Add one slicer (e.g., `region` or `segment`) and confirm everything updates together when you click it.

---

## Write It Down (Short)
6. In 2–3 sentences: which part of this dashboard came from data engineering (Weeks 1–3), and which part is new this week?

---

## Part 5 — Final Challenge: Rebuild It on the Kaggle Dataset

This is the medium-hard part of the project. Using the **Sample Sales Data** dataset from Day 3/4:

🔗 https://www.kaggle.com/datasets/kyanyoga/sample-sales-data

Rebuild the same dashboard — on your own, without a column-by-column mapping given to you this time:

7. Load the Kaggle dataset and set it up the way you set up `superstore_sales_sample` on Day 2.
8. Recreate `Total Sales`, `Total Profit` (or a stand-in if no profit column exists — e.g., `Total Sales` minus `MSRP`-based cost), and `Order Count`.
9. Build one report page with:
   - A **map or filled map** visual using `COUNTRY` / `TERRITORY`
   - A **line chart** of `Total Sales` by `ORDERDATE` (month)
   - A **bar chart** of `Total Sales` by `PRODUCTLINE`
   - **Card** visuals for your three measures
10. Add one slicer (e.g., `DEALSIZE` or `TERRITORY`) and confirm everything updates together.
11. In 2–3 sentences: what did you have to figure out yourself this time that was handed to you on Day 3/4?

---

## Deliverable — Due Monday, 9:30 AM

Submit **both** of the following:
- A **PDF export** of your finished Kaggle-dataset dashboard page (Part 5)
- A short **presentation** (slides) walking through your dashboard: what it shows, the measures you built, and one insight you found in the data

Be ready to present live at 9:30 AM Monday.

---

## End-of-Day Checklist
- [ ] Dashboard has a map, a line chart, a bar chart, and 3 cards
- [ ] One slicer works across all visuals
- [ ] I can point to this and say "I built this"
- [ ] I rebuilt the full dashboard on the Kaggle Sample Sales Data dataset
- [ ] I exported the Kaggle dashboard as a PDF
- [ ] I have a short presentation ready to walk through it
- [ ] Both are ready to submit/present Monday at 9:30 AM