旧索引：`sogou_weixin_articles`

新索引：`sogou_weixin_articles`

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 账号ID | biz | 字符串 |
| 消息ID | mid | 字符串 |
| 消息偏移 | idx | 字符串 |
| 文章标题 | title | 字符串 |
| 文章摘要 | description | 字符串 |
| 文章内容 | content | 字符串 |
| 指定链接 | source\_url | 字符串 |
| 插图链接 | cover | 字符串 |
| 作者 | author | 字符串 |
| 账号名 | username | 字符串 |
| 中文名 | nickname | 字符串 |
| 发布日期 | publish\_date | 字符串 |
| 发布时间 | publish\_time | 日期 |
| 阅读量 | read | 数值 |
| 点赞量 | like | 数值 |
| 采集链接 | crawl\_url | 字符串 |
| 文章链接 | content\_url | 字符串 |
| 采集时间 | create\_time | 日期 |

创建索引`sogou_weixin_articles`

```
curl -XPUT http://127.0.0.1:9222/sogou_weixin_articles
```

`mapping`

```
curl -XPUT http://127.0.0.1:9222/_template/zhihu_questions -d '
{
    "template": "sogou_weixin_articles*",
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
                "biz": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "mid": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "idx": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "title": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "description": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "content": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "source_url": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "cover": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "author": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "username": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "nickname": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "publish_date": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "publish_time": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "read": {
                    "type": "integer"
                },
                "like": {
                    "type": "integer"
                },
                "crawl_url": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "content_url": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "create_time": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                }
            }
        }
    }
}'


```



