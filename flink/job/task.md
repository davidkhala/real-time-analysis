![](https://images.ctfassets.net/gt6dp23g0g38/1lGTq8q6BOUYm114R4104R/6156dfa231a563c21c0c4142a678c300/jobgraph-in-webui.png)
This job graph shows a processing pipeline with two stages, called *tasks*. Each task in a Flink job consists of one or more operators that are directly connected, or *chained* together, and in each parallel instance (or *subtask*), those chained operators run in the same thread.
- example of operator: `GroupAggregate`, `ConstraintEnforcer` and `Sink`
- these metrics only report internal network communication happening within Flink
  - the source task will not report on traffic from an external service into Flink,
  - A sink task will not report on communication from Flink to the outside world.



# Subtask


## backpressure (metric)
Within each subtask, *backpressure* is reported as the percentage of time that the subtask was unable to send output downstream because the downstream subtask had fallen behind, and (temporarily) couldn't receive any more records.

## busy (metric)
The *busy* metric reported by each subtask is the percentage of time spent doing useful work (as opposed to being either idle or backpressured).
- In general, tasks that are always busy are a concern