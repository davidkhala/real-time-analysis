# Hive Catalog
- 最常用的持久化 Catalog

```
CREATE CATALOG my_hive WITH (
  'type'='hive',
  'default-database'='default',
  'hive-conf-dir'='/path/to/hive/conf'
);

USE CATALOG my_hive;
CREATE TABLE t (...) WITH (...);
```