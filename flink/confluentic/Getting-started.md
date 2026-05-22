
# Getting started with Apache Flink SQL on Kafka in Docker
- [source](https://developer.confluent.io/courses/apache-flink/docker-setup/)

bootstrap
```
git clone https://github.com/confluentinc/learn-apache-flink-101-exercises.git
cd learn-apache-flink-101-exercises
podman compose up --build -d
# wait for ready
```

to start the Flink SQL Client CLI
```
podman compose run sql-client
```
