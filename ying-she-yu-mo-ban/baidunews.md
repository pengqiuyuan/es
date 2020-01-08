# baidunews\_news

百度新闻

`index` 名称：`baidunews_news`

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 新闻ID（覆盖 es 中元数据 \_id ） | \_id | 字符串 |
| 关键字ID | keyId | 字符串 |
| 新闻链接 | url | 字符串 |
| 新闻标题 | title | 字符串 |
| 新闻来源 | author | 字符串 |
| 新闻摘要 | summary | 字符串 |
| 新闻发布时间 | publishedAt | 日期 |
| 新闻时间 | date | 字符串 |
| 新闻采集时间 | createdAt | 日期 |

注意：插入数据时，新闻ID字段值覆盖`elasticsearch`的元数据`_id`

创建索引`baidunews_news`

```text
curl -XPUT http://127.0.0.1:9222/baidunews_news
```

```text
curl -XPUT http://127.0.0.1:9222/_template/baidunews_news -d '
{
    "template": "baidunews_news*",
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
                "keyId": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "url": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "title": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "author": {
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
                "summary": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "publishedAt": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "date": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "createdAt": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                }
            }
        }
    }
}'
```

