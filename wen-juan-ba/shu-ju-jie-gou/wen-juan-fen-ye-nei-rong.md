---
description: 问卷分页内容表
---

# 问卷分页内容

`问卷表 wj_surveys_pages`

| 字段含义 | 字段名称 | 数据类型 | 解释 |
| :--- | :--- | :--- | :--- |
| 名称 | name | String | 1 |
| 当前页面题目ID | questions | String | 566e,566a |

`问卷吧 surveys`

```text
{
    "pages" : [
        {
            "name" : "new page", 
            "questions" : [
                "566e6d02eb0e5ba29a00000a", 
                "566e6d25eb0e5b17de000009", 
                "566e6d60eb0e5ba29a00000b", 
                "566e6d9beb0e5b17de00000c"
            ]
        }, 
        {
            "name" : "new page", 
            "questions" : [
                "566e6dc2eb0e5b17de00000d", 
                "566e6df3eb0e5b17de00000f", 
                "566e6e4beb0e5b17de000010"
            ]
        }
}
```

