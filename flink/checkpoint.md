# checkpoint
for point-of-time recovery
- 它通过 异步快照（Asynchronous Snapshots） 把以下内容保存下来：
  - 算子状态（Operator State）
  - 键控状态（Keyed State）
  - 偏移量（source offsets）
  - 水位线（watermarks）
- based on barrier alignment protocol
