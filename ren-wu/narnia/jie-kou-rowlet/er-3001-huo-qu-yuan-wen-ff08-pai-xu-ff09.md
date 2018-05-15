二、**获取库中匹配到的结果集（Tw、Fb）**

`POST` `http://127.0.0.1/stq/api/v1/rowlet/findEsTextByUserId`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
keywords为查询关键字，必填。默认空字符串
startDate为起始时间（含），必填。
endDate为结束时间（不含），必填。
category为数据源 tw、fb，必填
ids为账号Id数组，必填。可以为空集合
sortField为排序字段，必填。
    tw（默认 created_at 发布时间）：repost_count（转发）, comment_count（评论）, up_count（点赞）
    fb（默认 created_at 发布时间）：repost_count（转发）, comment_count（评论）, up_count（点赞）
sort为排序 asc（升序）、desc（降序，默认）
pageNumber为第几页，默认1
pageSize为每页多少条，默认10
queryMode为查询模式，是否只返回text文本内容。simple、normal，必填。queryMode:"" 默认为 normal。
```

`BODY` 体：

```
twitter

{
	"startDate": "2017-01-01",
	"endDate": "2017-12-31",
	"category": "tw",
	"ids": ["164007407"],
	"keywords": "china",
	"sortField": "repost_count",
	"sort": "desc",
	"pageNumber": "1",
	"pageSize": "10",
	"queryMode": "normal"
}

facebook

