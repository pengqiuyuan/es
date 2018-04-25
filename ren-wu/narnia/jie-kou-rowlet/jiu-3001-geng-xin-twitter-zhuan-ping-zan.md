**九**、更新 Twitter 转评赞

`GET` `http://127.0.0.1/stq/api/v1/rowlet/upsertTwitterEsById`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
id 推文Id 必填
retweet 转发 必填
reply 回复 必填
favorite 喜欢 必填
```

`response` 返回提示信息

```
成功：

{
  "message" : "任务成功",
  "status"  : "200"
}

失败：

{
  "message" : "任务失败",
  "status"  : "400"
}
```

Demo：

```
http://127.0.0.1/stq/api/v1/rowlet/upsertTwitterEsById?id=980111653458120704&retweet=2&reply=2&favorite=2
```






