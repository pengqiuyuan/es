tieba_logs（索引名称、分片名称）：`tieba_logs`、`tieba_logs`
qie_logs（索引名称、分片名称）：`qie_logs`、`qie_logs`
qie_articles_and_users（索引名称、分片名称）：`qie_articles_and_users`、`qie_articles_and_users`

**POST 请求写入数据到 **`kafka`

`POST` `http://127.0.0.1/stq/api/v1/pa/shareWrite/add`

`HEADERS`：`"Content-Type" => "application/json"`

`BODY` 体参数说明：List 集合、数组

```
[
    {
        "id": "1",
        "index_name": "索引名称",
        "type_name": "索引类型"
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

`response` 数据写入队列失败

```
{
  "success" : "false"
}
```
---

**POST 请求直接 Bulk 写入数据到 Elasticsearch**

注意：与上面的 `API` 相比，爬虫只用注意 `URL` 和 多出了两种返回值就好，其他一样。

`POST` `http://127.0.0.1/stq/api/v1/pabulk/shareWrite/add`

`HEADERS`：如上

`BODY` ：如上

`response` 数据 `bulk` 写入 `es` 成功

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



