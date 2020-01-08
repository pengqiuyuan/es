# 七、通过 keyword 获取任务的计算结果集（以获取微博数据接口为例）

七、**通过**`keyword`**获取任务的计算结果集（以获取微博数据接口为例）**

`POST` `http://127.0.0.1/stq/api/v1/words/findWeiboByKeywords`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```text
keyword为监测项名称，
startDate为监测项起始时间（含），
endDate为监测项结束时间（含），
```

`BODY` 体：

```text
{
      "keyWord": "百事可乐",
      "startDate": "2017-11-01",
      "endDate": "2017-11-03"
}
```

`response` Es查询有保存计算指标

```text
[
      {
            "name": "百事可乐",
            "keywords": "百事可乐",
            "source": "weibo",
            "startDateString": "2017-11-01",
            "endDateString": "2017-11-02",
            "updateDateString": "2017-12-21",
            "weibo_volume": 24102, #文章量
            "weibo_actualVolume": 435, #实际文章量
            "weibo_exposure": 151737346, #曝光量
            "weibo_interactive": 78980, #互动量
            "weibo_forwardDepth": 9, #转发深度
            "weibo_account": 431, #账号量（每日去重）
            "weibo_commentCount": 36916, #评论量
            "weibo_upCount": 42064, #点赞量
            "weibo_repostCount": 51540, #转发量
            "weibo_oldinteractive": 1088790, #互动量（旧）
            "weibo_primaryCount": 25, #原发提及量
            "weibo_firstLevelCount": 73, #一级转发量
            "weibo_secondLevelCount": 31, #二级转发量
            "weibo_thirdLevelCount": 306 #三级及以上转发量
      },
      {
            "name": "百事可乐",
            "keywords": "百事可乐",
            "source": "weibo",
            "startDateString": "2017-11-02",
            "endDateString": "2017-11-03",
            "updateDateString": "2017-12-21",
            "weibo_volume": 4929,
            "weibo_actualVolume": 90,
            "weibo_exposure": 5922386,
            "weibo_interactive": 4768,
            "weibo_forwardDepth": 9,
            "weibo_account": 84,
            "weibo_commentCount": 2073,
            "weibo_upCount": 2695,
            "weibo_repostCount": 2054,
            "weibo_oldinteractive": 118890,
            "weibo_primaryCount": 17,
            "weibo_firstLevelCount": 25,
            "weibo_secondLevelCount": 10,
            "weibo_thirdLevelCount": 38
      },
      {
            "name": "百事可乐",
            "keywords": "百事可乐",
            "source": "weibo",
            "startDateString": "2017-11-03",
            "endDateString": "2017-11-04",
            "updateDateString": "2017-12-21",
            "weibo_volume": 4478,
            "weibo_actualVolume": 101,
            "weibo_exposure": 147323129,
            "weibo_interactive": 63567,
            "weibo_forwardDepth": 8,
            "weibo_account": 93,
            "weibo_commentCount": 27467,
            "weibo_upCount": 36099,
            "weibo_repostCount": 30324,
            "weibo_oldinteractive": 375101,
            "weibo_primaryCount": 17,
            "weibo_firstLevelCount": 41,
            "weibo_secondLevelCount": 20,
            "weibo_thirdLevelCount": 23
      }
]
```

`response` Es查询没有保存计算指标

```text
[]
```

`response` 请求失败 500

