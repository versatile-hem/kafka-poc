# kafka-poc


# Kafka insallation 
## Install java
## Install standalone zookeeper


### Step 1 : Download zookeeper from the below URL.
http://bit.ly/2sDWSgJ


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



## Install broker


