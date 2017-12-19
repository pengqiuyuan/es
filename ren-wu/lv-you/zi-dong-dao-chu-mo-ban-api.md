**一**、自动导出月报模板

`POST` `http://127.0.0.1/stq/api/v1/poi/getMsFile`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
category 必填项，根据 category 定义导出相应模板文件。viewspot（景区）、hotel（酒店）、travel（旅游路线）
jsonData 必填项，json字符串。
```

`BODY` 体：

```
{
    "category": "viewspot",
    "jsonData": {
        "content": {
            "report_date": "2017-12月",
            "abstract": "根据TAPI中国旅游景区价格指数监测系统数据显示，全国5A级旅游景区平均价格指数116.2元，与上个月相比环比下降41.9%，比4A级旅游景区平均价格指数高25.3元，比3A级旅游景区平均价格指数高63.1元；全国31个省（市、自治区）旅游景区价格水平指数最高的省（市、自治区）是西藏，最低的是新疆；全国旅游景区价格波动幅度最大的省（市、自治区）是北京，与上个月相比环比下降50%。",
            "h1_p1": "2017年11月，全国5A级旅游景区平均价格指数116.2元，比4A级旅游景区平均价格指数高25.3元，比3A级旅游景区平均价格指数高63.1元。",
            "h1_sub1_bar": {
                "data": [
                    {
                        "level": "5星",
                        "price": 607.65
                    },
                    {
                        "level": "4星",
                        "price": 416.07
                    },
                    {
                        "level": "3星",
                        "price": 274.43
                    },
                    {
                        "level": "民宿客栈",
                        "price": 266.16
                    },
                    {
                        "level": "2星或以下",
                        "price": 228.73
                    },
                    {
                        "level": "经济型",
                        "price": 205.58
                    }
                ],
                "type": "bar"
            },
            ...
            ...
            ...
        }
    }
}
```

`response` 返回提示信息

```
成功：

{
    "msPath": "https://narnia.oss-cn-beijing.aliyuncs.com/TAPI%E4%B8%AD%E5%9B%BD%E6%97%85%E6%B8%B8%E6%99%AF%E5%8C%BA%E4%BB%B7%E6%A0%BC%E6%8C%87%E6%95%B0%E6%9C%88%E6%8A%A5_20171219131524.docx?Expires=1515487914&OSSAccessKeyId=LTAIARWAKGUIqkn6&Signature=nRosLQ36a%2BhTEA7hyNcg7db3Fzs%3D",
    "message": "任务执行成功"
}

失败：1、检查输入body体 category、jsonData 是否包含。2、检查 jsonData 是否value 含有 null 值。

{
    "msPath": "",
    "message": "任务执行错误"
}
```



