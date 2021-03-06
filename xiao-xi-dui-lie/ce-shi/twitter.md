# Twitter

Twitter（索引名称、分片名称）：`rowlet_twitter_articles`、`rowlet_twitter_articles`

**POST 请求写入数据到** `kafka`

`POST` `http://127.0.0.1/stq/api/v1/pa/topicRowletTwitter/add`

`HEADERS`：`"Content-Type" => "application/json"`

`BODY` 体参数说明：List 集合、数组

```text
[
    {
        "id": "848930551989915600",
        "index_name": "rowlet_twitter_articles",
        "type_name": "rowlet_twitter_articles",
        "created_at": "2017-03-19T04:21:00.000Z",
        "id_str": "848930551989915648",
        "text": "RT @TwitterMktg: Starting today, businesses can request and share locations when + engaging with people in Direct Messages. https://t.co/rpYn…",
        "truncated": false,
        "entities": {
            "hashtags": [
                {
                    "text": "NDAA",
                    "indices": [
                        49,
                        54
                    ]
                }
            ],
            "symbols": [],
            "user_mentions": [
                {
                    "screen_name": "TwitterMktg",
                    "name": "Twitter Marketing",
                    "id": 357750891,
                    "id_str": "357750891",
                    "indices": [
                        3,
                        15
                    ]
                }
            ],
            "urls": [
                {
                    "url": "https://t.co/JhHzV5s4AY",
                    "expanded_url": "https://twitter.com/i/web/status/942458104897261568",
                    "display_url": "twitter.com/i/web/status/9…",
                    "indices": [
                        116,
                        139
                    ]
                }
            ]
        },
        "source": "<ahref='http: //twitter.com' rel='nofollow'>TwitterWebClient</a>",
        "in_reply_to_status_id": 6253282334444,
        "in_reply_to_status_id_str": "6253282334444",
        "in_reply_to_user_id": 59887512221122,
        "in_reply_to_user_id_str": "59887512221122",
        "in_reply_to_screen_name": "twittermktg",
        "user": {
            "id": 6253282,
            "id_str": "6253282",
            "name": "Twitter API",
            "screen_name": "twitterapi",
            "location": "San Francisco, CA",
            "description": "The Real Twitter API. I tweet about API changes, service issues and happily answer  questions about Twitter and our API. Don't get an answer? It's on my website.",
            "url": "http://t.co/78pYTvWfJd",
            "entities": {
                "url": {
                    "urls": [
                        {
                            "url": "http://t.co/78pYTvWfJd",
                            "expanded_url": "https://dev.twitter.com",
                            "display_url": "dev.twitter.com",
                            "indices": [
                                0,
                                22
                            ]
                        }
                    ]
                },
                "description": {
                    "urls": [
                        {
                            "url": "http://t.co/78pYTvWfJd",
                            "expanded_url": "https://dev.twitter.com",
                            "display_url": "dev.twitter.com",
                            "indices": [
                                0,
                                22
                            ]
                        }
                    ]
                }
            },
            "protected": false,
            "followers_count": 6172353,
            "friends_count": 46,
            "listed_count": 13091,
            "created_at": "2017-03-19T04:21:00.000Z",
            "favourites_count": 26,
            "utc_offset": -25200,
            "time_zone": "Pacific Time (US & Canada)",
            "geo_enabled": true,
            "verified": true,
            "statuses_count": 3583,
            "lang": "en",
            "contributors_enabled": false,
            "is_translator": false,
            "is_translation_enabled": false,
            "profile_background_color": "C0DEED",
            "profile_background_image_url": "http://pbs.twimg.com/profile_background_images/656927849/miyt9dpjz77sc0w3d4vj.png",
            "profile_background_image_url_https": "https://pbs.twimg.com/profile_background_images/656927849/miyt9dpjz77sc0w3d4vj.png",
            "profile_background_tile": true,
            "profile_image_url": "http://pbs.twimg.com/profile_images/2284174872/7df3h38zabcvjylnyfe3_normal.png",
            "profile_image_url_https": "https://pbs.twimg.com/profile_images/2284174872/7df3h38zabcvjylnyfe3_normal.png",
            "profile_banner_url": "https://pbs.twimg.com/profile_banners/6253282/1431474710",
            "profile_link_color": "0084B4",
            "profile_sidebar_border_color": "C0DEED",
            "profile_sidebar_fill_color": "DDEEF6",
            "profile_text_color": "333333",
            "profile_use_background_image": true,
            "has_extended_profile": false,
            "default_profile": false,
            "default_profile_image": false,
            "following": true,
            "follow_request_sent": false,
            "notifications": false,
            "translator_type": "regular"
        },
        "geo": null,
        "coordinates": {
            "coordinates": [
                -75.14310264,
                40.05701649
            ],
            "type": "Point"
        },
        "place": {
            "attributes": {},
            "bounding_box": {
                "coordinates": [
                    [
                        [
                            -77.119759,
                            38.791645
                        ],
                        [
                            -76.909393,
                            38.791645
                        ],
                        [
                            -76.909393,
                            38.995548
                        ],
                        [
                            -77.119759,
                            38.995548
                        ]
                    ]
                ],
                "type": "Polygon"
            },
            "country": "United States",
            "country_code": "US",
            "full_name": "Washington, DC",
            "id": "01fbe706f872cb32",
            "name": "Washington",
            "place_type": "city",
            "url": "http://api.twitter.com/1/geo/id/01fbe706f872cb32.json"
        },
        "contributors": null,
        "retweeted_status": false,
        "is_quote_status": false,
        "retweet_count": 111,
        "favorite_count": 0,
        "favorited": false,
        "retweeted": false,
        "lang": "en"
    }
]
```

`response` 数据写入队列成功

```text
{
  "success" : "true"
}
```

`response` 数据写入队列失败（有一条消息写入失败就会触发。返回 `false` 的 场景是 `web server` 与 `kafka` 连接断开）

```text
{
  "success" : "false"
}
```

`logstash` **消费**`kafka`**中的数据到** `elasticsearch`

```text
...
```

从 `kafka` 队列中读取的数据，两条符合预期（`index_name`、`type_name`、`id`会在`logstash filter`中处理后移除，保存或者更新数据到 `es`）

```text
{
          "title" => "乒乓网1"
}
{
          "title" => "乒乓网2"
}
```

**POST 请求直接 Bulk 写入数据到 Elasticsearch**

注意：与上面的 `API` 相比，爬虫只用注意 `URL` 和 多出了两种返回值就好，其他一样。

`POST` `http://127.0.0.1/stq/api/v1/pabulk/topicRowletTwitter/add`

`HEADERS`：如上

`BODY` ：如上

`response` 数据 `bulk` 写入 `es` 成功

```text
{
  "success" : "true"
}
```

`response` 数据 `bulk` 写入 `es` 失败 ，返回 `bulkResponse.buildFailureMessage()` 的错误 `message`

```text
{
  "success" : "这里面的内容为 bulk 请求失败的 message 提示信息"
}
```

传入的 List 集合为空 `[]`，直接返回 `response`

```text
{
  "success" : "null"
}
```

