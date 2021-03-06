# TopicRank

话题排行榜 （索引名称、分片名称）：`topic_rank`、`topic_rank`

**POST 请求写入数据到** `kafka`

`POST` `http://127.0.0.1/stq/api/v1/pa/topicRank/add`

`HEADERS`：`"Content-Type" => "application/json"`

`BODY` 体参数说明：List 集合、数组

```text
[
    {
      "id": "10",
      "index_name": "topic_rank",
      "type_name": "topic_rank",
      ...
    },
    {
      "id": "11",
      "index_name": "topic_rank",
      "type_name": "topic_rank",
      ...
    }
]
```

`response` 数据写入队列成功

```text
{
  "success" : "true"
}
```

`response` 数据写入队列失败（有一条消息写入失败就会触发。返回 `false` 的 场景是 `web server` 与 `kafka` 连接断开）

```text
{
  "success" : "false"
}
```

`logstash` **消费**`kafka`**中的数据到** `elasticsearch`

```text
...
```

**POST 请求直接 Bulk 写入数据到 Elasticsearch**

注意：与上面的 `API` 相比，爬虫只用注意 `URL` 和 多出了两种返回值就好，其他一样。

`POST` `http://127.0.0.1/stq/api/v1/pabulk/topicRank/add`

`HEADERS`：如上

`BODY` ：如上

`response` 数据 `bulk` 写入 `es` 成功

```text
{
  "success" : "true"
}
```

`response` 数据 `bulk` 写入 `es` 失败 ，返回 `bulkResponse.buildFailureMessage()` 的错误 `message`

```text
{
  "success" : "这里面的内容为 bulk 请求失败的 message 提示信息"
}
```

传入的 List 集合为空 `[]`，直接返回 `response`

```text
{
  "success" : "null"
}
```

