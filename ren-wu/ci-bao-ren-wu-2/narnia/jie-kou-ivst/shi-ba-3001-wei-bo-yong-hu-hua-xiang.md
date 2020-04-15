# 十八、微博用户画像

十八、微博用户画像

`说明：`

```text
1、新增词包任务，会同时计算此词包关键词的用户画像数据，并保存。
2、从词包匹配的时间段内（2016-01-01 ~ 计算的当前时间），抽样选择 45000条（45个Es分片，每个取1000条） 文档进行用户画像分析。
```

`POST` `http://127.0.0.1/stq/api/v1/words/findEsWeiboUserAnalysis`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```text
keyword为监测项关键字（不为null或者空字符串），必填
```

`BODY` 体：

```text
{
    "keyword":"淘气爷孙"
}
```

`response` 返回数据：

```text
[
    {
        "_index": "cibao_user_analysis",
        "_type": "cibao_user_analysis",
        "_source": {
            "birthMap": {
                "19岁及以下": 37,
                "20-29岁": 542,
                "30-39岁": 301,
                "40-49岁": 59,
                "50岁及以上": 20
            },
            "cityMap": {
                "南宁": 14,
                "嘉兴": 10,
                "济南": 32,
                "昆明": 16,
                "徐州": 14,
                "临沂": 11,
                "厦门": 26,
                "宁波": 27,
                "东莞": 26,
                "石家庄": 14,
                "无锡": 15,
                "贵阳": 14,
                "肇庆": 12,
                "长春": 13,
                "哈尔滨": 13,
                "合肥": 17,
                "温州": 31,
                "珠海": 11,
                "青岛": 32,
                "大连": 14,
                "杭州": 110,
                "南昌": 17,
                "福州": 24,
                "成都": 65,
                "江门": 23,
                "沈阳": 24,
                "长沙": 36,
                "其他": 79,
                "镇江": 12,
                "唐山": 22,
                "中山": 15,
                "常州": 13,
                "武汉": 50,
                "深圳": 102,
                "惠州": 10,
                "广州": 197,
                "梅州": 11,
                "泉州": 16,
                "西安": 41,
                "郑州": 33,
                "烟台": 11,
                "台北市": 16,
                "南京": 46,
                "佛山": 45,
                "苏州": 16
            },
            "privinceMap": {
                "山东": 137,
                "福建": 93,
                "台湾": 35,
                "河南": 80,
                "河北": 66,
                "重庆": 43,
                "湖北": 81,
                "湖南": 61,
                "江西": 39,
                "海南": 13,
                "黑龙江": 21,
                "天津": 38,
                "陕西": 52,
                "贵州": 20,
                "新疆": 13,
                "澳门": 16,
                "江苏": 155,
                "安徽": 38,
                "西藏": 7,
                "上海": 226,
                "吉林": 26,
                "香港": 89,
                "山西": 19,
                "甘肃": 17,
                "宁夏": 7,
                "四川": 106,
                "其他": 135,
                "浙江": 215,
                "广西": 27,
                "云南": 30,
                "海外": 181,
                "内蒙古": 14,
                "辽宁": 61,
                "广东": 522,
                "青海": 4,
                "北京": 265
            },
            "updateDate": 1511193600000,
            "followerMap": {
                "999及以下": 89891,
                "100000以上": 2134,
                "1000-4999": 5289,
                "5000-49999": 4638,
                "50000-99999": 53
            },
            "keywords": "淘气爷孙",
            "endDate": 1511193600000,
            "verifyMap": {
                "0": 3148,
                "1": 122,
                "2": 248
            },
            "source": "weibo",
            "genderMap": {
                "0": 1646,
                "1": 1872
            },
            "relationMap": {
                "恋爱中": 2,
                "已婚": 5,
                "暗恋中": 1,
                "丧偶": 1,
                "离异": 1,
                "单身": 41,
                "求交往": 8
            },
            "eduMap": {
                "高中": 35,
                "大专": 262,
                "初中": 61,
                "小学": 22,
                "本科及以上": 420
            },
            "fansMap": {
                "999及以下": 98619,
                "100000以上": 0,
                "1000-4999": 3386,
                "5000-49999": 0,
                "50000-99999": 0
            },
            "updateDateString": "2017-11-21",
            "startDateString": "2016-01-01",
            "endDateString": "2017-11-21",
            "startDate": 1451577600000
        },
        "_id": "VTN1cUliVUZ6Nlpmdk1GWnphUUpqdWlld2VpYm8=",
        "_score": 1
    }
]

或者

[]
```
