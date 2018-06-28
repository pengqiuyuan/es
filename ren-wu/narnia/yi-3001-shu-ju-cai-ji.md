**一**、**创建任务**

`POST` `http://127.0.0.1/stq/api/v1/text/addTextTaskBySeeds?appId=1&token=2`

`HEADERS`：`"Content-Type" => "application/json"`

`BODY` 体：

```
{
    "keyword": "大鱼海棠",
    "startDate": "2017-01-01",
    "endDate": "2017-01-10",
    "category":"narnia" #注意：Narnia 项目使用 narnia，Ivst 项目使用 ivst，旅游项目使用 travel
}

```

`参数说明`：

```

```


```

`response` 数据写入成功，返回提示信息

```
{
    "message": "任务添加成功",
    "primaryId":[
        "4220"
    ]
}

或者

{
    "message": "任务修改失败，参数不能为空"
}
```

`response` 数据写入失败 500