旧索引：`news_articles`

新索引：`old_news_articles`

部分数据：

```
{
    "_id": "b6bb1ba5907d75916b8e9ed0164b198d",
    "_score": 6.383625,
    "_source": {
        "__v": 0,
        "url": "https://kuaibao.qq.com/s/20170212B0367Z00",
        "title": "过了一年，孩子长大了一岁，你成长了吗？",
        "source": "掌门1对1",
        "post_time": "1970-01-01T00:00:00.000Z",
        "sign": "2016-05",
        "site": "app_tian",
        "content": "小编写在前面过了一年，家里的孩子又长大了一岁，马上要开学了，你要为他准备好新书包，新文具。是啊，他又要进入新的学期，学习新的知识。学期末，你会问孩子考试考了多少分，班级排名多少，学了多少知识，可是，你呢？2016年，为人父母，你成长了多少？还是只是一心把所有的关注点都聚焦在孩子身上，却从来没有做好自己的事。你是否学习了新的技能，你是否提高了工作能力，你是否又学习了新的育儿知识，你是否……如果你的答案是没有，那么，你的孩子又能优秀到哪里去呢？为人父母，最重要的是首先做好自己的事，其次才是孩子。2017年，给自己一个好的开始，和掌门共读，每周一起共读一本好书，提升自我的素养，学习育儿知识，而不只是做一个一边玩手机的低头族，一边却责怪孩子不争气。上周内容回顾>>>>时文选粹寒冷的冬天，他只要供暖7天，背后的原因看哭了……孩子那么爱你，你却因为这1件危险的事，错过他的爱！本周中奖名单本周中奖名单出炉咯！以下10位读者均可获得《时文选粹》纸质书1本。来领奖请以上中奖读者在24小时内按照“姓名+电话+邮寄地址”的格式将您的邮寄方式发送给我们，小编老师将会尽快安排寄出纸质书籍喔。",
        "status": 3,
        "video_links": [],
        "image_links": [
            null,
            null
        ],
        "created_at": "2017-02-15T13:47:32.863Z",
        "last_modified_at": "1970-01-01T00:00:00.000Z",
        "id": "b6bb1ba5907d75916b8e9ed0164b198d"
    }
}
```

创建索引`old_news_articles`

```
curl -XPUT http://127.0.0.1:9222/old_news_articles
```

`mapping`

```
curl -XPUT http://127.0.0.1:9222/_template/old_news_articles -d '
{
    "template": "old_news_articles*",
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
                "date": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "channel": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "sign": {
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
                "type": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "source_uri": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "news_id": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "topic_source_id": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "show_num": {
                    "type": "integer"
                },
                "__v": {
                    "type": "integer"
                },
                "praise_num": {
                    "type": "integer"
                },
                "total_num": {
                    "type": "integer"
                },
                "reply_num": {
                    "type": "integer"
                },
                "id": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "imglinks": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "image": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "image_uri": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "pre_url": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "real_comment_num": {
                    "type": "integer"
                },
                "category_link": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "post_date": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "status": {
                    "type": "integer"
                },
                "comment_num": {
                    "type": "integer"
                },
                "uinname": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "comments_num": {
                    "type": "integer",
                    "ignore_malformed": true
                },
                "created_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "title": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "dispraise_num": {
                    "type": "integer"
                },
                "content": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "last_modified_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "sid": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "newsid": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "tian": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "commentid": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "docuri": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "summary": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "comments": {
                    "properties": {
                        "cmt_id": {
                            "type": "keyword",
                            "ignore_above": 256
                        },
                        "user_name": {
                            "type": "keyword",
                            "ignore_above": 256
                        },
                        "ip": {
                            "type": "keyword",
                            "ignore_above": 256
                        },
                        "location": {
                            "type": "keyword",
                            "ignore_above": 256
                        },
                        "content": {
                            "type": "text",
                            "analyzer": "ik_max_word",
                            "search_analyzer": "ik_max_word"
                        },
                        "post_time": {
                            "type": "keyword",
                            "ignore_above": 256
                        }
                    }
                },
                "item_id": {
                    "type": "string"
                },
                "docid": {
                    "type": "string"
                },
                "comment_uri": {
                    "type": "string"
                },
                "comment_id": {
                    "type": "string"
                },
                "uri": {
                    "type": "string"
                },
                "post_time": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "source_link": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "url": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "site": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "group_id": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "image_links": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "category": {
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



