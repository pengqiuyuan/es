天涯论坛（索引名称、分片名称）：`tianya_news`、`tianya_news`

**POST 请求写入数据到 **`kafka`

`POST` `http://127.0.0.1/stq/api/v1/pa/tianya/add`

`HEADERS`：`"Content-Type" => "application/json"`

`BODY` 体参数说明：List 集合、数组

```
[
    {
      "id": "10",
      "index_name": "tianya_news",
      "type_name": "tianya_news",
      "name": "乒乓网1",
      ...
    },
    {
      "id": "11",
      "index_name": "tianya_news",
      "type_name": "tianya_news",
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
          "name" => "乒乓网1"
}
{
          "name" => "乒乓网2"
}
```



