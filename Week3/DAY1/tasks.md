# Week 3, Day 1 — Tasks (6 Hrs)
## Concept Questions (Write Your Answers)



[![Watch the video](https://img.youtube.com/vi/vHbvbwSEYGo/0.jpg)](https://www.youtube.com/watch?v=vHbvbwSEYGo)

Today has **no coding**. Read today's Concepts doc first, then write short answers (a sentence or two each) to the questions below, in your own words. This is just to make sure the core ideas have actually landed before we start building anything tomorrow.


---

## Part 1 — Batch vs Streaming
1. What is the difference between batch processing and streaming?
**The main difference is when the data gets processed:**

- Batch processing: collects data over a period of time and processes it all at once.
  Example: Processing all of yesterday’s sales every night.
- Streaming: processes data continuously as it arrives, usually with very little delay.
  Example: Updating a dashboard whenever a new sale happens.
3. Why doesn't "just query the database every 5 seconds" work well when a lot of data is arriving quickly
### Because polling every 5 seconds can be slow, expensive, and inefficient when data arrives continuously.

**For example:**, if 10,000 records arrive in those 5 seconds, the database has to handle a large query repeatedly—and you may still have delays between queries. Streaming lets new data be processed as it arrives, rather than repeatedly checking whether anything new has appeared.
3. Give one real-world example (other than the ones in the Concepts doc) where you think streaming would be used instead of batch.
### One real-world example is fraud detection for credit-card transactions. Streaming can analyze each transaction as it happens and immediately flag suspicious       activity, rather than waiting for a batch of transactions to be processed later.
---

## Part 2 — Kafka Core Concepts
4. In your own words, what is a **topic** in Kafka?
### A topic in Kafka is like a named channel or category where messages are stored. Producers send messages to a topic, and consumers subscribe to that topic to       read the messages they’re interested in.

**For example:**, you might have separate topics for new-orders and new-signups.

5. What is the difference between a **producer** and a **consumer**?
### A producer sends or publishes messages to a topic, while a consumer reads or receives those messages.
**For example:**, imagine a restaurant:
- Producer: the kitchen puts new orders onto a ticket board.
- Consumer: a waiter reads the tickets and acts on them.
6. What does the **broker** do?
### A broker is an intermediary who connects two parties and helps arrange a transaction.
**For example:**
- Stock broker: buys and sells investments on your behalf.
- Real-estate broker: connects buyers and sellers and helps negotiate/property transactions.
- Insurance broker: helps you find and arrange insurance from different insurers.
- Business broker: helps buyers and sellers complete the sale of a business.
In simple terms: the broker stands between the buyer and seller, facilitates the deal, and usually earns a commission or fee.
   
7. If a company wanted to track "new orders" and "new sign-ups" separately, would that be one topic or two? Why?
They would be two separate topics.
- “New orders” is one topic because it represents order-related events.
- “New sign-ups” is another topic because it represents user-registration events.
  
The reason is that a topic should represent a distinct type of event or message that subscribers may want to receive independently.
For example, a service interested only in new orders could subscribe to the orders topic without receiving sign-up events. This keeps the system loosely coupled and avoids sending irrelevant messages to subscribers.
---

## Part 3 — Putting It Together
8. Fill in the blanks from memory:
   *"A producer sends ___messages___ into a __topic____, and a __consumer____ reads them out."*
9. Where does Databricks fit into this picture — is it acting as a producer, a consumer, or the broker?
- Databricks can be either a producer or a consumer, depending on what it’s doing—it’s not usually the broker.
10. Explain Kafka in 2–3 sentences to someone who has never heard of it, using any analogy you like (mailbox, group chat, or your own).
- Think of Kafka like a shared mailbox for a company: producers drop messages into labeled mailboxes (topics), and consumers can read those messages when they       need them. Kafka keeps the messages organized and available so multiple consumers can independently read and process them.
---

## End-of-Day Checklist
- [ ] I've written answers to all 10 questions in my own words
- [ ] I can say, without looking, the one-sentence model: *"A producer sends events into a topic, sitting on a broker, and a consumer reads those events out — in real time, as they happen."*
