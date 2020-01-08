# tieba\_posts

旧索引：`tieba_posts`

新索引：`tieba_posts`、类型名称：`tieba_posts`

部分数据：

```text
{
    "_id": "4995640819",
    "_score": 1,
    "_source": {
        "title": "比利林恩的中场战事-极限特工3-西游伏妖篇-功夫瑜伽，高清版",
        "author_name": "物旧yes",
        "author_id": "2719429553",
        "reply_num": 201,
        "content": " 二楼地址",
        "date": "2017-02-24T06:26:00.000Z",
        "created_at": 1488509090000,
        "last_reply_at": null,
        "tieba_id": null
    }
}
```

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 帖子标题 | title | 字符串 |
| 作者名称 | author\_name | 字符串 |
| 作者ID | author\_id | 字符串 |
| 回复数 | reply\_num | 数值 |
| 内容 | content | 字符串 |
| 帖子创建时间 | date | 日期 |
| 帖子爬取时间 | created\_at | 日期 |
| 帖子最后更新时间 | last\_reply\_at | 日期 |
| 所属贴吧 | tieba\_id | 字符串 |
| 贴吧关注量 | ba\_m\_num | 数值 |
| 贴吧主题量 | ba\_t\_num | 数值 |
| 贴吧帖子量 | ba\_p\_num | 数值 |

创建索引`tieba_posts`

```text
curl -XPUT http://127.0.0.1:9222/tieba_posts
```

`mapping`

```text
GET _template/tieba_posts

PUT /_template/tieba_posts
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
                    "ignore_above": 256
                },
                "date": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "last_reply_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "created_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "reply_num": {
                    "type": "integer"
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
                "content": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "tieba_id": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "ba_m_num": {
                    "type": "integer"
                },
                "ba_t_num": {
                    "type": "integer"
                },
                "ba_p_num": {
                    "type": "integer"
                }
            }
        }
    }
}
```

