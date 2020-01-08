# 接口 Rowlet

```text
GET /rowlet_twitter_articles/rowlet_twitter_articles/_search
{
          "query": {
            "bool": {
              "filter": [{
                "range": {
                  "created_at": {
                    "gte": "2016-12-09 00:00:00",
                    "lte": "2017-12-10 00:00:00",
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
                            "user.id_str" : "18172905"
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
                            "user.id_str" : "239871673"
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
            "includes": []
          },
          "aggs": {
            "users":{
              "terms": {
                "field": "user.id_str",
                "size": 10,
                "execution_hint": "map"
              },
              "aggs": {
                "date": {
                  "date_histogram": {
                    "field": "created_at",
                    "interval": "1d",
                    "time_zone": "Asia/Shanghai",
                    "format": "yyyy-MM-dd",
                    "min_doc_count": 0,
                    "extended_bounds" : { 
                        "min" : "2016-12-09",
                        "max" : "2017-12-10"
                    }
                  },
                  "aggs": {
                    "document_count": {
                        "sum": {
                            "script": "1"
                        }
                    },
                    "followers_count_sum": {
                        "sum": {
                            "field": "user.followers_count",
                            "missing": 0
                        }
                    },
                    "favourites_count_sum": {
                        "sum": {
                            "field": "user.favourites_count",
                            "missing": 0
                        }
                    },
                    "friends_count_sum": {
                        "sum": {
                            "field": "user.friends_count",
                            "missing": 0
                        }
                    },
                    "repost_sum": {
                        "sum": {
                            "field": "retweet_count",
                            "missing": 0
                        }
                    },
                    "repost_max": {
                        "max": {
                            "field": "retweet_count",
                            "missing": 0
                        }
                    },
                    "comment_sum": {
                        "sum": {
                            "field": "reply_count",
                            "missing": 0
                        }
                    },
                    "comment_max": {
                        "max": {
                            "field": "reply_count",
                            "missing": 0
                        }
                    },
                    "up_count_sum": {
                        "sum": {
                            "field": "favorite_count",
                            "missing": 0
                        }
                    },
                    "up_count_max": {
                        "max": {
                            "field": "favorite_count",
                            "missing": 0
                        }
                    }
                  }
                }
              }
            }
          }
}



GET /rowlet_facebook_articles/rowlet_facebook_articles/_search
{
          "query": {
            "bool": {
              "filter": [{
                "range": {
                  "create_at": {
                    "gte": "2017-12-09 00:00:00",
                    "lte": "2017-12-10 00:00:00",
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
                            "user.id" : "853073668057412"
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
                            "user.id" : "853073668057412"
                        }
                      }
                    ]
                  }
                }
              ],
              "minimum_should_match": "1"
            }
          },
          "size": 5,
          "_source": {
            "includes": ["user.fan_count","user.likes_count","share_count","comment_num","likes_num"]
          },
          "aggs": {
            "users":{
              "terms": {
                "field": "user.id",
                "size": 10,
                "execution_hint": "map"
              },
              "aggs": {
                "date": {
                  "date_histogram": {
                    "field": "create_at",
                    "interval": "1d",
                    "time_zone": "Asia/Shanghai",
                    "format": "yyyy-MM-dd",
                    "min_doc_count": 0,
                    "extended_bounds" : { 
                        "min" : "2017-12-09",
                        "max" : "2017-12-10"
                    }
                  },
                  "aggs": {
                    "document_count": {
                        "sum": {
                            "script": "1"
                        }
                    },
                    "fan_count_sum": {
                        "sum": {
                            "field": "user.fan_count",
                            "missing": 0
                        }
                    },
                    "likes_count_sum": {
                        "sum": {
                            "field": "user.likes_count",
                            "missing": 0
                        }
                    },
                    "repost_sum": {
                        "sum": {
                            "field": "share_count",
                            "missing": 0
                        }
                    },
                    "repost_max": {
                        "max": {
                            "field": "share_count",
                            "missing": 0
                        }
                    },
                    "comment_sum": {
                        "sum": {
                            "field": "comment_num",
                            "missing": 0
                        }
                    },
                    "comment_max": {
                        "max": {
                            "field": "comment_num",
                            "missing": 0
                        }
                    },
                    "up_sum": {
                        "sum": {
                            "field": "likes_num",
                            "missing": 0
                        }
                    },
                    "up_max": {
                        "max": {
                            "field": "likes_num",
                            "missing": 0
                        }
                    }
                  }
                }
              }
            }
          }
}
```

