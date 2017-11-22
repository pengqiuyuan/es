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