五、**获取库中匹配到的结果集（Tw、Fb）**

`POST` `http://127.0.0.1/stq/api/v1/rowlet/findEsTextByUserId`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
keywords为查询关键字，必填。默认空字符串
startDate为起始时间（含），必填。
endDate为结束时间（不含），必填。
category为数据源 tw、fb，必填
ids为账号Id数组，必填。
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
    "keywords": "",
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
            "_index": "rowlet_twitter_articles",
            "_type": "rowlet_twitter_articles",
            "_source": {
                "extended_entities": {},
                "possibly_sensitive": false,
                "created_at": "2017-12-09T13:21:24.000Z",
                "truncated": true,
                "source": "<a href=\"http://twitter.com/download/iphone\" rel=\"nofollow\">Twitter for iPhone</a>",
                "retweeted_status": false,
                "reply_count": 60994,
                "quoted_status_id": 0,
                "retweet_count": 37527,
                "retweeted": false,
                "is_quote_status": false,
                "entities": {
                    "urls": [{
                        "display_url": "twitter.com/i/web/status/9…",
                        "indices": [117, 140],
                        "expanded_url": "https://twitter.com/i/web/status/939485131693322240",
                        "url": "https://t.co/FoPRXAVjsh"
                    }],
                    "hashtags": [],
                    "user_mentions": [],
                    "symbols": []
                },
                "id_str": "939485131693322240",
                "quoted_status_id_str": "",
                "favorite_count": 148099,
                "text": "CNN’S slogan is CNN, THE MOST TRUSTED NAME IN NEWS. Everyone knows this is not true, that this could, in fact, be a… https://t.co/FoPRXAVjsh",
                "lang": "en",
                "matching_rules": [],
                "user": {
                    "utc_offset": -18000,
                    "friends_count": 45,
                    "profile_image_url_https": "https://pbs.twimg.com/profile_images/874276197357596672/kUuht00m_normal.jpg",
                    "listed_count": 81271,
                    "profile_background_image_url": "http://pbs.twimg.com/profile_background_images/530021613/trump_scotland__43_of_70_cc.jpg",
                    "default_profile_image": false,
                    "favourites_count": 24,
                    "created_at": "2009-03-18T13:46:38.000Z",
                    "description": "45th President of the United States of America🇺🇸",
                    "is_translator": false,
                    "profile_background_image_url_https": "https://pbs.twimg.com/profile_background_images/530021613/trump_scotland__43_of_70_cc.jpg",
                    "protected": false,
                    "screen_name": "realDonaldTrump",
                    "profile_link_color": "1B95E0",
                    "id_str": "25073877",
                    "is_translation_enabled": true,
                    "translator_type": "regular",
                    "id": 25073877,
                    "geo_enabled": true,
                    "profile_background_color": "6D5C18",
                    "lang": "en",
                    "has_extended_profile": false,
                    "profile_sidebar_border_color": "BDDCAD",
                    "profile_text_color": "333333",
                    "verified": true,
                    "profile_image_url": "http://pbs.twimg.com/profile_images/874276197357596672/kUuht00m_normal.jpg",
                    "time_zone": "Eastern Time (US & Canada)",
                    "contributors_enabled": false,
                    "url": "https://t.co/OMxB0x7xC5",
                    "profile_background_tile": true,
                    "profile_banner_url": "https://pbs.twimg.com/profile_banners/25073877/1514062099",
                    "entities": {
                        "description": {
                            "urls": []
                        },
                        "url": {
                            "urls": [{
                                "display_url": "Instagram.com/realDonaldTrump",
                                "indices": [0, 23],
                                "expanded_url": "http://www.Instagram.com/realDonaldTrump",
                                "url": "https://t.co/OMxB0x7xC5"
                            }]
                        }
                    },
                    "statuses_count": 36634,
                    "follow_request_sent": false,
                    "following": false,
                    "default_profile": false,
                    "profile_use_background_image": true,
                    "followers_count": 45143795,
                    "name": "Donald J. Trump",
                    "profile_sidebar_fill_color": "C5CEC0",
                    "location": "Washington, DC",
                    "notifications": false
                },
                "favorited": false
            },
            "_id": "939485131693322240",
            "sort": [60994]
        },
        {
            "_index": "rowlet_twitter_articles",
            "_type": "rowlet_twitter_articles",
            "_source": {
                "extended_entities": {
                    "media": [{
                        "display_url": "pic.twitter.com/64a93S07s7",
                        "indices": [26, 49],
                        "sizes": {
                            "small": {
                                "w": 680,
                                "h": 206,
                                "resize": "fit"
                            },
                            "large": {
                                "w": 1024,
                                "h": 310,
                                "resize": "fit"
                            },
                            "thumb": {
                                "w": 150,
                                "h": 150,
                                "resize": "crop"
                            },
                            "medium": {
                                "w": 1024,
                                "h": 310,
                                "resize": "fit"
                            }
                        },
                        "id_str": "939189414890221569",
                        "expanded_url": "https://twitter.com/realDonaldTrump/status/939189419386470401/photo/1",
                        "media_url_https": "https://pbs.twimg.com/media/DQiry_tWsAE1kdt.jpg",
                        "id": 939189414890221569,
                        "type": "photo",
                        "media_url": "http://pbs.twimg.com/media/DQiry_tWsAE1kdt.jpg",
                        "url": "https://t.co/64a93S07s7"
                    }]
                },
                "possibly_sensitive": false,
                "created_at": "2017-12-08T17:46:21.000Z",
                "truncated": false,
                "source": "<a href=\"http://twitter.com/download/iphone\" rel=\"nofollow\">Twitter for iPhone</a>",
                "retweeted_status": false,
                "reply_count": 31538,
                "quoted_status_id": 0,
                "retweet_count": 15047,
                "retweeted": false,
                "is_quote_status": false,
                "entities": {
                    "urls": [],
                    "hashtags": [],
                    "media": [{
                        "display_url": "pic.twitter.com/64a93S07s7",
                        "indices": [26, 49],
                        "sizes": {
                            "small": {
                                "w": 680,
                                "h": 206,
                                "resize": "fit"
                            },
                            "large": {
                                "w": 1024,
                                "h": 310,
                                "resize": "fit"
                            },
                            "thumb": {
                                "w": 150,
                                "h": 150,
                                "resize": "crop"
                            },
                            "medium": {
                                "w": 1024,
                                "h": 310,
                                "resize": "fit"
                            }
                        },
                        "id_str": "939189414890221569",
                        "expanded_url": "https://twitter.com/realDonaldTrump/status/939189419386470401/photo/1",
                        "media_url_https": "https://pbs.twimg.com/media/DQiry_tWsAE1kdt.jpg",
                        "id": 939189414890221569,
                        "type": "photo",
                        "media_url": "http://pbs.twimg.com/media/DQiry_tWsAE1kdt.jpg",
                        "url": "https://t.co/64a93S07s7"
                    }],
                    "user_mentions": [],
                    "symbols": []
                },
                "id_str": "939189419386470401",
                "quoted_status_id_str": "",
                "favorite_count": 67792,
                "text": "MAKE AMERICA GREAT AGAIN! https://t.co/64a93S07s7",
                "lang": "en",
                "matching_rules": [],
                "user": {
                    "utc_offset": -18000,
                    "friends_count": 45,
                    "profile_image_url_https": "https://pbs.twimg.com/profile_images/874276197357596672/kUuht00m_normal.jpg",
                    "listed_count": 81271,
                    "profile_background_image_url": "http://pbs.twimg.com/profile_background_images/530021613/trump_scotland__43_of_70_cc.jpg",
                    "default_profile_image": false,
                    "favourites_count": 24,
                    "created_at": "2009-03-18T13:46:38.000Z",
                    "description": "45th President of the United States of America🇺🇸",
                    "is_translator": false,
                    "profile_background_image_url_https": "https://pbs.twimg.com/profile_background_images/530021613/trump_scotland__43_of_70_cc.jpg",
                    "protected": false,
                    "screen_name": "realDonaldTrump",
                    "profile_link_color": "1B95E0",
                    "id_str": "25073877",
                    "is_translation_enabled": true,
                    "translator_type": "regular",
                    "id": 25073877,
                    "geo_enabled": true,
                    "profile_background_color": "6D5C18",
                    "lang": "en",
                    "has_extended_profile": false,
                    "profile_sidebar_border_color": "BDDCAD",
                    "profile_text_color": "333333",
                    "verified": true,
                    "profile_image_url": "http://pbs.twimg.com/profile_images/874276197357596672/kUuht00m_normal.jpg",
                    "time_zone": "Eastern Time (US & Canada)",
                    "contributors_enabled": false,
                    "url": "https://t.co/OMxB0x7xC5",
                    "profile_background_tile": true,
                    "profile_banner_url": "https://pbs.twimg.com/profile_banners/25073877/1514062099",
                    "entities": {
                        "description": {
                            "urls": []
                        },
                        "url": {
                            "urls": [{
                                "display_url": "Instagram.com/realDonaldTrump",
                                "indices": [0, 23],
                                "expanded_url": "http://www.Instagram.com/realDonaldTrump",
                                "url": "https://t.co/OMxB0x7xC5"
                            }]
                        }
                    },
                    "statuses_count": 36634,
                    "follow_request_sent": false,
                    "following": false,
                    "default_profile": false,
                    "profile_use_background_image": true,
                    "followers_count": 45143795,
                    "name": "Donald J. Trump",
                    "profile_sidebar_fill_color": "C5CEC0",
                    "location": "Washington, DC",
                    "notifications": false
                },
                "favorited": false
            },
            "_id": "939189419386470401",
            "sort": [31538]
        }
    ],
    "message": "任务成功"
}
```

`Facebook`

```
{
    "fb": [{
            "_index": "rowlet_facebook_articles",
            "_type": "rowlet_facebook_articles",
            "_source": {
                "comment_num": 6,
                "share_count": 31,
                "text": "Announced new legislation yesterday to block the FCC's proposed rollback of Net Neutrality rules. The internet is working fine as it is - if it ain't broke, don't fix it.",
                "likes_num": 164,
                "create_at": "2017-12-09T10:04:00.000Z",
                "user": {
                    "birthday": "03/14/2012",
                    "website": "http://seanmaloney.house.gov/",
                    "hometown": "Cold Spring, NY ",
                    "keywords": "Maloney, Sean Patrick",
                    "fan_count": 26987,
                    "about": "Proud to represent New York's 18th Congressional District",
                    "link": "https://www.facebook.com/repseanmaloney/",
                    "emails": ["info@seanmaloney.com"],
                    "likes_count": 27289,
                    "bySheet": "House of Representatives",
                    "name": "Representative Sean Patrick Maloney",
                    "location": {
                        "zip": "20515",
                        "country": "United States",
                        "city": "Washington",
                        "street": "1027 Longworth HOB",
                        "state": "DC"
                    },
                    "id": "551199354892891",
                    "_id": "5a2612604c7ffb6fc00bea2a",
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
                "last_untime": "1512842640"
            },
            "_id": "5a424fca4c7ffbff17715de2",
            "sort": [6]
        },
        {
            "_index": "rowlet_facebook_articles",
            "_type": "rowlet_facebook_articles",
            "_source": {
                "comment_num": "6",
                "share_count": "31",
                "text": "Announced new legislation yesterday to block the FCC's proposed rollback of Net Neutrality rules. The internet is working fine as it is - if it ain't broke, don't fix it.",
                "likes_num": "164",
                "create_at": "2017-12-09T10:04:00.000Z",
                "user": {
                    "birthday": "03/14/2012",
                    "hometown": "Cold Spring, NY ",
                    "website": "http://seanmaloney.house.gov/",
                    "fan_count": 26987,
                    "keywords": "Maloney, Sean Patrick",
                    "link": "https://www.facebook.com/repseanmaloney/",
                    "about": "Proud to represent New York's 18th Congressional District",
                    "emails": ["info@seanmaloney.com"],
                    "likes_count": 27289,
                    "bySheet": "House of Representatives",
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
                "last_untime": "1512842640"
            },
            "_id": "5a538622c311cb605dfc8355",
            "sort": [6]
        }
    ],
    "message": "任务成功"
}
```



