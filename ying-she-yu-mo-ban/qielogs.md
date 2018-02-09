索引：`qie_logs`

类型：`qie_logs`

**文章**

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 贴吧ID | tieba\_id | String |
| 贴吧关注量 | ba\_m\_num | Number |
| 贴吧主题量 | ba\_t\_num | Number |
| 时间版本号 | version | Date |
| 贴吧帖子量 | ba\_p\_num | Number |

创建索引`qie_logs`

```
PUT /qie_logs
```

`mapping`

```
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
        "version": {
          "format": "strict_date_optional_time||epoch_millis",
          "type": "date"
        },
        "tieba_id": {
          "type": "keyword"
        },
        "ba_m_num": {
          "type": "integer"
        },
        "ba_t_num": {
          "type": "integer"
        },
        "ba_p_num": {
          "type": "integer"
        }
      }
    }
  }
}
```



