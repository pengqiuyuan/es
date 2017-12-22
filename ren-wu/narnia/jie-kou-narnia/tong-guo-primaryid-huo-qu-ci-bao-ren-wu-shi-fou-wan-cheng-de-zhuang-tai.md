
二、**通过 **`primaryId`** 获取词包任务是否完成的状态**

`GET` `http://127.0.0.1/stq/api/v1/words/findTaskStatusByPrimaryId?primaryId=4221`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
primaryId：主任务Id，使用添加词包任务API之后返回。
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

`response` 请求失败 500

---