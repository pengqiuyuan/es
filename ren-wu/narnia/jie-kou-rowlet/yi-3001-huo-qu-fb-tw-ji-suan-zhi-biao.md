七、获取 **Fb、Tw** 计算指标

`POST` `http://127.0.0.1/stq/api/v1/rowlet/findEsStatsByUserId`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
startDate为监测项起始时间（含），
endDate为监测项结束时间（不含），
category分类，fb、tw
ids 集合。不大于 100。
```

`BODY` 体：

```
{
      "startDate":"2017-12-09",
      "endDate":"2017-12-10",
      "category":"fb",
      "ids":["18172905","239871673"]
}
```

`response` 成功

```
tw

{
  "tw" : [ {
    "date" : {
      "buckets" : [ {
        "key_as_string" : "2017-12-09",
        "key" : 1512748800000,
        "doc_count" : 7,        
        "document_count" : { //期间总发帖量N
          "value" : 7.0
        },
        "followers_count_sum" : { //日粉丝量F（总）
          "value" : 139174.0
        },
        "favourites_count_sum" : { //日用户like量L（总）
          "value" : 1218.0
        },
        "friends_count_sum" : { //日用户朋友数FR（总）
          "value" : 12229.0
        },
        "repost_sum" : { //文章总转发量R
          "value" : 376.0
        },
        "repost_max" : { //最大单篇转发量Rmax
          "value" : 299.0
        },
        "comment_sum" : { //文章总评论量C
          "value" : 781.0
        },
        "comment_max" : { //最大单篇评论量Cmax
          "value" : 537.0
        },
        "up_sum" : { //文章总点赞量Z
          "value" : 850.0
        },
        "up_max" : { //最大单篇点赞量Zmax
          "value" : 477.0
        }
      }, {
        "doc_count" : 0,
        "document_count" : {
          "value" : 0.0
        },
        "retweet_count_max" : { },
        "followers_count_sum" : {
          "value" : 0.0
        },
        "retweet_count_sum" : {
          "value" : 0.0
        },
        "reply_count_sum" : {
          "value" : 0.0
        },
        "key_as_string" : "2017-12-10",
        "reply_count_max" : { },
        "favourites_count_sum" : {
          "value" : 0.0
        },
        "favorite_count_sum" : {
          "value" : 0.0
        },
        "friends_count_sum" : {
          "value" : 0.0
        },
        "key" : 1512835200000,
        "favorite_count_max" : { }
      } ]
    },
    "doc_count" : 7,
    "key" : "239871673"
  }, {
    "date" : {
      "buckets" : [ {
        "doc_count" : 3,
        "document_count" : {
          "value" : 3.0
        },
        "retweet_count_max" : {
          "value" : 11.0
        },
        "followers_count_sum" : {
          "value" : 333267.0
        },
        "retweet_count_sum" : {
          "value" : 22.0
        },
        "reply_count_sum" : {
          "value" : 16.0
        },
        "key_as_string" : "2017-12-09",
        "reply_count_max" : {
          "value" : 8.0
        },
        "favourites_count_sum" : {
          "value" : 3948.0
        },
        "favorite_count_sum" : {
          "value" : 19.0
        },
        "friends_count_sum" : {
          "value" : 15168.0
        },
        "key" : 1512748800000,
        "favorite_count_max" : {
          "value" : 11.0
        }
      }, {
        "doc_count" : 0,
        "document_count" : { 
          "value" : 0.0
        },
        "retweet_count_max" : { },
        "followers_count_sum" : {
          "value" : 0.0
        },
        "retweet_count_sum" : {
          "value" : 0.0
        },
        "reply_count_sum" : {
          "value" : 0.0
        },
        "key_as_string" : "2017-12-10",
        "reply_count_max" : { },
        "favourites_count_sum" : {
          "value" : 0.0
        },
        "favorite_count_sum" : {
          "value" : 0.0
        },
        "friends_count_sum" : {
          "value" : 0.0
        },
        "key" : 1512835200000,
        "favorite_count_max" : { }
      } ]
    },
    "doc_count" : 3,
    "key" : "18172905"
  } ],
  "message" : "任务成功"
}


{
	"tw": [{
		"date": {
			"buckets": [{
				"repost_max": {
					"value": 35.0
				},
				"doc_count": 10,
				"comment_max": {
					"value": 6.0
				},
				"document_count": {
					"value": 10.0
				},
				"followers_count_sum": {
					"value": 624330.0
				},
				"repost_sum": {
					"value": 140.0
				},
				"comment_sum": {
					"value": 19.0
				},
				"key_as_string": "2017-12-09",
				"favourites_count_sum": {
					"value": 870.0
				},
				"friends_count_sum": {
					"value": 16960.0
				},
				"up_sum": {
					"value": 658.0
				},
				"key": 1512748800000,
				"up_max": {
					"value": 237.0
				}
			}, {
				"repost_max": {},
				"doc_count": 0,
				"comment_max": {},
				"document_count": {
					"value": 0.0
				},
				"followers_count_sum": {
					"value": 0.0
				},
				"repost_sum": {
					"value": 0.0
				},
				"comment_sum": {
					"value": 0.0
				},
				"key_as_string": "2017-12-10",
				"favourites_count_sum": {
					"value": 0.0
				},
				"friends_count_sum": {
					"value": 0.0
				},
				"up_sum": {
					"value": 0.0
				},
				"key": 1512835200000,
				"up_max": {}
			}]
		},
		"doc_count": 10,
		"key": "19471123"
	}],
	"docCountByDays": [{
		"id": "19471123",
		"key_as_string": "2017-12-09",
		"primaryAndForwardCommentCount": "10",
		"forwardCount": "2"
	}, {
		"id": "19471123",
		"key_as_string": "2017-12-10",
		"primaryAndForwardCommentCount": "0",
		"forwardCount": "0"
	}],
	"message": "任务成功"
}

fb


BODY
raw 
{
  "fb" : [ {
    "date" : {
      "buckets" : [ {
        "key_as_string" : "2017-12-09",
        "doc_count" : 5,
        "key" : 1512748800000,
        "fan_count_sum" : { //日粉丝量F（总）
          "value" : 64680.0
        },
        "likes_count_sum" : { //日用户被like数L（总）
          "value" : 64960.0
        },
        "document_count" : { //期间总发帖量N
          "value" : 5.0
        },
        "repost_sum" : { //文章总转发量R
          "value" : 0.0
        },
        "repost_max" : { //最大单篇转发量Rmax
          "value" : 0.0
        },
        "comment_sum" : { //文章总评论量C
          "value" : 195.0
        },
        "comment_max" : { //最大单篇评论量Cmax
          "value" : 39.0
        },
        "up_sum" : { //文章总点赞量Z
          "value" : 945.0
        },
        "up_max" : { //最大单篇点赞量Zmax
          "value" : 189.0
        }
      }, {
        "key_as_string" : "2017-12-10",
        "doc_count" : 0,
        "document_count" : {
          "value" : 0.0
        },
        "share_count_sum" : {
          "value" : 0.0
        },
        "comment_num_max" : { },
        "share_count_max" : { },
        "likes_num_max" : { },
        "comment_num_sum" : {
          "value" : 0.0
        },
        "likes_num_sum" : {
          "value" : 0.0
        },
        "key" : 1512835200000,
        "fan_count_sum" : { 
          "value" : 0.0
        },
        "likes_count_sum" : {
          "value" : 0.0
        }
      } ]
    },
    "doc_count" : 5,
    "key" : "853073668057412"
  } ],
  "message" : "任务成功"
}
```

`response` 失败

```
{  
    "message" : "任务失败"
}
```



