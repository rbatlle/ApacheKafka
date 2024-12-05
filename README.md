# Apache Kafka - MQ Broker

### Docker Compose Setup for 3 Brokers

```
networks:
  frontend:
    driver: bridge

services:
  zookeeper:
    image: confluentinc/cp-zookeeper:7.5.0
    container_name: zookeeper
    environment:
      ZOOKEEPER_CLIENT_PORT: 2181
      ZOOKEEPER_TICK_TIME: 2000
    networks:
      - frontend
    ports:
      - "192.168.254.128:2181:2181"

  kafka1:
    image: confluentinc/cp-kafka:7.5.0
    container_name: kafka1
    depends_on:
      - zookeeper
    environment:
      KAFKA_BROKER_ID: 1
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://192.168.254.128:9092
      KAFKA_LISTENERS: PLAINTEXT://0.0.0.0:9092
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 3
    networks:
      - frontend
    ports:
      - "192.168.254.128:9092:9092"

  kafka2:
    image: confluentinc/cp-kafka:7.5.0
    container_name: kafka2
    depends_on:
      - zookeeper
    environment:
      KAFKA_BROKER_ID: 2
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://192.168.254.128:9093
      KAFKA_LISTENERS: PLAINTEXT://0.0.0.0:9093
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 3
    networks:
      - frontend
    ports:
      - "192.168.254.128:9093:9093"

  kafka3:
    image: confluentinc/cp-kafka:7.5.0
    container_name: kafka3
    depends_on:
      - zookeeper
    environment:
      KAFKA_BROKER_ID: 3
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://192.168.254.128:9094
      KAFKA_LISTENERS: PLAINTEXT://0.0.0.0:9094
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 3
    networks:
      - frontend
    ports:
      - "192.168.254.128:9094:9094"

  kafka-ui:
    image: provectuslabs/kafka-ui:latest
    container_name: kafka-web
    depends_on:
      - kafka1
      - kafka2
      - kafka3
    environment:
      KAFKA_CLUSTERS_0_NAME: kafka-cluster
      KAFKA_CLUSTERS_0_BOOTSTRAPSERVERS: 192.168.254.128:9092,192.168.254.128:9093,192.168.254.128:9094
    networks:
      - frontend
    ports:
      - "192.168.254.128:8080:8080"
networks:
  frontend:
    driver: bridge
```



