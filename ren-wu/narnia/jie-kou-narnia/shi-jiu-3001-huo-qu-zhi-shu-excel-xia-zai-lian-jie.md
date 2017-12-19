十九、获取计算指标 Excel 下载链接

`POST` `http://127.0.0.1/stq/api/v1/words/findEsWeiboUserAnalysis`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
keyword为监测项名称，必填
startDate为监测项起始时间（含），必填
endDate为监测项结束时间（含），必填
taskType为数据源，必填，weibo、weixin、baiduindex
```

`BODY` 体：

```
{
  "keyword": "清华大学",
  "startDate": "2017-10-01",
  "endDate": "2017-12-02",
  "taskType":"weibo"
}
```

`response` 返回数据：

```
成功

{
    "msPath": "https://narnia.oss-cn-beijing.aliyuncs.com/20171219163117.xlsx?Expires=1515499666&OSSAccessKeyId=LTAIARWAKGUIqkn6&Signature=QHMUJKSKHjsZM6Ob91mjQ6tzrw0%3D",
    "message": "任务执行成功"
}

失败

{
    "msPath": "",
    "message": "任务执行失败"
}
```



