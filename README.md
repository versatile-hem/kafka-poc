# kafka-poc


# Kafka insallation 
## Install java
## Install standalone zookeeper


### Step 1 : Download zookeeper from the below URL.
https://zookeeper.apache.org/releases.html



### Step 2 : unzip jar

tar -zxf zookeeper-3.4.6.tar.gz 

mv zookeeper-3.4.6 /usr/local/zookeeper 

mkdir -p /var/lib/zookeeper 

### Step 3 : configure zookeeper for standalone

cat > /usr/local/zookeeper/conf/zoo.cfg << EOF
> tickTime=2000
> dataDir=/var/lib/zookeeper
> clientPort=2181
> EOF # export JAVA_HOME=/usr/java/jdk1.8.0_51 


### Step 4 : Start zookeeper

/usr/local/zookeeper/bin/zkServer.sh start
 

## Install Zookeeper ensemble 


tickTime=2000 
dataDir=/var/lib/zookeeper 
clientPort=2181 
initLimit=20 
syncLimit=5 
server.1=zoo1.example.com:2888:3888 
server.2=zoo2.example.com:2888:3888 
server.3=zoo3.example.com:2888:3888

First Things First


In this configuration, the initLimit is the amount of time to allow followers to connect with a leader. The syncLimit value limits how out-of-sync followers can be with the leader. Both values are a number of tickTime units, which makes the initLimit 20 * 2000 ms, or 40 seconds. The configuration also lists each server in the ensemble. The servers are specified in the format 


**server.X**=hostname:peerPort:leaderPort, with the following parameters:

The ID number of the server. This must be an integer, but it does not need to be zero-based or sequential.

**hostname** The hostname or IP address of the server.

**peerPort** The TCP port over which servers in the ensemble communicate with each other.

**leaderPort** The TCP port over which leader election is performed.



## Install broker


