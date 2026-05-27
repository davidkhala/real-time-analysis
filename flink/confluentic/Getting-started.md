
# Getting started with Apache Flink SQL on Kafka in Docker
- [source](https://developer.confluent.io/courses/apache-flink/docker-setup/)

bootstrap
```
git clone https://github.com/confluentinc/learn-apache-flink-101-exercises.git
cd learn-apache-flink-101-exercises
podman compose up --build -d
# wait for ready
```

To start the Flink SQL Client CLI
```
podman compose run sql-client
```

To view topics
```
podman compose exec -it kcat kcat -b broker:9092 -L
```

## `faker` connector

```
CREATE TABLE `pageviews` (
  `url` STRING,
  `user_id` STRING,
  `browser` STRING,
  `ts` TIMESTAMP(3),
  WATERMARK FOR `ts` AS ts - INTERVAL '5' SECOND
)
WITH (
  'connector' = 'faker',
  'rows-per-second' = '100',
  'fields.url.expression' = '/#{GreekPhilosopher.name}.html',
  'fields.user_id.expression' = '#{numerify ''user_##''}',
  'fields.browser.expression' = '#{Options.option ''chrome'', ''firefox'', ''safari'')}',
  'fields.ts.expression' =  '#{date.past ''5'',''1'',''SECONDS''}'
);
```

unbound query
```
SELECT
  browser,
  count(1) as cnt
FROM pageviews
GROUP BY browser;
```

TUMBLE
```
SELECT
  window_start, count(1) AS cnt
FROM TABLE(
  TUMBLE(DATA => TABLE pageviews, 
         TIMECOL => DESCRIPTOR(ts),
         SIZE => INTERVAL '1' SECOND))
GROUP BY window_start, window_end;
```

pattern matching
```
SELECT *
FROM pageviews
    MATCH_RECOGNIZE (
      PARTITION BY user_id
      ORDER BY ts
      MEASURES
        A.browser AS browser1,
        B.browser AS browser2,
        A.ts AS ts1,
        B.ts AS ts2
      PATTERN (A B) WITHIN INTERVAL '1' SECOND
      DEFINE
        A AS true,
        B AS B.browser <> A.browser
    );
```
- This pattern will match any two events A and B (for the same user_id), where B comes immediately after A (and within one second), and the two events used different browsers 

## `kafka` connector
Create table: At this point, the topic won't have been created.
```
CREATE TABLE json_table (
    `key` STRING,
    `value` STRING
) WITH (
    'connector' = 'kafka',
    'topic' = 'append',
    'properties.bootstrap.servers' = 'broker:9092',
    'format' = 'json',
    'scan.startup.mode' = 'earliest-offset'
);
```

Run Flink SQL to write topic into it
- the topic will be created because the broker defaults with `auto.create.topics.enable=true`
```
INSERT INTO json_table VALUES ('foo','one'), ('foo', 'two');
```

Read the data by `SELECT * FROM json_table;`

## `upsert-kafka` connector
the `upsert-kafka` connector interprets the topic as an updating stream
- upsert based on the table's primary key.

```
CREATE TABLE updating_table (
    `key` STRING PRIMARY KEY NOT ENFORCED,
    `value` STRING
) WITH (
    'connector' = 'upsert-kafka',
    'topic' = 'update',
    'properties.bootstrap.servers' = 'broker:9092',
    'key.format' = 'json',
    'value.format' = 'json'
);

INSERT INTO updating_table VALUES ('foo','one'), ('foo', 'two');

SELECT * FROM updating_table;
```