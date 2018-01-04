索引：`rowlet_facebook_articles`

类型：`rowlet_facebook_articles`

**文章**

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 发布时间 | create\_at | Date |
|  | last\_untime | String |
| 用户信息 | user | Object |
| 内容 | text | String |
| 评论数 | comment\_num | Number |
| 点赞量 | likes\_num | Number |
| 分享数 | share\_count | Number |

**用户**

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 用户名 | name | String |
| 用户id | id | String |
| 当前位置 | current\_location | String |
| 生日 | birthday | String |
| 主页类别 | category | String |
| 粉丝量 | fan\_count | Nubmer |
| 邮箱 | emails | String |
| 家乡 | hometown | String |
| Facebook 主页链接 | link | String |
| 地址 | location | Object |
| 个人网站 | website | String |
| 喜欢量 | likes\_count | Number |
| 个人简介 | about | String |
| 个人描述 | description | String |
| 是否认证 | verification\_status | Boolean |

创建索引`rowlet_facebook_articles`

```
curl -XPUT http://127.0.0.1:9222/rowlet_facebook_articles
```

`mapping`

```

```



