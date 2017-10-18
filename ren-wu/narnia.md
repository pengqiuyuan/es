**一**、**添加词包任务**

`POST` `http://127.0.0.1/stq/api/v1/words/addIvstWordsTask`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
添加剧目任务

keyword为监测项名称
startDate为监测项起始时间（含），不可以大于结束时间
endDate为监测项结束时间（含），不可以大于当前时间，可以为空字符串（代表无限期计算）
```

`BODY` 体：

```
{
    "keyword": "测试",
    "startDate": "2017-01-01",
    "endDate": "2017-01-10"
}
```

`response` 数据写入成功，返回提示信息

```
{
    "message": "任务添加成功"
}

或者

{
    "message": "任务已存在"
}
```

`response` 数据写入失败 500

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

