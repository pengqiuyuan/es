# 微信

```text
"声量","实际声量","总阅读量","总点赞量","统计占比","帐号提及量"
```

```text
GET weixin_articles_and_weixiners/weixin_articles_and_weixiner/_search
{
          "query": {
            "bool": {
              "filter": [{
                "range": {
                  "last_modified_at": {
                    "gte": "2017-07-01 00:00:00",
                    "lte": "2017-09-30 00:00:00",
                    "format": "yyyy-MM-dd HH:mm:ss||yyyy-MM-dd||epoch_millis",
                    "time_zone": "Asia/Shanghai"
                  }
                }
              }],
              "should": [
                {
                  "bool": {
                    "must": [
                      {
                        "match_phrase" : {
                            "content" : "腾格尔"
                        }
                      }
                    ]
                  }
                },
                {
                  "bool": {
                    "must": [
                      {
                        "match_phrase" : {
                            "title" : "腾格尔"
                        }
                      }
                    ]
                  }
                }
              ],
              "minimum_should_match": "1"
            }
          },
          "size": 1,
          "_source": {
            "excludes": []
          },
          "aggs": {
            "date": {
              "date_histogram": {
                "field": "last_modified_at",
                "interval": "1d",
                "time_zone": "Asia/Shanghai",
                "format": "yyyy-MM-dd",
                "min_doc_count": 0,
                "extended_bounds" : { 
                    "min" : "2017-07-01",
                    "max" : "2017-09-30"
                }
              }, 
              "aggs": {
                "account":{
                  "cardinality": {
                    "field": "biz",
                    "precision_threshold": 40000
                  }
                }
              }
            }
          }
}
```

