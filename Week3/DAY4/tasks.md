# Week 3, Day 4 — Tasks ( 6 Hrs )
## Watch a Live Total Update

Today builds directly on Day 3. Keep your Day 2 producer script running, and reuse your same Databricks setup from Day 3 — nothing new to create today.

Go slowly. Every code block below, just copy it in exactly as shown and run it — you don't need to change anything except where marked.

---

## Task 1 — Open Yesterday's Notebook

1. Open your `Day3_Kafka_Consumer` notebook from yesterday.
2. Save a copy of it as `Day4_Windowed_Aggregation` (so you don't lose yesterday's work).
3. Run every cell below, top to bottom, so your stream is connected and `parsed_df` exists.

```python
BOOTSTRAP_SERVERS = "YOUR_CLUSTER_BOOTSTRAP_SERVER"
API_KEY = "KVSN226VZUCGXMIE"
API_SECRET = "cfltd8VtX2TS0PpyY58UcLetDr6KlxFQQMQna9fI1gjwbJ0Lo4vLgBejm2U4w2Gg"
TOPIC_NAME = "sample_data_orders"

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

from pyspark.sql.types import StructType, StringType

order_schema = (
    StructType()
    .add("Order ID", StringType())
    .add("Product Name", StringType())
    .add("Sales", StringType())
    .add("Quantity", StringType())
    .add("Region", StringType())
)

from pyspark.sql.functions import from_json, col

parsed_df = (
    raw_stream_df
    .selectExpr("CAST(value AS STRING) as json_value")
    .select(from_json(col("json_value"), order_schema).alias("data"))
    .select("data.*")
)
```

> Don't run `display()` here — just build `parsed_df`. No need to watch the raw stream again today.

**Fill in:** your `BOOTSTRAP_SERVERS` value from your Confluent Cloud cluster settings page.

---

## Task 2 — Fix the Sales Column's Type

Yesterday we kept every column as text. Today we need `Sales` to actually be a number so we can add it up. Add this new cell:

```python
from pyspark.sql.functions import col

parsed_df = parsed_df.withColumn("Sales", col("Sales").cast("double"))
```

*(This is the same idea as fixing a column's type back in Week 1 — nothing new here, just a reminder step.)*

**Watch for:** if your `sample_data_orders` producer sends `Sales` with a `$` or commas (e.g. `"$1,234.50"`), `cast("double")` will silently return `null` instead of erroring. Try the plain cast above first — only if you see nulls later in Task 5, swap in this version instead:

```python
from pyspark.sql.functions import regexp_replace

parsed_df = parsed_df.withColumn(
    "Sales",
    regexp_replace(col("Sales"), "[$,]", "").cast("double")
)
```

---

## Task 3 — Add a Fake "Arrival Time" Column

Your data doesn't naturally carry a timestamp of when it arrived, so we'll add one using the current time. Add this cell:

```python
from pyspark.sql.functions import current_timestamp

parsed_df = parsed_df.withColumn("event_time", current_timestamp())
```

This just stamps every row with "the moment Databricks saw it" — that's what we'll use to build our time buckets.

---

## Task 4 — Create 1-Minute Windows and Add Up Sales

This is today's one new idea. Copy it exactly:

```python
from pyspark.sql.functions import window, sum

windowed_sales_df = (
    parsed_df
    .groupBy(window(col("event_time"), "1 minute"))
    .agg(sum("Sales").alias("total_sales"))
)
```

Read it out loud once: *"Group the rows into 1-minute windows, and add up Sales inside each window."* That's the entire task.

---

## Task 5 — Watch It Live

```python
display(windowed_sales_df)
```

Run this cell and watch it for **at least 2–3 minutes** — you need to see at least one window finish and a new one begin.

**Watch for:** if your producer is sending records slowly (e.g. one every 10+ seconds), a 1-minute window might only accumulate a handful of rows before closing, so `total_sales` could look like it "jumps" rather than climbs smoothly. If you want a smoother visual, you could temporarily speed up your Day 2 producer's send interval just for this exercise.

**Write down (a sentence or two each):**
1. What columns do you see in the result?
2. Did `total_sales` for the current window change while you watched? What did that feel like compared to a normal, static total?
3. Did you see a new window start? What changed when it did?

Stop the cell when you're done watching (click **Cancel** on the cell).

---

## End-of-Day Checklist

- [ ] I reused my Day 3 stream and fixed the `Sales` column's type
- [ ] I added an `event_time` column
- [ ] I grouped rows into 1-minute windows and summed `Sales`
- [ ] I watched the live total update and saw at least one window change
- [ ] I can say, in one sentence: a window is a time-based bucket, same idea as grouping by a category — just grouped by time instead
