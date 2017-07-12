挂载普通磁盘 ROOT 用户

```
fdisk -l 
fdisk /dev/vdc 对数据盘进行分区。根据提示，依次输入 n，p，1，两次回车，wq，分区就开始了。
fdisk -l 
mkfs.ext3 /dev/vdc1
echo /dev/vdc1 /kafka ext3 defaults 0 0 >> /etc/fstab
cat /etc/fstab
mkdir /kafka
mount /dev/vdc1 /kafka
df -h
```

集群：三台机器

```
node06 vpn_ip=10.28.1.1
node07 vpn_ip=10.28.2.2
node08 vpn_ip=10.27.2.3
```

容器：

```
docker pull wurstmeister/kafka:latest
docker pull wurstmeister/zookeeper:latest
```

先配置启动 `zookeeper` 集群（逐个启动）、再启动 `kafka` 集群（逐个启动），三台机器分别配置，目录结构如下：

```
~/kafka-docker

├── zb
│   ├── docker-compose.yml
│   └── zookeeper
│       ├── Dockerfile
│       ├── myid
│       └── zoo.cfg
├── kafka
│   └── docker-compose.yml
```

* 配置 `zb` 的 `docker-compose.yml` ，`KAFKA_ADVERTISED_HOST_NAME: "10.28.1.1"` 的值，分别配置对应 `IP`

```
zookeeper:
  build: ./zookeeper/
  volumes:
    - ./zookeeper/zoo.cfg:/opt/zookeeper-3.4.9/conf/zoo.cfg
    - ./zookeeper/myid:/opt/product/data/myid
  ports:
    - "2182:2181"
    - "2889:2888"
    - "3889:3888"
  restart: always
```

* 配置`zookeeper`  的 `Dockerfile`

```
FROM wurstmeister/zookeeper
RUN echo "Asia/Shanghai" > /etc/timezone
```

* 配置`zookeeper` 的`myid` ，文件内只有一个数字，分别为 `1`、`2`、`3` ，代表 `zookeeper` 的三台服务器

* 配置 `zoo.cfg`,注意 `0.0.0.0:2888:3888` 对应的是 `2888` 和 `3888`

`10.28.1.1`

```
tickTime=2000
initLimit=10
syncLimit=5
dataDir=/opt/product/data/
dataLogDir=/opt/product/data/zkdatalog
clientPort=2181
server.1=0.0.0.0:2888:3888
server.2=10.28.2.2:2889:3889
server.3=10.27.3.3:2889:3889
```

`10.28.2.2`

```
tickTime=2000
initLimit=10
syncLimit=5
dataDir=/opt/product/data/
dataLogDir=/opt/product/data/zkdatalog
clientPort=2182
server.1=10.28.1.1:2889:3889
server.2=0.0.0.0:2888:3888
server.3=10.27.3.3:2889:3889
```

`10.27.3.3`

```
tickTime=2000
initLimit=10
syncLimit=5
dataDir=/opt/product/data/
dataLogDir=/opt/product/data/zkdatalog
clientPort=2182
server.1=10.28.1.1:2889:3889
server.2=10.28.2.2:2889:3889
server.3=0.0.0.0:2888:3888
```

配置 `kafka` 的 `docker-compose.yml`

```
kafka:
  image: wurstmeister/kafka
  ports:
    - "9093:9093"
  environment:
    KAFKA_ADVERTISED_HOST_NAME: "10.28.1.1"
    KAFKA_ADVERTISED_PORT: "9093"
    KAFKA_PORT: "9093"
    KAFKA_ZOOKEEPER_CONNECT: "10.28.1.1:2182,10.28.2.2:2182,10.27.3.3:2182"
    KAFKA_MESSAGE_MAX_BYTES: 2000000
    KAFKA_LOG_ROLL_HOURS: 24
    KAFKA_LOG_RETENTION_HOURS: 72
  restart: always
  volumes:
    - /kafka/kafka/:/kafka/
```

分别启动容器：

`sudo docker-compose up -d`

---

Logtash 配置

```
input {
        kafka {
            bootstrap_servers => "10.28.1.1:9093,10.28.2.2:9093,10.27.3.3:9093"
            topics => ["weibo"]
            auto_offset_reset => "earliest"
            codec => "json"
            group_id => "weibo_group_1"
        }
      }  
```

Web Server 配置

```
    <!-- 生产者配置 -->  
    <bean id="template" class="org.springframework.kafka.core.KafkaTemplate">  
        <constructor-arg index="0">  
            <bean class="org.springframework.kafka.core.DefaultKafkaProducerFactory">  
                <constructor-arg>  
                    <map>  
                        <entry key="bootstrap.servers" value="10.28.1.1:9093,10.28.2.2:9093,10.27.2.2:9093"/>  
                        <entry key="acks" value="all"/>  
                        <entry key="retries" value="3"/>  
                        <entry key="batch.size" value="14000"/>  
                        <entry key="linger.ms" value="1"/>  
                        <entry key="buffer.memory" value="33554432"/> 
                        <!-- <entry key="max.block.ms" value="2000"/>    -->
                        <entry key="key.serializer" value="org.apache.kafka.common.serialization.StringSerializer"></entry>  
                        <entry key="value.serializer" value="org.apache.kafka.common.serialization.StringSerializer"></entry>  
                    </map>  
                </constructor-arg>  
            </bean>  
        </constructor-arg>  
        <property name="producerListener" ref="producerListener"/>
    </bean>  
```



