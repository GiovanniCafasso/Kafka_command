# Kafka Commands

### Start the Zookeper service
```bash
bin/zookeeper-server-start.sh config/zookeeper.properties
```

### Start kafka broker service
```bash
bin/kafka-server-start.sh config/server.properties
```

### Create a Topic
```bash
bin/kafka-topics.sh --create --topic quickstart-events --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1
```

## Write on Topic
```bash
bin/kafka-console-producer.sh --topic quickstart-events --bootstrap-server localhost:9092
```

### Read from Topic
```bash
bin/kafka-console-consumer.sh --topic quickstart-events --from-beginning --bootstrap-server localhost:9092
```

### Get details
```bash
bin/kafka-topics.sh --describe --topic quickstart-events --bootstrap-server localhost:9092
```


# Cluster Multi Node
Example node 2

### Duplicate config.properties 
In config folder duplicate config.properties and set new name (config-2.properties)

### Edit these rows
1. broker.id=0  --> broker.id=2
1. listeners=PLAINTEXT://:9092 --> listeners=PLAINTEXT://:9093
1. log.dirs=/tmp/kafka-logs --> log.dirs=/tmp/kafka-logs-2

### Run the new server
```bash
bin/kafka-server-start.sh config/server-2.properties
```

### Set minimal replicas
```bash
bin/kafka-configs.sh --bootstrap-server localhost:9092 --entity-type topics --entity-name myTopic --alter --add-config min.insync.replicas=2
```

# Manage cosumer

### Consume messages partition by partition
Specific the correct number of partition (ex: ``` --partition 0``` )
```bash
bin/kafka-console-consumer.sh --topic my-partitioned-topic --from-beginning --partition `<number>` --bootstrap-server localhost:9092
```

### Start multiple consumers in a single group
Run this command as time as you need
```bash
bin/kafka-console-consumer.sh --topic my-partitioned-topic --group my-consumer-group --bootstrap-server localhost:9092
```

### Receive messages from a specific offset of a single partition
Specific the correct number of offset (ex: ``` --offset 1``` )and the correct number of partition (ex: ``` --partition 1``` )
```bash
bin/kafka-console-consumer.sh --topic my-partitioned-topic --offset `<number>` --partition `<number>` --bootstrap-server localhost:9092
```
