# Week 4, Day 1 — Tasks (6 Hrs)
## Concept Questions (Write Your Answers)

Today has **no building in Power BI yet**. Read today's Concepts doc first, then write short answers (a sentence or two each) to the questions below, in your own words. This is just to make sure the core ideas have actually landed before opening Power BI Desktop tomorrow.

---

## Part 1 — Spreadsheets vs Reports
1. What is the difference between handing someone a raw spreadsheet and handing them a Power BI report?
  - A raw spreadsheet gives you the data and requires you to analyse it yourself.
  - A Power BI report turns that data into interactive visuals, KPIs, and insights for easier decision-making.

2. Why can emailing a CSV around a team cause problems over time?
  - Because different people may edit or save different versions, causing duplicate, outdated, or inconsistent data over time.
  - It also makes it harder to know which CSV is the latest and most accurate version.

3. Give one real-world example (other than the ones in the Concepts doc) where you think a dashboard would work better than a raw data export.
  - Example: A hospital could use a dashboard to monitor patient waiting times, bed availability, and emergency department activity in real time, rather than          relying on a raw data export that staff would have to analyse manually.
---

## Part 2 — The Power BI Mental Model
4. In your own words, what happens during the **Get Data** stage?
  - During the Get Data stage, you connect to and import data from different sources (such as Excel files, databases, or online services) so it can be used for        analysis in Power BI.
    
5. What is the **Model** stage for, and how does it relate to the joins you wrote in Spark SQL in Week 2?
  - The Model stage is used to connect and organise different tables so they work together. It is similar to the joins in Spark SQL, where you link tables using       common columns such as customer or product IDs.
    
6. What is the **Report** stage, and why is it the only stage most people in a company actually see?
  - The Report stage is where data is turned into charts, visuals, and dashboards. It is what most employees see because they use it to understand the data and         make decisions, without needing to see the underlying data or technical work.
    
7. If the data model is set up wrong (e.g., a relationship joins on the wrong column), what do you think happens to the report built on top of it?
  - If the data model is wrong, the report can show incorrect numbers and misleading charts. Filters and calculations may also give wrong results because the          tables are connected incorrectly.
---

## Part 3 — Putting It Together
8. Fill in the blanks from memory:
   *"Power BI connects to already-engineered data (___data warehouse_ ____), models the _relationships___ between tables, and _visualises___ the result as something a decision-maker can read in seconds."*

9. Why does Power BI have no way of knowing whether the data engineering work behind it was done correctly?
  - Because Power BI only works with the data it receives. It doesn’t automatically know whether the data was cleaned, transformed, or joined correctly upstream,      so incorrect data can still produce misleading reports.

10. Explain the Get Data → Model → Report flow in 2–3 sentences to someone who has never heard of Power BI, using any analogy you like (kitchen, grocery shopping, or your own).
  - Think of Power BI like a kitchen: Get Data is bringing in the ingredients, Model is organising and preparing them, and Report is serving the finished meal.        The final report gives decision-makers an easy-to-understand view of the information without needing to see all the work behind it.

---

## End-of-Day Checklist
- [ ] I've written answers to all 10 questions in my own words
- [ ] I can say, without looking, the one-sentence model: *"Power BI connects to already-engineered data, models the relationships between its tables, and reports the result as something a decision-maker can read in seconds."*
