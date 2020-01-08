# 接口 Ivst

**一**、**添加词包任务**

`POST` `http://127.0.0.1/stq/api/v1/words/addWordsTask`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```text
添加剧目任务

keyword为监测项关键字（不为null或者空字符串）
startDate为监测项起始时间（含），不可以大于结束时间
endDate为监测项结束时间（含），不可以大于当前时间，可以为空字符串（代表无限期计算）
category为标识字段（Narnia 项目使用 narnia，Ivst 项目使用 ivst，旅游项目使用 travel）
```

`BODY` 体：

```text
{
    "keyword": "大鱼海棠",
    "startDate": "2017-01-01",
    "endDate": "2017-01-10",
    "category":"ivst" #注意：Narnia 项目使用 narnia，Ivst 项目使用 ivst，旅游项目使用 travel
}
```

`response` 数据写入成功，返回提示信息

```text
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

