三、**通过 **`primaryId`** 集合，批量获取词包任务是否完成的状态，返回集合**

`POST` `http://127.0.0.1/stq/api/v1/words/findTaskStatusByPrimaryIdList`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
primaryId：主任务Id，使用添加词包任务API之后返回。
```

`BODY`体：

```
[1,2,3,1999]
```

`response` 任务执行的状态，四种结果。

```
{
    "message": "任务未开始",
    "taskStatus": "0"
}

{
    "message": "任务进行中",
    "taskStatus": "1"
}

{
    "message": "任务已完成",
    "taskStatus": "2"
}

{
    "message": "任务执行错误！",
    "taskStatus": "3"
}
```

`response` 数据写入成功，返回提示信息

```
[
    {
        "message": "任务已完成",
        "primaryId": "1",
        "taskStatus": "2"
    },
    {
        "message": "任务已完成",
        "primaryId": "2",
        "taskStatus": "2"
    },
    {
        "message": "任务已完成",
        "primaryId": "3",
        "taskStatus": "2"
    },
    {
        "message": "任务已完成",
        "primaryId": "1999",
        "taskStatus": "2"
    }
]
```

`response` 请求失败 500