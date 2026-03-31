---
date: 2026-03-30
title: Generating  Realistic Test Data for Database Benchmarks
layout: post
tags: [systems, testing, data, AI]
---

**Part 1 of a series: MongoDB vs. PostgreSQL for Audit Logs**

---

I recently had a frustrating project at the day job. I'll spare you the backstory... But while we were dealing with a very slow-running clean-up script, a hypothesis formed:


> how much faster would a SQL database be for a bulk update like this?


And so I set out to try it! A bake off!

This was really a scaling problem. Even a few thousand records would not be a real test. I thought that generating the data would be a great job for ChatGPT (or any of its LLM/Generative-AI cousins). Instead, ChatGPT walked me through creating my own "amplification" pipeline.

The basic flow is:

1. Create some representative data.
2. Configure how many of each example (ChatGPT called them "seeds") to generate.
3. Copy the data but change a few key elements to get some variety. (I changed timestamps and some plain text strings.)

That's basically it. The rest of this post is details. In "part 2" I'll explain the actual test case.

---

## Create Some Representative Data
I started out saying, "realistic" data... but perhaps "representative" is more accurate. As long as the basic structure was the same as it was at the day job, then my test code would encounter the same data-structure bottlenecks. I also wanted to make sure that identical records wouldn't skew the test by triggering caching or some other low-level optimization that I didn't know about.

### The Data Model

The use case I was modeling was an **audit log** — a record of every change made to an entity over time. Think of it like a Git history for your data: who changed what, and what did it used to be?

Each document is a self-contained entity record with its full event history embedded. Here's one of the smaller seed records, lightly truncated:

```json
{
  "id": "Yy1kFXizQ56rc9ynfWYsRw==",
  "entityId": "VOsouqE/TS2DDDnxe9wiSw==",
  "entityType": "Model",
  "version": 1,
  "createdAt": "2024-06-17T12:01:00+00:00",
  "updatedAt": "2024-06-17T12:12:00+00:00",
  "events": [
    {
      "operation": "updateValue",
      "timestamp": "2024-06-17T12:00:00+00:00",
      "key": "model.name",
      "oldValue": null,
      "newValue": "Example Model"
    },
    {
      "operation": "statusUpdate",
      "operationSubtype": "ModelSourceSynced",
      "timestamp": "2024-06-17T12:10:00+00:00",
      "key": "sources[0].syncStatus",
      "newValue": "success"
    },
    {
      "operation": "updateValue",
      "timestamp": "2024-06-18T12:00:00+00:00",
      "key": "model.description",
      "oldValue": "This is an example model created for testing purposes.",
      "newValue": "This is an updated description for the example model."
    }
    // ... 4 more events
  ]
}
```

A few things worth noting about this structure. First, it's document-native: the entity and all its history travel together as one object. Second, the event schema has a deliberate asymmetry — `updateValue` events have both `oldValue` and `newValue`, while `statusUpdate` events only carry `newValue`. That's realistic; a sync status update doesn't have a meaningful "before" value. Third, some `oldValue` fields are `null`, representing the initial setting of a field that didn't previously exist.

I started with what I'd call a "properties bag" — a loose structure that felt natural to write but would have been a nightmare to query. After some reflection I landed on this normalized shape, where each event captures a single field change: what changed (`key`), when (`timestamp`), and the before and after values. Simple, stable, queryable.

The document-native structure is also what makes the relational mapping non-trivial — but that's a problem for Part 2.

---

## Start With Seed Records

Rather than generating thousands of random records immediately, I start with a small set of **seed records** — hand-crafted documents that represent realistic examples of the data.

I came up with four seeds. Each one represents an "entity" (in this case, software models and use cases in a catalog) that has accumulated a history of changes. The events on each seed capture the kinds of field changes you'd actually see: name updates, description edits, status transitions, deployment environment changes.

## Let an AI Agent Help — But Verify

Once I had the first seed record looking right, I used the Copilot agent in my IDE to update the other three seeds to follow the same structure. This worked well — but with an interesting bonus.

The agent didn't just reformat the data. It also flagged inconsistencies I hadn't noticed. Two field names that should have been the same were slightly different: `modelSourceSynced` in one record, `modelSourceSync` in another. Without that catch, those inconsistencies would have propagated into my benchmark data and quietly corrupted my results.

This is worth noting: AI coding assistants aren't just autocomplete. Used as an agent on a structured task like this, they can act as a light code reviewer.

## Write a Check Script

Before scaling up, write a validation script — a unit test for your data. Mine verified things like:

- Every event record has all required fields
- Timestamps are valid ISO 8601 strings
- Field values are the right types
- Event counts per entity are in a reasonable range

