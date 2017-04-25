旧索引：`new_news_comments`

新索引：`news_comments`

部分数据：

```
{
    "_id": "a95d6cc936ec5638c43c942a44844007",
    "_score": 1.1613197,
    "_source": {
        "cmt_id": "1841126425",
        "user_name": "274",
        "location": "广东云浮",
        "post_time": "2017-03-29T01:20:48.000Z",
        "content": "看你头像和名字都不正常",
        "artcleid": "1aa2c228373edc1d1ce1ecde012edaf3",
        "site": "app_tencent",
        "channel": "",
        "created_at": "2017-03-29T01:31:22.604Z"
    }
}
```

创建索引`news_comments`

```
curl -XPUT http://127.0.0.1:9222/news_comments
```

`mapping`（原索引字段 `reply_count`、`total`、`praise_num`，类型为字符串）[测试](/fen-ci/ce-shi-ignore-malformed.md)

```
    "reply_count": {
        "ignore_malformed": true,
        "type": "integer"
    },
    "total": {
        "ignore_malformed": true,
        "type": "integer"
    },    
    "praise_num": {
        "ignore_malformed": true,
        "type": "integer"
    }
```

```
curl -XPUT http://127.0.0.1:9222/_template/news_comments -d '
{
    "template": "news_comments*",
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
                "artcleid": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "user_name": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "ip": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "channel": {
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
                "created_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "reply_count": {
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
                },
                "site": {
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
                "total": {
                    "ignore_malformed": true,
                    "type": "integer"
                },
                "cmt_id": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "praise_num": {
                    "ignore_malformed": true,
                    "type": "integer"
                },
                "location": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "is_following": {
                    "type": "keyword",
                    "ignore_above": 256
                }
            }
        }
    }
}'
```



