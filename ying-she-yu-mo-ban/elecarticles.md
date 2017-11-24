索引：`elec_articles`

类型：`elec_articles`

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 文章url | url | 字符串 |
| 发布时间 | published\_at | 日期 |
| 文章标题 | title | 字符串 |
| 发布者 | publisher | 字符串 |
| 来源 | source | 字符串 |
| 内容 | content | 字符串 |
| 爬取时间 | created\_at | 日期 |

创建索引`elec_articles`

```
curl -XPUT http://127.0.0.1:9222/elec_articles
```

`mapping`

```
curl -XPUT http://127.0.0.1:9222/_template/elec_articles -d '
{
  "template": "elec_articles*",
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
        "created_at": {
          "format": "strict_date_optional_time||epoch_millis",
          "type": "date"
        },
        "published_at": {
          "format": "strict_date_optional_time||epoch_millis",
          "type": "date"
        },
        "title": {
          "type": "text",
          "analyzer": "ik_max_word",
          "search_analyzer": "ik_max_word"
        },
        "url": {
          "type": "keyword"
        },
        "publisher": {
          "type": "keyword"
        },
        "source": {
          "type": "keyword"
        },
        "content": {
          "type": "text",
          "analyzer": "ik_max_word",
          "search_analyzer": "ik_max_word"
        }
      }
    }
  }
}'
```



