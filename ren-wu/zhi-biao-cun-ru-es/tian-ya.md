```
"实际声量","帐号提及量","帖子点击数","贴子回复数"
```

```
GET /tianya_news/tianya_news/_search
{
          "query": {
            "bool": {
              "filter": [{
                "range": {
                  "published_at": {
                    "gte": "2017-06-01 00:00:00",
                    "lte": "2017-07-01 00:00:00",
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
                            "content" : "守望"
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
                            "title" : "守望"
                        }
                      }
                    ]
                  }
                }
              ],
              "minimum_should_match": "1"
            }
          },
          "size": 10,
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
                    "min" : "2017-06-01",
                    "max" : "2017-07-01"
                }
              },
              "aggs": {
                "clicks_num_sum": {
                  "sum": {
                    "field": "clicks_num"
                  }
                },
                "replays_num_sum": {
                  "sum": {
                    "field": "replays_num"
                  }
                },
                "account_num":{
                  "cardinality": {
                    "field": "host",
                    "precision_threshold": 40000
                  }
                }
              }
            }
          }
}
```



