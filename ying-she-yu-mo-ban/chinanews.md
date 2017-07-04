新索引：`china_news`、类型名称：`china_news`

部分数据：

```
暂略
```

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 新闻标题 | news\_title | 字符串 |
| 新闻URL | news\_url | 字符串 |
| 新闻发表时间 | published\_at | 日期 |
| 新闻正文 | news\_text | 字符串 |
| 新闻类型 | news\_type | 字符串 |
| 新闻来源 | news\_source | 字符串 |
| 抓取时间 | crawled\_at | 日期 |

创建索引`china_news`

```
curl -XPUT http://127.0.0.1:9222/china_news
```

`mapping`

```
curl -u idatage:abc@123456 -XPUT http://127.0.0.1:9222/_template/china_news -d '
{
    "template": "china_news*",
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
                }
            ],
            "properties": {
                "published_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "crawled_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "news_title": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "news_url": {
                    "type": "keyword"
                },
                "news_text": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "news_source": {
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
                "news_type": {
                    "type": "keyword",
                    "ignore_above": 256
                }
            }
        }
    }
}
'
```



