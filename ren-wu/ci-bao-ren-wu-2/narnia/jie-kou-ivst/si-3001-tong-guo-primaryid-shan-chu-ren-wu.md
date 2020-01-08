# 四、通过 primaryId 删除任务

四、**通过** `primaryId` **删除任务**

`GET` `http://127.0.0.1/stq/api/v1/words/delTaskByPrimaryId?primaryId=4221&category=ivst`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```text
primaryId：主任务Id，使用添加词包任务API之后返回。
category：ivst。任务分类
```

`response` 任务执行的状态。

```text
{
    "message": "不存在 primaryId:4217的任务",
    "taskStatus": "0"
}

{
    "message": "任务删除成功",
    "taskStatus": "1"
}
```

`response` 请求失败 500