{
	"startDate": "2017-01-01",
	"endDate": "2017-12-31",
	"category": "fb",
	"ids": ["1002391179791389"],
	"keywords": "china",
	"sortField": "comment_count",
	"sort": "asc",
	"pageNumber": "1",
	"pageSize": "10",
	"queryMode": "normal"
}
```

`response` Es查询有保存计算指标

`Twitter`

```
{
	"tw": [{
		"highlight": {
			"full_text": ["country in the world that isn’t participating, and we’re ceding leadership to <em>China</em>. 2/3"]
		},
		"_index": "twitter_articles",
		"_type": "twitter_articles",
		"_source": {
			"leader": {
				"continent": 4,
				"country": 8,
				"sortName": "Eliot",
				"flag": "ikols",
				"gender": "M",
				"assignment": "Agriculture\nTransportation and Infrastructure",
				"created_at": "2018-05-08T15:45:50.957Z",
				"birth": "1947",
				"isBR": "f",
				"classification": "representatives",
				"is_deleted": false,
				"updated_at": "2018-05-08T15:45:50.957Z",
				"province": 150,
				"district": "16th",
				"__v": 0,
				"name": "Eliot Engel",
				"_id": 742,
				"state": "New York",
				"tag": "P",
				"party": "D"
			},
			"in_reply_to_status_id_str": "946813502890692609",
			"in_reply_to_status_id": 946813502890692600,
			"reply_count_str": "5",
			"created_at": "2017-12-29T18:42:45.000Z",
			"in_reply_to_user_id_str": "164007407",
			"source": "<a href=\"http://twitter.com\" rel=\"nofollow\">Twitter Web Client</a>",
			"crawled_at": "2018-05-13T02:11:07.979Z",
			"retweet_count": 6,
			"retweeted": false,
			"in_reply_to_screen_name": "RepEliotEngel",
			"is_quote_status": false,
			"full_text": "@POTUS And, the #ParisAgreement was a critical step to fight climate change that would have cost us little or nothing. Allowing #climatechange to get worse is very expensive. Now we’re the only country in the world that isn’t participating, and we’re ceding leadership to China. 2/3",
			"id_str": "946813759196139523",
			"retweet_count_str": "6",
			"in_reply_to_user_id": 164007407,
			"favorite_count": 12,
			"lang": "en",
			"favorited": false,
			"truncated": false,
			"reply_count": 5,
			"favorite_count_str": "12",
			"entities": {
				"urls": [],
				"hashtags": [{
					"indices": [16, 31],
					"text": "ParisAgreement"
				}, {
					"indices": [128, 142],
					"text": "climatechange"
				}],
				"user_mentions": [{
					"indices": [0, 6],
					"screen_name": "POTUS",
					"id_str": "822215679726100480",
					"name": "President Trump",
					"id": 822215679726100500
				}],
				"symbols": []
			},
			"display_text_range": [7, 282],
			"user": {
				"utc_offset": -14400,
				"friends_count": 823,
				"profile_image_url_https": "https://pbs.twimg.com/profile_images/523095197983309825/3TdNyI76_normal.jpeg",
				"listed_count": 928,
				"profile_background_image_url": "http://pbs.twimg.com/profile_background_images/433324934715015168/OV0E-LLI.jpeg",
				"default_profile_image": false,
				"favourites_count": 121,
				"description": "Congressman representing parts of the Bronx and Westchester Counties in New York #NY16",
				"created_at": "2010-07-07T20:34:17.000Z",
				"is_translator": false,
				"profile_background_image_url_https": "https://pbs.twimg.com/profile_background_images/433324934715015168/OV0E-LLI.jpeg",
				"protected": false,
				"screen_name": "RepEliotEngel",
				"id_str": "164007407",
				"profile_link_color": "0084B4",
				"is_translation_enabled": false,
				"translator_type": "none",
				"id": 164007407,
				"geo_enabled": true,
				"profile_background_color": "EBE6CE",
				"lang": "en",
				"has_extended_profile": false,
				"profile_sidebar_border_color": "FFFFFF",
				"profile_text_color": "333333",
				"verified": true,
				"profile_image_url": "http://pbs.twimg.com/profile_images/523095197983309825/3TdNyI76_normal.jpeg",
				"time_zone": "Eastern Time (US & Canada)",
				"url": "http://t.co/BVwX9Ov3sA",
				"contributors_enabled": false,
				"profile_background_tile": false,
				"profile_banner_url": "https://pbs.twimg.com/profile_banners/164007407/1517494271",
				"entities": {
					"description": {
						"urls": []
					},
					"url": {
						"urls": [{
							"display_url": "engel.house.gov",
							"indices": [0, 22],
							"expanded_url": "http://engel.house.gov",
							"url": "http://t.co/BVwX9Ov3sA"
						}]
					}
				},
				"statuses_count": 3618,
				"follow_request_sent": false,
				"followers_count": 22996,
				"profile_use_background_image": true,
				"default_profile": false,
				"following": false,
				"name": "Eliot Engel",
				"location": "",
				"profile_sidebar_fill_color": "DDEEF6",
				"notifications": false
			}
		},
		"_id": "946813759196139523",
		"sort": [6]
	}],
	"count": "1",
	"message": "任务成功"
}
```

`Facebook`

```
{
	"fb": [{
		"highlight": {
			"text": ["<em>China</em> has much to gain and Russia much to lose as gas and oil becomes easier to transport around the world."]
		},
		"_index": "facebook_articles",
		"_type": "facebook_articles",
		"_source": {
			"comment_num": 0,
			"share_count": 3,
			"leader": {
				"continent": 4,
				"country": 8,
				"sortName": "The New York Times Books",
				"flag": "ikols",
				"gender": "S",
				"created_at": "2018-05-08T15:46:00.569Z",
				"isBR": "f",
				"is_deleted": false,
				"updated_at": "2018-05-08T15:46:00.569Z",
				"__v": 0,
				"name": "The New York Times Books",
				"_id": 2301,
				"tag": "M"
			},
			"hashtags": [],
			"mentions": [],
			"created_at": "2017-12-30T13:00:00.000Z",
			"text": "China has much to gain and Russia much to lose as gas and oil becomes easier to transport around the world.",
			"likes_num": 8,
			"ownerid": "1002391179791389",
			"permalink_url": "/nytbooks/posts/1749535868410246",
			"crawled_at": "2018-05-15T06:28:46.017Z",
			"user": {
				"website": "http://www.nytimes.com",
				"verificationStatus": "t",
				"link": "https://www.facebook.com/nytbooks",
				"created_at": "2018-05-09T15:04:36.439Z",
				"leaderId": 2301,
				"fanCount": 155000,
				"likesCount": 151000,
				"is_deleted": false,
				"updated_at": "2018-05-09T15:04:36.439Z",
				"__v": 0,
				"name": "The New York Times Books",
				"next_sync_at": "2017-05-01T04:18:05.000Z",
				"_id": "1002391179791389",
				"latest_sync_at": "2017-05-01T04:18:05.000Z",
				"status": 1
			}
		},
		"_id": "1749535868410246",
		"sort": [0]
	}],
	"count": "1",
	"message": "任务成功"
}
```



