旧索引：`tieba_posts`

新索引：`tieba_posts`、类型名称：`tieba_posts`

部分数据：

```
{
    "_id": "4995640819",
    "_score": 1,
    "_source": {
        "id": "4995640819",
        "tieba_id": 537,
        "title": "比利林恩的中场战事-极限特工3-西游伏妖篇-功夫瑜伽，高清版",
        "author_name": "物旧yes",
        "author_id": "2719429553",
        "reply_num": 201,
        "content": " 二楼地址",
        "date": "2017-02-24T06:26:00.000Z",
        "created_at": 1488509090,
        "created_at_date": null,
        "updated_at": null,
        "updated_at_date": null
    }
}
```

创建索引`tieba_posts`

```
curl -XPUT http://127.0.0.1:9222/tieba_posts
```

`mapping`

```
curl -XPUT http://127.0.0.1:9222/_template/tieba_posts -d '
{
    "template": "tieba_posts*",
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
                "author_name": {
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
                "date": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "updated_at": {
                    "type": "long"
                },
                "created_at": {
                    "type": "long"
                },
                "tieba_id": {
                    "type": "long"
                },
                "reply_num": {
                    "type": "integer"
                },
                "id": {
                    "index": "not_analyzed",
                    "type": "string"
                },
                "author_id": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "title": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "updated_at_date": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "content": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "created_at_date": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                }
            }
        }
    }
}'
```



