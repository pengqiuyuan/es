# 天涯论坛（tianya\_news）

旧索引：`tianya_news`

新索引：`tianya_news`

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 帖子ID | id | 字符串 |
| 帖子标题 | title | 字符串 |
| 帖子链接 | url | 字符串 |
| 帖子内容 | content | 字符串 |
| 帖子作者 | host | 字符串 |
| 发帖时间 | published\_at | 日期 |
| 帖子点击数 | clicks\_num | 数值 |
| 帖子回复数 | replays\_num | 数值 |
| 爬取时间 | crawled\_at | 日期 |

注意：插入数据时，问题ID字段值覆盖`elasticsearch`的元数据`_id`，如下所示 `_id`和`questionId`（移除）重复

部分数据：

```text
{
  "_index": "tianya_news",
  "_type": "tianya_news",
  "_id": "19550593",
  "_score": 1,
  "_source": {
    "title": "蔡学镛在各种动态语言中为什么比较偏爱 REBOL？"
  }
}
```

创建索引`tianya_news`

```text
curl -XPUT http://127.0.0.1:9222/tianya_news
```

`mapping`，添加 `xpack` 执行需要用户名密码

```text
curl -u 用户名:密码 -XPUT http://127.0.0.1:9222/_template/tianya_news -d '
{
    "template": "tianya_news*",
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
                "crawled_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "published_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "id": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "title": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "url": {
                    "type": "keyword"
                },
                "content": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "host": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "clicks_num": {
                    "type": "integer"
                },
                "replays_num": {
                    "type": "integer"
                }
            }
        }
    }
}'
```

