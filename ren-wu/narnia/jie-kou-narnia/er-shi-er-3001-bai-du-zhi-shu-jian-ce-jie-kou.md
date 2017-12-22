二十二、百度指数检测接口

`POST` `http://127.0.0.1/stq/api/v1/words/checkBaiduIndex`

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
    "keyword": "High School Love On",
    "st": "2017-09-01",
    "et": "2017-09-09"
}
```

`response` 数据写入成功，返回提示信息，`isDataCompleted为true说明检测时间段内的数据是完整的，为false则说明检测时间段内的数据不完整` 

```
{
    "getDataSuccess": true,
    "isDataCompleted": true
}
```



