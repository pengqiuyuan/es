```
GET /weibo/weibo/_search?size=0
{
    "query": {
        "bool": {
            "filter": [{
                "range": {
                    "published_at": {
                        "gte": "2016-01-01 00:00:00",
                        "lte": "2017-11-21 00:00:00",
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
                                "match_phrase": {
                                    "content_full": "冰河追凶"
                                }
                            }
                        ]
                    }
                }
            ],
            "minimum_should_match": "1"
        }
    },
    "aggs": {
        "data_dayByday": {
            "sampler": {
                "shard_size": 1000
            },
            "aggs": {
                "data_dayByday": {
                    "date_histogram": {
                        "field": "published_at",
                        "interval": "day",
                        "time_zone": "Asia/Shanghai",
                        "format": "yyyy-MM-dd",
                        "min_doc_count": 1,
                        "extended_bounds" : { 
                            "min" : "2015-01-01",
                            "max" : "2017-11-20"
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
                                "group_by_fans": {
                                    "range": {
                                        "field": "fans_count",
                                        "ranges": [
                                          {"to": 999},
                                          {"from": 999,"to": 4999},
                                          {"from": 4999,"to": 49999},
                                          {"from": 49999,"to": 99999},
                                          {"from": 100000}
                                        ]
                                    }
                                },
                                "group_by_follower": {
                                    "range": {
                                        "field": "follower_count",
                                        "ranges": [
                                          {"to": 999},
                                          {"from": 999,"to": 4999},
                                          {"from": 4999,"to": 49999},
                                          {"from": 49999,"to": 99999},
                                          {"from": 100000}
                                        ]
                                    }
                                }
                            }
                        }
                    }
                }
            }
        },
        "group_by_province": {
            "sampler": {
                "shard_size": 1000
            },
            "aggs": {
                "group_by_province": {
                    "terms": {
                        "field": "province_agg",
                        "size": 50
                    }
                }
            }
        },
        "group_by_city": {
            "sampler": {
                "shard_size": 1000
            },
            "aggs": {
                "group_by_city": {
                    "terms": {
                        "field": "city_agg",
                        "size": 50
                    }
                }
            }
        },
        "group_by_relationship": {
            "sampler": {
                "shard_size": 1000
            },
            "aggs": {
                "group_by_relationship": {
                    "terms": {
                        "field": "relationship_agg",
                        "size": 10
                    }
                }
            }
        },
        "group_by_edu": {
            "sampler": {
                "shard_size": 1000
            },
            "aggs": {
                "group_by_edu": {
                    "terms": {
                        "field": "edu_str_agg",
                        "size": 5
                    }
                }
            }
        },
        "group_by_gender": {
            "sampler": {
                "shard_size": 1000
            },
            "aggs": {
                "group_by_gender": {
                    "terms": {
                        "field": "gender",
                        "size": 2
                    }
                }
            }
        },
        "group_by_verify": {
            "sampler": {
                "shard_size": 1000
            },
            "aggs": {
                "group_by_verify": {
                    "terms": {
                        "field": "verify",
                        "size": 3
                    }
                }
            }
        },
        "group_by_birth": {
            "sampler": {
                "shard_size": 1000
            },
            "aggs": {
                "group_by_birth": {
                    "date_range": {
                        "field": "birthday_date_agg",
                        "format": "yyy",
                        "ranges": [
                          {"to": "now-588M/M"},
                          {"from": "now-588M/M","to": "now-468M/M"},
                          {"from": "now-468M/M","to": "now-348M/M"},
                          {"from": "now-348M/M","to": "now-228M/M"},
                          {"from": "now-228M/M"}
                        ]
                    }
                }
            }
        }
    }
}
```



