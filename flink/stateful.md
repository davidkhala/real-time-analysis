stateful operations
- `GROUP BY`
- `WINDOW`
- `JOIN`
- `AGGREGATE`

Key-partitioned
- aka. keyBy shuffle, hash partitioning
- 同一个 key 的所有事件必须被发送到同一个subtask处理。
- 
