测试文档更新，`logstash` 添加 `output` 添加  `doc_as_upsert =>true` `action >"update"`，如：

```
output {
    if [@metadata][index_name] == "tieba_posts" {
        elasticsearch {
                hosts => ["127.0.0.1:9200"]
                index => "%{[@metadata][index_name]}"
                document_type => "%{[@metadata][type_name]}"
                document_id => "%{[@metadata][id]}"
                template_overwrite => false
                user => '用户名'
                password => '密码'
                doc_as_upsert => true
                action => "update"
            }
        }
}
```

希望结果：

* 文档不存在时，索引新文档

* 文档存在时（`_id` 判断），更新部分文档（爬虫上传的 `Body` 体内容）

测试结果：

第一步、`POST` 一条数据，如下：

```
[
    {
        "id": "test3",
        "index_name": "tieba_posts",
        "type_name": "tieba_posts",
        "tieba_id": 536,
        "title": "比利林恩的中场战事-极限特工3-西游伏妖篇-功夫瑜伽，高清版",
        "author_name": "物旧yes",
        "author_id": "2719429553",
        "reply_num": 201,
        "content": " 二楼地址",
        "date": "2017-02-24T06:26:00.000Z",
        "created_at": 1488509090000,
      	"tie_url": "http://",
        "updated_at": 1488509090000,
        "ba_name": "测试"
    }
]
```

`ES` 查询 `tieba_posts` 索引下的 `_id:"test3"` 的数据，结果如下，符合预期

```
{
  "_index": "tieba_posts",
  "_type": "tieba_posts",
  "_id": "test3",
  "_version": 4,
  "found": true,
  "_source": {
    "tieba_id": 536,
    "title": "比利林恩的中场战事-极限特工3-西游伏妖篇-功夫瑜伽，高清版",
    "author_name": "物旧yes",
    "reply_num": 201,
    "author_id": "2719429553",
    "date": "2017-02-24T06:26:00.000Z",
    "updated_at": 1488509090000,
    "created_at": 1488509090000,
    "tie_url": "http://",
    "ba_name": "测试",
    "content": " 二楼地址"
  }
}
```

第二步、`POST` 一条相同 `ID` 的部分数据数据，如下，我们预期的 `ES` 查询结果希望是原文档所有字段值都在，只有 `tieba_id` 被修改

```
[
    {
        "id": "test3",
        "index_name": "tieba_posts",
        "type_name": "tieba_posts",
        "tieba_id": 536111,
        "title": "比利林恩的中场战事-极限特工3-西游伏妖篇-功夫瑜伽，高清版",
        "author_name": "物旧yes"
    }
]
```

`ES` 查询 `tieba_posts` 索引下的 `_id:"test3"` 的数据，结果如下，符合预期`tieba_id` 被修改为 `"tieba_id": 536111` ，其他字段值没有改变

```
{
  "_index": "tieba_posts",
  "_type": "tieba_posts",
  "_id": "test3",
  "_version": 5,
  "found": true,
  "_source": {
    "tieba_id": 536111,
    "title": "比利林恩的中场战事-极限特工3-西游伏妖篇-功夫瑜伽，高清版",
    "author_name": "物旧yes",
    "reply_num": 201,
    "author_id": "2719429553",
    "date": "2017-02-24T06:26:00.000Z",
    "updated_at": 1488509090000,
    "created_at": 1488509090000,
    "tie_url": "http://",
    "ba_name": "测试",
    "content": " 二楼地址"
  }
}
```

结论：

添加 `doc_as_upsert =>true` 与`action >"update"`  ，能够达到预期更新、新增文档的效果

