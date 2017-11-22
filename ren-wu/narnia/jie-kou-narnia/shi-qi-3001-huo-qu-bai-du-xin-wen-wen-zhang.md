十七、获取百度新闻文章

`POST` `http://127.0.0.1/stq/api/v1/words/getBaiduXinwenArticle`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
fromId唯一标识字段，必填
keyword为监测项关键字（不为null或者空字符串），必填
startDate为监测项起始时间（含），必填
endDate为监测项结束时间（含），必填
```

`BODY` 体：

```
{
    "fromId":"soonfy-1113-21",
    "keyword":"猎场+胡歌||猎场+万茜",
    "startDate":"2017-01-01",
    "endDate":"2017-09-09"
}
```

`response` 返回文章数据和提示信息：

```
成功：
{
    "statusCode": 200,
    "keyword_id": "5a0be316cacb184e8e0aa9e3",
    "keyword": "猎场+胡歌||猎场+万茜",
    "total": 1,
    "news": [
        {
            "id": "5a0be316cacb184e8e0aa9e3httpmzmopcoma170707130115142html",
            "author": "猫扑",
            "title": "电视剧《猎场》能否挽回多事之秋的乐视?",
            "summary": "《猎场》是东阳青雨传媒股份有限公司、浙江影视集团、蓝色星空影业出品,由姜伟执导,胡歌、孙红雷、张嘉译、祖峰等大牌主演的国内首部以猎头在商界中纵横捭阖、在情感上",
            "date": "2017-07-07T05:00:00.000Z",
            "url": "http://mz.mop.com/a/170707130115142.html",
            "crawl_at": "2017-11-15T06:53:04.824Z"
        }
    ],
    "msg": "[百度新闻] 查询关键词原文content成功",
    "error": "",
    "stamp": 1510813121324
}

失败：
{
    "statusCode":400,
    "keyword_id":"",
    "keyword":"猎场+胡歌||猎场+万茜",
    "total":0,
    "news":[],
    "msg":"[百度新闻] 查询关键词原文content失败",
    "error":"content 请求没有匹配到关键词",
    "stamp":1510813215063
}
```