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