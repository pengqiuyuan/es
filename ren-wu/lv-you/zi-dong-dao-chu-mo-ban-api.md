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
    "category": "travel",
    "jsonData": {
        "content": {
            "report_date": "2017年12月",
            "abstract": "根据中国旅游线路价格指数监测系统数据显示，国内游线路平均价格指数329元/人天，与上个月相比环比下降7.36%，出境游线路平均价格指数1523元/人天，与上个月相比环比5.70%；全国31个省（市、自治区）旅游线路价格水平指数最高的省（市、自治区）是甘肃，最低的是河北；全国旅游线路价格波动幅度最大的省（市、自治区）是福建，与上个月相比环比增长144.0%。",
            "h1_p1": "2017年12月，国内游线路平均价格指数329元/人天，出境游线路平均价格指数1523元/人天。",
            "h1_sub1_bar": {
                "data": [
                    {
                        "area": "国内游",
                        "price": 329
                    },
                    {
                        "area": "出境游",
                        "price": 1523
                    }
                ],
                "type": "bar"
            },
            "h1_p2": "国内游-区域旅游线路平均价格指数最高的东北地区为441元/人天；国内游-区域旅游线路平均价格指数最低的西南地区为252元/人天。",
            "h1_sub2_bar": {
                "data": [
                    {
                        "area": "东北地区",
                        "price": 441
                    },
                    {
                        "area": "西北地区",
                        "price": 408
                    },
                    {
                        "area": "华南地区",
                        "price": 373
                    },
                    {
                        "area": "华中地区",
                        "price": 330
                    },
                    {
                        "area": "华北地区",
                        "price": 319
                    },
                    {
                        "area": "华东地区",
                        "price": 257
                    },
                    {
                        "area": "西南地区",
                        "price": 252
                    }
                ],
                "type": "bar"
            },
            "h1_p3": "出境游-区域旅游线路平均价格指数最高的南极为5550元/人天；出境游-区域旅游线路平均价格指数最低的东南亚为470元/人天。",
            "h1_sub3_bar": {
                "data": [
                    {
                        "area": "南极",
                        "price": 5550
                    },
                    {
                        "area": "北极",
                        "price": 2708
                    },
                    {
                        "area": "澳洲",
                        "price": 2136
                    },
                    {
                        "area": "南美",
                        "price": 2133
                    },
                    {
                        "area": "中东",
                        "price": 1833
                    },
                    {
                        "area": "南亚",
                        "price": 1733
                    },
                    {
                        "area": "非洲",
                        "price": 1396
                    },
                    {
                        "area": "欧洲",
                        "price": 1189
                    },
                    {
                        "area": "东亚",
                        "price": 982
                    },
                    {
                        "area": "港澳台",
                        "price": 860
                    },
                    {
                        "area": "北美洲",
                        "price": 860
                    },
                    {
                        "area": "俄罗斯",
                        "price": 660
                    },
                    {
                        "area": "东南亚",
                        "price": 470
                    }
                ],
                "type": "bar"
            },
            "h1_p4": "各省（市、自治区）旅游线路平均价格指数最高的3个省（市、自治区）为甘肃、宁夏和山西，其中，旅游线路平均价格指数最高的甘肃为548元；各省（市、自治区）旅游线路平均价格指数最低的3个省（市、自治区）为内蒙古、贵州和河北，其中，旅游线路平均价格指数最低的河北为120元/人天。",
            "h1_sub4_table": {
                "data": [
                    {
                        "province": "甘肃",
                        "price": 548
                    },
                    {
                        "province": "宁夏",
                        "price": 536
                    },
                    {
                        "province": "山西",
                        "price": 531
                    },
                    {
                        "province": "吉林",
                        "price": 506
                    },
                    {
                        "province": "辽宁",
                        "price": 480
                    },
                    {
                        "province": "湖南",
                        "price": 454
                    },
                    {
                        "province": "天津",
                        "price": 421
                    },
                    {
                        "province": "重庆",
                        "price": 418
                    },
                    {
                        "province": "海南",
                        "price": 397
                    },
                    {
                        "province": "广西",
                        "price": 364
                    },
                    {
                        "province": "广东",
                        "price": 356
                    },
                    {
                        "province": "新疆",
                        "price": 353
                    },
                    {
                        "province": "北京",
                        "price": 344
                    },
                    {
                        "province": "青海",
                        "price": 343
                    },
                    {
                        "province": "湖北",
                        "price": 342
                    },
                    {
                        "province": "黑龙江",
                        "price": 336
                    },
                    {
                        "province": "福建",
                        "price": 327
                    },
                    {
                        "province": "江西",
                        "price": 326
                    },
                    {
                        "province": "西藏",
                        "price": 324
                    },
                    {
                        "province": "山东",
                        "price": 312
                    },
                    {
                        "province": "安徽",
                        "price": 295
                    },
                    {
                        "province": "陕西",
                        "price": 256
                    },
                    {
                        "province": "江苏",
                        "price": 203
                    },
                    {
                        "province": "上海",
                        "price": 203
                    },
                    {
                        "province": "云南",
                        "price": 200
                    },
                    {
                        "province": "浙江",
                        "price": 198
                    },
                    {
                        "province": "河南",
                        "price": 196
                    },
                    {
                        "province": "四川",
                        "price": 182
                    },
                    {
                        "province": "内蒙古",
                        "price": 178
                    },
                    {
                        "province": "贵州",
                        "price": 133
                    },
                    {
                        "province": "河北",
                        "price": 120
                    }
                ],
                "type": "table"
            },
            "h2_p1": "2017年12月，国内游-区域旅游线路价格高出国内游旅游线路平均价格的区域为东北地区、西北地区、华南地区、华中地区，其中东北地区旅游线路价格最高，高出国内游旅游线路平均价格113元/人天；低于国内游旅游线路平均价格的区域为华北地区、华东地区、西南地区，其中西南地区旅游线路价格最低，低于国内游旅游线路平均价格77元/人天；.",
            "h2_sub1_bar": {
                "type": "bar",
                "data": [
                    {
                        "area": "东北地区",
                        "price": 113
                    },
                    {
                        "area": "西北地区",
                        "price": 79
                    },
                    {
                        "area": "华南地区",
                        "price": 44
                    },
                    {
                        "area": "华中地区",
                        "price": 2
                    },
                    {
                        "area": "华北地区",
                        "price": -9
                    },
                    {
                        "area": "华东地区",
                        "price": -72
                    },
                    {
                        "area": "西南地区",
                        "price": -77
                    }
                ]
            },
            "h2_p2": "2017年12月，出境游-区域旅游线路价格高出出境游旅游线路平均价格的区域为南极、北极、澳洲、南美、中东、南亚，其中南极旅游线路价格最高，高出出境游旅游线路平均价格4028元/人天；低于出境游旅游线路平均价格的区域为非洲、欧洲、东亚、港澳台、北美洲、俄罗斯、东南亚，其中东南亚旅游线路价格最低，低于出境游旅游线路平均价格1052元/人天。",
            "h2_sub2_bar": {
                "type": "bar",
                "data": [
                    {
                        "area": "南极",
                        "price": 4028
                    },
                    {
                        "area": "北极",
                        "price": 1186
                    },
                    {
                        "area": "澳洲",
                        "price": 614
                    },
                    {
                        "area": "南美",
                        "price": 611
                    },
                    {
                        "area": "中东",
                        "price": 311
                    },
                    {
                        "area": "南亚",
                        "price": 211
                    },
                    {
                        "area": "非洲",
                        "price": -126
                    },
                    {
                        "area": "欧洲",
                        "price": -333
                    },
                    {
                        "area": "东亚",
                        "price": -540
                    },
                    {
                        "area": "港澳台",
                        "price": -662
                    },
                    {
                        "area": "北美洲",
                        "price": -663
                    },
                    {
                        "area": "俄罗斯",
                        "price": -862
                    },
                    {
                        "area": "东南亚",
                        "price": -1052
                    }
                ]
            },
            "h2_p3": "2017年12月，全国31个省（市、自治区）旅游线路价格高出全国国内游旅游线路平均价格的省（市、自治区）为甘肃、宁夏、山西、吉林、辽宁、湖南、天津、重庆、海南、广西、广东、新疆、北京、青海、湖北、黑龙江16个，占比52%，其中甘肃旅游线路价格最高，高出国内游旅游线路平均价格220元/人天；低于全国国内游旅游线路平均价格最多的15个省（市、自治区）为福建、江西、西藏、山东、安徽、陕西、江苏、上海、云南、浙江、河南、四川、内蒙古、贵州、河北，其中河北旅游线路价格最低，低于国内游旅游线路平均价格208元/人天。",
            "h2_sub3_table": {
                "type": "bar",
                "data": [
                    {
                        "province": "甘肃",
                        "price": 220
                    },
                    {
                        "province": "宁夏",
                        "price": 208
                    },
                    {
                        "province": "山西",
                        "price": 203
                    },
                    {
                        "province": "吉林",
                        "price": 178
                    },
                    {
                        "province": "辽宁",
                        "price": 152
                    },
                    {
                        "province": "湖南",
                        "price": 126
                    },
                    {
                        "province": "天津",
                        "price": 93
                    },
                    {
                        "province": "重庆",
                        "price": 90
                    },
                    {
                        "province": "海南",
                        "price": 69
                    },
                    {
                        "province": "广西",
                        "price": 36
                    },
                    {
                        "province": "广东",
                        "price": 28
                    },
                    {
                        "province": "新疆",
                        "price": 25
                    },
                    {
                        "province": "北京",
                        "price": 16
                    },
                    {
                        "province": "青海",
                        "price": 15
                    },
                    {
                        "province": "湖北",
                        "price": 14
                    },
                    {
                        "province": "黑龙江",
                        "price": 8
                    },
                    {
                        "province": "福建",
                        "price": -1
                    },
                    {
                        "province": "江西",
                        "price": -2
                    },
                    {
                        "province": "西藏",
                        "price": -4
                    },
                    {
                        "province": "山东",
                        "price": -16
                    },
                    {
                        "province": "安徽",
                        "price": -33
                    },
                    {
                        "province": "陕西",
                        "price": -72
                    },
                    {
                        "province": "江苏",
                        "price": -125
                    },
                    {
                        "province": "上海",
                        "price": -125
                    },
                    {
                        "province": "云南",
                        "price": -128
                    },
                    {
                        "province": "浙江",
                        "price": -130
                    },
                    {
                        "province": "河南",
                        "price": -132
                    },
                    {
                        "province": "四川",
                        "price": -146
                    },
                    {
                        "province": "内蒙古",
                        "price": -150
                    },
                    {
                        "province": "贵州",
                        "price": -195
                    },
                    {
                        "province": "河北",
                        "price": -208
                    }
                ]
            },
            "h3_p1": "2017年12月，国内游和出境游旅游线路价格与上个月相比，波动幅度最小的是出境游旅游线路，国内游旅游线路环比下降7.36%；出境游旅游线路环比增长5.70%。",
            "h3_sub1_bar": {
                "data": [
                    {
                        "type": "国内游",
                        "value": "-0.07361"
                    },
                    {
                        "type": "境外游",
                        "value": "0.05704"
                    }
                ],
                "type": "bar"
            },
            "h3_p2": "2017年12月，国内游-区域旅游线路价格与上个月相比，波动幅度最大的地区为西北地区，环比下降36.49%；波动幅度最小的地区为华东地区，环比下降7.18%。",
            "h3_sub2_bar": {
                "data": [
                    {
                        "area": "西北地区",
                        "pole": -1,
                        "rate": 0.3649407361197755
                    },
                    {
                        "area": "华南地区",
                        "pole": 1,
                        "rate": 0.36053593179049925
                    },
                    {
                        "area": "东北地区",
                        "pole": -1,
                        "rate": 0.1747815230961298
                    },
                    {
                        "area": "华北地区",
                        "pole": 1,
                        "rate": 0.14758819294456443
                    },
                    {
                        "area": "华中地区",
                        "pole": 1,
                        "rate": 0.11789652247667515
                    },
                    {
                        "area": "西南地区",
                        "pole": 1,
                        "rate": 0.10554089709762533
                    },
                    {
                        "area": "华东地区",
                        "pole": -1,
                        "rate": 0.07181653590826809
                    }
                ],
                "type": "bar"
            },
            "h3_p3": "2017年12月，出境游-区域旅游线路价格与上个月相比，波动幅度最大的地区为中东，环比增长54.55%；波动幅度最小的地区为南亚，环比持平0.00%。",
            "h3_sub3_bar": {
                "data": [
                    {
                        "area": "中东",
                        "pole": 1,
                        "rate": 0.545531197301855
                    },
                    {
                        "area": "俄罗斯",
                        "pole": -1,
                        "rate": 0.43054357204486626
                    },
                    {
                        "area": "东亚",
                        "pole": 1,
                        "rate": 0.33062330623306235
                    },
                    {
                        "area": "北极",
                        "pole": 1,
                        "rate": 0.2040907069808804
                    },
                    {
                        "area": "澳洲",
                        "pole": 1,
                        "rate": 0.16403269754768393
                    },
                    {
                        "area": "北美洲",
                        "pole": 1,
                        "rate": 0.15913688469318948
                    },
                    {
                        "area": "港澳台",
                        "pole": 1,
                        "rate": 0.15591397849462366
                    },
                    {
                        "area": "东南亚",
                        "pole": 1,
                        "rate": 0.15055079559363524
                    },
                    {
                        "area": "欧洲",
                        "pole": -1,
                        "rate": 0.10128495842781557
                    },
                    {
                        "area": "非洲",
                        "pole": 1,
                        "rate": 0.044128646222887064
                    },
                    {
                        "area": "南极",
                        "pole": -1,
                        "rate": 0.024090029892737824
                    },
                    {
                        "area": "南美",
                        "pole": 0,
                        "rate": 0
                    },
                    {
                        "area": "南亚",
                        "pole": 0,
                        "rate": 0
                    }
                ],
                "type": "bar"
            },
            "h3_p4": "2017年12月，全国各省（市、自治区）旅游线路价格与上个月相比，波动幅度最大的省（市、自治区）为福建，环比增长144.03%；波动幅度最小的省（市、自治区）为内蒙古，环比持平0.00%。",
            "h3_sub4_table": {
                "data": [
                    {
                        "province": "福建",
                        "pole": 1,
                        "rate": 1.4402985074626866
                    },
                    {
                        "province": "西藏",
                        "pole": 1,
                        "rate": 1.25
                    },
                    {
                        "province": "河南",
                        "pole": 1,
                        "rate": 0.9797979797979798
                    },
                    {
                        "province": "广西",
                        "pole": 1,
                        "rate": 0.7333333333333333
                    },
                    {
                        "province": "新疆",
                        "pole": -1,
                        "rate": 0.7072968490878938
                    },
                    {
                        "province": "海南",
                        "pole": 1,
                        "rate": 0.5568627450980392
                    },
                    {
                        "province": "云南",
                        "pole": 1,
                        "rate": 0.47058823529411764
                    },
                    {
                        "province": "浙江",
                        "pole": -1,
                        "rate": 0.47058823529411764
                    },
                    {
                        "province": "湖南",
                        "pole": 1,
                        "rate": 0.4504792332268371
                    },
                    {
                        "province": "黑龙江",
                        "pole": -1,
                        "rate": 0.32934131736526945
                    },
                    {
                        "province": "山西",
                        "pole": 1,
                        "rate": 0.3046683046683047
                    },
                    {
                        "province": "陕西",
                        "pole": -1,
                        "rate": 0.26857142857142857
                    },
                    {
                        "province": "天津",
                        "pole": 1,
                        "rate": 0.2680722891566265
                    },
                    {
                        "province": "甘肃",
                        "pole": -1,
                        "rate": 0.2314165497896213
                    },
                    {
                        "province": "江苏",
                        "pole": -1,
                        "rate": 0.20078740157480315
                    },
                    {
                        "province": "上海",
                        "pole": -1,
                        "rate": 0.20078740157480315
                    },
                    {
                        "province": "山东",
                        "pole": -1,
                        "rate": 0.1937984496124031
                    },
                    {
                        "province": "辽宁",
                        "pole": -1,
                        "rate": 0.18781725888324874
                    },
                    {
                        "province": "重庆",
                        "pole": -1,
                        "rate": 0.18359375
                    },
                    {
                        "province": "安徽",
                        "pole": 1,
                        "rate": 0.16141732283464566
                    },
                    {
                        "province": "湖北",
                        "pole": -1,
                        "rate": 0.1513647642679901
                    },
                    {
                        "province": "青海",
                        "pole": -1,
                        "rate": 0.14463840399002495
                    },
                    {
                        "province": "江西",
                        "pole": -1,
                        "rate": 0.1043956043956044
                    },
                    {
                        "province": "四川",
                        "pole": -1,
                        "rate": 0.10344827586206896
                    },
                    {
                        "province": "贵州",
                        "pole": -1,
                        "rate": 0.06338028169014084
                    },
                    {
                        "province": "河北",
                        "pole": 1,
                        "rate": 0.05263157894736842
                    },
                    {
                        "province": "北京",
                        "pole": -1,
                        "rate": 0.03910614525139665
                    },
                    {
                        "province": "吉林",
                        "pole": -1,
                        "rate": 0.00784313725490196
                    },
                    {
                        "province": "宁夏",
                        "pole": 0,
                        "rate": 0
                    },
                    {
                        "province": "广东",
                        "pole": 0,
                        "rate": 0
                    },
                    {
                        "province": "内蒙古",
                        "pole": 0,
                        "rate": 0
                    }
                ],
                "type": "table"
            }
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



