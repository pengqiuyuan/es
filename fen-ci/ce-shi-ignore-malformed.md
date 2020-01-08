# 测试 ignore\_malformed

测试 `ignore_malformed`

测试原因：旧集群的索引，有许多数值类型的字段被自动映射成了`String`类型，原因可能是插入数据的时候，有字符串类型。

为了避免重新索引到新集群的时候出现，字段类型格式的错误。对`integer`类型字段使用 `"ignore_malformed": true`

[官网文档](https://www.elastic.co/guide/en/elasticsearch/reference/5.3/ignore-malformed.html)

测试如下：

创建 `mapping`

```text
    curl -XPOST http://localhost:9222/ikindex3/fulltext3/_mapping -d'
     {
         "fulltext3": {
             "properties": {
                 "id": {
                    "type": "integer",
                    "ignore_malformed": true
                 },
                 "title": {
                     "type": "text",
                     "analyzer": "ik_max_word",
                     "search_analyzer": "ik_max_word",
                     "include_in_all": "true",
                     "boost": 8
                 }
             }
         }
     }'
```

插入数据 `"id":"测试测试"` 数据插入无异常符合预期（对 `id` 做 `sum` 聚合计算 ，`id`为 "测试测试" 的值被忽略，只计算数值）

```text
    curl -XPOST http://127.0.0.1:9222/ikindex3/fulltext3/1 -d'
    {
        "id":1,
        "title":"测试 test"
    }'

    {"_index":"ikindex3","_type":"fulltext3","_id":"1","_version":2,"result":"updated","_shards":{"total":2,"successful":2,"failed":0},"created":false}

    curl -XPOST http://127.0.0.1:9222/ikindex3/fulltext3/2 -d'
    {
        "id":"2",
        "title":"测试 test"
    }'
    {"_index":"ikindex3","_type":"fulltext3","_id":"2","_version":3,"result":"updated","_shards":{"total":2,"successful":2,"failed":0},"created":false}

    curl -XPOST http://127.0.0.1:9222/ikindex3/fulltext3/3 -d'
    {
        "id":"测试测试",
        "title":"测试 test"
    }'
    {"_index":"ikindex3","_type":"fulltext3","_id":"2","_version":4,"result":"updated","_shards":{"total":2,"successful":2,"failed":0},"created":false}
```

