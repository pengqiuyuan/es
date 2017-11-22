十二、删除**百度指数任务**

`POST` `http://127.0.0.1/stq/api/v1/words/deleteBaiduIndexKeyword`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
theOnlyIdentifier唯一标识字段
```

`BODY` 体：

```
{
    "theOnlyIdentifier": "theOnlyIdentifier"
}
```

`response` 数据写入成功，返回提示信息

```
{
    "deleteBaiduIndexSuccess": true,
    "theOnlyIdentifier": "theOnlyIdentifier"
}
```