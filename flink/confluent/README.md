Confluent Cloud for Apache Flink is a serverless offering
- Details about the Job Managers and Task Managers are not exposed.

Confluent Flink Shell
- 不支持任何 result-mode 配置
- 不支持unbounded streaming queries，只能跑批 (Bounded SELECT)
    - 否则result fetcher 超时
- 可以跑 DDL（CREATE/DROP/ALTER
- 可以SHOW / DESCRIBE / EXPLAIN
- 可以 INSERT INTO（流式写入）
