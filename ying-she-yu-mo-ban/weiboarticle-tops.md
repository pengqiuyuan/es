旧索引：`weibo_article_tops`

新索引：`weibo_article_tops`

部分数据：

```
{
    "_index": "weibo_article_tops",
    "_type": "weibo_article_top",
    "_id": "4069783320189644",
    "_score": 1,
    "_source": {
        "is_hot": false,
        "is_pin": false,
        "id_short": "EthnK0NkM",
        "weiboer_id": "1777194770",
        "content": "转发微博",
        "content_full": "转发微博 //@慰慰娃娃 #侠探杰克#这个作品有阿汤哥非常有看头我希望自己可以去看一下这部电影的说。 ​​​​",
        "published_at": "2017-01-30T16:56:59.000Z",
        "repost_count": 0,
        "comment_count": 0,
        "up_count": 0,
        "repost_id": "4025425304592297",
        "repost_level": 1,
        "app_source": "微博 weibo.com",
        "href": "/1777194770/EthnK0NkM?from=page_1005051777194770_profile&wvr=6&mod=weibotime",
        "crawled_at": "2017-02-08T22:02:30.137Z",
        "video_links": [],
        "music_links": [],
        "web_links": [],
        "username": null,
        "name": "18岁的俊健Angelie",
        "intro": "他还没有填写个人简介",
        "gender": 0,
        "vip": 0,
        "verify": 0,
        "fans_count": 70,
        "follower_count": 318,
        "weibo_count": 6122,
        "level": 17,
        "last_weibo_at": "2015-05-30T05:47:40.000Z",
        "info": "",
        "location_str": "江苏 无锡",
        "birthday_str": "",
        "sexual": "",
        "relationship": "",
        "email": "",
        "tags": [
            "可爱控",
            "摩羯座",
            "吃货",
            "堀北真希",
            "唱歌",
            "starking"
        ],
        "province_agg": "江苏",
        "city_agg": "无锡",
        "_id": "4069783320189644"
    }
}
```

创建索引`weibo_article_tops`

```
curl -XPUT http://127.0.0.1:9222/weibo_article_tops
```

`mapping`

```

```



