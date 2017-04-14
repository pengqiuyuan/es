

```
curl 'http://127.0.0.1:9222/ikindex3/_analyze?analyzer=ik_max_word&pretty=true' -d '
{
"text":"$中西拳术。巅峰，对决@甄子丹#张晋打到飞起：茶客 #千机伞#[代发]耗时一个月自制-的『金属版』千机伞模型~支持全（形态）十三种变化，不锈钢结构，"
}'
```

结果

```
{
  "tokens" : [
    {
      "token" : "$",
      "start_offset" : 0,
      "end_offset" : 1,
      "type" : "CN_CHAR",
      "position" : 0
    },
    {
      "token" : "中西",
      "start_offset" : 1,
      "end_offset" : 3,
      "type" : "CN_WORD",
      "position" : 1
    },
    {
      "token" : "拳术",
      "start_offset" : 3,
      "end_offset" : 5,
      "type" : "CN_WORD",
      "position" : 2
    },
    {
      "token" : "拳",
      "start_offset" : 3,
      "end_offset" : 4,
      "type" : "CN_WORD",
      "position" : 3
    },
    {
      "token" : "术",
      "start_offset" : 4,
      "end_offset" : 5,
      "type" : "CN_CHAR",
      "position" : 4
    },
    {
      "token" : "。",
      "start_offset" : 5,
      "end_offset" : 6,
      "type" : "CN_CHAR",
      "position" : 5
    },
    {
      "token" : "巅峰",
      "start_offset" : 6,
      "end_offset" : 8,
      "type" : "CN_WORD",
      "position" : 6
    },
    {
      "token" : "巅",
      "start_offset" : 6,
      "end_offset" : 7,
      "type" : "CN_WORD",
      "position" : 7
    },
    {
      "token" : "峰",
      "start_offset" : 7,
      "end_offset" : 8,
      "type" : "CN_WORD",
      "position" : 8
    },
    {
      "token" : ",",
      "start_offset" : 8,
      "end_offset" : 9,
      "type" : "CN_CHAR",
      "position" : 9
    },
    {
      "token" : "对决",
      "start_offset" : 9,
      "end_offset" : 11,
      "type" : "CN_WORD",
      "position" : 10
    },
    {
      "token" : "@",
      "start_offset" : 11,
      "end_offset" : 12,
      "type" : "CN_CHAR",
      "position" : 11
    },
    {
      "token" : "甄子丹",
      "start_offset" : 12,
      "end_offset" : 15,
      "type" : "CN_WORD",
      "position" : 12
    },
    {
      "token" : "甄",
      "start_offset" : 12,
      "end_offset" : 13,
      "type" : "CN_WORD",
      "position" : 13
    },
    {
      "token" : "子",
      "start_offset" : 13,
      "end_offset" : 14,
      "type" : "CN_CHAR",
      "position" : 14
    },
    {
      "token" : "丹",
      "start_offset" : 14,
      "end_offset" : 15,
      "type" : "CN_WORD",
      "position" : 15
    },
    {
      "token" : "#",
      "start_offset" : 15,
      "end_offset" : 16,
      "type" : "CN_CHAR",
      "position" : 16
    },
    {
      "token" : "张",
      "start_offset" : 16,
      "end_offset" : 17,
      "type" : "CN_CHAR",
      "position" : 17
    },
    {
      "token" : "晋",
      "start_offset" : 17,
      "end_offset" : 18,
      "type" : "CN_WORD",
      "position" : 18
    },
    {
      "token" : "打到",
      "start_offset" : 18,
      "end_offset" : 20,
      "type" : "CN_WORD",
      "position" : 19
    },
    {
      "token" : "飞起",
      "start_offset" : 20,
      "end_offset" : 22,
      "type" : "CN_WORD",
      "position" : 20
    },
    {
      "token" : ":",
      "start_offset" : 22,
      "end_offset" : 23,
      "type" : "CN_CHAR",
      "position" : 21
    },
    {
      "token" : "茶客",
      "start_offset" : 23,
      "end_offset" : 25,
      "type" : "CN_WORD",
      "position" : 22
    },
    {
      "token" : "茶",
      "start_offset" : 23,
      "end_offset" : 24,
      "type" : "CN_WORD",
      "position" : 23
    },
    {
      "token" : "客",
      "start_offset" : 24,
      "end_offset" : 25,
      "type" : "CN_CHAR",
      "position" : 24
    },
    {
      "token" : " ",
      "start_offset" : 25,
      "end_offset" : 26,
      "type" : "CN_CHAR",
      "position" : 25
    },
    {
      "token" : "#",
      "start_offset" : 26,
      "end_offset" : 27,
      "type" : "CN_CHAR",
      "position" : 26
    },
    {
      "token" : "千",
      "start_offset" : 27,
      "end_offset" : 28,
      "type" : "TYPE_CNUM",
      "position" : 27
    },
    {
      "token" : "机",
      "start_offset" : 28,
      "end_offset" : 29,
      "type" : "CN_CHAR",
      "position" : 28
    },
    {
      "token" : "伞",
      "start_offset" : 29,
      "end_offset" : 30,
      "type" : "CN_CHAR",
      "position" : 29
    },
    {
      "token" : "#",
      "start_offset" : 30,
      "end_offset" : 31,
      "type" : "CN_CHAR",
      "position" : 30
    },
    {
      "token" : "[",
      "start_offset" : 31,
      "end_offset" : 32,
      "type" : "CN_CHAR",
      "position" : 31
    },
    {
      "token" : "代发",
      "start_offset" : 32,
      "end_offset" : 34,
      "type" : "CN_WORD",
      "position" : 32
    },
    {
      "token" : "发",
      "start_offset" : 33,
      "end_offset" : 34,
      "type" : "CN_WORD",
      "position" : 33
    },
    {
      "token" : "]",
      "start_offset" : 34,
      "end_offset" : 35,
      "type" : "CN_CHAR",
      "position" : 34
    },
    {
      "token" : "耗时",
      "start_offset" : 35,
      "end_offset" : 37,
      "type" : "CN_WORD",
      "position" : 35
    },
    {
      "token" : "耗",
      "start_offset" : 35,
      "end_offset" : 36,
      "type" : "CN_WORD",
      "position" : 36
    },
    {
      "token" : "时",
      "start_offset" : 36,
      "end_offset" : 37,
      "type" : "CN_CHAR",
      "position" : 37
    },
    {
      "token" : "一个月",
      "start_offset" : 37,
      "end_offset" : 40,
      "type" : "CN_WORD",
      "position" : 38
    },
    {
      "token" : "一个",
      "start_offset" : 37,
      "end_offset" : 39,
      "type" : "CN_WORD",
      "position" : 39
    },
    {
      "token" : "一",
      "start_offset" : 37,
      "end_offset" : 38,
      "type" : "TYPE_CNUM",
      "position" : 40
    },
    {
      "token" : "个月",
      "start_offset" : 38,
      "end_offset" : 40,
      "type" : "CN_WORD",
      "position" : 41
    },
    {
      "token" : "个",
      "start_offset" : 38,
      "end_offset" : 39,
      "type" : "COUNT",
      "position" : 42
    },
    {
      "token" : "月",
      "start_offset" : 39,
      "end_offset" : 40,
      "type" : "CN_CHAR",
      "position" : 43
    },
    {
      "token" : "自制",
      "start_offset" : 40,
      "end_offset" : 42,
      "type" : "CN_WORD",
      "position" : 44
    },
    {
      "token" : "制",
      "start_offset" : 41,
      "end_offset" : 42,
      "type" : "CN_WORD",
      "position" : 45
    },
    {
      "token" : "-",
      "start_offset" : 42,
      "end_offset" : 43,
      "type" : "CN_CHAR",
      "position" : 46
    },
    {
      "token" : "『",
      "start_offset" : 44,
      "end_offset" : 45,
      "type" : "CN_CHAR",
      "position" : 47
    },
    {
      "token" : "金属",
      "start_offset" : 45,
      "end_offset" : 47,
      "type" : "CN_WORD",
      "position" : 48
    },
    {
      "token" : "版",
      "start_offset" : 47,
      "end_offset" : 48,
      "type" : "CN_CHAR",
      "position" : 49
    },
    {
      "token" : "』",
      "start_offset" : 48,
      "end_offset" : 49,
      "type" : "CN_CHAR",
      "position" : 50
    },
    {
      "token" : "千",
      "start_offset" : 49,
      "end_offset" : 50,
      "type" : "TYPE_CNUM",
      "position" : 51
    },
    {
      "token" : "机",
      "start_offset" : 50,
      "end_offset" : 51,
      "type" : "CN_CHAR",
      "position" : 52
    },
    {
      "token" : "伞",
      "start_offset" : 51,
      "end_offset" : 52,
      "type" : "CN_CHAR",
      "position" : 53
    },
    {
      "token" : "模型",
      "start_offset" : 52,
      "end_offset" : 54,
      "type" : "CN_WORD",
      "position" : 54
    },
    {
      "token" : "模",
      "start_offset" : 52,
      "end_offset" : 53,
      "type" : "CN_WORD",
      "position" : 55
    },
    {
      "token" : "型",
      "start_offset" : 53,
      "end_offset" : 54,
      "type" : "CN_CHAR",
      "position" : 56
    },
    {
      "token" : "~",
      "start_offset" : 54,
      "end_offset" : 55,
      "type" : "CN_CHAR",
      "position" : 57
    },
    {
      "token" : "支持",
      "start_offset" : 55,
      "end_offset" : 57,
      "type" : "CN_WORD",
      "position" : 58
    },
    {
      "token" : "全",
      "start_offset" : 57,
      "end_offset" : 58,
      "type" : "CN_CHAR",
      "position" : 59
    },
    {
      "token" : "(",
      "start_offset" : 58,
      "end_offset" : 59,
      "type" : "CN_CHAR",
      "position" : 60
    },
    {
      "token" : "形态",
      "start_offset" : 59,
      "end_offset" : 61,
      "type" : "CN_WORD",
      "position" : 61
    },
    {
      "token" : ")",
      "start_offset" : 61,
      "end_offset" : 62,
      "type" : "CN_CHAR",
      "position" : 62
    },
    {
      "token" : "十三",
      "start_offset" : 62,
      "end_offset" : 64,
      "type" : "CN_WORD",
      "position" : 63
    },
    {
      "token" : "三种",
      "start_offset" : 63,
      "end_offset" : 65,
      "type" : "CN_WORD",
      "position" : 64
    },
    {
      "token" : "变化",
      "start_offset" : 65,
      "end_offset" : 67,
      "type" : "CN_WORD",
      "position" : 65
    },
    {
      "token" : ",",
      "start_offset" : 67,
      "end_offset" : 68,
      "type" : "CN_CHAR",
      "position" : 66
    },
    {
      "token" : "不锈钢",
      "start_offset" : 68,
      "end_offset" : 71,
      "type" : "CN_WORD",
      "position" : 67
    },
    {
      "token" : "不锈",
      "start_offset" : 68,
      "end_offset" : 70,
      "type" : "CN_WORD",
      "position" : 68
    },
    {
      "token" : "钢结构",
      "start_offset" : 70,
      "end_offset" : 73,
      "type" : "CN_WORD",
      "position" : 69
    },
    {
      "token" : "钢",
      "start_offset" : 70,
      "end_offset" : 71,
      "type" : "CN_WORD",
      "position" : 70
    },
    {
      "token" : "结构",
      "start_offset" : 71,
      "end_offset" : 73,
      "type" : "CN_WORD",
      "position" : 71
    },
    {
      "token" : ",",
      "start_offset" : 73,
      "end_offset" : 74,
      "type" : "CN_CHAR",
      "position" : 72
    }
  ]
}
```

插入数据



