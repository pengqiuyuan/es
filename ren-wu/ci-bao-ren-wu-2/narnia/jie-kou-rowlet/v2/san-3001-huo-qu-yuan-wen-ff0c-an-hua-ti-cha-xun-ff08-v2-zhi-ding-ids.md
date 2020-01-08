# 三、获取原文，按话题查询（v2 指定 ids）

二、**按话题查询获取原文 v2**

`POST` `http://127.0.0.1/stq/api/v2/rowlet/findEsTextByTopic`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```text
startDate为起始时间（含），必填。
endDate为结束时间（不含），必填。
category为数据源 tw、fb，必填
sortField为排序字段，必填。
    tw（默认 created_at 发布时间）：repost_count（转发）, comment_count（评论）, up_count（点赞）
    fb（默认 created_at 发布时间）：repost_count（转发）, comment_count（评论）, up_count（点赞）
pageSize，必填。获取多少条
hotTopics，话题集合。必填，不可为空
ids，必填。数组
```

`BODY` 体：

```text
twitter

{
    "startDate": "2016-10-09",
    "endDate": "2018-12-10",
    "category": "tw",
    "sortField": "repost_count",
    "pageSize": "10",
    "hotTopics": ["Trumpcare"],
    "ids": ["113036476", "216481299", "44254802", "231592153", "24004390", "912388475974012929", "2891165960", "66891808", "816282120767291392", "95943434", "1347285918", "90484508", "57963724", "232268199", "1712960918", "813792250497028102", "518700708", "4755913398", "194233791", "15678117", "415117361", "3023272478", "1321432124", "2978837542", "240778059", "113795716", "16335288", "234406945", "26103389", "90651198", "44482542", "60688326", "111530769", "104198706", "19471123", "2253968388", "42481696", "1077214808", "224294785", "69086398", "607332953", "3167789983", "33977070", "213795411", "76452765", "237299871", "2861616083", "381152398", "69326168", "2964949642", "28602948", "702601370344402944", "816652616625168388", "21509894", "229197216", "2966570782", "49217025", "1080844782", "20747881", "233693291", "2953974395", "50152441", "234469322", "112651673", "1592481150", "2852998461", "342677019", "1069124515", "25073877", "1071102246", "822127086194348032", "334894942", "813286", "1536791610", "88806753", "15773898", "818876014390603776", "108471631", "303861808", "950783972", "43986986", "799764016885329921", "1074412920", "176512266", "248699486", "935543239599419392", "21346398", "1906282568", "2953494478", "2968007206", "30252303", "817404026992152579", "842072478834909184", "15764644", "248735463", "24913074", "521731529", "377609596", "942156122", "826065858548133888"]
}
```

`response` Es查询有保存计算指标

`Twitter`

