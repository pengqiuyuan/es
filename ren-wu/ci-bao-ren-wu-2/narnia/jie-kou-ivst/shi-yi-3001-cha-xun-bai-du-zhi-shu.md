# 十一、查询百度指数

十一、查询**百度指数**

`POST` `http://127.0.0.1/stq/api/v1/words/getBaiduIndex`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```text
keyword为监测项关键字（不为null或者空字符串），必填
st为监测项起始时间（含），必填
et为监测项结束时间（含），必填
```

`BODY` 体：

```text
{
    "keyword": "keywordtesttest",
    "st": "2017-09-01",
    "et": "2017-09-09"
}
```

`response` 数据写入成功，返回提示信息

```text
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

十一、查询**百度指数** \(带数据最新更新时间\)

`POST` `http://127.0.0.1/stq/api/v1/words/getBaiduIndexWithRefreshDate`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```text
keyword为监测项关键字（不为null或者空字符串），必填
st为监测项起始时间（含），必填
et为监测项结束时间（含），必填
```

`BODY` 体：

```text
{
    "keyword": "寻龙诀",
    "st": "2017-09-01",
    "et": "2017-09-09"
}
```

`response` 数据写入成功，返回提示信息

```text
{
    "getDataSuccess": true,
    "refreshDate": "2017-11-26",
    "baiduIndexList": [
        {
            "acount": "1789",
            "date": "2017-09-01",
            "keyword": "寻龙诀"
        }
    ]
}
```

