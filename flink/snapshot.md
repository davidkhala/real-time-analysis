
Flink implement a variant of Chandy-Lamport distributed snapshot algo

- Flink provides exactly-once guarantees in certain scenarios
  - *SQL Query Result* in SQL Client as Sink
  - [cookbook: exactly-once sink to kafka](https://github.com/confluentinc/flink-cookbook/blob/master/kafka-exactly-once/README.md)
- Recovery involves **restarting the entire cluster** from the latest snapshot
  
# checkpoint

automatic snapshot

- created by Flink for failure recovery
- 它通过 异步快照（Asynchronous Snapshots） 把以下内容保存下来：
  - 算子状态（Operator State）
  - 键控状态（Keyed State）
  - 偏移量（source offsets）
  - 水位线（watermarks）
- based on barrier alignment protocol

## Configure

`set 'execution.checkpointing.interval' = '1000';`

# savepoint

manual snapshot
