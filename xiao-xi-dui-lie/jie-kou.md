微博（索引名称、分片名称）：`weibo_articles_and_weiboers`、`weibo_articles_and_weiboer`

微信（索引名称、分片名称）：`weixin_articles_and_weixiners`、`weixin_articles_and_weixiner`

头条（索引名称、分片名称）：`toutiao_articles_and_users`、`toutiao_articles_and_users`

百度新闻（索引名称、分片名称）：`baidunews_news`、`baidunews_news`

知乎问答（索引名称、分片名称）：`zhihu_questions`、`zhihu_questions`

科技资讯（索引名称、分片名称）：`tech_news`、[分片参考](/ying-she-yu-mo-ban/ke-ji-zi-xun-zhan-shu-ju.md)

**POST 请求写入数据到 **`kafka`

`POST` `http://127.0.0.1/stq/api/v1/pa/xxx/add`

`HEADERS`：`"Content-Type" => "application/json"`

`BODY` 体参数说明：List 集合、数组

```
[
    {
      "id": "10",
      "index_name": "xxx",
      "type_name": "xxx",
      ...
    },
    {
      "id": "11",
      "index_name": "xxx",
      "type_name": "xxx",
      ...
    }
]
```

`logstash`** 消费**`kafka`**中的数据到 **`elasticsearch`

```
...
```

从 `kafka` 队列中读取的数据，两条符合预期（`index_name`、`type_name`、`id`会在`logstash filter`中处理后移除，保存或者更新数据到 `es`）

```
{
    "avatar_img" => "xxx",
          "name" => "xxx"
}
{
    "avatar_img" => "xxx",
          "name" => "xxx"
}
```



