二、**按话题查询获取原文**

`POST` `http://127.0.0.1/stq/api/v1/rowlet/findEsTextByTopic`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
startDate为起始时间（含），必填。
endDate为结束时间（不含），必填。
category为数据源 tw、fb，必填
sortField为排序字段，必填。
    tw（默认 created_at 发布时间）：repost_count（转发）, comment_count（评论）, up_count（点赞）
    fb（默认 created_at 发布时间）：repost_count（转发）, comment_count（评论）, up_count（点赞）
pageSize，必填。获取多少条
hotTopics，话题集合。必填，不可为空
```

`BODY` 体：

```
twitter

{
	"startDate": "2017-01-01",
	"endDate": "2017-12-31",
	"category": "tw",
	"sortField": "repost_count",
	"pageSize": "1",
	"hotTopics": ["climatechange"]
}
```

`response` Es查询有保存计算指标

`Twitter`

```
{
	"tw": [{
		"_index": "twitter_articles",
		"_type": "twitter_articles",
		"_source": {
			"leader": {
				"continent": 4,
				"country": 8,
				"sortName": "Tom",
				"flag": "ikols",
				"gender": "M",
				"created_at": "2018-05-08T15:45:53.778Z",
				"birth": "1947",
				"isBR": "f",
				"classification": "senator",
				"is_deleted": false,
				"updated_at": "2018-05-08T15:45:53.778Z",
				"province": 124,
				"__v": 0,
				"name": "Tom Carper",
				"term": "2018",
				"_id": 972,
				"state": "Delaware",
				"tag": "P",
				"party": "D"
			},
			"possibly_sensitive": false,
			"reply_count_str": "8",
			"created_at": "2017-12-18T19:34:29.000Z",
			"truncated": false,
			"source": "<a href=\"http://twitter.com\" rel=\"nofollow\">Twitter Web Client</a>",
			"reply_count": 8,
			"crawled_at": "2018-05-12T16:52:26.287Z",
			"retweet_count": 57,
			"retweeted": false,
			"favorite_count_str": "74",
			"is_quote_status": false,
			"entities": {
				"urls": [{
					"display_url": "theguardian.com/us-news/2017/d…",
					"indices": [154, 177],
					"expanded_url": "https://www.theguardian.com/us-news/2017/dec/18/trump-drop-climate-change-national-security-strategy",
					"url": "https://t.co/UF9t45uQfD"
				}],
				"hashtags": [{
					"indices": [34, 48],
					"text": "climatechange"
				}],
				"user_mentions": [{
					"indices": [105, 119],
					"screen_name": "DeptofDefense",
					"id_str": "66369181",
					"name": "U.S. Dept of Defense",
					"id": 66369181
				}, {
					"indices": [121, 128],
					"screen_name": "USArmy",
					"id_str": "8775672",
					"name": "U.S. Army",
					"id": 8775672
				}, {
					"indices": [130, 137],
					"screen_name": "USNavy",
					"id_str": "54885400",
					"name": "U.S. Navy",
					"id": 54885400
				}, {
					"indices": [139, 145],
					"screen_name": "USGAO",
					"id_str": "34274380",
					"name": "U.S. GAO",
					"id": 34274380
				}, {
					"indices": [147, 152],
					"screen_name": "NASA",
					"id_str": "11348282",
					"name": "NASA",
					"id": 11348282
				}],
				"symbols": []
			},
			"full_text": "President Trump may not recognize #climatechange as a national security threat, but you know who does? \n\n@DeptofDefense.\n@USArmy.\n@USNavy.\n@USGAO.\n@NASA.\nhttps://t.co/UF9t45uQfD",
			"id_str": "942840512054288386",
			"retweet_count_str": "57",
			"display_text_range": [0, 177],
			"favorite_count": 74,
			"lang": "en",
			"user": {
				"utc_offset": -14400,
				"friends_count": 1336,
				"profile_image_url_https": "https://pbs.twimg.com/profile_images/378800000497501114/77d2bd85a246e66e8f77670018fbaaca_normal.jpeg",
				"listed_count": 1706,
				"profile_background_image_url": "http://pbs.twimg.com/profile_background_images/206172638/moran_twitter.jpg",
				"default_profile_image": false,
				"favourites_count": 1091,
				"description": "Husband, father, proud @USNavy veteran and former governor. U.S. Senator for Delaware and ranking member @EPWDems",
				"created_at": "2011-02-09T19:46:42.000Z",
				"is_translator": false,
				"profile_background_image_url_https": "https://pbs.twimg.com/profile_background_images/206172638/moran_twitter.jpg",
				"protected": false,
				"screen_name": "SenatorCarper",
				"id_str": "249787913",
				"profile_link_color": "1E3F66",
				"is_translation_enabled": false,
				"translator_type": "none",
				"id": 249787913,
				"geo_enabled": true,
				"profile_background_color": "D6DDE1",
				"lang": "en",
				"has_extended_profile": true,
				"profile_sidebar_border_color": "BAC1C4",
				"profile_text_color": "737373",
				"verified": true,
				"profile_image_url": "http://pbs.twimg.com/profile_images/378800000497501114/77d2bd85a246e66e8f77670018fbaaca_normal.jpeg",
				"time_zone": "Eastern Time (US & Canada)",
				"url": "http://t.co/0KSoFFra6j",
				"contributors_enabled": false,
				"profile_background_tile": false,
				"profile_banner_url": "https://pbs.twimg.com/profile_banners/249787913/1466708976",
				"entities": {
					"description": {
						"urls": []
					},
					"url": {
						"urls": [{
							"display_url": "carper.senate.gov",
							"indices": [0, 22],
							"expanded_url": "http://www.carper.senate.gov",
							"url": "http://t.co/0KSoFFra6j"
						}]
					}
				},
				"statuses_count": 6994,
				"follow_request_sent": false,
				"followers_count": 82641,
				"profile_use_background_image": true,
				"default_profile": false,
				"following": false,
				"name": "Senator Tom Carper",
				"location": "Delaware",
				"profile_sidebar_fill_color": "E2E8EB",
				"notifications": false
			},
			"favorited": false
		},
		"_id": "942840512054288386",
		"sort": [57]
	}],
	"count": "17",
	"message": "任务成功"
}
```