```text
{
    "tw": [{
        "_index": "rowlet_twitter_articles",
        "_type": "rowlet_twitter_articles",
        "_source": {
            "extended_entities": {},
            "possibly_sensitive": false,
            "created_at": "2017-03-10T16:16:30.000Z",
            "truncated": true,
            "source": "<a href=\"http://twitter.com/download/android\" rel=\"nofollow\">Twitter for Android</a>",
            "retweeted_status": true,
            "reply_count": "3339",
            "quoted_status_id": 0,
            "retweet_count": "26374",
            "url": "https://twitter.com/JaredHuffman/status/840234920723255296",
            "retweeted": false,
            "is_quote_status": false,
            "entities": {
                "urls": [],
                "hashtags": ["GOP", "Trumpcare"],
                "user_mentions": [{
                    "indices": [3, 9],
                    "screen_name": "NARAL",
                    "id_str": "17006036",
                    "name": "NARAL",
                    "id": 17006036
                }],
                "symbols": []
            },
            "id_str": "840234920723255296",
            "quoted_status_id_str": "",
            "favorite_count": "21287",
            "text": "WOW. The # GOP ’s reason to object to insurance covering prenatal care? “Why should men pay for it?” Watch: # Trumpcare # ProtectOurCare ",
            "lang": "en",
            "matching_rules": [],
            "user": {
                "utc_offset": -28800,
                "friends_count": 259,
                "profile_image_url_https": "https://pbs.twimg.com/profile_images/742907056298954752/D6NEjYJO_normal.jpg",
                "profile_background_image_url": "http://pbs.twimg.com/profile_background_images/319869712/JH_Logo.jpg",
                "listed_count": 217,
                "default_profile_image": false,
                "favourites_count": 5120,
                "created_at": "2011-07-13T20:49:36.000Z",
                "description": "Congressman for CA's 2nd Dist.  Posts on this page authorized by Huffman for Congress.  For my official House of Representatives feed please follow @RepHuffman",
                "is_translator": false,
                "profile_background_image_url_https": "https://pbs.twimg.com/profile_background_images/319869712/JH_Logo.jpg",
                "protected": false,
                "screen_name": "JaredHuffman",
                "id_str": "334894942",
                "profile_link_color": "0084B4",
                "is_translation_enabled": false,
                "translator_type": "none",
                "id": 334894942,
                "geo_enabled": true,
                "profile_background_color": "C0DEED",
                "lang": "en",
                "has_extended_profile": false,
                "profile_sidebar_border_color": "C0DEED",
                "profile_text_color": "333333",
                "verified": false,
                "profile_image_url": "http://pbs.twimg.com/profile_images/742907056298954752/D6NEjYJO_normal.jpg",
                "time_zone": "Pacific Time (US & Canada)",
                "contributors_enabled": false,
                "url": "http://t.co/vfmUDvrNRS",
                "profile_background_tile": false,
                "profile_banner_url": "https://pbs.twimg.com/profile_banners/334894942/1466965755",
                "entities": {
                    "description": {
                        "urls": []
                    },
                    "url": {
                        "urls": [{
                            "display_url": "jaredhuffman.com",
                            "indices": [0, 22],
                            "expanded_url": "http://www.jaredhuffman.com",
                            "url": "http://t.co/vfmUDvrNRS"
                        }]
                    }
                },
                "statuses_count": 6350,
                "follow_request_sent": false,
                "following": false,
                "default_profile": false,
                "profile_use_background_image": false,
                "followers_count": 4742,
                "name": "Rep. Jared Huffman",
                "location": "Northern California",
                "profile_sidebar_fill_color": "DDEEF6",
                "notifications": false
            },
            "favorited": false
        },
        "_id": "840234920723255296",
        "sort": [26374]
    }, {
        "_index": "rowlet_twitter_articles",
        "_type": "rowlet_twitter_articles",
        "_source": {
            "extended_entities": {},
            "possibly_sensitive": false,
            "created_at": "2017-05-04T15:11:29.000Z",
            "truncated": true,
            "source": "<a href=\"http://twitter.com\" rel=\"nofollow\">Twitter Web Client</a>",
            "retweeted_status": false,
            "reply_count": "385",
            "quoted_status_id": 0,
            "retweet_count": "9858",
            "url": "https://twitter.com/RepBarbaraLee/status/860149892760645634",
            "retweeted": false,
            "is_quote_status": false,
            "entities": {
                "urls": [],
                "hashtags": ["Trumpcare"],
                "user_mentions": [],
                "symbols": []
            },
            "id_str": "860149892760645634",
            "quoted_status_id_str": "",
            "favorite_count": "15465",
            "text": "Not going to sugarcoat it - this\n#\nTrumpcare bill is astonishingly evil. One of the worst bills I’ve seen in all my years in Congress.",
            "lang": "en",
            "matching_rules": [],
            "user": {
                "utc_offset": -28800,
                "friends_count": 16409,
                "profile_image_url_https": "https://pbs.twimg.com/profile_images/831276027674558470/o7pTafU9_normal.jpg",
                "profile_background_image_url": "http://pbs.twimg.com/profile_background_images/378800000180650221/0ojQYjvf.jpeg",
                "listed_count": 2674,
                "default_profile_image": false,
                "favourites_count": 3021,
                "created_at": "2011-02-07T16:28:28.000Z",
                "description": "Progressive Democrat representing the #EastBay in Congress. Promoting economic & racial justice, peace, & human rights. Proud member of the #resistance.",
                "is_translator": false,
                "profile_background_image_url_https": "https://pbs.twimg.com/profile_background_images/378800000180650221/0ojQYjvf.jpeg",
                "protected": false,
                "screen_name": "RepBarbaraLee",
                "id_str": "248735463",
                "profile_link_color": "B71234",
                "is_translation_enabled": false,
                "translator_type": "none",
                "id": 248735463,
                "geo_enabled": true,
                "profile_background_color": "C0DEED",
                "lang": "en",
                "has_extended_profile": true,
                "profile_sidebar_border_color": "FFFFFF",
                "profile_text_color": "333333",
                "verified": true,
                "profile_image_url": "http://pbs.twimg.com/profile_images/831276027674558470/o7pTafU9_normal.jpg",
                "time_zone": "Pacific Time (US & Canada)",
                "contributors_enabled": false,
                "url": "https://t.co/hfpx6kAg4s",
                "profile_background_tile": false,
                "profile_banner_url": "https://pbs.twimg.com/profile_banners/248735463/1438096272",
                "entities": {
                    "description": {
                        "urls": []
                    },
                    "url": {
                        "urls": [{
                            "display_url": "lee.house.gov",
                            "indices": [0, 23],
                            "expanded_url": "https://lee.house.gov/",
                            "url": "https://t.co/hfpx6kAg4s"
                        }]
                    }
                },
                "statuses_count": 7132,
                "follow_request_sent": false,
                "following": false,
                "default_profile": false,
                "profile_use_background_image": true,
                "followers_count": 169860,
                "name": "Rep. Barbara Lee",
                "location": "Washington, DC and Oakland, CA",
                "profile_sidebar_fill_color": "DDEEF6",
                "notifications": false
            },
            "favorited": false
        },
        "_id": "860149892760645634",
        "sort": [9858]
    }],
    "count": "365",
    "message": "任务成功"
}
```

