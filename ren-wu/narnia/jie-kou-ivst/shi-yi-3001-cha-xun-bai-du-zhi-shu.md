十一、查询**百度指数**

`POST` `http://127.0.0.1/stq/api/v1/words/getBaiduIndex`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
keyword为监测项关键字（不为null或者空字符串），必填
st为监测项起始时间（含），必填
et为监测项结束时间（含），必填
```

`BODY` 体：

```
{
    "keyword": "keywordtesttest",
    "st": "2017-09-01",
    "et": "2017-09-09"
}
```

`response` 数据写入成功，返回提示信息

```
{
    "getDataSuccess": true,
    "baiduIndexList":[
        {
            "acount": "0",
            "date": "2017-09-01",
            "keyword": "keywordtesttest"
        },
        ....
        {
            "acount": "0",
            "date": "2017-09-09",
            "keyword": "keywordtesttest"
        }
    ]
}
```