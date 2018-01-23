索引：`toutiao_logs`

类型：`toutiao_logs`

**文章**

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 用户ID | toutiaor\_id | String |
| 粉丝量 | fans\_count | Number |
| 关注量 | follower\_count | Number |
| 更新时间 | date | Date |

创建索引`toutiao_logs`

```
PUT /toutiao_logs
```

`mapping`

```
PUT /_template/toutiao_logs
{
  "template": "toutiao_logs*",
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
        "date": {
          "format": "strict_date_optional_time||epoch_millis",
          "type": "date"
        },
        "toutiaor_id": {
          "type": "keyword"
        },
        "fans_count": {
          "type": "integer"
        },
        "follower_count": {
          "type": "integer"
        }
      }
    }
  }
}
```



