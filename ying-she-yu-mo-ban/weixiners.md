旧索引：`weixiners`

新索引：`weixiners` 新类型：`weixiner`

元数据

```
{
    "_index": "weixiners",
    "_type": "weixiner",
    "_id": "MjM5NDE4MzIyMQ==",
    "_version": 3,
    "_score": 1,
    "_source": {
        "openid": "oIWsFt26nxiRG_F8ta8Jliq3dbVY",
        "name": "美丽之路",
        "username": "usashop",
        "intro": "关注世界,关注中国,只为让自己生活得更好!",
        "certification": "该帐号服务由重庆美丽之路电子商务有限公司提供.",
        "crawled_at": "2015-01-21T03:41:19.904Z",
        "updated_at": "2015-06-16T10:54:27.184Z",
        "tags": [ ],
        "_id": "MjM5NDE4MzIyMQ=="
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
    "index": "weixiners",
    "size": 100000
  },
  "dest": {
    "index": "weixiners",
    "type": "weixiner"
  },
  "script": {
    "inline": "ctx._source.uid = ctx._source.remove(\"_id\"); ctx._source.score = 1.0"
  }
}'
```

创建索引`weixiners`

```
curl -XPUT http://127.0.0.1:9222/weixiners
```

`Mapping`（`weixiners 738Mi/1.43Gi    504k`）

`"refresh_interval" : "60s"`、`"number_of_replicas" : "1"`、`"number_of_shards" : "15"`

索引名称（索引前缀名称为`weixiners`的都能匹配到，名称为`weixiners`的`mapping`模板，`*`为通配符）：如，`weixiners`

```
curl -XPUT http://localhost:9222/_template/weixiners -d '
{
  "template" : "weixiners*",
  "settings" : {  
    "refresh_interval" : "60s",  
    "number_of_replicas" : "1",  
    "number_of_shards" : "15"
  },
  "mappings" : {
    "_default_" : {
      "_all" : {"enabled" : true},
      "_source" : { "enabled" : true },
      "dynamic_templates" : [ {
        "message_field" : {
          "match" : "message",
          "match_mapping_type" : "string",
          "mapping" : {
            "type" : "text"
          }
        }
      }, {
        "string_fields" : {
          "match" : "*",
          "match_mapping_type" : "string",
          "mapping" : {
            "type" : "keyword"
          }
        }
      }, {
        "double_fields" : {
          "match" : "*",  
          "match_mapping_type" : "double",
          "mapping" : { "type" : "double"}
        }
      }, {
        "byte_fields" : {
          "match" : "*",
          "match_mapping_type" : "byte",
          "mapping" : { "type" : "byte"}
        }
      }, {
        "short_fields" : {
          "match" : "*",
          "match_mapping_type" : "short",
          "mapping" : { "type" : "short"}
        }
      }, {
        "integer_fields" : {
          "match" : "*",
          "match_mapping_type" : "integer",
          "mapping" : { "type" : "integer"}
        }
      }, {
        "long_fields" : {
          "match" : "*",
          "match_mapping_type" : "long",
          "mapping" : { "type" : "long"}
        }
      }, {
        "date_fields" : {
          "match" : "*",
          "match_mapping_type" : "date",
          "mapping" : { "type" : "date"}
        }
      }, {
        "geo_point_fields" : {
          "match" : "*",
          "match_mapping_type" : "geo_point",
          "mapping" : { "type" : "geo_point"}
        }
      } ],
      "properties" : {
        "@timestamp": { "type": "date"  },
        "score": {
            "type": "float"
        },
        "openid": {
            "type": "keyword"
        },
        "name": {
            "type": "keyword"
        },  
        "username": {
            "type": "keyword"
        },
        "intro": {
            "type": "text",
            "analyzer":"ik_max_word",
            "search_analyzer": "ik_max_word"
        },  
        "certification": {
            "type": "keyword",
            "fields": {
                "raw": {
                  "type": "text",
                  "analyzer":"ik_max_word",
                  "search_analyzer": "ik_max_word"
                }
            }        
        },
        "crawled_at": {
            "type": "date"
        },
        "updated_at": {
            "type": "date"
        },
        "tags": {
            "type": "keyword"
        },
        "categories": {
            "type": "keyword"        
            }
      }
    }
  }
}'
```



