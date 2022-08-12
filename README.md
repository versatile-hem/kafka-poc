# kafka-poc


# Kafka insallation 
## Install java
## Install standalone zookeeper


### Step 1 : Download zookeeper from the below URL.
https://zookeeper.apache.org/releases.html



### Step 2 : unzip jar

tar -zxf zookeeper-X.X.X.tar.gz 

mv zookeeper-X.X.X /usr/local/zookeeper 

mkdir -p /var/lib/zookeeper 

### Step 3 : configure zookeeper for standalone

vi /usr/local/zookeeper/conf/zoo.cfg  
```
tickTime=2000
dataDir=/var/lib/zookeeper
clientPort=2181
```
export JAVA_HOME=/usr/java/jdk1.8.0_51 


### Step 4 : Start zookeeper

/usr/local/zookeeper/bin/zkServer.sh start
 

## Install Zookeeper ensemble 

```
tickTime=2000 
dataDir=/var/lib/zookeeper 
clientPort=2181 
initLimit=20 
syncLimit=5 
server.1=zoo1.example.com:2888:3888 
server.2=zoo2.example.com:2888:3888 
server.3=zoo3.example.com:2888:3888

```

Brief description for above properties, 
```
**initLimit** is the amount of time to allow followers to connect with a leader. 
**syncLimit** value limits how out-of-sync followers can be with the leader. 
**server.X**=hostname:peerPort:leaderPort, with the following parameters:

**hostname** The hostname or IP address of the server.
**peerPort** The TCP port over which servers in the ensemble communicate with each other.
**leaderPort** The TCP port over which leader election is performed.
```

Both initLimit and syncLimit values are a number of tickTime units, which makes the initLimit 20 * 2000 ms, or 40 seconds. The configuration also lists each server in the ensemble. The servers are specified in the format 
The ID number of the server. This must be an integer, but it does not need to be zero-based or sequential.




## Install broker

### Step 1 : Download kafka broker from the below URL.
[https://zookeeper.apache.org/releases.html](https://kafka.apache.org/downloads.html)


### Step 2 : unzip jar and move broker to local user

tar -zxf zookeeper-X.X.X.tar.gz 

mv kafka_2.X-0.9.0.1 /usr/local/kafka


### Step 3 : configure kafka broker

vi /usr/local/kafka/config/server.properties
```
#The most important thing is that the integer must be unique within a single Kafka cluster.
broker.id=host1.example.com #this integer is set to 0, b

#if a port lower than 1024 is chosen, Kafka must be started as root. Running Kafka as root is not a recommended configuration.
port=8791

zookeeper.connect=localhost:2181

log.dirs=/User/hem/Desktop/kafka/


```

### Step 4 : Start kafka broker

/usr/local/kafka/bin/kafka-server-start.sh -daemon /usr/local/kafka/config/server.properties
 

Create and verify a topic:
```
#/usr/local/kafka/bin/kafka-topics.sh --create --zookeeper localhost:2181

--replication-factor 1 --partitions 1 --topic test Created topic "test".

#/usr/local/kafka/bin/kafka-topics.sh --zookeeper localhost:2181

--describe --topic test Topic:test PartitionCount:1 ReplicationFactor:1 Configs:

Topic: test Partition: 0 Leader: 0 Replicas: 0 Isr: 0 #
```


Produce messages to a test topic:
```
#/usr/local/kafka/bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test Test Message 1 Test Message 2 ^D #

```

Consume messages from a test topic:
```
#/usr/local/kafka/bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic test --from-beginning Test Message 1 Test Message 2 ^C Consumed 2 messages #

```





