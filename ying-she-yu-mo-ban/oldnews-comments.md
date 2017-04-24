旧索引：`news_comments`

新索引：`old_news_comments`

部分数据：

```
{
    "_id": "F40084E2-E6A6-4F4E-81CD-61F8E73C6A7A",
    "_score": 16.432579,
    "_source": {
        "user_name": " 人心",
        "content": "1",
        "location": "中国:北京:东城",
        "cmt_id": "6132813410738972030",
        "created_at": "2016-05-19T10:31:52.687Z",
        "post_time": "2016-05-02T08:10:59.000Z",
        "article_id": "bab3d6cda0027d13f31505d899491bcb",
        "site": "spt_tencent",
        "_id": "a43c3378310ae04eb4b7f5f7d7c12918",
        "comments_num": "1",
        "comments": [
            {
                "cmt_id": "6228037304716785076",
                "user_name": "海之声中华路店",
                "location": "中国:江苏:南京",
                "post_time": "2017-01-20T02:36:44.000Z",
                "content": "骗子的手段越来越多了"
            }
        ]
    }
}
```

创建索引`old_news_comments`

```
curl -XPUT http://127.0.0.1:9222/old_news_comments
```

`mapping`

```

```



