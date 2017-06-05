新、旧集群统一时间段数据对比

```
curl -u 用户名:密码 -XGET http://127.0.0.1:9200/weibo_articles/weibo_article/_search?pretty -d '
{
  "query": { 
    "range": { "published_at": { "gte": "2017-06-03T16:00:00.000Z","lte": "2017-06-04T16:00:00.000Z"}}
  }
  , "sort": { "published_at": "asc"}
  , "size":"1"
}'


curl -u 用户名:密码 -XGET http://127.0.0.1:9200/weibo_articles_and_weiboers/weibo_articles_and_weiboer/_search?pretty -d '
{
  "query": { 
    "range": { "published_at": { "gte": "2017-06-03T16:00:00.000Z","lte": "2017-06-04T16:00:00.000Z"}}
  }
  , "sort": { "published_at": "asc"}
  , "size":"1"
}'
```

`query_string` 全文查询

```
GET /weibo_articles_and_weiboers/weibo_articles_and_weiboer/_search
{
   "query": {
        "query_string" : {
            "fields" : ["content_full"],
            "query" : "\"@MONSTER_阿凉\""
        }
    }
}


GET /weibo_articles_and_weiboers/weibo_articles_and_weiboer/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "query_string" : {
              "fields" : ["content_full"],
              "query" : "\"@MONSTER_阿凉\""
          }
        }
      ]
    }
  }
}  
```



