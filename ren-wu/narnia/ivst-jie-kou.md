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
    "category":"ivst" #注意：Narnia 项目使用 narnia，Ivst 项目使用 ivst，旅游项目使用 travel
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

`GET` `http://127.0.0.1/stq/api/v1/words/delTaskByPrimaryId?primaryId=4221&category=ivst`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
primaryId：主任务Id，使用添加词包任务API之后返回。
category：ivst。任务分类
```

`response` 任务执行的状态。

```
{
    "message": "不存在 primaryId:4217的任务",
    "taskStatus": "0"
}

{
    "message": "任务删除成功",
    "taskStatus": "1"
}
```

`response` 请求失败 500

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

---

九、修改**词包任务**

`POST` `http://127.0.0.1/stq/api/v1/words/updateWordsTask`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
修改词包任务，支持4个字段的修改

keyword为监测项关键字（不为null或者空字符串）
startDate为监测项起始时间（含），不可以大于结束时间
endDate为监测项结束时间（含），不可以大于当前时间，可以为空字符串（代表无限期计算）
category为标识字段（Narnia 项目使用 narnia，Ivst 项目使用 ivst，旅游项目使用 travel）
primaryId为Long类型，与新增任务是返回的 primaryId 一致。
```

`BODY` 体：

```
{
  "keyword": "冰美人",
  "startDate": "2016-01-01",
  "endDate": "",
  "category":"ivst", #注意：Narnia 项目使用 narnia，Ivst 项目使用 ivst，旅游项目使用 travel
  "primaryId":4219
}
```

`response` 数据写入成功，返回提示信息

```
{
    "message": "任务修改成功",
    "primaryId":[
        "4219"
    ],
    "taskStatus": "1"
}

或者

{
    "message": "任务修改失败",
    "primaryId":[
        "4219"
    ],
    "taskStatus": "0"
}
```

`response` 数据写入失败 500

---

十、新增**百度指数**

`POST` `http://127.0.0.1/stq/api/v1/words/addBaiduIndexKeyword`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
theOnlyIdentifier唯一标识字段，必填
keyword为监测项关键字（不为null或者空字符串），必填
st为监测项起始时间（含），必填
et为监测项结束时间（含），此参数可以不传，表示无限计算百度指数
```

`BODY` 体：

```
{
    "theOnlyIdentifier": "theOnlyIdentifier",
    "keyword": "keywordtesttest",
    "st": "2017-01-01",
    "et": "2017-09-09"
}

或者（下面示例为无限）

{
    "theOnlyIdentifier": "theOnlyIdentifier",
    "keyword": "keywordtesttest",
    "st": "2017-01-01"
}
```

`response` 数据写入成功，返回提示信息

```
{
    "addBaiduIndexSuccess": true,
    "theOnlyIdentifier": "theOnlyIdentifier"
}
```

---

十一、查询**百度指数**

`POST` `http://127.0.0.1/stq/api/v1/words/getBaiduIndex`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
keyword为监测项关键字（不为null或者空字符串），必填
st为监测项起始时间（含），必填
et为监测项结束时间（含），必填
```

`BODY` 体：

```
{
    "keyword": "keywordtesttest",
    "st": "2017-09-01",
    "et": "2017-09-09"
}
```

`response` 数据写入成功，返回提示信息

```
{
    "getDataSuccess": true,
    "baiduIndexList":[
        {
            "acount": "0",
            "date": "2017-09-01",
            "keyword": "keywordtesttest"
        },
        ....
        {
            "acount": "0",
            "date": "2017-09-09",
            "keyword": "keywordtesttest"
        }
    ]
}
```

---

十二、删除**百度指数任务**

`POST` `http://127.0.0.1/stq/api/v1/words/deleteBaiduIndexKeyword`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
theOnlyIdentifier唯一标识字段
```

`BODY` 体：

```
{
    "theOnlyIdentifier": "theOnlyIdentifier"
}
```

`response` 数据写入成功，返回提示信息

```
{
    "deleteBaiduIndexSuccess": true,
    "theOnlyIdentifier": "theOnlyIdentifier"
}
```
---

十三、新增**百度新闻**

`POST` `http://127.0.0.1/stq/api/v1/words/addBaiduXinwen`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
fromId唯一标识字段，必填
keyword为监测项关键字（不为null或者空字符串），必填
startDate为监测项起始时间（含），必填
endDate为监测项结束时间（含），此参数可以不传，表示无限计算百度新闻
```

`BODY` 体：

```
{
	"fromId":"soon-1113-21",
	"keyword":"猎场+胡歌||猎场+万茜",
	"startDate":"2017-09-01",
	"endDate":"2017-09-09"
}
```

`response` 数据写入成功，返回提示信息

```
成功：
{
	"statusCode":200,
	"keyword_id":"5a0d2fc318bd074c1e0aade8",
	"keyword":"猎场+胡歌||猎场+万茜",
	"msg":"[百度新闻] 添加关键词add成功",
	"error":"",
	"stamp":1510813635596
}

