旧索引：`latest_news_articles`

新索引：`news_articles`

部分数据：

```
{
    "_id": "8b3ed44146955abd324fe100cd38c686",
    "_version": 1,
    "_score": 1,
    "_source": {
        "skipType": "text",
        "skipID": 0,
        "post_time": "2017-03-19T04:21:00.000Z",
        "title": "网易红彩APP下载2年前男篮逆转抗韩歌唱祖国 国足添喜长沙真福地疆媒:感谢辽宁感谢&quot;表&quot; 让纷争过去今晚看场好球半决赛场均轰20+12+3帽 生涯首个总决赛等着他男篮众国手道贺国足:轮到足球克韩 长沙真是福地",
        "newsid": "CG7UHLRV0005877V",
        "votecount": 391,
        "replyCount": 482,
        "source": "网易体育晨运荟网易体育网易体育",
        "setid": 0,
        "channel": "CBA",
        "docid": "CG7UHLRV0005877V",
        "content": "　　网易体育月日报道：　　今晚，中国男足在世界杯预选赛中击败老对手韩国队，对于之前一场未胜的国足来说，今晚比赛的胜利实在令人欢欣鼓舞，外界早就喊出了“保卫长沙”的口号。而就在两年前，中国男篮正是在“长沙保卫战”中逆转韩国，进而一路披荆斩棘重夺亚锦赛冠军，当时球迷现场高唱《歌唱祖国》的场景仍然历历在目。!#　　在出征那一届亚锦赛之前，由于曾折戟马尼拉，仁川亚运会的战绩也不佳，因此，中国男篮并不被外界所看好。没想到的是，困难来的那么早，小组赛第二战，韩国队在老将梁东根和赵成愍的带领下一上来就连投连中，将比分拉开，中国男篮这边仅靠易建联和周鹏苦苦支撑，上半场一度落后了分之多。　　第三节最后几分钟，中国男篮开始发力追赶，不断迫近比分。这场比赛，周琦成为球队的英雄，最后一分钟，周琦的扣篮将比分反超为，此时，从赛场的某个角落传出了《歌唱祖国》的歌声。　　渐渐地，歌声开始蔓延开来，全场球迷都高声唱着《歌唱祖国》，队员们深受鼓舞，最终完成了大逆转。终场时刻，《歌唱祖国》的歌声，伴随着男篮将士们的怒吼声交织在一起，被定格为中国男篮历史上一幅经典的画面。　　从那场比赛之后，中国男篮如同打通了任督二脉，他们一路向前，最终夺得冠军，并拿到了最为珍贵的里约奥运会的入场券。那届比赛后，很多球迷回忆起最难忘的瞬间时，不是半决赛复仇伊朗，也不是决赛战胜菲律宾夺冠，而是小组赛在《歌唱祖国》的歌声中逆转韩国，那一战，打出血性，打出了精气神。　　今晚，长沙再次成为国足的福地，击败韩国，恭喜中国足球国家队！　　作者： 强森!",
        "comment_uri": "https://comment.api.163.com/api/v1/products/a2869674571f77b5a0867c3d71db5856/threads/CG7UHLRV0005877V/app/comments/newList?format=building&headLimit=3&ibc=newsappios&offset=0&limit=10&tailLimit=2&timestamp=1486547457.106524&showLevelThreshold=5",
        "comment_num": 10,
        "site": "app_netease",
        "created_at": "2017-03-27T01:14:40.095Z"
    }
}
```

新索引需要移除的重复字段：略

创建索引`news_articles`

```
curl -XPUT http://127.0.0.1:9222/news_articles
```

`mapping`

```
curl -XPUT http://127.0.0.1:9222/_template/news_articles -d '
{
    "template": "news_articles*",
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
                "comment_num": {
                    "type": "integer"
                },
                "uinname": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "comments_num": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "channel": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "skipID": {
                    "type": "integer"
                },
                "created_at": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "source": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "title": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "coment_id": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "content": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "sid": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "newsid": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "cmt_id": {
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
                "id": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "imglinks": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "summary": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "votecount": {
                    "type": "integer"
                },
                "item_id": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "docid": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "pname": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "comment_uri": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "uri": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "post_time": {
                    "format": "strict_date_optional_time||epoch_millis",
                    "type": "date"
                },
                "replyCount": {
                    "type": "integer"
                },
                "site": {
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
                "group_id": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "skipType": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "setid": {
                    "type": "integer"
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



