```
curl -XPUT http://127.0.0.1:9222/cibao_index

curl -XPUT http://127.0.0.1:9222/_template/cibao_index -d '
{
  "template": "cibao_index*",
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
        }
      ],
      "properties": {
        "startDate": {
          "format": "strict_date_optional_time||epoch_millis",
          "type": "date"
        },
        "endDate": {
          "format": "strict_date_optional_time||epoch_millis",
          "type": "date"
        },
        "keywords": {
          "type": "keyword"
        },
        "source": {
          "type": "keyword",
          "ignore_above": 256
        },
        "volume": {
          "type": "long"
        },
        "actualVolume": {
          "type": "integer"
        },
        "exposure": {
          "type": "long"
        },
        "interactive": {
          "type": "integer"
        },
        "oldInteractive": {
          "type": "integer"
        },
        "forwardDepth": {
          "type": "integer"
        }
      }
    }
  }
}'
```



