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
    "startDate": "2017-12-09",
    "endDate": "2017-12-10",
    "category": "tw",
    "ids": ["18172905", "239871673", "113036476", "216481299", "44254802", "231592153", "24004390", "912388475974012929", "2891165960", "66891808", "816282120767291392", "95943434", "1347285918", "90484508", "57963724", "232268199", "1712960918", "813792250497028102", "518700708", "4755913398", "194233791", "15678117", "415117361", "3023272478", "1321432124", "2978837542", "240778059", "113795716", "16335288", "234406945", "26103389", "90651198", "44482542", "60688326", "111530769", "104198706", "19471123", "2253968388", "42481696", "1077214808", "224294785", "69086398", "607332953", "3167789983", "33977070", "213795411", "76452765", "237299871", "2861616083", "381152398", "69326168", "2964949642", "28602948", "702601370344402944", "816652616625168388", "21509894", "229197216", "2966570782", "49217025", "1080844782", "20747881", "233693291", "2953974395", "50152441", "234469322", "112651673", "1592481150", "2852998461", "342677019", "1069124515", "25073877", "1071102246", "822127086194348032", "334894942", "813286", "1536791610", "88806753", "15773898", "818876014390603776", "108471631", "303861808", "950783972", "43986986", "799764016885329921", "1074412920", "176512266", "248699486", "935543239599419392", "21346398", "1906282568", "2953494478", "2968007206", "30252303", "817404026992152579", "842072478834909184", "15764644", "248735463", "24913074", "521731529", "377609596", "942156122", "826065858548133888"],
    "keywords": "china",
    "sortField": "comment_count",
    "sort": "desc",
    "pageNumber": "1",
    "pageSize": "10",
    "queryMode":"normal"
}

facebook

