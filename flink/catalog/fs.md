# Filesystem Catalog

CREATE CATALOG my_fs WITH (
  'type'='filesystem',
  'default-database'='default',
  'warehouse'='file:///tmp/catalog'
);