失败：
{
	"statusCode":400,	
	"keyword_id":"",
	"keyword":"猎场+胡歌||猎场+万茜",
	"msg":"[百度新闻] 添加关键词add失败",
	"error":"add 请求参数不完整",
	"stamp":1510813812817
}

```

---

十四、检测百度新闻爬取情况

`POST` `http://127.0.0.1/stq/api/v1/words/checkBaiduXinwenStatus`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
fromId唯一标识字段，必填
keyword为监测项关键字（不为null或者空字符串），必填
startDate为监测项起始时间（含），必填
endDate为监测项结束时间（含），必填
```

`BODY` 体：

```
{
	"fromId":"soon-1113-21",
	"keyword":"猎场+胡歌||猎场+万茜",
	"startDate":"2017-09-01",
	"endDate":"2017-09-09"
}
```

`response` 数据写入成功，返回提示信息

```
成功：
{
	"statusCode":200,
	"keyword_id":"5a0d2fc318bd074c1e0aade8",
	"keyword":"猎场+胡歌||猎场+万茜",
	"status":"数据完整",
	"msg":"[百度新闻] 查询关键词状态status成功",
	"error":"",
	"stamp":1510814653954
}

失败:
{
	"statusCode":400,
	"keyword_id":"5a0d2fc318bd074c1e0aade8",
	"keyword":"猎场+胡歌||猎场+万茜",
	"status":"数据不完整",
	"msg":"[百度新闻] 查询关键词状态status失败",
	"error":"查询结束时间(2017-11-30)大于结束监测时间(2017-09-09)",
	"stamp":1510815253712
}
```

---

十五、删除**百度新闻任务**

`POST` `http://127.0.0.1/stq/api/v1/words/deleteBaiduXinwen`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
fromId唯一标识字段，必填
keyword为监测项关键字（不为null或者空字符串），必填
```

`BODY` 体：

```
{
	"fromId":"soon-1113-21",
	"keyword":"猎场+胡歌||猎场+万茜"
}
```

`response` 删除任务返回提示信息：

```
{
	"statusCode":200,
	"keyword_id":"5a0d306918bd074c1e0aade9",
	"keyword":"猎场+胡歌||猎场+万茜",
	"msg":"[百度新闻] 删除关键词delete成功",
	"error":"",
	"stamp":1510815605552
}
```

---

十六、获得百度新闻声量数据

`POST` `http://127.0.0.1/stq/api/v1/words/getBaiduXinwenVolume`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
fromId唯一标识字段，必填
keyword为监测项关键字（不为null或者空字符串），必填
startDate为监测项起始时间（含），必填
endDate为监测项结束时间（含），必填
```

`BODY` 体：

```
{
	"fromId":"soon-1113-21",
	"keyword":"猎场+胡歌||猎场+万茜",
	"startDate":"2017-11-01",
	"endDate":"2017-11-02"
}
```

`response` 数据写入成功，返回提示信息

```
{
    "statusCode": 200,
    "keyword_id": "5a0d393318bd074c1e0aadeb",
    "keyword": "猎场+胡歌||猎场+万茜",
    "news": [
        {
            "_id": "5a0d39a61613daceb7eeb4b4",
            "date": "2017-11-01T00:00:00.000Z",
            "key_id": "5a0d393318bd074c1e0aadeb",
            "create_at": "2017-11-16T07:09:26.206Z",
            "count": 91
        },
        {
            "_id": "5a0d39ae1613daceb7eeb4b7",
            "date": "2017-11-02T00:00:00.000Z",
            "key_id": "5a0d393318bd074c1e0aadeb",
            "create_at": "2017-11-16T07:09:34.151Z",
            "count": 127
        }
    ],
    "msg": "[百度新闻] 查询关键词提及量get成功",
    "error": "",
    "stamp": 1510816463419
}
```

---

十七、获取百度新闻文章

`POST` `http://127.0.0.1/stq/api/v1/words/getBaiduXinwenArticle`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
fromId唯一标识字段，必填
keyword为监测项关键字（不为null或者空字符串），必填
startDate为监测项起始时间（含），必填
endDate为监测项结束时间（含），必填
```

`BODY` 体：

```
{
	"fromId":"soonfy-1113-21",
	"keyword":"猎场+胡歌||猎场+万茜",
	"startDate":"2017-01-01",
	"endDate":"2017-09-09"
}
```

`response` 返回文章数据和提示信息：

```

