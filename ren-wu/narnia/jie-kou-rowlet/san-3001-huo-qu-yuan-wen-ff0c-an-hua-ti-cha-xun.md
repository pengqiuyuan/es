二、**按话题查询获取原文**

`POST` `http://127.0.0.1/stq/api/v1/rowlet/findEsTextByUserId`

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
	"startDate": "2016-10-09",
	"endDate": "2017-12-10",
	"category": "tw",
	"sortField": "repost_count",
	"pageSize": "2",
	"hotTopics": ["DefendDACA"]
}

```

`response` Es查询有保存计算指标

`Twitter`

```
{
	"tw": [{
		"_index": "rowlet_twitter_articles",
		"_type": "rowlet_twitter_articles",
		"_source": {
			"extended_entities": {},
			"possibly_sensitive": false,
			"created_at": "2017-09-02T23:12:01.000Z",
			"truncated": false,
			"source": "<a href=\"http://sproutsocial.com\" rel=\"nofollow\">Sprout Social</a>",
			"retweeted_status": false,
			"reply_count": "3253",
			"quoted_status_id": 0,
			"retweet_count": "50165",
			"retweeted": false,
			"is_quote_status": false,
			"entities": {
				"urls": [],
				"hashtags": ["DefendDACA"],
				"user_mentions": [],
				"symbols": []
			},
			"id_str": "904119753287110656",
			"quoted_status_id_str": "",
			"favorite_count": "105663",
			"text": "There is nothing crueler than deporting kids who grew up in America back to a country they don’t even know. #DefendDACA",
			"lang": "en",
			"matching_rules": [],
			"user": {
				"utc_offset": -28800,
				"friends_count": 716,
				"profile_image_url_https": "https://pbs.twimg.com/profile_images/877902898889412608/6Vfu5kVd_normal.jpg",
				"profile_background_image_url": "http://pbs.twimg.com/profile_background_images/688156932/fb90b2e73377f4603feedb04df168d29.jpeg",
				"listed_count": 6466,
				"default_profile_image": false,
				"favourites_count": 213,
				"created_at": "2009-04-11T00:42:07.000Z",
				"description": "Senator for California. Former CA Attorney General. Dedicated to fighting for justice & giving voice to the voiceless. Wife, s-mom, sister, aunt. Aspiring chef.",
				"is_translator": false,
				"profile_background_image_url_https": "https://pbs.twimg.com/profile_background_images/688156932/fb90b2e73377f4603feedb04df168d29.jpeg",
				"protected": false,
				"screen_name": "KamalaHarris",
				"id_str": "30354991",
				"profile_link_color": "4468A6",
				"is_translation_enabled": false,
				"translator_type": "none",
				"id": 30354991,
				"geo_enabled": true,
				"profile_background_color": "FFFFFF",
				"lang": "en",
				"has_extended_profile": false,
				"profile_sidebar_border_color": "FFFFFF",
				"profile_text_color": "333333",
				"verified": true,
				"profile_image_url": "http://pbs.twimg.com/profile_images/877902898889412608/6Vfu5kVd_normal.jpg",
				"time_zone": "Pacific Time (US & Canada)",
				"contributors_enabled": false,
				"url": "http://t.co/IbL01p7pYJ",
				"profile_background_tile": false,
				"profile_banner_url": "https://pbs.twimg.com/profile_banners/30354991/1485113375",
				"entities": {
					"description": {
						"urls": []
					},
					"url": {
						"urls": [{
							"display_url": "KamalaHarris.org",
							"indices": [0, 22],
							"expanded_url": "http://KamalaHarris.org",
							"url": "http://t.co/IbL01p7pYJ"
						}]
					}
				},
				"statuses_count": 7097,
				"follow_request_sent": false,
				"following": false,
				"default_profile": false,
				"profile_use_background_image": false,
				"followers_count": 1215705,
				"name": "Kamala Harris",
				"location": "California",
				"profile_sidebar_fill_color": "FFFFFF",
				"notifications": false
			},
			"favorited": false
		},
		"_id": "904119753287110656",
		"sort": [50165]
	}, {
		"_index": "rowlet_twitter_articles",
		"_type": "rowlet_twitter_articles",
		"_source": {
			"extended_entities": {},
			"possibly_sensitive": false,
			"created_at": "2017-09-04T01:54:02.000Z",
			"truncated": false,
			"source": "<a href=\"http://twitter.com\" rel=\"nofollow\">Twitter Web Client</a>",
			"retweeted_status": true,
			"reply_count": "3253",
			"quoted_status_id": 0,
			"retweet_count": "50165",
			"retweeted": false,
			"is_quote_status": false,
			"entities": {
				"urls": [],
				"hashtags": ["DefendDACA"],
				"user_mentions": [{
					"indices": [3, 16],
					"screen_name": "KamalaHarris",
					"id_str": "30354991",
					"name": "Kamala Harris",
					"id": 30354991
				}],
				"symbols": []
			},
			"id_str": "904522913436635136",
			"quoted_status_id_str": "",
			"favorite_count": "105663",
			"text": "RT @KamalaHarris: There is nothing crueler than deporting kids who grew up in America back to a country they don’t even know. #DefendDACA",
			"lang": "en",
			"matching_rules": [],
			"user": {
				"utc_offset": -28800,
				"friends_count": 716,
				"profile_image_url_https": "https://pbs.twimg.com/profile_images/877902898889412608/6Vfu5kVd_normal.jpg",
				"profile_background_image_url": "http://pbs.twimg.com/profile_background_images/688156932/fb90b2e73377f4603feedb04df168d29.jpeg",
				"listed_count": 6466,
				"default_profile_image": false,
				"favourites_count": 213,
				"created_at": "2009-04-11T00:42:07.000Z",
				"description": "Senator for California. Former CA Attorney General. Dedicated to fighting for justice & giving voice to the voiceless. Wife, s-mom, sister, aunt. Aspiring chef.",
				"is_translator": false,
				"profile_background_image_url_https": "https://pbs.twimg.com/profile_background_images/688156932/fb90b2e73377f4603feedb04df168d29.jpeg",
				"protected": false,
				"screen_name": "KamalaHarris",
				"id_str": "30354991",
				"profile_link_color": "4468A6",
				"is_translation_enabled": false,
				"translator_type": "none",
				"id": 30354991,
				"geo_enabled": true,
				"profile_background_color": "FFFFFF",
				"lang": "en",
				"has_extended_profile": false,
				"profile_sidebar_border_color": "FFFFFF",
				"profile_text_color": "333333",
				"verified": true,
				"profile_image_url": "http://pbs.twimg.com/profile_images/877902898889412608/6Vfu5kVd_normal.jpg",
				"time_zone": "Pacific Time (US & Canada)",
				"contributors_enabled": false,
				"url": "http://t.co/IbL01p7pYJ",
				"profile_background_tile": false,
				"profile_banner_url": "https://pbs.twimg.com/profile_banners/30354991/1485113375",
				"entities": {
					"description": {
						"urls": []
					},
					"url": {
						"urls": [{
							"display_url": "KamalaHarris.org",
							"indices": [0, 22],
							"expanded_url": "http://KamalaHarris.org",
							"url": "http://t.co/IbL01p7pYJ"
						}]
					}
				},
				"statuses_count": 7097,
				"follow_request_sent": false,
				"following": false,
				"default_profile": false,
				"profile_use_background_image": false,
				"followers_count": 1215705,
				"name": "Kamala Harris",
				"location": "California",
				"profile_sidebar_fill_color": "FFFFFF",
				"notifications": false
			},
			"favorited": false
		},
		"_id": "904522913436635136",
		"sort": [50165]
	}],
	"message": "任务成功"
}
```



