六、 **按照指定字段排序，通过 **`keyword`** 获取 **`Es`** 库中匹配到的热门结果集（微博、微信）**

`POST` `http://127.0.0.1/stq/api/v1/words/findEsHotListByKeyword`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
keyword为监测项名称，
startDate为监测项起始时间（含），
endDate为监测项结束时间（含），
taskType为数据源 weibo、weixin
sortField 为排序字段 粉丝数（weibo）、阅读量（weixin）
sort为排序 asc（升序）、desc（降序）
size获取多少个排序结果，不超过20。传空字符串“”时，默认为10。
```

`BODY` 体：

```
{
"keyword": "欧美+电影",
"startDate": "2017-05-01",
"endDate": "2017-05-02",
"taskType":"weibo",
"sortField":"粉丝数",
"sort":"desc",
"size":"10"
}
```

`response` ，`List`集合

```
[
  {
    "_index": "weixin_articles_and_weixiners",
    "_type": "weixin_articles_and_weixiner",
    "_source":{"sentiment": 1, "copyright": false, "mid": 2653395749, "created_at": "2016-10-12T00:00:00.000Z",…},
    "_id": "MTA5NTIzNDE2MQ==:2653395749:1",
    "sort":[
      96488
    ],
    "_werxiner":{"_index": "weixiners", "_type": "weixiner", "_source":{"crawled_status": 0,…}
  },
  {
    "_index": "weixin_articles_and_weixiners",
    "_type": "weixin_articles_and_weixiner",
    "_source":{"sentiment": 0, "copyright": false, "mid": 2651897595, "created_at": "2016-10-12T00:00:00.000Z",…},
    "_id": "MjM5NzE0Mjk2Mg==:2651897595:3",
    "sort":[
      32528
    ],
    "_werxiner":{"_index": "weixiners", "_type": "weixiner", "_source":{"crawled_status": 0,…}
  },
  {
    "_index": "weixin_articles_and_weixiners",
    "_type": "weixin_articles_and_weixiner",
    "_source":{"sentiment": 0, "copyright": false, "mid": 2651885836, "stat_status": 3, "title": "杨幂、景甜、唐嫣等流量小花们，P图团队哪家强？",…},
    "_id": "MzAxODIxNjg0Nw==:2651885836:3",
    "sort":[
      24090
    ],
    "_werxiner":{"_index": "weixiners", "_type": "weixiner", "_source":{"crawled_status": -1,…}
  }
]

单条结果

[ {
  "_index" : "weixin_articles_and_weixiners",
  "_type" : "weixin_articles_and_weixiner",
  "_source" : {
    "sentiment" : 1,
    "copyright" : false,
    "mid" : 2653395749,
    "created_at" : "2016-10-12T00:00:00.000Z",
    "stat_status" : 3,
    "title" : "杨幂佟丽娅隐形臀，Baby颖儿排骨胸，赵丽颖穿裙子得用夹子：太瘦啦！",
    "crawled_at" : "2017-05-29T18:10:34.149Z",
    "content" : "本文由腾讯娱乐原创",
    "last_modified_at" : "2017-04-30T20:46:27.000Z",
    "biz" : "MTA5NTIzNDE2MQ==",
    "account_crawled_at" : "2017-01-20T07:38:11.256Z",
    "__v" : 4,
    "intro" : "在这里，读懂娱乐圈。",
    "sn" : "1202a49ff79f96f1e078c4a90bc4b801",
    "categories" : [ ],
    "stat_like_count" : 92,
    "author" : "2017-04-30小番",
    "openid" : "oIWsFt_74QFYxUOwGriBEwExPnGw",
    "account_updated_at" : "2017-01-20T07:38:11.376Z",
    "certification" : "深圳市腾讯计算机系统有限公司",
    "tags" : [ ],
    "stat_real_read_num" : 0,
    "name" : "腾讯娱乐",
    "stat_read_count" : 96488,
    "idx" : 1,
    "stat_info_crawled_at" : "2017-05-29T18:07:31.095Z",
    "stat_interval" : 2496064095,
    "username" : "txent"
  },
  "_id" : "MTA5NTIzNDE2MQ==:2653395749:1",
  "sort" : [ 96488 ],
  "_werxiner" : {
    "_index" : "weixiners",
    "_type" : "weixiner",
    "_source" : {
      "crawled_status" : 0,
      "gs_crawled_status" : 2,
      "created_at" : "2017-06-30T06:00:27.445000",
      "nr_crawled_status" : 2,
      "crawled_at" : "2017-10-19T01:00:16.229000",
      "certification" : "深圳市腾讯计算机系统有限公司",
      "tags" : [ ],
      "gs_id" : "dQHBhDlSbJnqQiO0O0On",
      "nr_crawled_at" : "2017-11-07T03:03:36.965000",
      "updated_at" : "2017-07-01T00:00:00",
      "nr_id" : "7F9B5A0E2DDCC49BD0FF10BBFB76A8CE",
      "intro" : "在这里，读懂娱乐圈。",
      "__v" : 4,
      "name" : "腾讯娱乐",
      "gs_crawled_at" : "2017-11-06T23:22:45.625000",
      "categories" : [ ],
      "username" : "txent"
    },
    "_id" : "MTA5NTIzNDE2MQ==",
    "_score" : 1.0
  }
} ]
```