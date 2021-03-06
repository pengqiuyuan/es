# qie\_logs

索引：`qie_logs`

类型：`qie_logs`

**文章**

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 企鹅号ID | penguin\_id | String |
| 头像图片链接 | avatar\_img | String |
| 企鹅号名称 | name | String |
| 企鹅号简介 | introduction | String |
| 关注量 | follower\_count | Number |
| 粉丝量 | fans\_count | Number |
| 浏览量 | read\_count | Number |
| 抓取时间 | crawled\_at | Date |

创建索引`qie_logs`

```text
PUT /qie_logs
```

`mapping`

```text
PUT /_template/qie_logs
{
  "template": "qie_logs*",
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
      "dynamic_templates": [{
        "message_field": {
          "match": "message",
          "match_mapping_type": "string",
          "mapping": {
            "type": "text"
          }
        }
      }, {
        "string_fields": {
          "match": "*",
          "match_mapping_type": "string",
          "mapping": {
            "type": "keyword"
          }
        }
      }, {
        "double_fields": {
          "match": "*",
          "match_mapping_type": "double",
          "mapping": {
            "type": "double"
          }
        }
      }, {
        "long_fields": {
          "match": "*",
          "match_mapping_type": "long",
          "mapping": {
            "type": "long"
          }
        }
      }, {
        "date_fields": {
          "match": "*",
          "match_mapping_type": "date",
          "mapping": {
            "type": "date"
          }
        }
      }, {
        "geo_point_fields": {
          "match": "*",
          "match_mapping_type": "geo_point",
          "mapping": {
            "type": "geo_point"
          }
        }
      }],
      "properties": {
        "crawled_at": {
          "format": "strict_date_optional_time||epoch_millis",
          "type": "date"
        },
        "penguin_id": {
          "type": "keyword"
        },
        "avatar_img": {
          "type": "keyword"
        },
        "introduction": {
          "type": "text",
          "analyzer": "ik_max_word",
          "search_analyzer": "ik_max_word"
        },
        "tieba_id": {
          "type": "keyword"
        },
        "follower_count": {
          "type": "long"
        },
        "fans_count": {
          "type": "long"
        },
        "read_count": {
          "type": "long"
        }
      }
    }
  }
}
```

