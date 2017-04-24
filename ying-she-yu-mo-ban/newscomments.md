旧索引：`new_news_comments`

新索引：`news_comments`

部分数据：

```
{
    "_id": "a95d6cc936ec5638c43c942a44844007",
    "_score": 1.1613197,
    "_source": {
        "cmt_id": "1841126425",
        "user_name": "274",
        "location": "广东云浮",
        "post_time": "2017-03-29T01:20:48.000Z",
        "content": "看你头像和名字都不正常",
        "artcleid": "1aa2c228373edc1d1ce1ecde012edaf3",
        "site": "app_tencent",
        "channel": "",
        "created_at": "2017-03-29T01:31:22.604Z"
    }
}
```

创建索引`news_comments`

```
curl -XPUT http://127.0.0.1:9222/news_comments
```

`mapping`

