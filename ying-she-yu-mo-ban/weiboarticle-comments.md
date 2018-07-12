

```
{
	"id": "4236281494343340",
	"text": "时间会证明一切",
	"created_at": "2018-05-05T03:41:00.000Z",
	"created_at_str": "5月5日 11:41",
	"crawled_at": "2018-07-12T08:11:57.459Z",
	"user": {
		"id": "2366593365",
		"screen_name": "上天赐予1"
	},
	"commented_article_id": "4236280822994436"
}

```

创建索引`weibo_article_comments`

```
PUT /weibo_article_comments
```

`mapping`

```
PUT /_template/weibo_article_comments
{
	"template": "weibo_article_comments*",
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
			}],
			"properties": {
				"created_at": {
					"format": "strict_date_optional_time||epoch_millis",
					"type": "date"
				},
				"crawled_at": {
					"format": "strict_date_optional_time||epoch_millis",
					"type": "date"
				},
				"created_at_str": {
					"type": "keyword"
				},
				"commented_article_id": {
					"type": "keyword"
				},
				"text": {
					"type": "text",
					"analyzer": "ik_max_word",
					"search_analyzer": "ik_max_word"
				},
				"user": {
					"properties": {
						"id": {
							"type": "keyword"
						},
						"screen_name": {
							"type": "keyword"
						}
					}
				}
			}
		}
	}
}
```





