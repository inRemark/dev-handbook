# Kafka Cluster Install

## 创建用户

```bash
# on node1 node2 node3
groupadd appuser
useradd appuser -g appuser -d /app
chmod 755 /app
```

## 检查JDK

```bash
# on node1 node2 node3
java -version
```

## 安装

```bash
# on node1 node2 node3
su - appuser
export scale_version=2.13
export kafka_version=3.5.2

wget https://archive.apache.org/dist/kafka/${kafka_version}/kafka_${scale_version}-${kafka_version}.tgzkafka_${scale_version}-${kafka_version}.tgz

tar zxf kafka_${scale_version}-${kafka_version}.tgz -C /app/kafka --strip=1

```

## 自定义配置文件

```bash
# on node1 node2 node3
cd /app/kafka/
mkdir kafka-logs
export kafka_logs_dir=/app/kafka/kafka-logs
```

**创建自定义配置文件**
```bash
# on node1 node2 node3
export kafka_ip=192.168.0.1
export kafka_port=9092
export zk_connect="192.168.0.1:2181,192.168.0.2:2181,192.168.0.3:2181"
vim /app/kafka/config/kafkaServer.properties
```

**添加内容并保存**

```bash
# on node1
broker.id=1
port=${kafka_port}
listeners=PLAINTEXT://${kafka_ip}:${kafka_port}
advertised.listeners=PLAINTEXT://${kafka_ip}:${kafka_port}
num.network.threads=3
num.io.threads=8
socket.send.buffer.bytes=102400
socket.receive.buffer.bytes=102400
socket.request.max.bytes=104857600
log.dirs=${kafka_logs_dir}
num.partitions=1
num.recovery.threads.per.data.dir=1
offsets.topic.replication.factor=1
transaction.state.log.replication.factor=1
transaction.state.log.min.isr=1
log.retention.hours=168
log.segment.bytes=1073741824
log.retention.check.interval.ms=300000
group.initial.rebalance.delay.ms=0
# by inRemark
```

```bash
# on node2
broker.id=2
port=${kafka_port}
listeners=PLAINTEXT://${kafka_ip}:${kafka_port}
advertised.listeners=PLAINTEXT://${kafka_ip}:${kafka_port}
num.network.threads=3
num.io.threads=8
socket.send.buffer.bytes=102400
socket.receive.buffer.bytes=102400
socket.request.max.bytes=104857600
log.dirs=${kafka_logs_dir}
num.partitions=1
num.recovery.threads.per.data.dir=1
offsets.topic.replication.factor=1
transaction.state.log.replication.factor=1
transaction.state.log.min.isr=1
log.retention.hours=168
log.segment.bytes=1073741824
log.retention.check.interval.ms=300000
group.initial.rebalance.delay.ms=0
# by inRemark
```

```bash
# node3
broker.id=3
port=${kafka_port}
listeners=PLAINTEXT://${kafka_ip}:${kafka_port}
advertised.listeners=PLAINTEXT://${kafka_ip}:${kafka_port}
num.network.threads=3
num.io.threads=8
socket.send.buffer.bytes=102400
socket.receive.buffer.bytes=102400
socket.request.max.bytes=104857600
log.dirs=${kafka_logs_dir}
num.partitions=1
num.recovery.threads.per.data.dir=1
offsets.topic.replication.factor=1
transaction.state.log.replication.factor=1
transaction.state.log.min.isr=1
log.retention.hours=168
log.segment.bytes=1073741824
log.retention.check.interval.ms=300000
group.initial.rebalance.delay.ms=0
zookeeper.connection.timeout.ms=18000
zookeeper.connect=${zk_connect}
# by inRemark
```

## 启动

```bash
# on node1 node2 node3
/app/kafka/bin/kafka-server-start.sh -daemon /app/kafka/config/kafkaServer.properties
```
