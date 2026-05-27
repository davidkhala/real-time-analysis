
# windowing
windowing requires
- an input table that is append-only
- a designated timestamp column (*time attribute*) with timestamps that are known to be advancing

[*time attribute*](https://nightlies.apache.org/flink/flink-docs-stable/docs/dev/table/concepts/time_attributes/) can be either
- [event time](./time.md#event-time)
  - In general, the use of event time is to be preferred
- [processing time](./time.md#processing-time)


# window functions
[learning video(confluent)](https://developer.confluent.io/courses/flink-sql/window-aggregations/)

`TUMBLE()`

`HOP()`

`CUMULATE()`

`SESSIONS()`
