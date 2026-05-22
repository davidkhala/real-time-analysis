# watermark
- Watermark are calculated from the largest event time that has been seen so far
- Watermark 的本质是event time的进度指示器(像blockchain的lastest block，但是没有timeout机制，只看 count）
  - 告诉 Flink watermark之前的数据已经到齐(finality), 可以安全地关闭窗口，触发时间相关计算
  - Event‑time windows cannot close until all partitions’ watermarks advance past the window boundary.
  - The operator’s global watermark = the minimum of all subtasks’ watermarks.
- watermark = 当前已看到的最大事件时间（max event time）减去允许的延迟（lateness）
  - max event time: 它不是最新到达的事件，而是事件时间字段（event timestamp）里最大的值。
  - lateness: aka. 乱序容忍, out-of-orderness, default to 0
In Flink, event‑time windows close only when the operator’s watermark advances past the window end.
- Batch processing does not need a mechanism like watermark because of not having out‑of‑order issue
