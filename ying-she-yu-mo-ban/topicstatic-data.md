**话题静态数据**

索引：`topic_static_data`

类型：`topic_static_data`

创建索引`topic_static_data`

```
curl -XPUT http://127.0.0.1:9222/topic_static_data
```

`mapping`

```
curl -XPUT http://127.0.0.1:9222/_template/topic_static_data -d '
{
  "template": "topic_static_data*",
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
        "latest_sync_at": {
          "format": "strict_date_optional_time||epoch_millis",
          "type": "date"
        },
        "next_sync_at": {
          "format": "strict_date_optional_time||epoch_millis",
          "type": "date"
        },
        "title": {
          "type": "text",
          "analyzer": "ik_max_word",
          "search_analyzer": "ik_max_word",
          "fields": {
            "standard": {
              "type": "text",
              "analyzer": "standard",
              "search_analyzer": "standard"
            }
          }
        },
        "host_id": {
          "type": "keyword"
        },
        "category": {
          "type": "keyword"
        },
        "location": {
          "type": "keyword"
        },
        "tag": {
          "type": "keyword"
        },
        "status": {
          "type": "keyword"
        },
        "location": {
          "type": "keyword"
        },
        "content": {
          "type": "text",
          "analyzer": "ik_max_word",
          "search_analyzer": "ik_max_word",
          "fields": {
            "standard": {
              "type": "text",
              "analyzer": "standard",
              "search_analyzer": "standard"
            }
          }
        },
        "is_monitored": {
          "type": "boolean"
        },
        "monitored_priority": {
          "type": "float"
        },
        "monitor_cycle": {
          "type": "float"
        },
        "refresh_status": {
          "type": "boolean"
        }
      }
    }
  }
}'

```



