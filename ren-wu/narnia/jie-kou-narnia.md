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