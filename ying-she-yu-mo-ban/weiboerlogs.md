# weiboer\_logs

索引：`weiboer_logs`

类型：`weiboer_logs`

**文章**

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 用户ID | weiboer\_id | String |
| 关注量 | fans\_count | Number |
| 粉丝量 | follower\_count | Number |
| 发帖量 | weibo\_count | Number |
| 爬取时间 | crawled\_at | Date |

创建索引`weiboer_logs`

```text
PUT /weiboer_logs
```

`mapping`

```text
PUT /_template/weiboer_logs
{
  "template": "weiboer_logs*",
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
        "weiboer_id": {
          "type": "keyword"
        },
        "fans_count": {
          "type": "integer"
        },
        "follower_count": {
          "type": "integer"
        },
        "weibo_count": {
          "type": "integer"
        }
      }
    }
  }
}
```

