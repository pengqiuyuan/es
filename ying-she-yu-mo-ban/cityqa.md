索引：`city_qa_articles`

类型：`city_qa_articles`

**文章**

| 字段含义 | 字段名称 | 数据类型 | 是否分词 |
| :--- | :--- | :--- | :--- |
| 站点名称 | website | String | 不分词 |
| 来源 | source | String | 分词+不分词 |
| 链接 | url | String | 不分词 |
| 标题 | title | String | 分词 |
| 摘要 | summary | Number | 不分词 |
| 内容 | content | Number | 分词 |
| 发布时间 | publish\_time | Date |  |
| 抓取时间 | create\_time | Date |  |

创建索引`city_qa_articles`

```
PUT /city_qa_articles
```

`mapping`

```
PUT /_template/city_qa_articles
{
    "template": "city_qa_articles*",
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
            "dynamic_templates": [{
                "message_field": {
                    "match": "message",
                    "match_mapping_type": "string",
                    "mapping": {
                        "type": "text"
                    }
                }
            }, {
                "string_fields": {
                    "match": "*",
                    "match_mapping_type": "string",
                    "mapping": {
                        "type": "keyword"
                    }
                }
            }, {
                "double_fields": {
                    "match": "*",
                    "match_mapping_type": "double",
                    "mapping": {
                        "type": "double"
                    }
                }
            }, {
                "long_fields": {
                    "match": "*",
                    "match_mapping_type": "long",
                    "mapping": {
                        "type": "long"
                    }
                }
            }, {
                "date_fields": {
                    "match": "*",
                    "match_mapping_type": "date",
                    "mapping": {
                        "type": "date"
                    }
                }
            }],
            "properties": {
                "publish_time": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "create_time": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "website": {
                    "type": "keyword"
                },
                "source": {
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
                "url": {
                    "type": "keyword"
                },
                "title": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "summary": {
                    "type": "keyword"
                },
                "content": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                }
            }
        }
    }
}
```



