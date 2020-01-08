# 头条

```text
"实际声量","帐号提及量","关注量","粉丝量","阅读量","评论量","点赞量","踩量"
```

```text
GET /toutiao_articles_and_users/toutiao_articles_and_users/_search
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
                            "content" : "小宝宝"
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
                            "title" : "小宝宝"
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
                "follower_count_sum": {
                  "sum": {
                    "field": "follower_count"
                  }
                },
                "fans_count_sum": {
                  "sum": {
                    "field": "fans_count"
                  }
                },
                "read_count_sum": {
                  "sum": {
                    "field": "read_count"
                  }
                },
                "comment_count_sum": {
                  "sum": {
                    "field": "comment_count"
                  }
                },
                "up_count_sum": {
                  "sum": {
                    "field": "up_count"
                  }
                },
                "down_count_sum": {
                  "sum": {
                    "field": "down_count"
                  }
                },
                "account_num":{
                  "cardinality": {
                    "field": "toutiaor_id",
                    "precision_threshold": 40000
                  }
                }
              }
            }
          }
}
```