{
    "startDate": "2017-12-09",
    "endDate": "2017-12-10",
    "category": "fb",
    "ids": ["7606381190", "551199354892891"],
    "keywords": "legislation",
    "sortField": "comment_count",
    "sort": "asc",
    "pageNumber": "1",
    "pageSize": "10",
    "queryMode":"normal"
}
```

`response` Es查询有保存计算指标

`Twitter`

```
{
	"tw": [{
		"highlight": {
			"text": ["\"Nebraska's beef exports to <em>China</em> were $8.7 million as of Oct. 31, 50.5% of the U.S. total of $17.2", " million.\"\n#\nGrowNE Check out the rest of the article on Nebraska's beef exports to <em>China</em>:"]
		},
		"_index": "rowlet_twitter_articles",
		"_type": "rowlet_twitter_articles",
		"_source": {
			"extended_entities": {},
			"possibly_sensitive": false,
			"created_at": "2017-12-08T21:43:01.000Z",
			"truncated": true,
			"source": "<a href=\"http://twitter.com\" rel=\"nofollow\">Twitter Web Client</a>",
			"retweeted_status": false,
			"reply_count": "2",
			"quoted_status_id": 939245827112960010,
			"retweet_count": "23",
			"url": "https://twitter.com/GovRicketts/status/939248980046897152",
			"retweeted": false,
			"is_quote_status": true,
			"entities": {
				"urls": [{
					"display_url": "twitter.com/i/web/status/9…",
					"indices": [111, 134],
					"expanded_url": "https://twitter.com/i/web/status/939248980046897152",
					"url": "https://t.co/cR06zqgi4s"
				}],
				"hashtags": [],
				"user_mentions": [],
				"symbols": []
			},
			"id_str": "939248980046897152",
			"quoted_status_id_str": "939245827112960010",
			"favorite_count": "48",
			"text": "\"Nebraska's beef exports to China were $8.7 million as of Oct. 31, 50.5% of the U.S. total of $17.2 million.\"\n#\nGrowNE Check out the rest of the article on Nebraska's beef exports to China:",
			"lang": "en",
			"matching_rules": [],
			"user": {
				"utc_offset": -21600,
				"friends_count": 1045.0,
				"profile_image_url_https": "https://pbs.twimg.com/profile_images/571738181293191168/7U9JX8Bu_normal.jpeg",
				"profile_background_image_url": "http://abs.twimg.com/images/themes/theme1/bg.png",
				"listed_count": 274,
				"default_profile_image": false,
				"favourites_count": 283.0,
				"created_at": "2014-11-05T21:15:44.000Z",
				"is_translator": false,
				"description": "40th Governor of Nebraska",
				"profile_background_image_url_https": "https://abs.twimg.com/images/themes/theme1/bg.png",
				"protected": false,
				"screen_name": "GovRicketts",
				"id_str": "2891165960",
				"profile_link_color": "1DA1F2",
				"is_translation_enabled": false,
				"translator_type": "none",
				"profile_background_color": "C0DEED",
				"id": 2891165960,
				"geo_enabled": true,
				"lang": "en",
				"has_extended_profile": false,
				"profile_sidebar_border_color": "C0DEED",
				"profile_text_color": "333333",
				"verified": true,
				"profile_image_url": "http://pbs.twimg.com/profile_images/571738181293191168/7U9JX8Bu_normal.jpeg",
				"time_zone": "Central Time (US & Canada)",
				"url": "https://t.co/XH644geIIN",
				"contributors_enabled": false,
				"profile_banner_url": "https://pbs.twimg.com/profile_banners/2891165960/1493414718",
				"profile_background_tile": false,
				"entities": {
					"description": {
						"urls": []
					},
					"url": {
						"urls": [{
							"display_url": "governor.nebraska.gov",
							"indices": [0, 23],
							"expanded_url": "http://governor.nebraska.gov",
							"url": "https://t.co/XH644geIIN"
						}]
					}
				},
				"follow_request_sent": false,
				"statuses_count": 3130,
				"followers_count": 13109.0,
				"default_profile": true,
				"following": false,
				"profile_use_background_image": true,
				"name": "Gov. Pete Ricketts",
				"location": "Nebraska",
				"profile_sidebar_fill_color": "DDEEF6",
				"notifications": false
			},
			"favorited": false
		},
		"_id": "939248980046897152",
		"sort": [2]
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
			"text": ["I’m introducing <em>legislation</em> to save the internet - the Save Net Neutrality Act."]
		},
		"_index": "rowlet_facebook_articles",
		"_type": "rowlet_facebook_articles",
		"_source": {
			"comment_num": 59,
			"share_count": 207,
			"update_status": true,
			"text": "I’m introducing legislation to save the internet - the Save Net Neutrality Act.",
			"likes_num": 874,
			"create_at": "2017-12-08T17:34:58.000Z",
			"permalink_url": "https://facebook.com/repseanmaloney/videos/1761295353883279/",
			"user": {
				"friends_count": 0.0,
				"hometown": "Cold Spring, NY ",
				"website": "http://seanmaloney.house.gov/",
				"fan_count": 30363.0,
				"keywords": "Maloney, Sean Patrick",
				"facebookId": "551199354892891",
				"favourites_count": 0.0,
				"link": "https://www.facebook.com/repseanmaloney/",
				"about": "Proud to represent New York's 18th Congressional District",
				"likes_count": 27488.0,
				"bySheet": "House of Representatives",
				"followers_count": 0.0,
				"name": "Representative Sean Patrick Maloney",
				"location": {
					"zip": "20515",
					"country": "United States",
					"city": "Washington",
					"street": "1027 Longworth HOB",
					"state": "DC"
				},
				"_id": "5a2612604c7ffb6fc00bea2a",
				"id": "551199354892891",
				"category": "Government Official",
				"likes": {
					"data": [{
						"name": "West Point Professional Firefighters",
						"id": "277336965536"
					}, {
						"name": "Planned Parenthood Mid-Hudson Valley Action",
						"id": "133318081972"
					}, {
						"name": "City of Newburgh Firefighters  IAFF Local 589",
						"id": "131726836605"
					}],
					"paging": {
						"next": "https://graph.facebook.com/v2.10/551199354892891/likes?access_token=EAACEdEose0cBAO22T6Yq1KZAZACVAKHnna8kEZBF8i9U1xMKHJ2PUhnV6l7cjmYL4S3wRnYAizvFgoCv8ZAWn1ZAsB7ZCVuKaH0jwnfNFhEUhtyLhHCxuZAWdEbQaYprGi95V5vhVY4B3xjE3w2YVkAaKZBWpuQ4WvIGHEpUM8ZCXPlxYiJmToSsCRciqOVPcViWV9T2sopeMuwFdsIxCR3HT&limit=3&after=MTMxNzI2ODM2NjA1",
						"cursors": {
							"before": "Mjc3MzM2OTY1NTM2",
							"after": "MTMxNzI2ODM2NjA1"
						}
					}
				}
			},
			"topick": [],
			"last_untime": "1512754498"
		},
		"_id": "0f9491a9075e6f9c208e90daed0f7d6d",
		"sort": [59]
	}],
	"count": "1",
	"message": "任务成功"
}
```



