当 key 不一致时，Flink 会插入一个昂贵的内部算子，并插入：
- Changelog Normalize
- Upsert Materialization
- Keyed Deduplication
