六、**获取原文，关键字或账号ID**

`GET` `http://127.0.0.1/stq/api/v1/rowlet/findEsTextByUserIdOrKeywords?startDate=2017-12-09&endDate=2017-12-10&category=tw&keywords=benefit`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
startDate为起始时间（含），必填。
endDate为结束时间（不含），必填。
category为数据源 tw、fb，必填
keywords，非必填。查询关键词
ids，非必填。账号ID
```

`response`

`Twitter` 查询语句

`http://127.0.0.1/stq/api/v1/rowlet/findEsTextByUserIdOrKeywords?startDate=2017-12-09&endDate=2017-12-10&category=tw&keywords=benefit`

`或者`

`http://127.0.0.1/stq/api/v1/rowlet/findEsTextByUserIdOrKeywords?startDate=2017-12-09&endDate=2017-12-10&category=tw&ids=33750798`

```
{
    "tw": [{
        "_index": "rowlet_twitter_articles",
        "_type": "rowlet_twitter_articles",
        "_source": {
            "entities": {
                "hashtags": []
            },
            "favorite_count": "16",
            "text": "“Gov. Walker touts Foxconn’s benefit to Green Bay”: https://t.co/KFJBHVmclW",
            "reply_count": "14",
            "retweet_count": "4"
        },
        "_id": "939194401120759813",
        "_score": 6.664112
    }],
    "count": "1",
    "message": "任务成功"
}
```

`Twitter` 查询语句

`http://127.0.0.1/stq/api/v1/rowlet/findEsTextByUserIdOrKeywords?startDate=2017-12-09&endDate=2017-12-10&category=fb&keywords=legislation`

`或者`

`http://127.0.0.1/stq/api/v1/rowlet/findEsTextByUserIdOrKeywords?startDate=2017-12-09&endDate=2017-12-10&category=tw&ids=33750798`

```
{
    "fb": [{
        "_index": "rowlet_facebook_articles",
        "_type": "rowlet_facebook_articles",
        "_source": {
            "comment_num": 1,
            "share_count": 3,
            "text": "Public officials are not above the American people. I introduced legislation to hold lawmakers accountable.",
            "likes_num": 15,
            "topick": []
        },
        "_id": "38a40ea98cd08927608ffe6a4ccc6ab3",
        "_score": 4.4529905
    }],
    "count": "1",
    "message": "任务成功"
}
```



