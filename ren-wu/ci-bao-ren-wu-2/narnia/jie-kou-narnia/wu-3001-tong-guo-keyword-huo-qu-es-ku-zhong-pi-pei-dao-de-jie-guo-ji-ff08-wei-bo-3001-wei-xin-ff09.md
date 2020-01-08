# 五、通过 keyword 获取 Es 库中匹配到的结果集（微博、微信）

五、**通过**`keyword`**获取** `Es` **库中匹配到的结果集（微博、微信）**

`POST` `http://127.0.0.1/stq/api/v1/words/findEsListByKeyword`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```text
keyword为监测项名称，
startDate为监测项起始时间（含），
endDate为监测项结束时间（含），
taskType为数据源 weibo、weixin
sortField为排序字段
    微博（默认 published_at 爬取时间）：fans_count（关注数）, follower_count（粉丝数）, repost_count（转发）, comment_count（评论）, up_count（点赞）
    微信（默认 last_modified_at 爬取时间）：stat_read_count（阅读数）, stat_like_count（点赞）
sort为排序 asc（升序）、desc（降序）
pageNumber为第几页，默认1
pageSize为每页多少条，默认10
```

`BODY` 体：

```text
{
  "keyword": "欧美+电影",
  "startDate": "2017-05-01",
  "endDate": "2017-05-02",
  "taskType":"weibo",
  "sortField":"up_count",
  "sort":"desc",
  "pageNumber":"1",
  "pageSize":"10"
}
```

`response` Es查询有保存计算指标

微博

```text
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

微信

```text
{
  "total" : 103,
  "lists" : [ {
    "highlight" : {
      "content" : [ "的儿童读物进行了重点推荐。淘气包系列在国外以幽默搞笑著称，可以说是<em>欧美</em>孩子的必读书目之一。爱捣蛋的亨利的形象，也成为<em>欧美</em>孩子心中另类的英雄。这套书字里行间透露出的幽默感，其实也是在教会孩子们用乐观积极的心态", "目前为止，淘气包系列已经被翻译成26种语言，在24个国家出版。根据淘气包的故事改编成的<em>电影</em>、漫画、动画片更是不计其数。20几年间《淘气包亨利》所获得的大奖和荣誉就更难统计了，小悦悦随便说两个，朋友们" ]
    },
    "_index" : "weixin_articles_and_weixiners",
    "_type" : "weixin_articles_and_weixiner",
    "_source" : {
      "copyright" : false,
      "mid" : 2651384839,
      "stat_status" : 3,
      "title" : "这套书，全球5000万孩子都在看，等了20年终于来到中国！",
      "crawled_at" : "2017-05-04T06:36:23.697Z",
      "content" : "欣赏君每隔一段时间",
      "last_modified_at" : "2017-05-01T03:56:09.000Z",
      "biz" : "MjM5NTk3ODQ0NA==",
      "account_crawled_at" : "2017-01-20T07:02:20.658Z",
      "__v" : 1,
      "intro" : "让人生更智慧，练达，从容，有力。 让生活更美妙。",
      "sn" : "2120bdefa046b24459faff7cbedb6e64",
      "categories" : [ ],
      "stat_like_count" : 0,
      "author" : "2017-05-01",
      "openid" : "oIWsFt3ccHqqOt2gbbhAMuGwAM8U",
      "account_updated_at" : "2017-01-20T07:02:20.790Z",
      "certification" : "读者出版传媒股份有限公司",
      "tags" : [ ],
      "stat_real_read_num" : 0,
      "name" : "读者欣赏",
      "stat_read_count" : 413,
      "idx" : 2,
      "stat_info_crawled_at" : "2017-05-04T06:22:17.248Z",
      "stat_interval" : 267968248,
      "username" : "duzhexsweixin"
    },
    "_id" : "MjM5NTk3ODQ0NA==:2651384839:2",
    "sort" : [ 1493610969000 ]
  }, {
    "highlight" : {
      "content" : [ " 初二上册全部语法内容都在这里了！04. 初三全册语法内容都在这里了！05. 初中英语学不好，是因为你没养成这些好习惯！06. 20首<em>欧美经典电影</em>主题曲（含视频/音频）关于初中英语初中英语隶属于三好网", "，是全国最具影响力的初中英语学习服务平台，每天提供最精准知识总结、最有效学习技巧、最新中考英语资讯，以及学习娱乐两不误的经典英文歌曲、<em>电影</em>等。有关初中英语学习的一切精彩，等你来关注！" ]
    },
    "_index" : "weixin_articles_and_weixiners",
    "_type" : "weixin_articles_and_weixiner",
    "_source" : {
      "copyright" : false,
      "mid" : 2650735023,
      "stat_status" : 3,
      "title" : "向五一节还在学英语的同学致敬！",
      "crawled_at" : "2017-05-06T03:31:16.941Z",
      "content" : "感谢您关注初中英语公众号，",
      "last_modified_at" : "2017-05-01T03:47:37.000Z",
      "biz" : "MjM5ODM0NjQyNg==",
      "account_crawled_at" : "2017-01-20T05:04:59.902Z",
      "__v" : 1,
      "intro" : "“初中英语”公众号，是由三好网（sanhao.com）发起并运营的、国内最大的专门服务于初中英语学习的平台。",
      "sn" : "b34a274b534e4941c8f2ff077910310f",
      "categories" : [ ],
      "stat_like_count" : 7,
      "author" : "2017-05-01小简老师",
      "openid" : "oIWsFt9d1n_z2C98R3tuzqdQ8OqQ",
      "account_updated_at" : "2017-01-20T05:05:00.023Z",
      "certification" : "北京三好互动教育科技有限公司",
      "tags" : [ ],
      "stat_real_read_num" : 0,
      "name" : "初中英语",
      "stat_read_count" : 2569,
      "idx" : 2,
      "stat_info_crawled_at" : "2017-05-06T03:27:34.624Z",
      "stat_interval" : 430797624,
      "username" : "chuzhong-yingyu"
    },
    "_id" : "MjM5ODM0NjQyNg==:2650735023:2",
    "sort" : [ 1493610457000 ],
    "_werxiner": {}
  } ]
}
```

