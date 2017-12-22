```
"实际声量","帐号提及量","问题数","关注人数","查看人数","回答人数"
```

```
GET /zhihu_questions/zhihu_questions/_search
{
          "query": {
            "bool": {
              "filter": [{
                "range": {
                  "published_at": {
                    "gte": "2017-06-24 00:00:00",
                    "lte": "2017-09-11 00:00:00",
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
                            "desc" : "中国有嘻哈"
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
                            "title" : "中国有嘻哈"
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
                    "min" : "2017-06-24",
                    "max" : "2017-09-11"
                }
              },
              "aggs": {
                "follows_num_sum": {
                  "sum": {
                    "field": "follows_num"
                  }
                },
                "views_num_sum": {
                  "sum": {
                    "field": "views_num"
                  }
                },
                "answers_num_sum": {
                  "sum": {
                    "field": "answers_num"
                  }
                },
                "account_num":{
                  "cardinality": {
                    "field": "author_id",
                    "precision_threshold": 40000
                  }
                }
              }
            }
          }
}
```



