---
date: 2026-04-13
title: Cleaning Up a Crufty Dataset in MongoDB vs. PostgreSQL
layout: post
tags: [systems, testing, data, performance]
---

**Continuing with Part 2 of my series on evaluating MongoDB vs PostgreSQL for this particular workload**

(Is it really "a series" if it just has two parts?)

---

In Part 1 I told of my adventures generating data to match the shape of a recent problem at my day job: "Audit Records" for "Entities". So, each entity would have a handful of "changes" or "events" added to it as the entity lived its life in the system.

I was testing my script on about 2 million records from the internal QA instance of our application. The customers who needed the cleanup had up to 10 million records. At the day job, the entities were **Models** (AI or otherwise) being managed by this application.

As I was testing our script on the QA data set, I had a strong hunch that updating a couple million records wouldn't make a traditional SQL database break a sweat. But here in this MongoDB / AWS Document DB it was taking hours and hours!

Both approaches are perfectly valid across a variety of scenarios. There are plenty of articles describing when each approach might be a better fit. I believe that MongoDB was selected here for the flexibility it provides in a changing environment. No schema migrations needed!

# The Test
I wanted to be a Professional Cloud Practitioner and run all this stuff on someone else's infrastructure. It would be a valid test because differences in database instances would be baked in to production workloads. But it was simpler and more consistent to run everything locally. So, I just installed some Docker images on my trusty 2018 MacBook Pro.

(2018 means it's an Intel machine, boys and girls! It was pretty hefty back then: i9 with 32GB of RAM!)

For each entity type we listed out several "change paths" or "event keys" that we were going to delete (keeping any changes not found on the list). I wanted to enhance my data-generation script to include more paths with more indexed segments, but I don't think that would have changed the results.

In MongoDB we stored each **entity** as a document, with an array of **updates** as a property. In PostgreSQL, we split it into two tables: **entities** and **entity_updates** with each **entity_update** having a reference to its parent **entity**.

## Execution
### 1,000
I generated a thousand records and loaded them into the databases. **A thousand!** That's 1x10^3. Can you believe it!!? I verified the cleanup script by running it, and both completed in a few milliseconds. I didn't realize it at the time, but the performance difference was already showing. My Mongo script took about 450ms to run the clean job while the Postgres script only took 35ms. But what's a couple hundred milliseconds between friends?

### Generating more data
I ran my data-generation script for 1k, 10k, 100k, 1M, 3M, and 10M records.
But I ended up skipping the tests on 10k and 100k. 

### Results
The relative performance ended up staying about the same through 1M, 3M, and 10M records.

<table>
  <thead>
    <tr>
      <th rowspan="2">Records</th>
      <th colspan="2">MongoDB seconds</th>
      <th colspan="2">PostgreSQL seconds</th>
    </tr>
    <tr>
      <th>Load</th>
      <th>Clean</th>
      <th>Load</th>
      <th>Clean</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>1M</td><td>117</td><td>488</td><td>638</td><td>105</td></tr>
    <tr><td>3M</td><td>189</td><td>2,400</td><td>2,382</td><td>326</td></tr>
    <tr><td>10M</td><td>638</td><td>5,679</td><td>5,906</td><td>2,993</td></tr>
  </tbody>
</table>
    
> ### A Note
> I realized that I had failed to create any indexes ("indices" :smirk:). So I re-ran the 3M records after adding an index for `entity_type` in Mongo and `entity_type` on the `entities` table and `entity_id` on the `entity_updates` table.
> Those are the numbers included in the results for 3M records.

> ### Another Note
> It seems like PostgreSQL might have hit some performance threshold for the 10M-record mark. If this was more important I'd want to run a few more tests. At least run the 10M test a few times, maybe run 5M, 8M, 12M, 20M just to see...
    
## Conclusion
So, yes, the cleanup phase was much, much faster for the SQL tables.

But, the load time for the SQL tables reveals the bottleneck: iterating over each entity's list of events. For Postgres, I had to do it at load time. In Mongo, I didn't iterate over the events until cleanup time.

In this test, the differences pretty much balanced out: loading Postgres took about as long as cleaning Mongo. Tests with tighter controls and better data might tip the scales one way or the other.

But in the real-life case, there wasn't any "load" of millions of records. The application logged each change as it happened. I think this would actually favor the SQL design more because updating a record to write one event would probably be slower than adding one event to the `event_updates` table. But, in those cases, both databases would be more than fast enough.

Also, this cleanup workload was a one-time task. So, even if a traditional SQL database would have performed faster in each case, MongoDB was well within functional requirements. And if the schema for the entity records changed very much before I arrived on the team, then the Mongo choice makes even more sense.

So, the moral of the story is: I WAS RIGHT!!! MONGO SUCKS! RDBMS FOREVER, SUCKERS!

LOL. No. The traditional database _was_ faster _in this case_. At the day job, it didn't matter. We were running a one-time cleanup job on data that was already in MongoDB and DocumentDB.

If we were having a design discussion about which option to choose... maybe this case's performance would have been relevant. Maybe. But the slower load time suggests that the real bottleneck was the script iterating over each entity's list of events. In MongoDB, I had to pay that cost during the cleanup. In PostgreSQL, I paid it while setting up the test. I traded it off. **Tradeoffs**. It's always tradeoffs.

![Gilda Radner as Roseanne Roseannadanna telling Jane Curtin, "It's always something!"]({{ site.url }}/assets/ItsAlwaysSomething.gif){: .photo }
