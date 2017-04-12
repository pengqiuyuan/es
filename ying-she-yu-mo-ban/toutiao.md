`toutiao`

元数据，来源`mongodb`

```
{
    "_id": "6403210803599639041",
    "duration": [
        0
    ],
    "title": [
        "失婚者（三）"
    ],
    "crawled_at": 1491820893.4040003,
    "down_count": [
        0
    ],
    "up_count": [
        0
    ],
    "type": [
        0
    ],
    "comments_count": [
        0
    ],
    "images": [],
    "behot_time": 1490863693,
    "labels": [
        "婚姻",
        "崇源院",
        "怀孕",
        "故事"
    ],
    "read _count": [
        12
    ],
    "content": "阿江是一个知识分子的家庭出来的孩子...。",
    "toutiaor_id": "3739949332"
}
```

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 头条号ID | toutiaor\_id | 字符串 |
| 资源ID | item\_id | 字符串 |
| 文章标题 | title | 字符串 |
| 文章内容 | content | 字符串 |
| 文章图片 | images | 数组（链接） |
| 关键分词 | labels | 数组 |
| 阅读量 | read\_count | 数值 |
| 评论量 | comment\_count | 数值 |
| 点赞量 | up\_count | 数值 |
| 踩量 | down\_count | 数值 |
| 发布时间 | published\_at | 日期（时间戳） |
| 抓取时间 | crawled\_at | 日期（时间戳） |
| 类型 | type | 数值 |
| 视频时长 | duration | 数值（秒） |



```
curl -XPUT http://127.0.0.1:9222/_template/toutiao -d '
{
    "template": "toutiao*",
    "settings": {
        "refresh_interval": "60s",
        "number_of_replicas": "1",
        "number_of_shards": "5"
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
                "toutiaor_id": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "item_id": {
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
                "images": {
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
                "labels": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "read_count": {
                    "type": "integer"
                },
                "comment_count": {
                    "type": "integer"
                },
                "up_count": {
                    "type": "integer"
                },
                "down_count": {
                    "type": "integer"
                },
                "published_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "crawled_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "type": {
                    "type": "integer"
                },
                "duration": {
                    "type": "integer"
                }
            }
        }
    }
}'
```



