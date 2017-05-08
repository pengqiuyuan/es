旧索引：`sogou_weixin_articles`

新索引：`sogou_weixin_articles`

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 账号ID | biz | 字符串 |
| 消息ID | mid | 字符串 |
| 消息偏移 | idx | 字符串 |
| 文章标题 | title | 字符串 |
| 文章摘要 | description | 字符串 |
| 文章内容 | content | 字符串 |
| 指定链接 | source\_url | 字符串 |
| 插图链接 | cover | 字符串 |
| 作者 | author | 字符串 |
| 账号名 | username | 字符串 |
| 中文名 | nickname | 字符串 |
| 发布日期 | publish\_date | 字符串 |
| 发布时间 | publish\_time | 日期 |
| 阅读量 | read | 数值 |
| 点赞量 | like | 数值 |
| 采集链接 | crawl\_url | 字符串 |
| 文章链接 | content\_url | 字符串 |
| 采集时间 | create\_time | 日期 |

创建索引`sogou_weixin_articles`

```
curl -XPUT http://127.0.0.1:9222/sogou_weixin_articles
```

`mapping`



