# Week 3, Day 5 — Concepts
## Explaining What You Built

---

## Question of the Day
**"Can I explain, simply, what I just spent a week learning?"**

No new technical concept today. In a real job, building something is only half the work — the other half is explaining it clearly to someone who wasn't there (a manager, a teammate, an interviewer). Today you practice that.

---

## 1. Quick Recap of the Whole Week
Before building your slides, refresh yourself on the five things you learned this week:

| Day | Idea | One-line summary |
|-----|------|-------------------|
| 1 | Batch vs. Streaming | Batch waits for data to pile up; streaming reacts as it arrives |
| 1 | Topic, Producer, Consumer, Broker | A producer sends events into a topic (on a broker); a consumer reads them out |
| 2 | Producing | You wrote a script that sent rows from a CSV into a Kafka topic, one at a time |
| 3 | Consuming with `readStream` | Databricks connected to your topic and read the stream live, turning raw bytes into real columns |
| 4 | Windowed Aggregation | Grouped rows into 1-minute time buckets and summed Sales inside each — same idea as `GROUP BY`, just by time |

That table is basically your whole presentation outline already.

---

## 2. Why Canva, and Why Simple Slides?
The goal isn't a fancy design — it's **clarity**. A good technical summary slide has:
- One main idea per slide (don't cram 3 concepts onto 1 slide)
- Short phrases, not paragraphs
- A simple visual or diagram where possible (even a basic 3-box arrow diagram helps more than a wall of text)

If someone can understand your slide in 10 seconds without you explaining it out loud, it's a good slide.

---

## 3. What Success Looks Like Today
By the end of Day 5, you should have a short Canva presentation (5–6 slides) that:
- Explains what Kafka is, in plain language
- Explains the 4 core terms (topic, producer, consumer, broker)
- Shows what you personally built each day this week
- Ends with what you found most interesting or surprising

This is something you can genuinely show a manager or put in a portfolio — "I don't just know Kafka exists, I built a live pipeline and can explain it."