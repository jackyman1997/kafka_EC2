# JAVA 1.8
```
sudo apt-get install openjdk-8-jdk
```
check version: (it should be 1.8)
```
java -version
```

# download confluent (kafka)
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

# locate essential files 
all exacutables are stored at `~/confluent-5.0.1/bin`: 
```
ls ~/confluent-5.0.1/bin/
```
and the corresponding configs are at `~/confluent-5.0.1/etc/kafka`:  
```
ls ~/confluent-5.0.1/etc/kafka/
```
logs are at `~/confluent-5.0.1/logs`, if you have run something (ie errors encountered)

# start zookeeper with config
basically `{exacutable} {config file}`: 
```
~/confluent-5.0.1/bin/zookeeper-server-start ~/confluent-5.0.1/etc/kafka/zookeeper.properties
```

# start brokers with config
```
~/confluent-5.0.1/bin/kafka-server-start ~/confluent-5.0.1/etc/kafka/server.properties
```