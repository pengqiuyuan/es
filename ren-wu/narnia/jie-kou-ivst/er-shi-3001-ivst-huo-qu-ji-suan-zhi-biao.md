十九、Ivst 根据`keyword`、`startDate`、`endDate`、`updateDate` 获取计算指标

`POST` `http://127.0.0.1/stq/api/v1/words/findIvstCibaoIndexByKeyword`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
keyword为监测项名称，不可为空
startDate为监测项起始时间（含），传空字符串，默认为当前时间
endDate为监测项结束时间（结果不包含这一天），传空字符串，默认为当前时间+1天
updateDate为数据源更新时间，传空字符串，默认为当前时间
```

`BODY` 体：

```
{
  "keyword": "西游伏妖篇",
  "startDate": "2016-01-01",
  "endDate": "2017-11-29",
  "updateDate":"2017-11-28"
}
```

`response` Es查询

结果

```
{
  "weibo":[{"_index": "cibao_index", "_type": "cibao_index", "_source":{"updateDate": "1511798400000",…],
  "weixin":[{"_index": "cibao_index", "_type": "cibao_index", "_source":{"updateDate": "1511798400000",…]
}
```



