# Kejizixun 测试

科技资讯（索引名称、分片名称）：`tech_news`、[分片参考](../../ying-she-yu-mo-ban/ke-ji-zi-xun-zhan-shu-ju.md)（`tech_36kr_articles`、`tech_q36kr_articles`、`tech_huxiu_articles`、`tech_leiphone_articles`、`tech_cyzone_articles`、`tech_tmtpost_articles`、`tech_geekpark_articles`、`tech_ikanchai_articles`、`tech_qianzhan_articles`、`tech_techxue_articles`、`tech_pingwest_articles`）

**POST 请求写入数据到** `kafka`

`POST` `http://127.0.0.1/stq/api/v1/pa/kejizixun/add`

`HEADERS`：`"Content-Type" => "application/json"`

`BODY` 体参数说明：List 集合、数组

```text
[
    {
      "id": "10",
      "index_name": "tech_news",
      "type_name": "tech_36kr_articles",
      "avatar_img": "http://p3.pstatp.com/thumb/6427/6955928713",
      "name": "乒乓网1",
      ...
    },
    {
      "id": "11",
      "index_name": "tech_news",
      "type_name": "tech_36kr_articles",
      "avatar_img": "http://p3.pstatp.com/thumb/6427/6955928713",
      "name": "乒乓网2",
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

从 `kafka` 队列中读取的数据，两条符合预期（`index_name`、`type_name`、`id`会在`logstash filter`中处理后移除，保存或者更新数据到 `es`）

```text
{
    "avatar_img" => "http://p3.pstatp.com/thumb/6427/6955928713",
          "name" => "乒乓网1"
}
{
    "avatar_img" => "http://p3.pstatp.com/thumb/6427/6955928713",
          "name" => "乒乓网2"
}
```

**POST 请求直接 Bulk 写入数据到 Elasticsearch**

注意：与上面的 `API` 相比，爬虫只用注意 `URL` 和 多出了两种返回值就好，其他一样。

`POST` `http://127.0.0.1/stq/api/v1/pabulk/kejizixun/add`

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

