索引（`_index`）：`tech_news`，同一个`_index`，不同`_type`

类型（`_type`）

36kr（文章、快讯）：`tech_36kr_articles`、`tech_q36kr_articles`

虎嗅（资讯）：`tech_huxiu_articles`

雷锋（文章）：`tech_leiphone_articles`

创业邦（文章）：`tech_cyzone_articles`

钛媒体（文章）：`tech_tmtpost_articles`

极客公园（文章）：`tech_geekpark_articles`

砍柴网（文章）：`tech_ikanchai_articles`

前瞻网（文章）：`tech_qianzhan_articles`

互联网分析沙龙（文章）：`tech_techxue_articles`

品玩（文章）：`tech_pingwest_articles`

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 标题 | title | 字符串 |
| 内容 | content | 字符串 |
| 发布日期 | published\_at | 日期 |
| 简介 | desc | 字符串 |
| 图片 | pics | 数组 |
| 链接 | url | 字符串 |
| 文章分类 | type | 字符串 |
| 关键词 | keywords | 数组 |
| 点赞量 | supports\_num | 数值 |
| 收藏量 | collections\_num | 数值 |
| 评论量 | comments\_num | 数值 |
| 浏览量 | views\_num | 数值 |
| 作者 ID 或者链接 | author\_id | 字符串 |

创建索引`tech_news`

```
curl -XPUT http://127.0.0.1:9222/tech_news
```

`mapping`

```
curl -XPUT http://127.0.0.1:9222/_template/tech_news -d '
{
    "template": "tech_news*", 
    "settings": {
        "refresh_interval": "60s", 
        "number_of_replicas": "1", 
        "number_of_shards": "30"
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
                "published_at": {
                    "format": "strict_date_optional_time||epoch_millis", 
                    "type": "date"
                }, 
                "desc": {
                    "type": "text", 
                    "analyzer": "ik_max_word", 
                    "search_analyzer": "ik_max_word"
                }, 
                "pics": {
                    "type": "keyword", 
                    "ignore_above": 256
                }, 
                "url": {
                    "type": "keyword", 
                    "ignore_above": 256
                }, 
                "type": {
                    "type": "keyword", 
                    "ignore_above": 256
                }, 
                "keywords": {
                    "type": "keyword", 
                    "ignore_above": 256
                }, 
                "supports_num": {
                    "type": "integer", 
                    "ignore_malformed": true
                }, 
                "collections_num": {
                    "type": "integer", 
                    "ignore_malformed": true
                }, 
                "comments_num": {
                    "type": "integer", 
                    "ignore_malformed": true
                }, 
                "views_num": {
                    "type": "integer", 
                    "ignore_malformed": true
                }, 
                "author_id": {
                    "type": "keyword", 
                    "ignore_above": 256
                }
            }
        }
    }
}'
```



