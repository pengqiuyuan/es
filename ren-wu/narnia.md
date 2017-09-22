**POST 请求添加词包任务**

`POST` `http://127.0.0.1/stq/api/v1/words/addWordsTask`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
taskList：
添加子任务，数组结构。keyword为监测项名称，startDate为监测项起始时间（含），endDate为监测项结束时间（含），subDate是否分天（0不分天，1分天）

taskType：
监测项计算任务的数据源。weibo、weixin等等，需要约定。
```

`BODY` 体：

```
{
    "taskList": [
        {
            "keyword": "测试",
            "startDate": "2017-01-01",
            "endDate": "2017-01-10",
            "subDate": "0"
        },
        {
            "keyword": "测试",
            "startDate": "2017-01-01",
            "endDate": "2017-01-10",
            "subDate": "1"
        }
    ],
    "taskType": "weibo"
}
```

`response` 数据写入成功，返回主任务ID，通过ID可以查询出任务执行的状态

```
{
    "primaryId": 45
}
```

`response` 数据写入失败 500





