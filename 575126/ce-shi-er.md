# 测试二

聚合查询的两种写法，查询时间相差几百倍，索引大小 `5T`

第一种，正常的 `terms aggs` 查询，每次需要10多秒

```text
GET /weibo_articles_and_weiboers/weibo_articles_and_weiboer/_search
{
          "query": {
            "bool": {
              "filter": [{
                "query_string": {
                  "fields": ["content_full"],
                  "query" : "\"@小米主题\""
                }
              }, {
                "range": {
                  "published_at": {
                    "gte": "2016-05-01",
                    "lte": "2017-05-01"
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
            "sdf": {
              "terms": {
                "field": "weiboer_id"
              }
            }
          }
}
```

结果 `10秒+`

```text
{
  "took": 10682,
  "timed_out": false,
  "_shards": {
    "total": 45,
    "successful": 45,
    "failed": 0
  },
  "hits": {
    "total": 11043,
    "max_score": 0,
    "hits": []
  },
  "aggregations": {
    "sdf": {
      "doc_count_error_upper_bound": 51,
      "sum_other_doc_count": 10298,
      "buckets": [
        {
          "key": "1657835230",
          "doc_count": 140
        }
      ]
    }
  }
}
```

第一种， `terms aggs` 查询的 `painless script`写法

```text
GET /weibo_articles_and_weiboers/weibo_articles_and_weiboer/_search
{
          "query": {
            "bool": {
              "filter": [{
                "query_string": {
                  "fields": ["content_full"],
                  "query" : "\"@小米主题\""
                }
              }, {
                "range": {
                  "published_at": {
                    "gte": "2014-05-01",
                    "lte": "2017-05-01"
                  }
                }
              }]
            }
          },
          "size": 0,
          "_source": {
            "excludes": []
          },
          "aggs" : {
              "clientip_top10" : {
                  "terms" : {
                      "script" : {
                          "lang" : "painless",
                          "inline" : "doc['weiboer_id'].value"
                      }
                  }
              }
          }
}
```

结果，`183` 毫秒一般都在 `1` 秒以下

```text
{
  "took": 183,
  "timed_out": false,
  "_shards": {
    "total": 45,
    "successful": 45,
    "failed": 0
  },
  "hits": {
    "total": 19317,
    "max_score": 0,
    "hits": []
  },
  "aggregations": {
    "clientip_top10": {
      "doc_count_error_upper_bound": 81,
      "sum_other_doc_count": 18041,
      "buckets": [
        {
          "key": "1649471152",
          "doc_count": 447
        }
      ]
    }
  }
}
```

