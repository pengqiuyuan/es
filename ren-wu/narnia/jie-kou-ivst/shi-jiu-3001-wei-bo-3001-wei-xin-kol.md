五、微博、微信 KOL

`POST` `http://127.0.0.1/stq/api/v1/words/findEsListByKeyword`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
keyword为监测项名称，
startDate为监测项起始时间（含），
endDate为监测项结束时间（含），
taskType为数据源 weibo、weixin
sortField为排序字段
    微博（默认 published_at 爬取时间）：fans_count（关注数）, follower_count（粉丝数）, repost_count（转发）, comment_count（评论）, up_count（点赞）
    微信（默认 last_modified_at 爬取时间）：stat_read_count（阅读数）, stat_like_count（点赞）
sort为排序 asc（升序）、desc（降序）
```

`BODY` 体：

```
{
  "keyword": "西游伏妖篇",
  "startDate": "2016-05-01",
  "endDate": "2017-05-02",
  "taskType":"weibo",
  "sortField":"follower_count",
  "sort":"desc"
}
```

`response` Es查询

微博

```
{
"threeKolArticle":[
  {"_index": "weibo_articles_and_weiboers", "_type": "weibo_articles_and_weiboer", "_source":{"comment_count": 14,…},
  {"_index": "weibo_articles_and_weiboers", "_type": "weibo_articles_and_weiboer", "_source":{"comment_count": 3315,…},
  {"_index": "weibo_articles_and_weiboers", "_type": "weibo_articles_and_weiboer", "_source":{"comment_count": 2502,…}
],
"1266321801":[{"_index": "weibo_articles_and_weiboers", "_type": "weibo_articles_and_weiboer", "_source":{"comment_count": 14,…],
"3952070245":[{"_index": "weibo_articles_and_weiboers", "_type": "weibo_articles_and_weiboer", "_source":{"comment_count": 3315,…],
"1259193624":[{"_index": "weibo_articles_and_weiboers", "_type": "weibo_articles_and_weiboer", "_source":{"comment_count": 2502,…]
}
```

微信

```
{
"threeKolArticle":[
  {"_index": "weixin_articles_and_weixiners", "_type": "weixin_articles_and_weixiner", "_source":{"sentiment": 1,…},
  {"_index": "weixin_articles_and_weixiners", "_type": "weixin_articles_and_weixiner", "_source":{"sentiment": 1,…},
  {"_index": "weixin_articles_and_weixiners", "_type": "weixin_articles_and_weixiner", "_source":{"sentiment": -1,…}
],
"MjM5MzY0MTkzOQ==":[{"_index": "weixin_articles_and_weixiners", "_type": "weixin_articles_and_weixiner", "_source":{"biz": "MjM5MzY0MTkzOQ==",…],
"MjM5MTc3NTYzMw==":[{"_index": "weixin_articles_and_weixiners", "_type": "weixin_articles_and_weixiner", "_source":{"biz": "MjM5MTc3NTYzMw==",…],
"MzA5MDY3MjMwOQ==":[{"_index": "weixin_articles_and_weixiners", "_type": "weixin_articles_and_weixiner", "_source":{"biz": "MzA5MDY3MjMwOQ==",…]
}
```



