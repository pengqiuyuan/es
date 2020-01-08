# 四、获取热门话题 TopN

四、**获取热门话题 TopN**

`POST` `http://127.0.0.1/stq/api/v1/rowlet/findTopNTopics`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```text
startDate为起始时间（含），必填。
endDate为结束时间（不含），必填。
category为数据源 tw、fb，必填
pageSize，必填。获取多少条
ids 必填。数组
```

`BODY` 体：

```text
twitter

{
    "startDate": "2016-10-09",
    "endDate": "2017-12-10",
    "category": "tw",
    "pageSize": "10",
    "ids": ["113036476", "216481299", "44254802"]
}
```

`response` Es查询有保存计算指标

`Twitter`

```text
{
    "tw": [{
            "doc_count": 59,
            "key": "MISOTS17"
        },
        {
            "doc_count": 39,
            "key": "MIBudget"
        },
        {
            "doc_count": 28,
            "key": "Michigan"
        },
        {
            "doc_count": 24,
            "key": "25by25MN"
        },
        {
            "doc_count": 22,
            "key": "GoingPROinMI"
        },
        {
            "doc_count": 20,
            "key": "NAIAS"
        },
        {
            "doc_count": 16,
            "key": "Detroit"
        },
        {
            "doc_count": 16,
            "key": "MPC17"
        },
        {
            "doc_count": 15,
            "key": "mnleg"
        },
        {
            "doc_count": 14,
            "key": "MyMNCapitol"
        }
    ],
    "message": "任务成功"
}
```

