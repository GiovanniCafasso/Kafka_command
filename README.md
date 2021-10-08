# Kafka Commands

## Start the Zookeper service
```bash
bin/zookeeper-server-start.sh config/zookeeper.properties
```

## Start kafka broker service
```bash
bin/kafka-server-start.sh config/server.properties
```

## Create a Topic
```bash
bin/kafka-topics.sh --create --topic quickstart-events --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1
```

## Write on Topic
```bash
bin/kafka-console-producer.sh --topic quickstart-events --bootstrap-server localhost:9092
```

## Read from Topic
```bash
bin/kafka-console-consumer.sh --topic quickstart-events --from-beginning --bootstrap-server localhost:9092
```
