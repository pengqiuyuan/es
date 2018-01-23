WeiboLogs（索引名称、分片名称）：`weiboer_logs`、`weiboer_logs`

**POST 请求写入数据到 **`kafka`

`POST` `http://127.0.0.1/stq/api/v1/pa/weiboerLogs/add`

`HEADERS`：`"Content-Type" => "application/json"`

`BODY` 体参数说明：List 集合、数组

```
[
    {
        "id": "5a41c0554c7ffb8b1900f5d9",
        "index_name": "rowlet_facebook_articles",
        "type_name": "rowlet_facebook_articles",
        "name": "Donald J. Trump",
        "create_at": "2017-03-19T04:21:00.000Z",
        "last_untime": "1514254504",
        "permalink_url": "/DonaldTrump/videos/10160350034295725/",
        "text": "First Melania and I hope everyone is having a VERY MERRY CHRISTMAS!!!ビデオの再生に問題が発生しているようです。その場合は、ブラウザの再起動をお試しください。 閉じる Donald J. Trump さんの投稿 再生279,771回",
        "share_num": "3542",
        "likes_num": "127397",
        "comment_num": "12021",
        "site": "facebook",
        "share_count": "20325",
        "update_status": true,
        "user": {
            "name": "Donald J. Trump",
            "id": "153080620724",
            "category": "Public Figure",
            "link": "https://www.facebook.com/DonaldTrump/",
            "location": {
                "city": "New York",
                "country": "United States",
                "state": "NY",
                "street": "725 Fifth Ave",
                "zip": "10022"
            },
            "website": "http://www.donaldjtrump.com"
        }
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
          "title" => "乒乓网1"
}
{
          "title" => "乒乓网2"
}
```

---

**POST 请求直接 Bulk 写入数据到 Elasticsearch**

注意：与上面的 `API` 相比，爬虫只用注意 `URL` 和 多出了两种返回值就好，其他一样。

`POST` `http://127.0.0.1/stq/api/v1/pabulk/topicRowletFacebook/add`

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



