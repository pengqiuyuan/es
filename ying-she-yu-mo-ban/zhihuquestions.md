# zhihu\_questions

旧索引：`zhihu_questions`

新索引：`zhihu_questions`

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 问题标题 | title | 字符串 |
| 问题关键字分类 | topics | 数组 |
| 问题描述 | desc | 字符串 |
| 关注者数 | follows\_num | 数值 |
| 被浏览数 | views\_num | 数值 |
| 回答数 | answers\_num | 数值 |
| 问题爬取时间 | created\_at | 日期 |
| 问题发布时间 | published\_at | 日期 |
| 问题作者 | author | 字符串 |
| 问题作者ID | author\_id | 字符串 |

注意：插入数据时，问题ID字段值覆盖`elasticsearch`的元数据`_id`，如下所示 `_id`和`questionId`（移除）重复

部分数据：

```text
{
  "_index": "zhihu_questions",
  "_type": "zhihu_questions",
  "_id": "19550593",
  "_score": 1,
  "_source": {
    "title": "蔡学镛在各种动态语言中为什么比较偏爱 REBOL？",
    "topics": [
      "「未归类」话题_19776751"
    ],
    "desc": "null",
    "follows_num": 13,
    "views_num": 132194,
    "answers_num": 1,
    "published_at": "2010-12-23T07:41:28.000Z",
    "author": "杨昆",
    "author_id": "37c382e4fa4703f18b2ac7ccc589c1bc"
  }
}
```

创建索引`zhihu_questions`

```text
curl -XPUT http://127.0.0.1:9222/zhihu_questions
```

`mapping`

```text
curl -XPUT http://127.0.0.1:9222/_template/zhihu_questions -d '
{
  "template": "zhihu_questions*",
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
        "created_at": {
          "format": "strict_date_optional_time||epoch_millis",
          "type": "date"
        },
        "published_at": {
          "format": "strict_date_optional_time||epoch_millis",
          "type": "date"
        },
        "topics": {
          "type": "keyword",
          "ignore_above": 256
        },
        "answers_num": {
          "type": "integer"
        },
        "title": {
          "type": "text",
          "analyzer": "ik_max_word",
          "search_analyzer": "ik_max_word"
        },
        "views_num": {
          "type": "long"
        },
        "desc": {
          "type": "text",
          "analyzer": "ik_max_word",
          "search_analyzer": "ik_max_word"
        },
        "follows_num": {
          "type": "integer"
        },
        "author": {
          "type": "keyword",
          "ignore_above": 256
        },
        "author_id": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    }
  }
}'
```

