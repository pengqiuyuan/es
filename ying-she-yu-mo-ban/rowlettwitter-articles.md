[^1]索引：`rowlet_twitter_articles`

类型：`rowlet_twitter_articles`

**文章**

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 推文创建时间 | created\_at | Date |
| 推文id | id\_str | String |
| 推文内容 | text | String |
| 推文发布来源\(哪一种客户端\) | source | String |
| 标志推文是否在显示的时候截断 | truncated | String |
| 标志推文是否是回复性推文 | in\_reply\_to\_status\_id | Int64 |
| 若推文为回复性推文，该字段为原始推文id | in\_reply\_to\_status\_id\_str | String |
| 回复性推文  原始推文用户名 | in\_reply\_to\_screen\_name | String |
| 回复性推文  原始推文用户id | in\_reply\_to\_user\_id | Int64 |
| 回复性推文  原始推文用户id | in\_reply\_to\_user\_id\_str | String |
| 推文账户信息 | user | Object |
| 推文发送坐标 | coordinates | Object |
| 推文发送地点 | place | Object |
| 引用性推文 原始推文id | quoted\_status\_id | Int64 |
| 引用性推文 原始推文id | quoted\_status\_id\_str | String |
| 是否为引用性推文 | is\_quote\_status | Boolean |
| 指示此推文是否已由身份验证用户转推 | retweeted\_status | Boolean |
| 回复数 | reply\_count | Number |
| 转发数 | retweet\_count | Number |
| 点赞数 | favorite\_count | Number |
| 推文解析后的对象 | entities | Object |
|  | extended\_entities | Object |
|  | favorited | Boolean |
| 标志推文是否被转发 | retweeted | Boolean |
|  | possibly\_sensitive | Boolean |
|  | filter\_level | String |
| 语言 | lang | String |
|  | matching\_rules | Array |

**用户**

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 用户Twitter id | id | int64 |
| Twitter id 字符串 | id\_str | String |
| 名字 | name | String |
| 用户名 | screen\_name | String |
| 位置 | location | String |
| 用户url | url | String |
| 用户描述信息 | description | String |
| 派生的一些用户属性 | derived | Array |
| 该用户是否选择保护隐私 | protected | Boolean |
| 是否认证 | verified | Boolean |
| 粉丝量 | followers\_count | Number |
| 朋友数量 | friends\_count | Number |
| 此用户所属公共链表的数量 | listed\_count | Number |
| 这个账户喜欢的推文数量 | favourites\_count | Number |
| 用户发布推文的总量 | statuses\_count | Number |
| 用户列表数量 | list\_num | Number |
| 创建时间 | created\_at | Date |
| 时区偏移 | utc\_offset | Int |
| 时区 | time\_zone | String |
| 表示用户是否启用地理标记 | geo\_enabled | Boolean |
| 语言 | lang | String |
| 是否启用贡献者模式 | contributors\_enabled | Boolean |
| 用户背景色 | profile\_background\_color | String |
| 用户背景图片http协议url | profile\_background\_image\_url | String |
| 用户背景图片https协议url | profile\_background\_image\_url\_https | String |
| 背景图片是否平铺 | profile\_background\_tile | Boolean |
| 配置文件横幅 | profile\_banner\_url | String |
| 用户头像图片http url | profile\_image\_url | String |
| 用户头像图片的https url | profile\_image\_url\_https | String |
| 用户头像url显示的颜色 | profile\_link\_color | String |
| 用户头像边框颜色 | profile\_sidebar\_border\_color | String |
| 侧边栏背景色 | profile\_sidebar\_fill\_color | String |
| 账户文本颜色 | profile\_text\_color | String |
| 是否用户自己上传的背景图片 | profile\_use\_background\_image | Boolean |
| 是否默认主题 | default\_profile | Boolean |
| 是否默认图片 | default\_profile\_image | Boolean |
| 用户国家代码表示 | withheld\_in\_countries | String |
| 指示被隐藏的部分是状态还是用户 | withheld\_scope | String |

创建索引`rowlet_twitter_articles`

```
curl -XPUT http://127.0.0.1:9222/rowlet_twitter_articles
```

`mapping`

```

```

[^1]: Enter footnote here.
