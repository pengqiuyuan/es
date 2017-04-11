`weibo_articles_and_weiboers`

```
curl -XPUT http://localhost:9222/_template/weibo_articles_and_weiboers -d '
{
    "template": "weibo_articles_and_weiboers*",
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
                "@timestamp": {
                    "type": "date"
                },
                "is_hot": {
                    "type": "boolean"
                },
                "is_pin": {
                    "type": "boolean"
                },
                "id_short": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "weiboer_id": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "content": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "content_full": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "published_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "repost_count": {
                    "type": "integer"
                },
                "comment_count": {
                    "type": "integer"
                },
                "up_count": {
                    "type": "integer"
                },
                "repost_id": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "repost_level": {
                    "type": "integer"
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
                "href": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "crawled_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "video_links": {
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
                "music_links": {
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
                "web_links": {
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
                "weibo_articles_uid": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "relationship_agg": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "gender": {
                    "type": "integer"
                },
                "status_info": {
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
                "follower_count": {
                    "type": "integer"
                },
                "weiboers_uid": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "updated_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "province_agg": {
                    "type": "keyword",
                    "ignore_above": 256
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
                "constellation_agg": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "relationship": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "vip": {
                    "type": "integer"
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
                "status_updated_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "birthday_date_agg": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "industry_str": {
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
                "birthday_str": {
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
                "level": {
                    "type": "integer"
                },
                "city_agg": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "location_str": {
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
                "sys_tags": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "tags": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "fans_count": {
                    "type": "integer"
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
                    "ignore_above": 256,
                    "fields": {
                        "raw": {
                            "type": "text",
                            "analyzer": "ik_max_word",
                            "search_analyzer": "ik_max_word"
                        }
                    }
                },
                "status": {
                    "type": "integer"
                },
                "username": {
                    "type": "keyword",
                    "ignore_above": 256
                }
            }
        }
    }
}'
```



