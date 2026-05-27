Materializing: dangerously stateful

- regular `GROUP BY`
- regular `JOIN`

Temporal: safely stateful

- time-windowed aggregation
  - [windowing](./windowing.md)
- internal joins
- time-versioned joins
- [pattern matching](./MATCH_RECOGNIZE.md)
  

Key-partitioned

- aka. keyBy shuffle, hash partitioning
- 同一个 key 的所有事件必须被发送到同一个subtask处理。

