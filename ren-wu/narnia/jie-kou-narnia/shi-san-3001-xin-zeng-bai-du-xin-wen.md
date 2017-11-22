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