**一**、**添加词包任务**

`POST` `http://127.0.0.1/stq/api/v1/words/addWordsTask`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
添加剧目任务

keyword为监测项关键字（不为null或者空字符串）
startDate为监测项起始时间（含），不可以大于结束时间
endDate为监测项结束时间（含），不可以大于当前时间，可以为空字符串（代表无限期计算）
category为标识字段（Narnia项目使用 narnia）
```

`BODY` 体：

```
{
    "keyword": "大鱼海棠",
    "startDate": "2017-01-01",
    "endDate": "2017-01-10",
    "category":"narnia"
}
```

`response` 数据写入成功，返回提示信息

```
{
    "message": "任务添加成功",
    "primaryId":[
        "4220"
    ]
}

或者

{
    "message": "任务已存在",
    "primaryId":[
        "4221"
    ]
}

或者
{
    "message": "任务添加失败，关键词为空"
}
```

`response` 数据写入失败 500

---

二、**通过 **`primaryId`** 获取词包任务是否完成的状态**

`GET` `http://127.0.0.1/stq/api/v1/words/findTaskStatusByPrimaryId?primaryId=4221`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
primaryId：主任务Id，使用添加词包任务API之后返回。
```

`response` 任务执行的状态，四种结果。

```
{
    "message": "任务未开始",
    "taskStatus": "0"
}

{
    "message": "任务进行中",
    "taskStatus": "1"
}

{
    "message": "任务已完成",
    "taskStatus": "2"
}

{
    "message": "任务执行错误！",
    "taskStatus": "3"
}
```

`response` 请求失败 500

---

三、**通过 **`primaryId`** 集合，批量获取词包任务是否完成的状态，返回 **`List`

`POST` `http://127.0.0.1/stq/api/v1/words/findTaskStatusByPrimaryIdList`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
primaryId：主任务Id，使用添加词包任务API之后返回。
```

`BODY`体：

```
[1,2,3,1999]
```

`response` 任务执行的状态，四种结果。

```
{
    "message": "任务未开始",
    "taskStatus": "0"
}

{
    "message": "任务进行中",
    "taskStatus": "1"
}

{
    "message": "任务已完成",
    "taskStatus": "2"
}

{
    "message": "任务执行错误！",
    "taskStatus": "3"
}
```

`response` 数据写入成功，返回提示信息

```
[
    {
        "message": "任务已完成",
        "primaryId": "1",
        "taskStatus": "2"
    },
    {
        "message": "任务已完成",
        "primaryId": "2",
        "taskStatus": "2"
    },
    {
        "message": "任务已完成",
        "primaryId": "3",
        "taskStatus": "2"
    },
    {
        "message": "任务已完成",
        "primaryId": "1999",
        "taskStatus": "2"
    }
]
```

`response` 请求失败 500

四、**通过 **`primaryId`** 删除任务**

`GET` `http://127.0.0.1/stq/api/v1/words/delTaskByPrimaryId?primaryId=4221`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
primaryId：主任务Id，使用添加词包任务API之后返回。
```

`response` 任务执行的状态，四种结果。

```
{
    "message": "任务删除失败",
    "taskStatus": "0"
}

