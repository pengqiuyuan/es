**一**、自动导出月报模板

`POST` `http://127.0.0.1/stq/api/v1/poi/downNarniaReportByJsonDate`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
jsonData 必填项，json字符串。
```

`BODY` 体：

```
{
      "jsonData":{
        "code": 0,
        "msg": "",
        "data": {
            "title": "王老吉",
            "titleDate": "2017年12月18日-2017年12月21日",
            "summary": "根据数太奇大数据平台监测数据显示",
            "h1": {
                "h1": "王老吉",
                "h1_p3": {
                    "h1_p3_s1": {
                        "h1_p3_s1": "王老吉",
                        "h1_p3_s1_tabletitle": "王老吉",
                        "h1_p3_s1_tablebody": [],
                        "h1_p3_s1_content": "暂无数据"
                    },
                    "h1_p3": "王老吉"
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
    "msPath": "https://narnia.oss-cn-beijing.aliyuncs.com/Narnia%E8%87%AA%E5%8A%A8%E6%8A%A5%E5%91%8A_20171222193647.docx?Expires=1515769995&OSSAccessKeyId=LTAIARWAKGUIqkn6&Signature=dcTTkKPd53iYhZFxDF9xQJXNQtE%3D",
    "message": "任务执行成功"
}

失败：1、检查输入body体 jsonData 是否包含。2、检查 value 是否含有 null 值。

{
    "msPath": "",
    "message": "任务执行错误"
}
```



