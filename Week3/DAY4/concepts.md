# Week 3, Day 4 — Concepts
## Summarizing Data That Never Stops

---

## Question of the Day
**"How do I summarize data that never stops arriving?"**

Today has **one single new idea**. Everything else you already know from Weeks 1–2 and Day 3. Take it slow — re-read a section twice if you need to, that's completely fine.

---

## 1. Quick Reminder: Something You Already Know
Back in Week 1, you learned `GROUP BY` — putting rows into buckets and summarizing each bucket. For example: group orders by Region, then sum the Sales in each Region.

**Today is the exact same idea. Just one thing changes: instead of grouping by Region, we group by time.**

That's it. That's the whole new concept. The rest of this page just explains that one sentence slowly.

---

## 2. The Problem: A Stream Never "Ends"
With a normal CSV, you know exactly when the data stops — it's the last row of the file. You can safely say "add up ALL the Sales" because there's a clear finish line.

A stream has no finish line. It just keeps going. So the question "what's the total Sales?" doesn't really make sense anymore — total *so far*? Total *ever*? It keeps changing every second.

**The fix:** instead of asking for one giant total, we chop time into small, equal-sized chunks — like 1-minute buckets — and ask "what's the total *inside each bucket*?" Each bucket has a clear start and end, even though the stream itself doesn't.

> **Analogy:** Imagine counting cars driving past your window. You can't ever say "the total number of cars" — cars keep coming. But you *can* say "12 cars passed between 3:00 and 3:01," and then start a fresh count for 3:01 to 3:02. Each minute is its own bucket.

---

## 3. This Bucket Has a Name: a "Window"
In Spark, one of these time-buckets is called a **window**. A window just means: "a fixed slice of time, like 1 minute or 5 minutes, that we group rows into based on when they arrived."

So instead of:
```
GROUP BY Region
```
today you'll write something closer to:
```
GROUP BY (1-minute time window)
```

Same `GROUP BY` idea. The bucket is just made of time instead of a category.

---

## 4. What You'll Actually Calculate Today
Just one simple thing: **total Sales per 1-minute window.**

As new rows keep arriving, Spark keeps updating the current window's total, live, right in front of you. When a minute ends, a new window starts fresh.

---

## 5. What Success Looks Like Today
By the end of Day 4, you should be able to:
- Explain, in one sentence, what a "window" is (a time-based bucket, same idea as grouping by Region, just by time instead)
- Watch a live total update in front of you as new rows keep arriving
- See one window "close" and a new one begin

Tomorrow (Day 5) is the last day — you'll put everything from this whole week together into one small pipeline, start to finish.