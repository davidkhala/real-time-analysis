# `confluent-flink-quickstart` on confluent Cloud

- [source](https://developer.confluent.io/courses/apache-flink/cloud-setup/)

1. install plugin and login

    - `confluent plugin install confluent-flink-quickstart`
    - `confluent login --save`

2. provision

    ```
    confluent flink quickstart \
        --name flink101 \
        --max-cfu 10 \
        --region us-central1 \
        --cloud gcp
    ```

    - `confluent flink quickstart` 不能复用现有的环境
    - you can come back later by `confluent flink shell`
3. Run in Confluent Flink Shell

    ```
        EXPLAIN
        SELECT
            orders.`$rowtime`,
            orders.price,
            customers.postcode
        FROM examples.marketplace.orders
        JOIN examples.marketplace.customers
        FOR SYSTEM_TIME AS OF orders.`$rowtime`
        ON orders.customer_id = customers.customer_id;
    ```

4. Go to Confluent Cloud Console, then into a SQL Workspace
5. query in a SQL Workspace

    ```
    EXPLAIN
    SELECT
        orders.`$rowtime`,
        orders.price,
        customers.postcode
    FROM examples.marketplace.orders
    JOIN examples.marketplace.customers
    FOR SYSTEM_TIME AS OF orders.`$rowtime`
    ON orders.customer_id = customers.customer_id;
    ```
