# Mongodb数据源

`mongodb`数据源

使用`mongo-connector`实现`MongoDB`与`elasticsearch`实时同步

`unbuntu16.04` `mongodb3.2.8` 傻瓜搭建流程

* 导入公钥所使用的包管理系统。

```text
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
```

* 创建一个列表文件MongoDB。

```text
echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
```

* 本地更新

```text
sudo apt-get update
```

* 安装

```text
sudo apt-get install -y mongodb-org=3.2.8 mongodb-org-server=3.2.8 mongodb-org-shell=3.2.8 mongodb-org-mongos=3.2.8 mongodb-org-tools=3.2.8
```

* 创建系统服务文件

```text
vim /lib/systemd/system/mongod.service
```

然后输入下面的话

```text
[Unit]
Description=High-performance, schema-free document-oriented database
After=network.target
Documentation=https://docs.mongodb.org/manual

[Service]
User=mongodb
Group=mongodb
ExecStart=/usr/bin/mongod --quiet --config /etc/mongod.conf

[Install]
WantedBy=multi-user.target
```

* 启动

```text
sudo service mongod start
```

远程连接 `mongodb`

```text
mongo --host 127.0.0.0:7777  -u root -p xxxx --authenticationDatabase admin
```

```text
mgset-3056331:PRIMARY> use toutiao
switched to db toutiao
mgset-3056331:PRIMARY> db.toutiaors.find()
{ "_id" : "2973008615", "introduction" : "李磊，山东人在南京，曾经的南航人，现在利安人寿HR。", "follower_count" : "11", "crawled_at" : 1491044224.9921331, "fans_count" : "20", "name" : "擀饼杖", "avatar_img" : "http://tp4.sinaimg.cn/2641718951/50/5664883664/1" }
```

安装 `pip install 'mongo-connector[elastic5]'`

执行

```text
mongo-connector --auto-commit-interval=0 -m 127.0.0.1:3717 -t 127.0.0.1:9222 -a username -p password -d elastic2_doc_manager -n toutiao.toutiaors -g test.test
```

后台执行

```text
nohup mongo-connector --auto-commit-interval=0 -m 127.0.0.1:3717 -t 127.0.0.1:9222 -a username -p password -d elastic2_doc_manager -n toutiao.toutiaors -g test.test &
```

```text
--auto-commit-interval=0 #表示实时同步将mongodb中的修改同步到ES
-m 127.0.0.1:3717 #连接mongodb
-t 127.0.0.1:9222 #连接es
-a username #mongo 用户名
-p password #mongo 密码
-d elastic2_doc_manager 
-n toutiao.toutiaors #mongo里面的db.Collection
-g test.test #写入es的index和type
```

有 xpack 的情况

```text
nohup mongo-connector --auto-commit-interval=0 -m 127.0.0.1:3717 -t 用户名:密码@127.0.0.1:9222 -a username -p password -d elastic2_doc_manager -n toutiao.toutiaors -g test.test &
```

[`mongo-connector` 文档](https://github.com/mongodb-labs/mongo-connector/wiki/Configuration-Options)

`config.json` 模式，`mongo-connector -c toutiao.json`

```text
{
    "mainAddress": "127.0.0.1:3717",
    "authentication": {
          "adminUsername": "用户名",
          "password": "密码"
    },
    "namespaces": {
        "include": ["toutiao.toutiaors"],
        "mapping": {
          "toutiao.toutiaors": "toutiaors.toutiaors"
        }
    },
    "docManagers": [
      {
        "docManager": "elastic2_doc_manager",
        "targetURL": "用户名:密码@node01:9222",
        "autoCommitInterval":0,
        "bulkSize":3000,
        "args": {
          "meta_index_name": "mongodb_toutiaors",
          "meta_type": "mongodb_toutiaors"
        }
      }
    ]
}
```

遇到的问题：

[问题一](https://github.com/mongodb-labs/elastic2-doc-manager/pull/2)

```text
"docManagers": [
{
  "docManager": "elastic2_doc_manager",
  "targetURL": "localhost:9200",
  "args": {
    "meta_index_name": "my_custom_mongo_connector_meta_index",
    "meta_type": "my_custom_mongo_connector_meta_type"
  }
}
]
```

[问题二](https://github.com/mongodb-labs/mongo-connector/issues/641)

mongo-connector only logs warnings and errors by default. Try setting the [verbosity](https://github.com/mongodb-labs/mongo-connector/wiki/Configuration-Options#verbosity) to 2 for INFO logging:

```text
{
"mainAddress": "localhost:3006",
"verbosity": 2,
"namespaces": {
  "meteor.dockerStatsToKeep": true
},
"docManagers":[
{
  "docManager": "elastic_doc_manager",
  "targetURL": "localhost:9200"
}]
}
```

[问题三](https://github.com/mongodb-labs/mongo-connector/blob/master/config.json)

