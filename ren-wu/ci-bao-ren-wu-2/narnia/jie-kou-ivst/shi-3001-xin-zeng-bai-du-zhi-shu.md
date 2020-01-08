# 十、新增百度指数

十、新增**百度指数**

`POST` `http://127.0.0.1/stq/api/v1/words/addBaiduIndexKeyword`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```text
theOnlyIdentifier唯一标识字段，必填
keyword为监测项关键字（不为null或者空字符串），必填
st为监测项起始时间（含），必填
et为监测项结束时间（含），此参数可以不传，表示无限计算百度指数
```

`BODY` 体：

```text
{
    "theOnlyIdentifier": "theOnlyIdentifier",
    "keyword": "keywordtesttest",
    "st": "2017-01-01",
    "et": "2017-09-09"
}

或者（下面示例为无限）

{
    "theOnlyIdentifier": "theOnlyIdentifier",
    "keyword": "keywordtesttest",
    "st": "2017-01-01"
}
```

`response` 数据写入成功，返回提示信息

```text
{
    "addBaiduIndexSuccess": true,
    "theOnlyIdentifier": "theOnlyIdentifier"
}
```

