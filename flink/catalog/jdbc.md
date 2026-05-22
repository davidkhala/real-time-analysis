# JDBC Catalog
```
CREATE CATALOG my_jdbc WITH (
  'type'='jdbc',
  'default-database'='public',
  'username'='...',
  'password'='...',
  'base-url'='jdbc:postgresql://...'
);
```