{
    "message": "任务删除成功",
    "taskStatus": "1"
}
```

`response` 请求失败 500

---

五、**通过**`keyword`**获取 **`Es`** 库中匹配到的结果集（微博、微信）**

`POST` `http://127.0.0.1/stq/api/v1/words/findEsListByKeyword`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
keyword为监测项名称，
startDate为监测项起始时间（含），
endDate为监测项结束时间（含），
taskType为数据源 weibo、weixin
sort为排序 asc（升序）、desc（降序）
pageNumber为第几页，默认1
pageSize为每页多少条，默认10
```

`BODY` 体：

```
{
    "keyword": "欧美+电影",
    "startDate": "2017-05-01",
    "endDate": "2017-05-02",
    "taskType":"weibo",
    "sort":"desc",
    "pageNumber":"1",
    "pageSize":"10"
}
```

`response` Es查询有保存计算指标

```
{
  "total" : 376,
  "lists" : [ {
    "highlight" : {
      "content_full" : [ "这些我有。想看的可以私信我 //@爱<em>电影</em>吧 #最热安利# 十二部重口&大尺度的<em>欧美</em>影片，部部皆高分佳作，片荒的马了看起来~ ​​​​" ]
    },
    "_index" : "weibo_articles_and_weiboers",
    "_type" : "weibo_articles_and_weiboer",
    "_source" : {
      "comment_count" : 0,
      "repost_count" : 0,
      "repost_level" : 1,
      "gender" : 0,
      "web_links" : [ ],
      "vote_links" : [ ],
      "weiboer_id" : "2703327391",
      "up_count" : 1,
      "crawled_at" : "2017-07-27T05:09:14.142Z",
      "music_links" : [ ],
      "follower_count" : 1045,
      "content" : "这些我有。想看的可以私信我",
      "updated_at" : "2017-05-26T13:27:39.400Z",
      "is_hot" : false,
      "__v" : 0,
      "intro" : "电影爱好者，喜欢整理各种资源",
      "verify" : 0,
      "video_links" : [ ],
      "content_full" : "这些我有。想看的可以私信我 //@爱电影吧 #最热安利# 十二部重口&大尺度的欧美影片，部部皆高分佳作，片荒的马了看起来~ ​​​​",
      "href" : "/2703327391/F17kqfzlB?from=page_1005052703327391_profile&wvr=6&mod=weibotime",
      "published_at" : "2017-05-01T10:37:07.000Z",
      "relationship" : "单身",
      "weibo_count" : 2382,
      "vip" : 0,
      "email" : "",
      "info" : "",
      "birthday_str" : "1991年11月20日",
      "level" : 30,
      "account_updated_at" : "2017-01-03T21:13:07.744Z",
      "location_str" : "山东",
      "sys_tags" : [ ],
      "is_pin" : false,
      "is_top" : true,
      "tags" : [ ],
      "app_source" : "HUAWEI Mate 9",
      "fans_count" : 854,
      "id_short" : "F17kqfzlB",
      "last_weibo_at" : "2017-05-26T01:40:36.000Z",
      "name" : "策划是种享受",
      "repost_id" : "4102142559804823",
      "sexual" : "异性恋",
      "edu_str" : "青岛农业大学海都学院"
    },
    "_id" : "4102665023710799",
    "sort" : [ 1493635027000 ]
  }, {
    "highlight" : {
      "content_full" : [ "//@莫里___:酒池肉林！！！！！ //@塞北羽山 #背后注意# L【<em>欧美</em><em>电影</em>混剪】【六十八名男神的酒池肉林】...和@斯迪奥夫曼斯基 的第二次合作~人名按出场顺序排序：Josh Hartnett" ]
    },
    "_index" : "weibo_articles_and_weiboers",
    "_type" : "weibo_articles_and_weiboer",
    "_source" : {
      "comment_count" : 0,
      "repost_count" : 0,
      "repost_level" : 2,
      "gender" : 1,
      "web_links" : [ ],
      "vote_links" : [ ],
      "weiboer_id" : "1751994034",
      "up_count" : 0,
      "crawled_at" : "2017-07-06T15:08:57.432Z",
      "music_links" : [ ],
      "follower_count" : 205,
      "content" : "",
      "updated_at" : "2017-05-25T10:53:18.034Z",
      "province_agg" : "福建",
      "is_hot" : false,
      "intro" : "。",
      "__v" : 1,
      "verify" : 0,
      "video_links" : [ "http://t.cn/RXFA2X4" ],
      "content_full" : "//@莫里___:酒池肉林！！！！！ //@塞北羽山 #背后注意# L【欧美电影混剪】【六十八名男神的酒池肉林】...和@斯迪奥夫曼斯基 的第二次合作~人名按出场顺序排序：Josh Hartnett，伊万，Ezra，Joe Manganiello，莱兔，加菲，海登，卷西，RR，384，加斯帕德尤利尔，大本，凯西，CE，贝克汉姆，尼子，塔总，伊桑霍克，RPJ，DTT，Christian Coulson，Lucas Till，亨亨，Jamie Campbell Bower，Mat Gordon，马修，JC，裘花，呆萌，阿汤，脸叔，钩子，Joe Alwyn，Colton Haynes，撸哥，Jay Hernandez，安煮，诺曼，火腿叔，铁叔，锤子，SPF，JD，三哥，汤甜，高司令，艾迪，囧林，Ben Barnes，裤破，RDJ，诺顿，布总，科总，污拉，李秉宪，鲨总，阿詹，帕帕，基默，Jim Sturgess，麦子，Mark Seibert，四哥，炮总，丹丹龙，Jensen，芭乐。还有一些身体局部友情客串的，例如，奥夫剪的，史皇的胸。BGM: Sexy Back by 贾婷婷¡查看图片",
      "href" : "/1751994034/F17kn2AyJ?from=page_1005051751994034_profile&wvr=6&mod=weibotime",
      "published_at" : "2017-05-01T10:37:00.000Z",
      "relationship" : "",
      "weibo_count" : 6962,
      "vip" : 0,
      "email" : "",
      "info" : "简介：    \t\t\t\t\t\t    \t\t\t\t\t\t    \t\t\t\t\t\t\t。",
      "birthday_str" : "",
      "level" : 34,
      "city_agg" : "泉州",
      "account_updated_at" : "2017-03-13T06:49:34.621Z",
      "location_str" : "福建 泉州",
      "sys_tags" : [ ],
      "is_pin" : false,
      "is_top" : true,
      "tags" : [ "老夫常作而不死", "努力当个自干五", "壮哉我大处女座", "神经病也不容易", "每天都在玩精分", "深不可测的烧饼" ],
      "app_source" : "iPhone 7 Plus",
      "fans_count" : 228,
      "id_short" : "F17kn2AyJ",
      "last_weibo_at" : "2017-05-25T09:43:26.000Z",
      "name" : "一茕二白白白白",
      "repost_id" : "4102633972893913",
      "sexual" : "异性恋",
      "username" : "moekuma"
    },
    "_id" : "4102664990617193",
    "sort" : [ 1493635020000 ]
  } ]
}
```

六、**通过**`keyword`**获取 **`IVST`** 剧目任务的计算结果集（以获取微博数据接口为例）**

`POST` `http://127.0.0.1/stq/api/v1/words/findWeiboByKeywords`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
keyword为监测项名称，
startDate为监测项起始时间（含），
endDate为监测项结束时间（含），
```

`BODY` 体：

```
{
    "keyWord": "大鱼海棠",
    "startDate": "2017-01-01",
    "endDate": "2017-01-03"
}
```

`response` Es查询有保存计算指标

```
[
    {
        "name": "大鱼海棠",
        "keywords": "大鱼海棠",
        "source": "weibo",
        "startDateString": "2017-01-01",
        "endDateString": "2017-01-02",
        "weibo_volume": 7272,
        "weibo_actualVolume": 240,
        "weibo_exposure": 9660401,
        "weibo_interactive": 7306,
        "weibo_forwardDepth": 9,
        "weibo_account": 233,
        "weibo_commentCount": 2857,
        "weibo_upCount": 4449,
        "weibo_repostCount": 1535
    },
    {
        "name": "大鱼海棠",
        "keywords": "大鱼海棠",
        "source": "weibo",
        "startDateString": "2017-01-02",
        "endDateString": "2017-01-03",
        "weibo_volume": 4736,
        "weibo_actualVolume": 127,
        "weibo_exposure": 33728971,
        "weibo_interactive": 2642,
        "weibo_forwardDepth": 7,
        "weibo_account": 119,
        "weibo_commentCount": 560,
        "weibo_upCount": 2082,
        "weibo_repostCount": 1174
    },
    {
        "name": "大鱼海棠",
        "keywords": "大鱼海棠",
        "source": "weibo",
        "startDateString": "2017-01-03",
        "endDateString": "2017-01-04",
        "weibo_volume": 4769,
        "weibo_actualVolume": 122,
        "weibo_exposure": 18982573,
        "weibo_interactive": 1671,
        "weibo_forwardDepth": 8,
        "weibo_account": 120,
        "weibo_commentCount": 318,
        "weibo_upCount": 1353,
        "weibo_repostCount": 706
    }
]
```

`response` Es查询没有保存计算指标

```
[]
```

`response` 请求失败 500

七、**通过**`keyword`**获取 **`IVST`** 剧目任务的计算结果集（微信、贴吧、知乎问题、天涯、头条、资讯博客）**

`POST` `http://127.0.0.1/stq/api/v1/words/findWeixinByKeywords`

`POST` `http://127.0.0.1/stq/api/v1/words/findTiebaByKeywords`

`POST` `http://127.0.0.1/stq/api/v1/words/findZhihuByKeywords`

`POST` `http://127.0.0.1/stq/api/v1/words/findTianyaByKeywords`

`POST` `http://127.0.0.1/stq/api/v1/words/findToutiaoByKeywords`

`POST` `http://127.0.0.1/stq/api/v1/words/findZixunByKeywords`

`参数说明`：同微博

`BODY` 体：同微博

`response` ：同微博

