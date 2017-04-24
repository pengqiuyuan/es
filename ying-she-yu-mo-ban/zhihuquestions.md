旧索引：`zhihu_questions`

新索引：`zhihu_questions`

| 字段含义 | 字段名称 | 数据类型 |
| :---: | :---: | :---: |
| 头条号ID | id | 字符串 |
| 头像图片链接 | avatar\_img | 字符串 |
| 头条号名称 | name | 字符串 |
| 头条号简介 | introduction | 字符串 |
| 关注量 | follower\_count | 数值 |
| 粉丝量 | fans\_count | 数值 |
| 抓取时间 | crawled\_at | 日期 |

部分数据：

```
{
    "_id": "19551476",
    "_version": 1,
    "_score": 1,
    "_source": {
        "title": "你如何评估街旁开放平台？",
        "topics": "19551979",
        "desc": "一个很早期做开放的案例，或许值得关注一下子。 显示全部",
        "followsNum": 64,
        "viewsNum": 0,
        "answersNum": 15,
        "questionId": "19551476"
    }
}
```

创建索引`zhihu_questions`

```
curl -XPUT http://127.0.0.1:9222/zhihu_questions
```

`mapping`

```

```



