百度新闻（索引名称、分片名称）：sogou\_weixin\_articles、sogou\_weixin\_articles



**POST 请求写入数据到 **`kafka`

`POST` `http://127.0.0.1/stq/api/v1/pa/baidu/add`

`HEADERS`：`"Content-Type" => "application/json"`

`BODY` 体参数说明：List 集合、数组

```
[
    {
      "id": "10",
      "index_name": "baidunews_news",
      "type_name": "baidunews_news",
      "avatar_img": "http://p3.pstatp.com/thumb/6427/6955928713",
      "name": "乒乓网1"
    },
    {
      "id": "11",
      "index_name": "baidunews_news",
      "type_name": "baidunews_news",
      "avatar_img": "http://p3.pstatp.com/thumb/6427/6955928713",
      "name": "乒乓网2"
    }
]
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



