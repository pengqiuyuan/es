索引（`_index`）：`tech_news`

类型（`_type`）：

36kr：`tech_36kr_articles`、`tech_36kr_news`

虎嗅：`tech_huxiu_news`

雷锋：`tech_leiphone_articles`

创业邦：`tech_cyzone_articles`

钛媒体：`tech_tmtpost_articles`

极客公园：`tech_geekpark_articles`

砍柴网：`tech_ikanchai_articles`

前瞻网：`tech_qianzhan_articles`

互联网分析沙龙：`tech_techxue_articles`

品玩：`tech_pingwest_articles`

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 问题ID（覆盖 es 中元数据 \_id ，移除） | questionId | 字符串 |
| 问题标题 | title | 字符串 |
| 问题关键字分类 | topics | 数组 |
| 问题描述 | desc | 字符串 |
| 关注者数 | followsNum | 数值 |
| 被浏览数 | viewsNum | 数值 |
| 回答数 | answersNum | 数值 |
| 问题评论量 | commentsNum | 数值 |
| 问题时间 | createdAt | 日期 |



