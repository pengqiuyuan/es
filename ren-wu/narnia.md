**添加词包任务**

`POST` `http://127.0.0.1/stq/api/v1/words/addWordsTask`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
taskList：
添加子任务，数组结构。keyword为监测项名称，startDate为监测项起始时间（含），endDate为监测项结束时间（含），subDate是否分天（0不分天，1分天）

taskType：
监测项计算任务的数据源。weibo、weixin等等，需要约定。
```

`BODY` 体：

```
{
    "taskList": [
        {
            "keyword": "测试",
            "startDate": "2017-01-01",
            "endDate": "2017-01-10",
            "subDate": "0"
        },
        {
            "keyword": "测试",
            "startDate": "2017-01-01",
            "endDate": "2017-01-10",
            "subDate": "1"
        }
    ],
    "taskType": "weibo"
}
```

`response` 数据写入成功，返回主任务ID，通过ID可以查询出任务执行的状态

```
{
    "primaryId": 45
}
```

`response` 数据写入失败 500

---

**通过 **`primaryId`** 获取词包任务是否完成的状态**

`GET` `http://127.0.0.1/stq/api/v1/words/findTaskStatusByPrimaryId?primaryId=3`

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
    "message": "任务已完成，可以调用 findByKeywords 接口查询！",
    "taskStatus": "2"
}

{
    "message": "任务执行错误！",
    "taskStatus": "3"
}
```

`response` 请求失败 500

---

**通过**`keyword`**获取词包任务的计算结果集**

`POST` `http://127.0.0.1/stq/api/v1/words/findByKeywords`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
keyword为监测项名称，startDate为监测项起始时间（含），endDate为监测项结束时间（含），subDate是否分天（0不分天，1分天）
，taskType监测项计算任务的数据源 weibo、weixin等等，需要约定。
```

`BODY` 体：

```
{
    "keyWord": "你的名字+电影",
    "startDate": "2016-11-02",
    "endDate": "2016-11-04",
    "subDate": "1",
    "taskType": "weibo"
}
```

`response` Es查询有保存计算指标

```
[
    {
        "keywords": "你的名字+电影",
        "startDate": "2016-11-02",
        "endDate": "2016-11-03",
        "volume": "3183",
        "actualVolume": "90",
        "exposure": "8431309",
        "interactive": "781",
        "oldInteractive": "13968",
        "forwardDepth": "6"
    },
    {
        "keywords": "你的名字+电影",
        "startDate": "2016-11-03",
        "endDate": "2016-11-04",
        "volume": "3523",
        "actualVolume": "104",
        "exposure": "11498147",
        "interactive": "1556",
        "oldInteractive": "35741",
        "forwardDepth": "7"
    },
        {
        "keywords": "你的名字+电影",
        "startDate": "2016-11-04",
        "endDate": "2016-11-05",
        "volume": "1361",
        "actualVolume": "52",
        "exposure": "5158912",
        "interactive": "481",
        "oldInteractive": "7410",
        "forwardDepth": "3"
    }
]
```

`response` Es查询没有保存计算指标

```
[]
```

`response` 请求失败 500

