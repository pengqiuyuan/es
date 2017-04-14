`index` 名称：`toutiao_articles_and_users`  
`type`  名称：`toutiao_articles_and_users`

头条文章、用户合并后的索引，删除重复字段：头条号ID（`id`）、抓取时间（`crawled_at`）

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 头条号ID | toutiaor\_id | 字符串 |
| 资源ID | item\_id | 字符串 |
| 文章标题 | title | 字符串 |
| 文章内容 | content | 字符串 |
| 文章图片 | images | 数组（链接） |
| 关键分词 | labels | 数组 |
| 阅读量 | read\_count | 数值 |
| 评论量 | comment\_count | 数值 |
| 点赞量 | up\_count | 数值 |
| 踩量 | down\_count | 数值 |
| 发布时间 | published\_at | 日期（时间戳） |
| 抓取时间 | crawled\_at | 日期（时间戳） |
| 类型 | type | 数值 |
| 视频时长 | duration | 数值（秒） |

---

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 头像图片链接 | avatar\_img | 字符串 |
| 头条号名称 | name | 字符串 |
| 头条号简介 | introduction | 字符串 |
| 关注量 | follower\_count | 数值 |
| 粉丝量 | fans\_count | 数值 |



