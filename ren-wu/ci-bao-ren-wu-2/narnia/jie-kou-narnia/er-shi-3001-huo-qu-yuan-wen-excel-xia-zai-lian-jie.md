# 二十、获取原文 Excel 下载链接

十九、获取原文 Excel 下载链接

`POST` `http://127.0.0.1/stq/api/v1/words/downArticleExcelByKeyword`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```text
keyword为监测项名称，必填
startDate为监测项起始时间（含），必填
endDate为监测项结束时间（含），必填
taskType为数据源，必填，weibo、weixin
sortField 为排序字段 ，必填
        weibo ：follower_count（粉丝数，默认）、fans_count（关注数）、comment_count（评论）、up_count（点赞）、repost_count（转发）
        weixin：stat_read_count（阅读数，默认）、stat_like_count（点赞数）
sort为排序 asc（升序）、desc（降序）
size获取多少个排序结果，不超过100，必填
```

`BODY` 体：

```text
{
  "keyword": "芈月传",
  "startDate": "2016-03-01",
  "endDate": "2017-05-02",
  "taskType":"weixin",
  "sortField":"stat_read_count",
  "sort":"desc",
  "size":"20"
}
```

`response` 返回数据：

```text
成功

{
    "msPath": "https://narnia.oss-cn-beijing.aliyuncs.com/20171221193940.xlsx?Expires=1515683768&OSSAccessKeyId=LTAIARWAKGUIqkn6&Signature=jEQW0G9hGdXTtBVFDqgnCk%2FWwyw%3D",
    "message": "任务执行成功"
}

失败

{
    "msPath": "",
    "message": "任务执行失败"
}
```

