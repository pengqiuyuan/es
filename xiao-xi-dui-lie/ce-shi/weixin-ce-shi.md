微信（索引名称、分片名称）：`weixin_articles_and_weixiners`、`weixin_articles_and_weixiner`

**POST 请求写入数据到 **`kafka`

`POST` `http://127.0.0.1/stq/api/v1/pa/weixin/add`

`HEADERS`：`"Content-Type" => "application/json"`

`BODY` 体参数说明：List 集合、数组

```
[
    {
      "id": "10",
      "index_name": "weixin_articles_and_weixiners",
      "type_name": "weixin_articles_and_weixiner",
      "avatar_img": "http://p3.pstatp.com/thumb/6427/6955928713",
      "name": "乒乓网1",
      ...
    },
    {
      "id": "11",
      "index_name": "weixin_articles_and_weixiners",
      "type_name": "weixin_articles_and_weixiner",
      "avatar_img": "http://p3.pstatp.com/thumb/6427/6955928713",
      "name": "乒乓网2",
      ...
    }
]
```

`response` 数据写入队列成功

```
{
  "success" : "true"
}
```

`response` 数据写入队列失败（有一条消息写入失败就会触发。返回 `false` 的 场景是 `web server` 与 `kafka` 连接断开）

```
{
  "success" : "false"
}
```

`logstash`** 消费**`kafka`**中的数据到 **`elasticsearch`

```
...
```

从 `kafka` 队列中读取的数据，两条符合预期（`index_name`、`type_name`、`id`会在`logstash filter`中处理后移除，保存或者更新数据到 `es`）

```
{
    "avatar_img" => "http://p3.pstatp.com/thumb/6427/6955928713",
          "name" => "乒乓网1"
}
{
    "avatar_img" => "http://p3.pstatp.com/thumb/6427/6955928713",
          "name" => "乒乓网2"
}
```

---

**POST 请求直接 Bulk 写入数据到 Elasticsearch**

`response` 数据写入队列成功

```
{
  "success" : "true"
}
```

`response` 数据 `bulk` 写入 `es` 失败 ，返回 `bulkResponse.buildFailureMessage()` 的错误 `message`

```
{
  "success" : "这里面的内容为 bulk 请求失败的 message 提示信息"
}
```

传入的 List 集合为空 `[]`，直接返回 `response`

```
{
  "success" : "null"
}
```