Run this against your seed records before generating anything at scale. It costs almost nothing and saves you from running a long benchmark against data that was broken from the start.

---

## Build a Configuration Block

Now that I had some validated seed records, it was time to start sprinkling water on these mogwai. (I mean, replicating the data. You see, "mogwai" were in the movie Gremlins... nevermind.)

ChatGPT insisted that I create a little "config block" and feed it into the "generate" methods. ChatGPT was right. It made it much easier to run and reproduce results.

```python
config1k = {
    'filename': 'generated_records_1k',
    'numbers_by_seed_record': {
        'model_medium1': 400,
        'model_medium2': 100,
        'model_small':   200,
        'use_case_medium': 300
    }
}

config10M = {
    'filename': 'generated_records_10M',
    'numbers_by_seed_record': {
        'model_medium1': 4_000_000,
        'model_medium2': 1_000_000,
        'model_small':   2_000_000,
        'use_case_medium': 3_000_000
    }
}
```

The counts reflect the distribution I'd expect in production: roughly 70% Model entities, 30% UseCases. Scaling up is just swapping one config for another — the generator doesn't change.

---

## Scale It Up!

The generation loop iterates over each seed (example record), creates `N` copies with randomized values, and writes them out in batches to a gzipped JSONL file. The structure stays consistent; the content varies. To paraphrase Missy Elliott: put your thing down, randomize it and repeat it! (Dad! Stop!)

```python
config = config10M
config['filename'] += '.jsonl.gz'

with gzip.open(config['filename'], 'wt', encoding='utf-8') as outfile:
    for seed_record_name, seed_record in sample_entity_records.items():
        num_to_generate = config['numbers_by_seed_record'][seed_record_name]
        total = 0
        batch = []

        while total < num_to_generate:
            batch.append(json.dumps(new_from_sample(seed_record)) + '\n')
            total += 1
            if len(batch) >= BATCH_SIZE:
                outfile.writelines(batch)
                batch.clear()

        if batch:           # flush the final partial batch
            outfile.writelines(batch)
```

> **Full source, seed records, and check script on GitHub →** *(TODO: paste the link here, n8)*

Here's what came out at 1,000 entities:

```
Total records: 1,000
Total events: 11,600
Average events per record: 11.60
Entity type summaries:
   10,100 events over 700 Model records    (14.43 avg per record)
    1,500 events over 300 UseCase records  (5.00 avg per record)
```

Proportions look right. Average event counts are plausible. The check script passed.

Scale to 100,000:

```
Total records: 100,000
Total events: 1,160,000
Average events per record: 11.60
```

The averages held. That's the sign of a healthy generator — the statistical properties scale linearly. (Thanks for the analysis, you generative pre-trained transformer!)

---

## Scaling to 10 Million Records was "fun"!

Scaling to 10 million entities introduced problems I hadn't anticipated at smaller sizes.

**File size.** The raw JSON output was getting big. 100,000 records was, like, 300MB. Nothing like "big data", but I only have so much room on my 8-years-old laptop. I switched to `gzip.open` to write compressed output. JSON usually compresses well. And this was very repetitive data (with some randomly added variety!). The generated data compressed down to something like 1/25 of its original size. And I don't think it slowed things down too much.

**Batch size.** I spent more time than I'd like to admit tuning the batch size for writing records to the output file. Here's a sample of that experimentation:

| Batch size | Records | Total run time |
|------------|---------|----------------|
| 100        | 100k    | 12,848 ms      |
| 1k         | 100k    | 12,786 ms      |
| 8k         | 100k    | 12,595 ms      |
| 50k        | 100k    | 12,694 ms      |

It ended up barely mattering. The spread across all batch sizes was less than 5%. I eventually concluded that speeding up the generation wasn't worth it, and stopped trying to optimize it. Sometimes the best performance tuning decision is knowing when to stop. (Good aphorism, Claude!)

At 10M records, generation was slow but steady: roughly 20,000 records every 4 seconds. With some fluctuation. It ran while I went and did other things.

---

## What You End Up With

By the time you've gone through this process, you have:

1. A small set of hand-crafted, validated seed records that accurately represent your domain
2. A configuration-driven generator that produces statistically consistent data at any scale
3. A check script that verifies the output at every scale
4. Documented generation times so you know what to expect when you need to regenerate

That last point matters more than it sounds. When you're mid-benchmark and you realize you need to regenerate your data with a slightly different schema, you'll want to know whether that's a five-minute task or a two-hour one.

---

## Up Next: The Bake-Off

With 10 million realistic audit records in hand, I loaded them into MongoDB and PostgreSQL and ran the same operations against both.

The results surprised me — in both directions.

---

**Part 2: MongoDB vs. PostgreSQL for Audit Logs — What the Numbers Actually Showed** →
