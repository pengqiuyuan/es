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



