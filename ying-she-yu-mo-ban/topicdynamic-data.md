**话题动态数据**

索引：`topic_dynamic_data`

类型：`topic_dynamic_data`

创建索引`topic_dynamic_data`

```
curl -XPUT http://127.0.0.1:9222/topic_dynamic_data
```

`mapping`

```
curl -XPUT http://127.0.0.1:9222/_template/topic_dynamic_data -d '
{
  "template": "topic_dynamic_data*",
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
        "topic_id": {
          "type": "keyword"
        },
        "read_num": {
          "type": "keyword"
        },
        "comment_num": {
          "type": "keyword"
        },
        "fans": {
          "type": "keyword"
        },
        "read_num_pure": {
          "type": "float"
        },
        "comment_num_pure": {
          "type": "float"
        },
        "fans_pure": {
          "type": "float"
        },
        "is_fit": {
          "type": "boolean"
        }
      }
    }
  }
}'

```



