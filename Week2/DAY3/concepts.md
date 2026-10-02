# Week 2 — Day 3: Concepts
## Derived Columns — "Making the Data Answer Questions It Was Never Asked"

---

## Recap of Week 2 Day 1 & 2 (10 min)
Before starting anything new, quickly repeat out loud:
1. What's the difference between INNER JOIN and LEFT JOIN?
2. What new table did we create yesterday? (`superstore_sales_joined`)
3. What column did we join the two tables on? (`Category`)

---

## Today Is a Bit Different — Today You Become a Rule-Maker
So far, every column we've worked with already existed in the data — we selected it, filtered it, summed it, joined it. **Today, for the first time, you create a column that didn't exist before, out of nothing but logic.**

**Key line to repeat to student:** *"Today, you stop being someone who just reads data — you become someone who teaches the data new tricks. You're going to write a business rule, and Spark will apply it to every single row automatically."*

This is genuinely one of the more fun days — because the output feels like magic the first time you see it: one query, and suddenly 412 rows all get labeled correctly, instantly, without you touching a single row by hand.

---

## Why Derived Columns Matter
Raw data almost never comes with the exact labels a business wants. Nobody stores a column called `Is_This_A_High_Value_Order` — but a manager will absolutely ask: *"Which of our orders are high value?"* You have to **create that answer yourself**, using logic based on other columns (like `Sales`).

**Excel comparison:** This is exactly what an `IF()` formula does in Excel — "if this condition is true, show this; otherwise, show that." Spark SQL's version is called `CASE WHEN`, and it can handle far more conditions at once, across thousands (or millions) of rows instantly.

---

## The "Wow" Moment Today
Imagine typing **one single query** and instantly seeing every one of your 412 orders automatically labeled:
- "High Value Order" 💰
- "Standard Order"
- "Low Value Order"

No manual work. No scrolling through Excel checking each row. No copy-pasting formulas down a column one at a time. **One rule, applied everywhere, instantly.** This is the exact moment most students realize why companies pay Data Engineers — this is real, useful automation, not just "typing SQL."

---

## The Core Idea Today: CASE WHEN

`CASE WHEN` lets you say: *"If a condition is true, label it this way. Otherwise, check the next condition. If nothing matches, use a default label."*

**Plain-language structure:**
```
CASE
  WHEN condition_1 THEN 'Label A'
  WHEN condition_2 THEN 'Label B'
  ELSE 'Label C'
END
```

You can build as many conditions as you want, and Spark checks them top to bottom for every single row.

---

## Other Ways to Create Derived Columns Today
Besides `CASE WHEN` (for labels/categories), we can also create derived columns using simple **math on existing columns** — for example, calculating `Profit_Margin` as `Profit ÷ Sales`. This turns two existing numbers into a brand-new business metric that didn't exist in the raw data at all.

---

## Key Terms Introduced Today
| Term | Plain-Language Meaning |
|------|--------------------------|
| Derived column | A new column created from logic or math applied to existing columns |
| `CASE WHEN` | A rule-based way to label rows based on conditions (like Excel's `IF`) |
| `ELSE` | The default label used when no condition matches |
| Calculated field | A new numeric column built from math on existing columns (e.g. Profit ÷ Sales) |

---

## What Success Looks Like Today
By the end of today, the student should be able to say, in their own words:
1. What a derived column is, and why raw data usually doesn't have the exact labels a business needs
2. How `CASE WHEN` works, using the Excel `IF()` comparison
3. How to build a simple calculated field using math on two existing columns

**Closing line for the day:** *"Today you didn't just read data — you taught it something new. Every future report built on this table will automatically know which orders are high value, without anyone ever checking manually again. Tomorrow, we save this kind of work permanently — learning how a pipeline hands its output off to the next stage."*