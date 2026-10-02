# Week 3, Day 3 — Tasks ( 6 Hrs )
## Read Your Stream Into Databricks



Today you'll connect Databricks to the **same topic and cluster you built yesterday**. Keep your Day 2 notes handy — you'll need your bootstrap server, API key, and API secret again.

Make sure your `producer.py` script from Day 2 is running (or re-run it) so there's actually something to read while you work.

---

## Task 1 — Start a New Notebook
1. Open Databricks and create a new notebook.
2. Name it `Day3_Kafka_Consumer`.
3. Set the language to **Python**.

---

## Task 2 — Reconnect to Your Kafka Cluster
In the first cell, fill in your own values from Day 2:

```python
BOOTSTRAP_SERVERS = "YOUR_CLUSTER_BOOTSTRAP_SERVER"
API_KEY = "YOUR_API_KEY"
API_SECRET = "YOUR_API_SECRET"
TOPIC_NAME = "sample_data_orders"
```

**Write down:** where did you find each of these values again? (You looked them up yesterday — note where, so you remember for next time.)

---

## Task 3 — Read the Raw Stream
In the next cell, connect to Kafka using `readStream`:

```python
raw_stream_df = (
    spark.readStream
    .format("kafka")
    .option("kafka.bootstrap.servers", BOOTSTRAP_SERVERS)
    .option("kafka.security.protocol", "SASL_SSL")
    .option("kafka.sasl.mechanism", "PLAIN")
    .option(
        "kafka.sasl.jaas.config",
        f'org.apache.kafka.common.security.plain.PlainLoginModule required username="{API_KEY}" password="{API_SECRET}";'
    )
    .option("subscribe", TOPIC_NAME)
    .option("startingOffsets", "earliest")
    .load()
)
```

Run this cell. It should run without error — but you won't see any data yet, because you haven't displayed it.

---

## Task 4 — Look at the Raw Shape First
Before parsing anything, just look at what Kafka hands you by default:

```python
display(raw_stream_df.selectExpr("CAST(value AS STRING) as raw_value"))
```

Run this cell and watch it for 15–20 seconds.

**Write down:** what does one raw row look like? Does it look like readable data, or does it need more work to become usable?

Stop this cell before moving on (click the cell's **Cancel** button — streaming cells run until you stop them).

---

## Task 5 — Define the Schema
Now tell Spark what columns to expect, matching the CSV columns from Week 1. Adjust the field names below if your CSV's column headers are different:

```python
from pyspark.sql.types import StructType, StringType, DoubleType

order_schema = (
    StructType()
    .add("Order ID", StringType())
    .add("Product Name", StringType())
    .add("Sales", StringType())
    .add("Quantity", StringType())
    .add("Region", StringType())
)
```

*(Keep every field as `StringType()` for now — we'll worry about proper number types later in the week. The goal today is just seeing structured columns instead of raw text.)*
<img width="1015" height="656" alt="image" src="https://github.com/user-attachments/assets/a71bd189-ee69-49c2-8f9b-130487cad3e7" />
<img width="1033" height="550" alt="image" src="https://github.com/user-attachments/assets/98685cdf-9635-4b0f-b94c-9d608f1c3099" />

---

## Task 6 — Parse the Stream Into Real Columns
```python
from pyspark.sql.functions import from_json, col

parsed_df = (
    raw_stream_df
    .selectExpr("CAST(value AS STRING) as json_value")
    .select(from_json(col("json_value"), order_schema).alias("data"))
    .select("data.*")
)
```

---

## Task 7 — Watch It Live
```python
display(parsed_df)
```

Run this cell and watch for 30 seconds to a minute.
<img width="1015" height="645" alt="image" src="https://github.com/user-attachments/assets/368905da-6b20-46ab-8892-89291e4d6803" />

**Write down:** now that the data is parsed, does it look like a table you'd recognize from Week 1? What's the same, and what feels different about watching it "live" versus loading a CSV all at once?

Stop the cell when you're done watching.

---

## End-of-Day Checklist
- [ ] I connected a Databricks notebook to my own Kafka topic from Day 2
- [ ] I looked at the raw, unparsed stream first
- [ ] I defined a schema and parsed the stream into real columns
- [ ] I watched live, structured rows appear inside Databricks using `display()`
