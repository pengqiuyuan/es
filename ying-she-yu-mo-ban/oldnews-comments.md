旧索引：`news_comments`

新索引：`old_news_comments`

部分数据：

```
{
    "_id": "F40084E2-E6A6-4F4E-81CD-61F8E73C6A7A",
    "_score": 16.432579,
    "_source": {
        "user_name": " 人心",
        "content": "1",
        "location": "中国:北京:东城",
        "cmt_id": "6132813410738972030",
        "created_at": "2016-05-19T10:31:52.687Z",
        "post_time": "2016-05-02T08:10:59.000Z",
        "article_id": "bab3d6cda0027d13f31505d899491bcb",
        "site": "spt_tencent",
        "_id": "a43c3378310ae04eb4b7f5f7d7c12918",
        "comments_num": "1",
        "comments": [
            {
                "cmt_id": "6228037304716785076",
                "user_name": "海之声中华路店",
                "location": "中国:江苏:南京",
                "post_time": "2017-01-20T02:36:44.000Z",
                "content": "骗子的手段越来越多了"
            }
        ]
    }
}
```

创建索引`old_news_comments`

```
curl -XPUT http://127.0.0.1:9222/old_news_comments
```

`mapping`

```
curl -XPUT http://127.0.0.1:9222/_template/old_news_comments -d '
{
    "template": "old_news_comments*",
    "settings": {
        "refresh_interval": "60s",
        "number_of_replicas": "1",
        "number_of_shards": "15"
    },
    "mappings": {
        "_default_": {
            "_all": {
                "enabled": true
            },
            "_source": {
                "enabled": true
            },
            "dynamic_templates": [
                {
                    "message_field": {
                        "match": "message",
                        "match_mapping_type": "string",
                        "mapping": {
                            "type": "text"
                        }
                    }
                },
                {
                    "string_fields": {
                        "match": "*",
                        "match_mapping_type": "string",
                        "mapping": {
                            "type": "keyword"
                        }
                    }
                },
                {
                    "double_fields": {
                        "match": "*",
                        "match_mapping_type": "double",
                        "mapping": {
                            "type": "double"
                        }
                    }
                },
                {
                    "byte_fields": {
                        "match": "*",
                        "match_mapping_type": "byte",
                        "mapping": {
                            "type": "byte"
                        }
                    }
                },
                {
                    "short_fields": {
                        "match": "*",
                        "match_mapping_type": "short",
                        "mapping": {
                            "type": "short"
                        }
                    }
                },
                {
                    "integer_fields": {
                        "match": "*",
                        "match_mapping_type": "integer",
                        "mapping": {
                            "type": "integer"
                        }
                    }
                },
                {
                    "long_fields": {
                        "match": "*",
                        "match_mapping_type": "long",
                        "mapping": {
                            "type": "long"
                        }
                    }
                },
                {
                    "date_fields": {
                        "match": "*",
                        "match_mapping_type": "date",
                        "mapping": {
                            "type": "date"
                        }
                    }
                },
                {
                    "geo_point_fields": {
                        "match": "*",
                        "match_mapping_type": "geo_point",
                        "mapping": {
                            "type": "geo_point"
                        }
                    }
                }
            ],
            "properties": {
                "0": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "artcleid": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "against": {
                    "type": "integer"
                },
                "user_name": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "comments_num": {
                    "ignore_malformed": true,
                    "type": "integer"
                },
                "channel": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "sign": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "created_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "type": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "content": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "article_id": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "uid": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "total": {
                    "ignore_malformed": true,
                    "type": "integer"
                },
                "cmt_id": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "praise_num": {
                    "type": "integer"
                },
                "posted_time": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "posted_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "item": {
                    "properties": {
                        "uid": {
                            "type": "long"
                        },
                        "cmt_id": {
                            "type": "long"
                        },
                        "user_name": {
                            "type": "keyword",
                            "ignore_above": 256,
                            "fields": {
                                "raw": {
                                    "type": "text",
                                    "analyzer": "ik_max_word",
                                    "search_analyzer": "ik_max_word"
                                }
                            }
                        },
                        "praise_num": {
                            "ignore_malformed": true,
                            "type": "integer"
                        },
                        "content": {
                            "type": "text",
                            "analyzer": "ik_max_word",
                            "search_analyzer": "ik_max_word"
                        },
                        "post_time": {
                            "format": "strict_date_optional_time||epoch_millis",
                            "type": "date"
                        }
                    }
                },
                "comments": {
                    "properties": {
                        "cmt_id": {
                            "type": "keyword",
                            "ignore_above": 256
                        },
                        "user_name": {
                            "type": "keyword",
                            "ignore_above": 256,
                            "fields": {
                                "raw": {
                                    "type": "text",
                                    "analyzer": "ik_max_word",
                                    "search_analyzer": "ik_max_word"
                                }
                            }
                        },
                        "location": {
                            "type": "keyword",
                            "ignore_above": 256,
                            "fields": {
                                "raw": {
                                    "type": "text",
                                    "analyzer": "ik_max_word",
                                    "search_analyzer": "ik_max_word"
                                }
                            }
                        },
                        "content": {
                            "type": "text",
                            "analyzer": "ik_max_word",
                            "search_analyzer": "ik_max_word"
                        },
                        "post_time": {
                            "format": "strict_date_optional_time||epoch_millis",
                            "type": "date"
                        }
                    }
                },
                "ip": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "agree": {
                    "type": "integer"
                },
                "reply_count": {
                    "ignore_malformed": true,
                    "type": "integer"
                },
                "wb_img": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "post_time": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "site": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "next_sync_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "replylist": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "location": {
                    "type": "keyword",
                    "ignore_above": 256,
                    "fields": {
                        "raw": {
                            "type": "text",
                            "analyzer": "ik_max_word",
                            "search_analyzer": "ik_max_word"
                        }
                    }
                },
                "create_at": {
                    "type": "long"
                },
                "is_following": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "status": {
                    "type": "integer"
                }
            }
        }
    }
}'
```



