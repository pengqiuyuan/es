# city\_qa\_articles

索引名称、分片名称：`city_qa_articles`、`city_qa_articles`

`POST` `http://127.0.0.1/stq/api/v1/pabulk/shareWrite/add`

`HEADERS`：`"Content-Type" => "application/json"`

`BODY` 体参数说明：List 集合、数组（id、index\_name、type\_name必填）

```text
[{
        "id": "test11",
        "index_name": "city_qa_articles",
        "type_name": "city_qa_articles",
        "title": "测试测试测试1",
        "publish_time": "2018-07-09T07:31:19.000Z",
        "create_time ": "2018-07-09T07:31:19.000Z"
    },
    {
        "id": "test12",
        "index_name": "city_qa_articles",
        "type_name": "city_qa_articles",
        "title": "测试测试测试2",
        "publish_time": "2018-07-09T07:31:19.000Z",
        "create_time ": "2018-07-09T07:31:19.000Z"
    }
]
```

`response` 数据写入队列成功

```text
{
  "success" : "true"
}
```

`response` 数据写入队列失败

