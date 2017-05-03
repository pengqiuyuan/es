写入数据

`POST` `http://127.0.0.1/api/v1/pa`

`BODY` 体参数说明：

```
index_name：索引名称（字符串）
type_name：分类名称（字符串）
index_message：消息体（数组、集合），消息体内的每一个对象都有 id（字符串） 参数。
```

`HEADERS`：`"Content-Type" => "application/json"`

`BODY` 体：

```js
{

    "index_name": "test",
    "type_name": "test",
    "index_message": [
        {
            "id": "10",
            "intro": "望城17.5影城, 及时影讯、互动活动发布",
            "categories": ["美食"],
            "tags": ["美女"],
            "updated_at": "2015-06-16T10: 35: 40.316Z",
            "username": "gh_275fc782851f",
            "name": "望城今典影城",
            "sentiment": 0,
            "trtl_tags": [
                "电影",
                "57b12aeaa78b9eb67a7104e1",
                "57de2f8d731f6c8f5a782062",
                "58564b1b731f6c8f5a854d3c"
            ]
        },
        {
            "id": "11",
            "intro": "222222望城17.5影城, 及时影讯、互动活动发布",
            "categories": ["旅游"],
            "tags": ["体育"],
            "updated_at": "2015-06-16T10: 35: 40.316Z",
            "username": "gh_275fc782851f",
            "name": "望城今典影城",
            "sentiment": 0,
            "trtl_tags": [
                "电影",
                "57b12aeaa78b9eb67a7104e1",
                "57de2f8d731f6c8f5a782062",
                "58564b1b731f6c8f5a854d3c"
            ]
        }
    ]
}
```



