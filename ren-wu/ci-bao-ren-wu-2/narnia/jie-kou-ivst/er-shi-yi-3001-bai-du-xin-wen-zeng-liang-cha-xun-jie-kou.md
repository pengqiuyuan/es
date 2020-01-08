# 二十一、百度新闻增量查询接口

二十一、百度新闻增量查询接口

`POST` `http://127.0.0.1/stq/api/v1/words/getBaiduXinwenUpdate`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```text
fromId唯一标识字段，必填
keyword为监测项关键字（不为null或者空字符串），必填
startDate为监测项起始时间（含），必填
endDate为监测项结束时间（含），必填
updateDate为上次增量更新时间点，必填
```

`BODY` 体：

```text
{
    "fromId":"58560a44731f6c8f5a851bf2",
    "keyword":"猎场",
    "startDate":"2017-11-01",
    "endDate":"2017-11-02",
    "updateDate":"2017-11-21"
}
```

`response` Es查询

结果

```text
{
    "statusCode": 200,
    "keyword_id": "58560a44731f6c8f5a851bf2",
    "keyword": "猎场",
    "news": [
        {
            "_id": "5a1cb3cb1613daceb7fe79c1",
            "date": "2017-11-01T00:00:00.000Z",
            "keyword": "猎场",
            "create_at": "2017-11-28T00:54:35.353Z",
            "count": 86
        },
        {
            "_id": "5a1cb3d61613daceb7fe7a5d",
            "date": "2017-11-02T00:00:00.000Z",
            "keyword": "猎场",
            "create_at": "2017-11-28T00:54:46.471Z",
            "count": 88
        }
    ],
    "msg": "[百度新闻] 查询关键词提及量get成功",
    "error": "",
    "stamp": 1511922948490
}
```

