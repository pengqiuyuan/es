一、问题

在使用 `match_phrase` 查询 `金砖国家` 时，预期命中 60 条，实际命中30条。

```
第一条，没有命中的文档包含语句段，如下
"text":  "金砖国家世界文化遗产"

第二条
"text":  "彭丽媛为金砖国家和对话会受邀国"

其他二十八条
"text":  "金砖国家工商论坛"

其他三十条，属于命中文档。

```

分词："金砖国家世界文化遗产"

```

{
  "tokens": [
    {
      "token": "金砖",
      "start_offset": 0,
      "end_offset": 2,
      "type": "CN_WORD",
      "position": 0
    },
    {
      "token": "国家",
      "start_offset": 2,
      "end_offset": 4,
      "type": "CN_WORD",
      "position": 1
    },
    {
      "token": "家世",
      "start_offset": 3,
      "end_offset": 5,
      "type": "CN_WORD",
      "position": 2
    },
    {
      "token": "家",
      "start_offset": 3,
      "end_offset": 4,
      "type": "CN_WORD",
      "position": 3
    },
    {
      "token": "世界文化",
      "start_offset": 4,
      "end_offset": 8,
      "type": "CN_WORD",
      "position": 4
    },
    {
      "token": "世界",
      "start_offset": 4,
      "end_offset": 6,
      "type": "CN_WORD",
      "position": 5
    },
    {
      "token": "文化遗产",
      "start_offset": 6,
      "end_offset": 10,
      "type": "CN_WORD",
      "position": 6
    },
    {
      "token": "文化",
      "start_offset": 6,
      "end_offset": 8,
      "type": "CN_WORD",
      "position": 7
    },
    {
      "token": "遗产",
      "start_offset": 8,
      "end_offset": 10,
      "type": "CN_WORD",
      "position": 8
    },
    {
      "token": "遗",
      "start_offset": 8,
      "end_offset": 9,
      "type": "CN_WORD",
      "position": 9
    },
    {
      "token": "产",
      "start_offset": 9,
      "end_offset": 10,
      "type": "CN_CHAR",
      "position": 10
    }
  ]
}
```

分词："彭丽媛为金砖国家和对话会受邀国"

```
{
  "tokens": [
    {
      "token": "彭丽媛",
      "start_offset": 0,
      "end_offset": 3,
      "type": "CN_WORD",
      "position": 0
    },
    {
      "token": "彭",
      "start_offset": 0,
      "end_offset": 1,
      "type": "CN_WORD",
      "position": 1
    },
    {
      "token": "丽",
      "start_offset": 1,
      "end_offset": 2,
      "type": "CN_WORD",
      "position": 2
    },
    {
      "token": "媛",
      "start_offset": 2,
      "end_offset": 3,
      "type": "CN_WORD",
      "position": 3
    },
    {
      "token": "为",
      "start_offset": 3,
      "end_offset": 4,
      "type": "CN_CHAR",
      "position": 4
    },
    {
      "token": "金砖",
      "start_offset": 4,
      "end_offset": 6,
      "type": "CN_WORD",
      "position": 5
    },
    {
      "token": "国家",
      "start_offset": 6,
      "end_offset": 8,
      "type": "CN_WORD",
      "position": 6
    },
    {
      "token": "家和",
      "start_offset": 7,
      "end_offset": 9,
      "type": "CN_WORD",
      "position": 7
    },
    {
      "token": "家",
      "start_offset": 7,
      "end_offset": 8,
      "type": "CN_WORD",
      "position": 8
    },
    {
      "token": "和",
      "start_offset": 8,
      "end_offset": 9,
      "type": "CN_CHAR",
      "position": 9
    },
    {
      "token": "对话会",
      "start_offset": 9,
      "end_offset": 12,
      "type": "CN_WORD",
      "position": 10
    },
    {
      "token": "对话",
      "start_offset": 9,
      "end_offset": 11,
      "type": "CN_WORD",
      "position": 11
    },
    {
      "token": "会受",
      "start_offset": 11,
      "end_offset": 13,
      "type": "CN_WORD",
      "position": 12
    },
    {
      "token": "受邀",
      "start_offset": 12,
      "end_offset": 14,
      "type": "CN_WORD",
      "position": 13
    },
    {
      "token": "邀",
      "start_offset": 13,
      "end_offset": 14,
      "type": "CN_WORD",
      "position": 14
    },
    {
      "token": "国",
      "start_offset": 14,
      "end_offset": 15,
      "type": "CN_CHAR",
      "position": 15
    }
  ]
}
```

分词："金砖国家工商论坛"

```
{
  "tokens": [
    {
      "token": "金砖",
      "start_offset": 0,
      "end_offset": 2,
      "type": "CN_WORD",
      "position": 0
    },
    {
      "token": "国家工商",
      "start_offset": 2,
      "end_offset": 6,
      "type": "CN_WORD",
      "position": 1
    },
    {
      "token": "国家",
      "start_offset": 2,
      "end_offset": 4,
      "type": "CN_WORD",
      "position": 2
    },
    {
      "token": "家",
      "start_offset": 3,
      "end_offset": 4,
      "type": "CN_WORD",
      "position": 3
    },
    {
      "token": "工商",
      "start_offset": 4,
      "end_offset": 6,
      "type": "CN_WORD",
      "position": 4
    },
    {
      "token": "论坛",
      "start_offset": 6,
      "end_offset": 8,
      "type": "CN_WORD",
      "position": 5
    },
    {
      "token": "坛",
      "start_offset": 7,
      "end_offset": 8,
      "type": "CN_WORD",
      "position": 6
    }
  ]
}
```

二、解决办法

```
1、修改索引 Mapping field 

"search_analyzer": "ik_max_word"
改为
"search_analyzer": "ik_smart"

或者

2、查询语句添加 analyzer 和 slop 的设置

"match_phrase" : {
  "content_full" : {
    "query": "金砖国家",
    "analyzer": "ik_smart",
    "slop":1
  }
}
```

三、原因

`match_phrase` 适合分出来的词没有位置重叠的场景。我们在使用 `ik_max_word` 的时候，词以及词的位置都有交叠。

`match_phrase`

【1】要求查询语句与匹配的文档之间，分出来的词的相对位置要一致。

【2】`match_phrase` 适合分出来的词没有位置重叠的场景。

索引 `mapping` 设置， `"search_analyzer": "ik_max_word" `为默认查询使用分词

```
"content_full": {
    "search_analyzer": "ik_max_word",
    "analyzer": "ik_max_word",
    "type": "text"
}
```

四、使用 `_all` 能匹配出所有文档的原因

`_all` 字段并没有设置 ik 分词，使用默认分词 standard analyzer ，所以不会有像 `ik_max_word` 词与词位置重叠的情况。

不同的分词会产生不同的分词结果，`ik_max_word`产生的词位置有重叠；`ik_smart`不会有位置重叠；

```
 "_all": {
  "enabled": true
 }
```



