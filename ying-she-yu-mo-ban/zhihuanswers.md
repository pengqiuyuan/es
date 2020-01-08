# zhihu\_answers

索引：`zhihu_answers`

类型：`zhihu_answers`

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 简略回答 | excerpt | 字符串 |
| 发布时间 | published\_at | 日期 |
| 爬取时间 | created\_at | 日期 |
| 作者名字 | author\_name | 字符串 |
| 作者ID | author\_id | 字符串 |
| 关注作者人数 | author\_follower\_count | 数值 |
| 回答点赞量 | voteup\_count | 数值 |
| 回答回复量 | comment\_count | 数值 |
| 问题ID | question\_id | 字符串 |
| 回答完整内容 | content | 字符串 |

创建索引`zhihu_answers`

```text
curl -XPUT http://127.0.0.1:9222/zhihu_answers
```

`mapping`

```text
curl -XPUT http://127.0.0.1:9222/_template/zhihu_answers -d '
{
  "template": "zhihu_answers*",
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
        "excerpt": {
          "type": "text",
          "analyzer": "ik_max_word",
          "search_analyzer": "ik_max_word"
        },
        "author_name": {
          "type": "keyword",
          "ignore_above": 256
        },
        "author_id": {
          "type": "keyword",
          "ignore_above": 256
        },
        "author_follower_count": {
          "type": "integer"
        },
        "voteup_count": {
          "type": "integer"
        },
        "comment_count": {
          "type": "integer"
        },
        "question_id": {
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

