# Zookeeper Cluster Install

## 创建用户

```bash
# on node1 node2 node3
groupadd appuser
useradd appuser -g appuser -d /app
chmod 755 /app
```

## 检查JDK

```bash
# on node1 node2 node2
# test java
java 
java -version
```

## 安装

```bash
# on node1 node2 node3
su - appuser
export zk_version=3.8.3
wget https://archive.apache.org/dist/zookeeper/zookeeper-${zk_version}/apache-zookeeper-${zk_version}-bin.tar.gz

tar zxf apache-zookeeper-${zk_version}-bin.tar.gz -C ${os_home}/${install_folder} --strip=1

```

## 配置

**创建自定义配置文件**

```bash
# on node1 node2 node3
cd /app/zookeeper/
mkdir data
mkdir logs
export zk_client_port=2181
export data_dir=/app/zookeeper/data
export logs_dir=/app/zookeeper/logs
vim /app/zookeeper/conf/zoo.cfg
```

**添加配置文件内容**

```bash
# on node1 node2 node3 
cat >> /app/zookeeper/conf/zoo.cfg << EOF
admin.serverPort=8888
tickTime=2000
initLimit=10
syncLimit=5
dataDir=${data_dir}
dataLogDir=${logs_dir}
clientPort=${zk_client_port}
server.1=192.168.0.1:2888:3888
server.2=192.168.0.2:2888:3888
server.3=192.168.0.3:2888:3888
4lw.commands.whitelist=*
# by inRemark
EOF
```

## 启动
```bash
# on node1 node2 node3
/app/zookeeper/bin/zkServer.sh start
```

## 验证

```bash
ps -ef |grep zookeeper
```

## 配置开机启动

```bash
echo "/app/zookeeper/bin/zkServer.sh start" >> /etc/rc.local
```

## 配置文件说明

* `admin.serverPort`：zookeeper的管理端口
* `tickTime`：zookeeper中使用的时间单元，以毫秒为单位
* `initLimit`：zookeeper启动时，集群中的follower节点与leader节点之间初始化连接时限制
* `syncLimit`：zookeeper启动时，follower节点与leader节点之间的同步限制
* `dataDir`：zookeeper存储数据的目录
* `dataLogDir`：zookeeper存储日志的目录
* `clientPort`：zookeeper监听客户端连接的端口
* 


## 参考

1. [官方文档](https://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_zkMulitServerSetup)

## 附录

- [Zookeeper FAQ](zookeeper-faq.md)
- [Kafka Standalone Install](kafka-install.md)
- [Kafka Cluster Install](kafka-cluster-install.md)
