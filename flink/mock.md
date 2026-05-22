# [flink-faker](https://github.com/knaufk/flink-faker)
flink-faker is a convenient and powerful mock data generator designed to be used with Flink SQL.

Sample
```
CREATE TABLE `streaming_pageviews` (
  `url` STRING,
  `ts` TIMESTAMP(3)
)
WITH (
  'connector' = 'faker',
  'rows-per-second' = '100',
  'fields.url.expression' = '/#{GreekPhilosopher.name}.html',
  'fields.ts.expression' =  '#{date.past ''5'',''1'',''SECONDS''}'
);
```
- 数据源`'faker'`注册：因为当前运行的 Flink SQL Client 的 lib/ 目录里已经包含了 flink-faker 的 JAR
  - JAR里一定有一个factory类声明
    ```
        @Override
        public String factoryIdentifier() {
            return "faker";
        }
    ```