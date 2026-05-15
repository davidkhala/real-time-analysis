# Flink SQL
Conforms to the ANSI SQL
- Alternative access to Table API

Is Flink SQL a database? No. Bring your own data
- The table object is only a metadata describing the schema and connection
- Rows can be updated or deleted
  - `-U`: Update Before: Retract an earlier result: 抵消上一个insert/update （归零）
  - `+U`: Update After: Update an earlier result: 插入值= `-U`值 + delta in current update
  - `-D`: Delete an earlier result
  - `+I`: Insertion: always insert from select

## Streaming mode
- order by time (only): cannot order by other vars
- provide special optimized join (with temporal table | with external lookup table) 

## Flink SQL Client CLI
https://nightlies.apache.org/flink/flink-docs-stable/docs/dev/table/sqlclient/
