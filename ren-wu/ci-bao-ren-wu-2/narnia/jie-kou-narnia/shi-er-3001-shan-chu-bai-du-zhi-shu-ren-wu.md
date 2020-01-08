# 十二、删除百度指数任务

十二、删除**百度指数任务**

`POST` `http://127.0.0.1/stq/api/v1/words/deleteBaiduIndexKeyword`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```text
theOnlyIdentifier唯一标识字段
```

`BODY` 体：

```text
{
    "theOnlyIdentifier": "theOnlyIdentifier"
}
```

`response` 数据写入成功，返回提示信息

```text
{
    "deleteBaiduIndexSuccess": true,
    "theOnlyIdentifier": "theOnlyIdentifier"
}
```

