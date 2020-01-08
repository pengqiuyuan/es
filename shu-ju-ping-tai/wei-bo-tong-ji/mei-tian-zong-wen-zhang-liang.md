# 每天总文章量

每日文章量

```text
GET /weibo_articles_and_weiboers/weibo_articles_and_weiboer/_search 
{
          "query": {
            "bool": {
              "filter": [{
                "range": {
                  "crawled_at": {
                    "gte": "2017-08-14 00:00:00",
                    "lte": "2017-08-17 00:00:00",
                    "format": "yyyy-MM-dd HH:mm:ss||yyyy-MM-dd||epoch_millis",
                    "time_zone": "Asia/Shanghai"
                  }
                }
              }]
            }
          },
          "size": 0,
          "_source": {
            "excludes": []
          },
          "aggs": {
            "date": {
              "date_histogram": {
                "field": "published_at",
                "interval": "1d",
                "time_zone": "Asia/Shanghai",
                "format": "yyyy-MM-dd",
                "min_doc_count": 0,
                "extended_bounds" : { 
                    "min" : "2017-06-14",
                    "max" : "2017-08-17"
                }
              }
            }
          }
}
```

