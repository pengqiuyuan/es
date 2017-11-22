十五、删除**百度新闻任务**

`POST` `http://127.0.0.1/stq/api/v1/words/deleteBaiduXinwen`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
fromId唯一标识字段，必填
keyword为监测项关键字（不为null或者空字符串），必填
```

`BODY` 体：

```
{
	"fromId":"soon-1113-21",
	"keyword":"猎场+胡歌||猎场+万茜"
}
```

`response` 删除任务返回提示信息：

```
{
	"statusCode":200,
	"keyword_id":"5a0d306918bd074c1e0aade9",
	"keyword":"猎场+胡歌||猎场+万茜",
	"msg":"[百度新闻] 删除关键词delete成功",
	"error":"",
	"stamp":1510815605552
}
```