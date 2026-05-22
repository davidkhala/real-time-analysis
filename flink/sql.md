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

[Catalog types](./catalog/)

## Streaming mode
- switch to by `SET 'execution.runtime-mode' = 'streaming';`
- order by time (only): cannot order by other vars
- provide special optimized join (with temporal table | with external lookup table)

### changelog (result mode)
In `changelog` mode, the SQL Client doesn't just update the count in place, but instead displays each message in the stream of updates it's receiving from the Flink SQL runtime.
- switch to by `SET 'sql-client.execution.result-mode' = 'changelog';`
- You cannot have changelog mode in batch mode
  - ```
    [ERROR] Could not execute SQL statement. 
    Reason: org.apache.flink.table.client.gateway.SqlExecutionException: Results of batch queries can only be served in table or tableau mode.
    ```

## Batch mode
- switch to by `SET 'execution.runtime-mode' = 'batch'`


## table (result mode)
- the default display mode
- switch to by `SET 'sql-client.execution.result-mode' = 'table';`

## Flink SQL Client CLI
https://nightlies.apache.org/flink/flink-docs-stable/docs/dev/table/sqlclient/
