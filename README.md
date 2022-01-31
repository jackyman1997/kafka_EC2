# kafka on EC2
I try to run a kafka server/broker on a free-tier EC2. Here is some records on the technical difficulties I was facing. 

# kafka basic
data in -> producers -> brokers -> consumers -> data out   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;^  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;zookeeper  

And watch [this](https://www.youtube.com/watch?v=B5j3uNBH8X4) and [this 3-hr tutorial](https://www.youtube.com/watch?v=CU44hKLMg7k) for more.

# Procedure 
Here are the steps I made. 
## JAVA 1.8
```
sudo apt-get install openjdk-8-jdk
```
check version: (it should be 1.8)
```
java -version
```

## download confluent (kafka)
```
curl -O http://packages.confluent.io/archive/5.0/confluent-oss-5.0.1-2.11.zip
```
unzip: 
```
unzip confluent-oss-5.0.1-2.11.zip
```
if `unzip` is not installed: 
```
sudo apt install unzip
```
here is an extra step from random online source, I dunno what this is for: 
```
export KAFKA_HEAP_OPTS="-Xmx8G -Xms8G"
```

## locate essential files 
all exacutables are stored at `~/confluent-5.0.1/bin`: 
```
ls ~/confluent-5.0.1/bin/
```
and the corresponding configs are at `~/confluent-5.0.1/etc/kafka`:  
```
ls ~/confluent-5.0.1/etc/kafka/
```
logs are at `~/confluent-5.0.1/logs`, if you have run something (ie errors encountered)

## start zookeeper with config
basically `{exacutable} {config file}`: 
```
~/confluent-5.0.1/bin/zookeeper-server-start ~/confluent-5.0.1/etc/kafka/zookeeper.properties
```

## start brokers with config
```
~/confluent-5.0.1/bin/kafka-server-start ~/confluent-5.0.1/etc/kafka/server.properties
```
so here is where i got memory issues, simply my EC2 doesn't have enough memory to run JVM/JDK for kafka. See logs folder for more. 
