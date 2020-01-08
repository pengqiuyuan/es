# 一、数据采集

**一**、**创建任务**

`POST` `http://127.0.0.1/stq/api/v1/text/addTextTaskBySeeds?appId=1&token=2`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```text
appId 必填 权限验证字段
token 必填 权限验证字段
date 必填 获取哪一天的关键词数据
keyword 必填 获取数据的关键词
```

`BODY` 体：

```text
[{
    "date": "2018-01-01",
    "keyword": "杨洋"
}, {
    "date": "2018-01-01",
    "keyword": "关晓彤"
}]
```

`response` 返回提示信息

```text
没有访问权限
{
    "code": "0",
    "msg": "no authorization to access"
}

任务添加成功
{
    "code": "1",
    "msg": "create task success",
    "jobId": "16",
}

任务添加失败
{
    "code": "0",
    "msg": "create task faild, too much task in queue"
}
```

**二**、**查询任务状态**

`GET` `http://127.0.0.1/stq/api/v1/text/findTaskStatusByJobId?jobId=26&appId=1&token=1`

`HEADERS`：`"Content-Type" => "application/json"`

`请求参数说明`：

```text
appId 必填 权限验证字段
token 必填 权限验证字段
jobId 必填 根据创建任务成功时返回的 jobId 查询任务执行状态
```

`返回参数说明`：

```text
statue
    waiting 等待执行
    running 任务执行中
    exported 任务已完成
```

`response` 返回提示信息

```text
没有访问权限
{
    "code": "0",
    "msg": "no authorization to access"
}

成功
{
    "code": "1",
    "msg": "getting data state success",
    "jobId": "16",
    "statue": "exported"
}

失败
{
    "code": "0",
    "msg": "getting data state failure"
}
```

**三**、**获取数据下载地址**

`GET` `http://127.0.0.1/stq/api/v1/text/getTaskResultByJobId?jobId=26&appId=1&token=1`

`HEADERS`：`"Content-Type" => "application/json"`

`请求参数说明`：

```text
appId 必填 权限验证字段
token 必填 权限验证字段
jobId 必填 根据创建任务成功时返回的 jobId 获取结果
```

`返回参数说明`：

```text
statue
    waiting 等待执行
    running 任务执行中
    exported 任务已完成
url
    数据保存地址
```

`response` 返回提示信息

```text
没有访问权限
{
    "code": "0",
    "msg": "no authorization to access"
}

成功
{
    "msg": "getting data result success",
    "jobId": "25",
    "code": "1",
    "statue": "exported",
    "url": "https://narnia.oss-cn-beijing.aliyuncs.com/tencent_20180628144404061_20180628144423.xlsx?Expires=1845528267&OSSAccessKeyId=LTAIARWAKGUIqkn6&Signature=A9vIzAKYqfp6kuqtKC2nZNt9LHQ="
}

失败
{
    "code": "0",
    "msg": "getting data result failure"
}
```

