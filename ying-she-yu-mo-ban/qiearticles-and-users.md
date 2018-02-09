索引：`qie_articles_and_users`

类型：`qie_articles_and_users`

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
| 发布时间 | published\_at | Date |
| 资源ID | resource\_id | String |
| 文章标题 | title | String |
| 文章内容 | content | String |
| 文章图片 | images | String |
| 评论量 | comment\_count | Number |
| 点赞量 | up\_count | Number |
| 播放量 | play\_count | Number |
| 类型 | type | Number |

创建索引`qie_articles_and_users`

```
PUT /qie_articles_and_users
```

`mapping`

```
PUT /_template/qie_articles_and_users
{
  "template": "qie_articles_and_users*",
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
        "published_at": {
          "format": "strict_date_optional_time||epoch_millis",
          "type": "date"
        },
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
        "name": {
          "type": "keyword"
        },
        "introduction": {
          "type": "text",
          "analyzer": "ik_max_word",
          "search_analyzer": "ik_max_word"
        },
        "follower_count": {
          "type": "integer"
        },
        "fans_count": {
          "type": "integer"
        },
        "read_count": {
          "type": "integer"
        },
        "resource_id": {
          "type": "keyword"
        },
        "title": {
          "type": "text",
          "analyzer": "ik_max_word",
          "search_analyzer": "ik_max_word"
        },
        "content": {
          "type": "text",
          "analyzer": "ik_max_word",
          "search_analyzer": "ik_max_word"
        },
        "images": {
          "type": "keyword"
        },
        "comment_count": {
          "type": "integer"
        },
        "up_count": {
          "type": "integer"
        },
        "play_count": {
          "type": "integer"
        },
        "type": {
          "type": "integer"
        }
      }
    }
  }
}
```



