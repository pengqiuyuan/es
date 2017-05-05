旧索引：`zhihu_questions`

新索引：`zhihu_questions`

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 问题ID（覆盖 es 中元数据 \_id ，移除） | questionId | 字符串 |
| 问题标题 | title | 字符串 |
| 问题关键字分类 | topics | 数组 |
| 问题描述 | desc | 字符串 |
| 关注者数 | followsNum | 数值 |
| 被浏览数 | viewsNum | 数值 |
| 回答数 | answersNum | 数值 |
| 问题评论量 | commentsNum | 数值 |
| 问题时间 | createdAt | 日期 |

注意：插入数据时，问题ID字段值覆盖`elasticsearch`的元数据`_id`，如下所示 `_id`和`questionId`（移除）重复

部分数据：

```
{
    "_id": "19551476",
    "_version": 1,
    "_score": 1,
    "_source": {
        "title": "你如何评估街旁开放平台？",
        "topics": "19551979",
        "desc": "一个很早期做开放的案例，或许值得关注一下子。 显示全部",
        "followsNum": 64,
        "viewsNum": 0,
        "answersNum": 15,
        "questionId": "19551476"
    }
}
```

创建索引`zhihu_questions`

```
curl -XPUT http://127.0.0.1:9222/zhihu_questions
```

`mapping`

```
curl -XPUT http://127.0.0.1:9222/_template/zhihu_questions -d '
{
    "template": "zhihu_questions*",
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
                "createdAt": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "topics": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "answersNum": {
                    "type": "integer"
                },
                "title": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "viewsNum": {
                    "type": "integer"
                },
                "desc": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "followsNum": {
                    "type": "integer"
                },
                "commentsNum": {
                    "type": "integer"
                }
            }
        }
    }
}'
```



