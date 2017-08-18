原发提及占比 分子

```
GET /weibo_articles_and_weiboers/weibo_articles_and_weiboer/_search 
{
          "query": {
            "bool": {
              "filter": [{
                "range": {
                  "published_at": {
                    "gte": "2017-06-01 00:00:00",
                    "lte": "2017-08-01 00:00:00",
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
                            "content_full" : "饭饭桶饭自己"
                        }
                      },
                      {
                        "match_phrase" : {
                            "content_full" : "网易新闻"
                        }
                      }
                    ]
                  }
                }
              ],
              "minimum_should_match": "1"
            }
          },
          "size": 0,
          "_source": {
            "excludes": []
          },
          "aggs": {
            "data_dayByday": {
              "date_histogram": {
                "field": "published_at",
                "interval": "1d",
                "time_zone": "Asia/Shanghai",
                "format": "yyyy-MM-dd",
                "min_doc_count": 0,
                "extended_bounds" : { 
                    "min" : "2017-06-01",
                    "max" : "2017-08-01"
                }
              }, 
              "aggs": {
                "groupByIsTop": {
                  "terms": {
                    "field": "is_top",
                    "size": 2,
                    "missing": false,
                    "execution_hint": "map"
                  },
                  "aggs": {
                    "repost_level_e0": {
                      "sum": {
                        "script": "int num3 = 0; if (doc.repost_level.value == 0) {num3 = 1} else {num3 = 0} return num3;"
                      }
                    }    
                  }
                }
              }
            }
          }
}
```

原发提及占比 分母

```
GET /weibo_articles_and_weiboers/weibo_articles_and_weiboer/_search 
{
          "query": {
            "bool": {
              "filter": [{
                "range": {
                  "published_at": {
                    "gte": "2017-06-01 00:00:00",
                    "lte": "2017-08-01 00:00:00",
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
                            "content_full" : "饭饭桶饭自己"
                        }
                      },
                      {
                        "match_phrase" : {
                            "content_full" : "网易新闻"
                        }
                      }
                    ]
                  }
                }
              ],
              "minimum_should_match": "1"
            }
          },
          "size": 0,
          "_source": {
            "excludes": []
          },
          "aggs": {
            "data_dayByday": {
              "date_histogram": {
                "field": "published_at",
                "interval": "1d",
                "time_zone": "Asia/Shanghai",
                "format": "yyyy-MM-dd",
                "min_doc_count": 0,
                "extended_bounds" : { 
                    "min" : "2017-06-01",
                    "max" : "2017-08-01"
                }
              }
            }
          }
}

```



