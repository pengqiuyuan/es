Logstash 使用了[容器](https://hub.docker.com/_/logstash/)

停止、删除容器

```
sudo docker-compose stop
sudo docker-compose rm
```

**第一步**

```
#修改 docker-compose.yml，挂载 logstash.yml，logstash.yml 需要新增的三行

xpack.monitoring.elasticsearch.url: ["http://127.0.0.1:9222"]  
xpack.monitoring.elasticsearch.username: "用户名"
xpack.monitoring.elasticsearch.password: "密码"

# docker-compose.yml

logstash:
    build: ./opt/logstash/
    volumes:
      - ./opt/logstash/index.conf:/opt/logstash/conf/index.conf
      - ./opt/logstash/logstash.yml:/etc/logstash/logstash.yml
    command: -f /opt/logstash/conf/index.conf -b 600 -w 6
    restart: always
logstash_kejizixun:
    build: ./opt/logstash/
    volumes:
      - ./opt/logstash/index_kejizixun.conf:/opt/logstash/conf/index.conf
      - ./opt/logstash/logstash.yml:/etc/logstash/logstash.yml
    command: -f /opt/logstash/conf/index.conf -b 600 -w 6
    restart: always
```

**第二步**

```
index.conf 与 index_kejizixun.conf output es 添加

user => '用户名'
password => '密码'
```

**第三步**

```
#修改 Dockerfile

FROM logstash:5.4.0
ADD x-pack-5.4.0.zip /x-pack-5.4.0.zip
RUN logstash-plugin install file:///x-pack-5.4.0.zip
```

**第四步**

```
#启动

sudo docker-compose build
sudo docker-compose up -d
```



