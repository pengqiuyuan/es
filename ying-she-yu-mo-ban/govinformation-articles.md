```
url,webName,webChannelName,webType,webChannel,artContent,artTime,artFrom,artTitle
除了artTime文章时间,均为字符串类型
```

```
[{
  "id":"test",
  "index_name":"gov_information_articles",
  "type_name":"gov_information_articles",
  "artTime": "2018-04-27T20:46:20.000Z",
  "artContent":"ceshi11"
}]
```

创建索引`gov_information_articles`

```
PUT /gov_information_articles
```

`mapping`

```
PUT /_template/gov_information_articles
{
	"template": "gov_information_articles*",
	"settings": {
		"refresh_interval": "60s",
		"number_of_replicas": "1",
		"number_of_shards": "15",
		"index.mapping.total_fields.limit": 2000
	},
	"mappings": {
		"_default_": {
			"_all": {
				"enabled": false
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
				}
			],
			"properties": {
				"artTime": {
					"format": "strict_date_optional_time||epoch_millis",
					"type": "date"
				},
				"url": {
					"type": "keyword"
				},
				"webName": {
					"type": "keyword"
				},
				"webChannelName": {
					"type": "keyword"
				},
				"webType": {
					"type": "keyword"
				},
				"webChannel": {
					"type": "keyword"
				},
				"artContent": {
					"type": "text",
					"analyzer": "ik_max_word",
					"search_analyzer": "ik_max_word"
				},
				"artFrom": {
					"type": "keyword"
				},
				"artTitle": {
					"type": "keyword",					
					"fields": {
						"raw": {
							"type": "text",
							"analyzer": "ik_max_word",
							"search_analyzer": "ik_max_word"
						}
					}
				}
			}
		}
	}
}
```



