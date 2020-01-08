# toutiaors

索引名称（索引前缀名称为`toutiaors`的都能匹配到，名称为`toutiaors`的`mapping`模板，`*`为通配符）：如，`toutiaors`

`index` 名称：`toutiaors`

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 头条号ID | id | 字符串 |
| 头像图片链接 | avatar\_img | 字符串 |
| 头条号名称 | name | 字符串 |
| 头条号简介 | introduction | 字符串 |
| 关注量 | follower\_count | 数值 |
| 粉丝量 | fans\_count | 数值 |
| 抓取时间 | crawled\_at | 日期 |

创建索引`toutiaors`

```text
curl -XPUT http://127.0.0.1:9222/toutiaors
```

```text
curl -XPUT http://127.0.0.1:9222/_template/toutiaors -d '
{
    "template": "toutiaors*",
    "settings": {
        "refresh_interval": "60s",
        "number_of_replicas": "1",
        "number_of_shards": "10"
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
                "id": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "avatar_img": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "name": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "introduction": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "follower_count": {
                    "type": "integer"
                },
                "fans_count": {
                    "type": "integer"
                },
                "crawled_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                }
            }
        }
    }
}'
```

