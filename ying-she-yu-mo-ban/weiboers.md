元数据

```
{
  "_index": "weiboers",
  "_type": "weiboer",
  "_id": "2100962065",
  "_version": 2,
  "_score": 1,
  "_source": {
    "username": null,
    "name": "Jashem",
    "intro": "外表正太，内心却有三百六十五道裂痕，每道裂痕上书春夏秋冬四字，沧桑到妖。",
    "gender": 0,
    "vip": 0,
    "verify": 0,
    "fans_count": 131,
    "follower_count": 7,
    "weibo_count": 2,
    "level": 2,
    "last_weibo_at": "2011-11-09T00:07:51.000Z",
    "info": "简介： 外表正太，内心却有三百六十五道裂痕，每道裂痕上书春夏秋冬四字，沧桑到妖。",
    "location_str": "山西 太原",
    "birthday_str": "1989年12月21日",
    "sexual": "",
    "relationship": "",
    "email": "",
    "tags": [ ],
    "updated_at": "2015-06-05T11:58:44.800Z",
    "sys_tags": [ ],
    "_id": "2100962065"
  }
}
```

使用 `Reindex Api`，重新索引

```
curl -XPOST http://localhost:9222/_reindex?requests_per_second=100000 -d '
{
  "source": {
    "remote": {
      "host": "http://10.0.0.1:9200"
    },
    "index": "weiboers",
    "size": 100000
  },
  "dest": {
    "index": "weiboers",
    "type": "weiboer"
  },
  "script": {
    "inline": "ctx._source.uid = ctx._source.remove(\"_id\");"
  }
}'
```

`Mapping`（`weiboers 28.0Gi/55.9Gi    52.1M`）

`"refresh_interval" : "60s"`、`"number_of_replicas" : "1"`、`"number_of_shards" : "5"`

```
curl -XPUT http://localhost:9222/_template/weiboers -d '
{
    "template": "weiboers*",
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
                "relationship_agg": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "gender": {
                    "type": "long"
                },
                "status_info": {
                    "type": "keyword",
                    "ignore_above": 256,
                    "fields": {
                        "raw": {
                            "type": "text",
                            "analyzer":"ik_max_word",
                            "search_analyzer": "ik_max_word"
                        }
                    }
                },
                "follower_count": {
                    "type": "long"
                },
                "uid": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "updated_at": {
                    "type": "date"
                },
                "province_agg": {
                    "type": "keyword",
                    "ignore_above": 256
                },
                "intro": {
                    "type": "text",
                    "analyzer":"ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "verify": {
                    "type": "long"
                },
                "company": {
                    "type": "keyword",
                    "ignore_above": 256,
                    "fields": {
                        "raw": {
                            "type": "text",
                            "analyzer":"ik_max_word",
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
                    "type": "long"
                },
                "weibo_count": {
                    "type": "long"
                },
                "email": {
                    "type": "keyword",
                    "ignore_above": 256,
                    "fields": {
                        "raw": {
                            "type": "text",
                            "analyzer":"ik_max_word",
                            "search_analyzer": "ik_max_word"
                        }
                    }
                },
                "info": {
                    "type": "text",
                    "analyzer":"ik_max_word",
                    "search_analyzer": "ik_max_word"
                },
                "status_updated_at": {
                    "type": "date"
                },
                "birthday_date_agg": {     
                    "type": "date"
                },
                "industry_str": {
                    "type": "keyword",
                    "ignore_above": 256,
                    "fields": {
                        "raw": {
                            "type": "text",
                            "analyzer":"ik_max_word",
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
                            "analyzer":"ik_max_word",
                            "search_analyzer": "ik_max_word"
                        }
                    }
                },
                "level": {
                    "type": "long"
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
                            "analyzer":"ik_max_word",
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
                    "type": "long"
                },
                "last_weibo_at": {
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
                            "analyzer":"ik_max_word",
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
                            "analyzer":"ik_max_word",
                            "search_analyzer": "ik_max_word"
                        }
                    }
                },
                "status": {
                    "type": "long"
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



