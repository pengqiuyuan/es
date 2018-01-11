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
{
  "tw" : [ {
    "date" : {
      "buckets" : [ {
        "doc_count" : 7,
        "document_count" : { //期间总发帖量N
          "value" : 7.0
        },
        "retweet_count_max" : { //最大单篇转发量Rmax
          "value" : 299.0
        },
        "followers_count_sum" : { //日粉丝量F（总）
          "value" : 139174.0
        },
        "retweet_count_sum" : { //文章总转发量R
          "value" : 376.0
        },
        "reply_count_sum" : { //文章总评论量C
          "value" : 781.0
        },
        "key_as_string" : "2017-12-09",
        "reply_count_max" : { //最大单篇评论量Cmax
          "value" : 537.0
        },
        "favourites_count_sum" : { //日用户like量L（总）
          "value" : 1218.0
        },
        "favorite_count_sum" : { //文章总点赞量Z
          "value" : 850.0
        },
        "friends_count_sum" : { //日用户朋友数FR（总）
          "value" : 12229.0
        },
        "key" : 1512748800000,
        "favorite_count_max" : { //最大单篇点赞量Zmax
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
```

`response` 失败

```
{  
    "message" : "任务失败"
}
```