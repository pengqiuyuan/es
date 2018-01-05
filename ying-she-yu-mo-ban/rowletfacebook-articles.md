索引：`rowlet_facebook_articles`

类型：`rowlet_facebook_articles`

**文章**

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 发布时间 | create\_at | Date |
|  | last\_untime | String |
| 用户信息 | user | Object |
| 内容 | text | String |
| 评论数 | comment\_num | Number |
| 点赞量 | likes\_num | Number |
| 分享数 | share\_count | Number |

**用户**

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 用户名 | name | String |
| 用户id | id | String |
| 当前位置 | current\_location | String |
| 生日 | birthday | String |
| 主页类别 | category | String |
| 粉丝量 | fan\_count | Nubmer |
| 邮箱 | emails | String |
| 家乡 | hometown | String |
| Facebook 主页链接 | link | String |
| 地址 | location | Object |
| 个人网站 | website | String |
| 喜欢量 | likes\_count | Number |
| 个人简介 | about | String |
| 个人描述 | description | String |
| 是否认证 | verification\_status | Boolean |

创建索引`rowlet_facebook_articles`

```
PUT /rowlet_facebook_articles
```

`mapping`

```
PUT /_template/rowlet_facebook_articles
{
  "template": "rowlet_facebook_articles*",
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
        "create_at": {
          "format": "strict_date_optional_time||epoch_millis",
          "type": "date"
        },
        "last_untime": {
          "type": "keyword"
        },
        "text": {
          "type": "text",
          "analyzer": "ik_max_word",
          "search_analyzer": "ik_max_word"
        },
        "comment_num": {
          "type": "long"
        },
        "likes_num": {
          "type": "long"
        },
        "share_count": {
          "type": "long"
        },
        "user": {
            "properties": {
                "id": {
                  "type": "keyword"
                },
                "name": {
                  "type": "keyword"
                },
                "current_location": {
                  "type": "keyword"
                },
                "birthday": {
                  "type": "keyword"
                },
                "category": {
                  "type": "keyword"
                },
                "fan_count": {
                  "type": "long"
                },
                "emails": {
                  "type": "keyword"
                },
                "hometown": {
                  "type": "keyword"
                },
                "link": {
                  "type": "keyword"
                },
                "location": {
                    "properties": {
                        "city": {
                          "type": "keyword"
                        },
                        "country": {
                          "type": "keyword"
                        },
                        "state": {
                          "type": "keyword"
                        },
                        "street": {
                          "type": "keyword"
                        },
                        "zip": {
                          "type": "keyword"
                        }
                    }    
                },
                "website": {
                  "type": "keyword"
                },
                "likes_count": {
                  "type": "long"
                },
                "about": {
                  "type": "text",
                  "analyzer": "ik_max_word",
                  "search_analyzer": "ik_max_word"
                },
                "description": {
                  "type": "text",
                  "analyzer": "ik_max_word",
                  "search_analyzer": "ik_max_word"
                },
                "verification_status": {
                  "type": "boolean"
                }
            }
        }
      }
    }
  }
}
```



