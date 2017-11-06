**一**、**添加词包任务**

`POST` `http://127.0.0.1/stq/api/v1/words/addWordsTask`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
添加剧目任务

keyword为监测项关键字（不为null或者空字符串）
startDate为监测项起始时间（含），不可以大于结束时间
endDate为监测项结束时间（含），不可以大于当前时间，可以为空字符串（代表无限期计算）
category为标识字段（Narnia 项目使用 narnia，Ivst 项目使用 ivst，旅游项目使用 travel）
```

`BODY` 体：

```
{
    "keyword": "大鱼海棠",
    "startDate": "2017-01-01",
    "endDate": "2017-01-10",
    "category":"narnia" #注意：Narnia 项目使用 narnia，Ivst 项目使用 ivst，旅游项目使用 travel
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

三、**通过 **`primaryId`** 集合，批量获取词包任务是否完成的状态，返回集合**

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

微博

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

微信

```
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
      "content" : "欣赏君每隔一段时间，就会向各位孩儿爸孩儿妈们推荐一些特别棒的童书。很多爸爸妈妈会在后台给我们留言，比如：“你们推荐的每一套童书宝贝都爱不释手，现在我们就是跟着你推荐的节奏给孩儿买书呢！坐等下一套推荐~”正是这样的信任，激励我们不断去发现一套套的好童书，分享给大家，和我们的孩子们一起阅读，共同成长。来看看今天的童书推荐——《淘气包亨利》风靡全球20年，获奖无数，好评如潮《淘气包亨利》的故事，最早出版是在1994年，当年一出版就横扫各大图书销量排行榜。此后每年，作者都会出版一到两本淘气包亨利的故事。也就由此成为了一个系列。《淘气包亨利》仅仅在英国销售就超过了2000万册。朋友们千万别觉得少，英国总人口也才6000多万而已。咱们中国的爸爸妈妈们对J.K.罗琳创作的《哈利·波特》应该是比较熟悉的，其实在《哈利·波特》问世之前，霸占各大销售量总榜冠军的，一直都是《淘气包亨利》。从两套书出版问世开始，《淘气包亨利》和《哈利•波特》系列一直在激烈竞争，直到现在。相比而言，《哈利·波特》故事相对比较复杂，书籍很厚，字数又多，咱们中国孩子选英文读物，淘气包系列更贴近生活，也更符合孩子们的阅读能力。目前为止，淘气包系列已经被翻译成26种语言，在24个国家出版。根据淘气包的故事改编成的电影、漫画、动画片更是不计其数。20几年间《淘气包亨利》所获得的大奖和荣誉就更难统计了，小悦悦随便说两个，朋友们感受一下这套书的分量。《淘气包亨利》曾荣获英国童书年度大奖；作者弗朗西丝卡·西蒙凭借着《淘气包亨利之可恶大雪人》获得了银河图书奖的最佳童书奖。▲作者：弗朗西丝卡•西蒙英国的银河图书奖一般是不会颁给外籍作者的，09年美国前总统奥巴马曾经凭借《无畏的希望》和《我父亲的梦想》进入了年度银河图书奖的候选名单，不过他落选了，所以西蒙也是唯一一位获得英国银河图书奖的美国作家。《淘气包亨利》在世界童书界的地位就是这么高，说是7-14岁孩子英语读物的首选并不为过。故事好玩有趣，在幽默中收获成长小悦悦之所以钟情于《淘气包亨利》，主要是因为这套书通俗易懂、好玩有趣，故事情节又搞笑又贴近生活。一些已经购买过《淘气包亨利》家长朋友是这样评价这套童书的：◆“孩子很喜欢，说特别有趣，每天带去学校和同学一起看。”◆“孩子太小，不能自己看。自从给他读了两个故事以后，每天要求听，听一遍笑一遍。”◆“女儿非常喜欢，看到有意思的地方还给我们讲，值了！”◆“孩子最喜欢的一套书，自己看得哈哈笑。外国人的幽默真是没法比。”◆“闺女不仅自己看，还给弟弟讲。看孩子的兴奋劲儿，我也想和他们一起看了。”◆“特别符合孩子的心理，想再买一套送人。”孩子们喜欢这套书，小悦悦丝毫不意外。之前世界范围内享有盛誉的《泰晤士报》曾推出一个《百本新经典分级阅读童书推荐》，选取了最近10年出版的100本最值得推荐的童书，这套《淘气包亨利》就作为最适合的儿童读物进行了重点推荐。淘气包系列在国外以幽默搞笑著称，可以说是欧美孩子的必读书目之一。爱捣蛋的亨利的形象，也成为欧美孩子心中另类的英雄。这套书字里行间透露出的幽默感，其实也是在教会孩子们用乐观积极的心态来面对问题。淘气包虽然顽皮，也有缺点，但是他可是个内向强大的孩子。有时候会把事情搞砸，但他绝不自怨自艾，丧失信心。这种幽默的能量，也是这套书经久不衰的一大法宝。纯正英语，给孩子地道语言文化对于《淘气包亨利》的引进，是20几年间中国出版社首次拿到英文版授权。出版社很用心的把这套书设计成了AB面的双语版。只看中文版的故事，就已经是特别值得入手的一套好书了。再加上英文原版的内容，又让这套书有了培养孩子英语语感和英语思维的效果。既可做亲子共读的读本，也可以让孩子独立阅读，如果有些英语基础，可以让孩子翻看英文部分做对照阅读，丰富词汇量和提高英语水平。市面上的很多双语书常常把中文英文放在一起，这样容易导致孩子只看中文而忽略英文。这套《淘气包亨利》两面都是封面，一面翻开是中文的故事，而把书调转过来，另一面则是地道的英文版故事。中文英文互为补充，却互不影响。不会干扰孩子完整的阅读体验。很多专家和一线教师们，都建议家长朋友给孩子提供一些原汁原味的英语读物。原因很简单，无论学习哪一门语言，语感都十分重要。咱们很多孩子学英语很吃力，是因为无法适应英语思维。死记硬背单词和语法，效果不佳。小编之所以这么看重《淘气包亨利》这套书，也是因为里面大量生活化、口语化的对白，特别适合14岁以下孩子阅读。淘气包的故事多半发生在家庭里和校园里，而且每个故事都不长，大概20页左右，里面的单词又贴近生活。淘气包亨利跟弟弟彼得斗嘴、跟爸爸妈妈调皮这些情节，都很容易让孩子读进去。这其实就是一个很好地培养孩子英语思维和让孩子了解英语文化背景的过程。随书还附赠了英语音频。朋友们只需要扫描书封面上的二维码或者内页上方的二维码，就可以直接用手机听对应的故事了。英语音频都是外教纯正英国腔，节奏控制得比较好。给孩子做英语口语练习，没事儿磨耳朵，再合适不过。是“淘气包”们的知音，也是良师益友英国《卫报》评论：淘气包亨利是一个当代喜剧经典。他是一个了不起的反英雄形象，他只做大多数孩子梦里敢做的事情。亨利不是一个完美的小孩。整个故事里，也没有一个完美的小孩。但是每个孩子，甚至我们大人，又都可以在淘气包亨利身上，找到自己的影子。亨利的故事里，把孩子们心里想的都畅快滴表达了出来。小亨利的种种淘气，也都很符合孩子这个年龄段的特征。亨利不爱吃蔬菜，就用尽各种办法把蔬菜放到弟弟的盘子里；亨利不想做家务，就在干活过程中投机取巧，让爸爸妈妈误以为他不适合做家务……这些故事的发展和结局能让孩子自己体会到行为和结果之间的关系，也在潜移默化中让孩子明白什么该做什么不该做。亨利是个名副其实的淘气包，但就像台湾金鼎奖儿童文学家幸佳慧评价的那样：“弗朗西斯卡相信她的故事，能让孩子们种种不舒服的情绪有个安全的排放出口。因为，当你看到亨利做了某件事，就好像你也跟着做过了。因此，我们也会学着考虑，如果做了会有什么后果。”父母们如果愿意跟孩子们一起读这套书，就一定会明白孩子们淘气背后的种种原因。孩子们也可以从这个“知音”亨利身上，知道如何解决问题是对的，如何解决问题会弄巧成拙。小编觉得，理解孩子们淘气的小心思，用宽容的态度陪伴孩子的成长，让孩子学会自己解决麻烦，远比让孩子事事听话，永远依赖父母要重要得多。顶级插画师配图，戏剧效果加倍这套《淘气包亨利》里面的插画，跟其他一些色彩艳丽的绘本有很大不同，因为是平装本，所以插画也是黑白的。不过爸爸妈妈们可别因此就小看了这本书的插画，它可是出自托尼·罗斯之手。 ▲英国最负盛名的插画家、绘本画家：托尼·罗斯托尼·罗斯是英国国宝级的绘本画家，也是插画界老顽童般的存在，获得过国际安徒生奖和凯特·格林威奖双重提名。他的插画，以调皮活泼著称，具有强烈的情感张力。在他看来，孩子们有自己的世界、自己的敌人、自己的规则，所以他赋予了《淘气包亨利》里每个角色不同的形象，可以看得出来，每张画的动作表情都惟妙惟肖。因为他的加入，淘气包的戏剧效果一下子就加倍了。孩子们一边读书，一边看着这样幽默调皮的插图，对故事的理解，也会越发的深刻。绿色环保，印刷精良，价格实惠这套书特别贴心的一点就是它选用了超轻纯纸浆，绿色印刷。这套书一共有8本，每一本都是很轻很薄的32开本。每一册里有4篇亨利的故事，读起来压力很小，7-14岁的孩子们看到不会有畏难情绪，还能在出行的时候随时带着翻两页。一套8本，原价142.4元，欣赏君家的悦读专享价是92元，平均一本不到12块钱，就能给孩子买一套享誉世界的、原汁原味的英语读物。书的数量有限，想入手的爸爸妈妈们可以行动了。这一次我们向大家推荐的是《淘气包亨利》第二辑一套8本原价 142.4元/套悦读专享价 92元/套全国包邮快点击下图让孩子去书中找“知音”吧长按二维码  关注【悦读书屋】发现更多好童书",
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
      "content" : "感谢您关注初中英语公众号，如您尚未关注，请点击上方蓝字“初中英语”关注我们，获取更多知识方法。每日更新，与您不见不散！今天是五一劳动节，我们正在享受三天的假期。我知道很多同学在这几天里还要学习，在这里向你们致敬了，俗话说“劳动最光荣”嘛！可是，小简老师也要提醒大家，在繁忙的学习之余也要注意身体，照顾好自己，俗话也说“身体是革命的本钱”嘛！来看看今天我给大家准备的关于五一劳动节的内容吧！★★★五一劳动节的由来★★★五一劳动节又称“五一国际劳动节”、“国际示威游行日”（International Workers’ Day或者May Day），是世界上80多个国家的全国性节日。定在每年的五月一日。它是全世界劳动人民共同拥有的节日。1889年7月，由恩格斯领导的第二国际在巴黎举行代表大会。会议通过决议，规定1890年5月1日国际劳动者举行游行，并决定把5月1日这一天定为国际劳动节。中国中央人民政府政务院于1949年12月作出决定，将5月1日确定为劳动节。各国五一劳动节的习俗中国——中央人民政府政务院于1949年12月将5月1日定为法定的劳动节，是日全国放假一天。节日里，举国欢庆，人们换上节日的盛装，兴高采烈地聚集在公园、剧院、广场，参加各种庆祝集会或文体娱乐活动，并对有突出贡献的劳动者进行表彰。泰国—— 在“五一”全国统一放假一天，在首都以及一些大城市会有相关的庆祝活动，不过规模一般都不会太大。今年泰国1日放假，2日补休。日本——日本是一个节日比较多的国家，5月1日前后的节日就很多，如4月29日植树节、5月3日宪法纪念日、4日国民假日、5日儿童节，这些假日连起来，一般日本人至少有一周休息时间，最长的甚至达11天。美国——恰逢周末，美国30日、1日都休假，但以往都只在1日休假一天，没什么庆祝活动。俄罗斯——5月1—3日全国放假，届时各政党都会齐聚红场进行演讲等，普通市民会举行游行。德国——1日放假一天，今年周末和五一节重合，但德国也只休一天，并不会补休。据悉，每年德国很多人都会借五一这个机会闹事，抗议政府，要求减税。意大利——意大利尽管承认“五一”国际劳动节，政府也表示尊重劳工，但一般人并不举行专门的庆祝活动，也没有全国性的“五一”假期。墨西哥—— 今年5月1日也是墨西哥的儿童节，但墨西哥没有全国性的休假。以前有过在五一这天工人罢工或游行等活动，但今年没有。秘鲁——1日放假，2日补休。没有什么庆祝活动。波兰——1日放假，由于3日是波兰国庆节，有的单位会从1日休到3日。5月1日时，波兰全国工会协议会、民主左派联盟党、社会民主党、劳动联盟等左派团体和政党举行了庆祝“五一”群众游行活动，游行队伍打着“8小时工作日”等标语。与劳动相关的英语词汇Labour for public good  公益劳动labor and social seurity  劳动保障rehandling duplication of labor  重复劳动fruit of labor  劳动成果labor contract law  劳动合同法physical work/manual work  体力劳动manpower demand forecasting  人才需求预测systems engineering for manpower 人才系统工程Labor and Social Security Bureau  劳动和社会保障局 labor arbitration  劳动仲裁international labor day(may day)  五一劳动节labor force/manpower  劳动力labor legislation  劳动法labor intensive  劳动密集型labour disputes  劳动争议labour discipline  劳动纪律labor of love  义务劳动  reeducation through labor  劳动教养labor economics  劳动经济学working capacity/labor capacity  劳动能力labour handbook  劳动手册paid labour  有偿劳动更多优秀文章推荐01. 中考英语1600词分类速记，赶紧收藏~02. 初一上册全部语法内容都在这里了！03. 初二上册全部语法内容都在这里了！04. 初三全册语法内容都在这里了！05. 初中英语学不好，是因为你没养成这些好习惯！06. 20首欧美经典电影主题曲（含视频/音频）关于初中英语初中英语隶属于三好网，是全国最具影响力的初中英语学习服务平台，每天提供最精准知识总结、最有效学习技巧、最新中考英语资讯，以及学习娱乐两不误的经典英文歌曲、电影等。有关初中英语学习的一切精彩，等你来关注！",
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
    "sort" : [ 1493610457000 ]
  } ]
}
```

---

六、**按照指定字段排序，通过 **keyword  **获取 **`Es`** 库中匹配到的热门结果集（微博、微信）**

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
        "_index": "weibo_articles_and_weiboers",
        "_type": "weibo_articles_and_weiboer",
        "_source":{"comment_count": 4, "sentiment": -2, "repost_count": 22, "repost_level": 0, "gender": 0,…},
        "_id": "4102512023694826",
        "sort":[
            10827132
        ]
    },
    {
        "_index": "weibo_articles_and_weiboers",
        "_type": "weibo_articles_and_weiboer",
        "_source":{"comment_count": 34, "repost_count": 145, "repost_level": 0, "gender": 1, "web_links":[],…},
        "_id": "4102550297426847",
        "sort":[
            5758927
        ]
    },
    {
        "_index": "weibo_articles_and_weiboers",
        "_type": "weibo_articles_and_weiboer",
        "_source":{"comment_count": 177, "web_links":[], "vote_links":[], "up_count": 2054,…},
        "_id": "4102679036436232",
        "sort":[
            1014487
        ]
    }
]
```

---

七、**通过**`keyword`**获取任务的计算结果集（以获取微博数据接口为例）**

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

八、**通过**`keyword`**获取任务的计算结果集（微信、贴吧、知乎问题、天涯、头条、资讯博客）**

`POST` `http://127.0.0.1/stq/api/v1/words/findWeixinByKeywords`

`POST` `http://127.0.0.1/stq/api/v1/words/findTiebaByKeywords`

`POST` `http://127.0.0.1/stq/api/v1/words/findZhihuByKeywords`

`POST` `http://127.0.0.1/stq/api/v1/words/findTianyaByKeywords`

`POST` `http://127.0.0.1/stq/api/v1/words/findToutiaoByKeywords`

`POST` `http://127.0.0.1/stq/api/v1/words/findZixunByKeywords`

`参数说明`：同微博

`BODY` 体：同微博

`response` ：同微博

