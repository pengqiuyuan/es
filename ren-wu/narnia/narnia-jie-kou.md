**一**、**添加词包任务**

`POST` `http://127.0.0.1/stq/api/v1/words/addWordsTask`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
添加剧目任务

keyword为监测项关键字
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

三、**通过 **`primaryId`** 删除任务**

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

四、**通过**`keyword`**获取 **`Es`** 库中匹配到的结果集（微博、微信）**

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

```


五、**通过**`keyword`**获取 **`IVST`** 剧目任务的计算结果集（以获取微博数据接口为例）**

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

三、**通过**`keyword`**获取 **`IVST`** 剧目任务的计算结果集（微信、贴吧、知乎问题、天涯、头条、资讯博客）**

`POST` `http://127.0.0.1/stq/api/v1/words/findWeixinByKeywords`

`POST` `http://127.0.0.1/stq/api/v1/words/findTiebaByKeywords`

`POST` `http://127.0.0.1/stq/api/v1/words/findZhihuByKeywords`

`POST` `http://127.0.0.1/stq/api/v1/words/findTianyaByKeywords`

`POST` `http://127.0.0.1/stq/api/v1/words/findToutiaoByKeywords`

`POST` `http://127.0.0.1/stq/api/v1/words/findZixunByKeywords`

`参数说明`：同微博

`BODY` 体：同微博

`response` ：同微博