成功：
{
    "statusCode": 200,
    "keyword_id": "5a0be316cacb184e8e0aa9e3",
    "keyword": "猎场+胡歌||猎场+万茜",
    "total": 1,
    "news": [
        {
            "id": "5a0be316cacb184e8e0aa9e3httpmzmopcoma170707130115142html",
            "author": "猫扑",
            "title": "电视剧《猎场》能否挽回多事之秋的乐视?",
            "summary": "《猎场》是东阳青雨传媒股份有限公司、浙江影视集团、蓝色星空影业出品,由姜伟执导,胡歌、孙红雷、张嘉译、祖峰等大牌主演的国内首部以猎头在商界中纵横捭阖、在情感上",
            "date": "2017-07-07T05:00:00.000Z",
            "url": "http://mz.mop.com/a/170707130115142.html",
            "crawl_at": "2017-11-15T06:53:04.824Z"
        }
    ],
    "msg": "[百度新闻] 查询关键词原文content成功",
    "error": "",
    "stamp": 1510813121324
}

失败：
{
	"statusCode":400,
	"keyword_id":"",
	"keyword":"猎场+胡歌||猎场+万茜",
	"total":0,
	"news":[],
	"msg":"[百度新闻] 查询关键词原文content失败",
	"error":"content 请求没有匹配到关键词",
	"stamp":1510813215063
}

```

---

十八、微博用户画像

`POST` `http://127.0.0.1/stq/api/v1/words/findEsWeiboUserAnalysis`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
keyword为监测项关键字（不为null或者空字符串），必填
```

`BODY` 体：

```
{
    "keyword":"淘气爷孙"
}
```

`response` 返回数据：

```
[
    {
        "_index": "cibao_user_analysis",
        "_type": "cibao_user_analysis",
        "_source": {
            "birthMap": {
                "19岁及以下": 37,
                "20-29岁": 542,
                "30-39岁": 301,
                "40-49岁": 59,
                "50岁及以上": 20
            },
            "cityMap": {
                "南宁": 14,
                "嘉兴": 10,
                "济南": 32,
                "昆明": 16,
                "徐州": 14,
                "临沂": 11,
                "厦门": 26,
                "宁波": 27,
                "东莞": 26,
                "石家庄": 14,
                "无锡": 15,
                "贵阳": 14,
                "肇庆": 12,
                "长春": 13,
                "哈尔滨": 13,
                "合肥": 17,
                "温州": 31,
                "珠海": 11,
                "青岛": 32,
                "大连": 14,
                "杭州": 110,
                "南昌": 17,
                "福州": 24,
                "成都": 65,
                "江门": 23,
                "沈阳": 24,
                "长沙": 36,
                "其他": 79,
                "镇江": 12,
                "唐山": 22,
                "中山": 15,
                "常州": 13,
                "武汉": 50,
                "深圳": 102,
                "惠州": 10,
                "广州": 197,
                "梅州": 11,
                "泉州": 16,
                "西安": 41,
                "郑州": 33,
                "烟台": 11,
                "台北市": 16,
                "南京": 46,
                "佛山": 45,
                "苏州": 16
            },
            "privinceMap": {
                "山东": 137,
                "福建": 93,
                "台湾": 35,
                "河南": 80,
                "河北": 66,
                "重庆": 43,
                "湖北": 81,
                "湖南": 61,
                "江西": 39,
                "海南": 13,
                "黑龙江": 21,
                "天津": 38,
                "陕西": 52,
                "贵州": 20,
                "新疆": 13,
                "澳门": 16,
                "江苏": 155,
                "安徽": 38,
                "西藏": 7,
                "上海": 226,
                "吉林": 26,
                "香港": 89,
                "山西": 19,
                "甘肃": 17,
                "宁夏": 7,
                "四川": 106,
                "其他": 135,
                "浙江": 215,
                "广西": 27,
                "云南": 30,
                "海外": 181,
                "内蒙古": 14,
                "辽宁": 61,
                "广东": 522,
                "青海": 4,
                "北京": 265
            },
            "updateDate": 1511193600000,
            "followerMap": {
                "999及以下": 89891,
                "100000以上": 2134,
                "1000-4999": 5289,
                "5000-49999": 4638,
                "50000-99999": 53
            },
            "keywords": "淘气爷孙",
            "endDate": 1511193600000,
            "verifyMap": {
                "0": 3148,
                "1": 122,
                "2": 248
            },
            "source": "weibo",
            "genderMap": {
                "0": 1646,
                "1": 1872
            },
            "relationMap": {
                "恋爱中": 2,
                "已婚": 5,
                "暗恋中": 1,
                "丧偶": 1,
                "离异": 1,
                "单身": 41,
                "求交往": 8
            },
            "eduMap": {
                "高中": 35,
                "大专": 262,
                "初中": 61,
                "小学": 22,
                "本科及以上": 420
            },
            "fansMap": {
                "999及以下": 98619,
                "100000以上": 0,
                "1000-4999": 3386,
                "5000-49999": 0,
                "50000-99999": 0
            },
            "updateDateString": "2017-11-21",
            "startDateString": "2016-01-01",
            "endDateString": "2017-11-21",
            "startDate": 1451577600000
        },
        "_id": "VTN1cUliVUZ6Nlpmdk1GWnphUUpqdWlld2VpYm8=",
        "_score": 1
    }
]

或者

[]

```

