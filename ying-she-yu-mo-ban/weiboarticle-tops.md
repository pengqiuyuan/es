# weibo\_article\_tops

旧索引：`weibo_article_tops`

新索引：`weibo_article_tops`

部分数据：

```text
{
    "_index": "weibo_article_tops",
    "_type": "weibo_article_top",
    "_id": "4069783320189644",
    "_score": 1,
    "_source": {
        "is_hot": false,
        "is_pin": false,
        "id_short": "EthnK0NkM",
        "weiboer_id": "1777194770",
        "content": "转发微博",
        "content_full": "转发微博 //@慰慰娃娃 #侠探杰克#这个作品有阿汤哥非常有看头我希望自己可以去看一下这部电影的说。 ​​​​",
        "published_at": "2017-01-30T16:56:59.000Z",
        "repost_count": 0,
        "comment_count": 0,
        "up_count": 0,
        "repost_id": "4025425304592297",
        "repost_level": 1,
        "app_source": "微博 weibo.com",
        "href": "/1777194770/EthnK0NkM?from=page_1005051777194770_profile&wvr=6&mod=weibotime",
        "crawled_at": "2017-02-08T22:02:30.137Z",
        "video_links": [],
        "music_links": [],
        "web_links": [],
        "username": null,
        "name": "18岁的俊健Angelie",
        "intro": "他还没有填写个人简介",
        "gender": 0,
        "vip": 0,
        "verify": 0,
        "fans_count": 70,
        "follower_count": 318,
        "weibo_count": 6122,
        "level": 17,
        "last_weibo_at": "2015-05-30T05:47:40.000Z",
        "info": "",
        "location_str": "江苏 无锡",
        "birthday_str": "",
        "sexual": "",
        "relationship": "",
        "email": "",
        "tags": [
            "可爱控",
            "摩羯座",
            "吃货",
            "堀北真希",
            "唱歌",
            "starking"
        ],
        "province_agg": "江苏",
        "city_agg": "无锡",
        "_id": "4069783320189644"
    }
}
```

创建索引`weibo_article_tops`

```text
curl -XPUT http://127.0.0.1:9222/weibo_article_tops
```

`mapping`

```text
curl -XPUT http://127.0.0.1:9222/_template/weibo_article_tops -d '
{
    "template": "weibo_article_tops*",
    "settings": {
        "refresh_interval": "60s",
        "number_of_replicas": "1",
        "number_of_shards": "45"
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
                "comment_count": {
                    "type": "integer"
                },
                "relationship_agg": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "repost_count": {
                    "type": "integer"
                },
                "repost_level": {
                    "type": "integer"
                },
                "gender": {
                    "type": "integer"
                },
                "web_links": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "weiboer_id": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "up_count": {
                    "type": "integer"
                },
                "crawled_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "follower_count": {
                    "type": "integer"
                },
                "music_links": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "content": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "province_agg": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "is_hot": {
                    "type": "boolean"
                },
                "intro": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "verify": {
                    "type": "integer"
                },
                "company": {
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
                "video_links": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "constellation_agg": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "content_full": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "href": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "published_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "relationship": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "vip": {
                    "type": "long"
                },
                "weibo_count": {
                    "type": "integer"
                },
                "email": {
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
                "info": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "birthday_date_agg": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "industry_str": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "birthday_str": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "level": {
                    "type": "integer"
                },
                "city_agg": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "location_str": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "is_pin": {
                    "type": "boolean"
                },
                "tags": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "app_source": {
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
                "fans_count": {
                    "type": "integer"
                },
                "id_short": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "last_weibo_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "edu_str_agg": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "name": {
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
                "repost_id": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "county_agg": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "sexual": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "edu_str": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "username": {
                    "type": "keyword",
                    "ignore_above": 256,
                    "fields": {
                        "raw": {
                            "type": "text",
                            "analyzer": "ik_max_word",
                            "search_analyzer": "ik_max_word"
                        }
                    }
                }
            }
        }
    }
}'
```

