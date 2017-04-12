`match_phrase` 测试，`es5.3.0` 、`elasticsearch-analysis-ik-5.3.0`

前提：`elasticsearch-analysis-ik-5.3.0` 修改过 `CharacterUtil`

测试 ：验证`match_phrase` 查询，能否命中带有特殊符号的短语、词组

创建索引

`curl -XPUT http://127.0.0.1:9222/ikindex3`

设置分词`mapping`

```
curl -XPOST http://127.0.0.1:9222/ikindex3/fulltext2/_mapping -d'
 {
     "fulltext2": {
         "properties": {
             "content": {
                 "type": "text",
                 "analyzer": "ik_max_word",
                 "search_analyzer": "ik_max_word"
             }
         }
     }
 }'
```

插入数据

```
curl -XPOST http://127.0.0.1:9222/ikindex3/fulltext2/1 -d'
{
    "content": "啦啦啦啦啦啦《叶问3》功夫升级 中西拳术巅峰对决甄子丹张晋打到飞起"
}'

curl -XPOST http://127.0.0.1:9222/ikindex3/fulltext2/2 -d'
{
    "content": "叶问遇到了“棘手”的对手，《叶问3》功夫升级 中西拳术@巅峰对决甄子丹张晋打到飞起"
}'

curl -XPOST http://127.0.0.1:9222/ikindex3/fulltext2/3 -d'
{
    "content": "中西拳术巅峰对决甄子丹张晋打到飞起"
}'

curl -XPOST http://127.0.0.1:9222/ikindex3/fulltext2/4 -d'
{
    "content": "#中西拳术@巅峰。"
}'

curl -XPOST http://127.0.0.1:9222/ikindex3/fulltext2/5 -d'
{
    "content": "#中西甄子丹张晋打到飞起"
}'
curl -XPOST http://127.0.0.1:9222/ikindex3/fulltext2/6 -d'
{
    "content": "$中西拳术。巅峰，对决@甄子丹#张晋打到飞起"
}'
```

测试分词结果中是否有特殊符号（`$`、`。`、`，`、`@`、`#`），结果含有：`$`、`。`、`，`、`@`、`#`

```
curl 'http://127.0.0.1:9222/ikindex3/_analyze?analyzer=ik_smart&pretty=true' -d '
{
"text":"$中西拳术。巅峰，对决@甄子丹#张晋打到飞起"
}'
```

如下：

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
      "token" : "。",
      "start_offset" : 5,
      "end_offset" : 6,
      "type" : "CN_CHAR",
      "position" : 3
    },
    {
      "token" : "巅峰",
      "start_offset" : 6,
      "end_offset" : 8,
      "type" : "CN_WORD",
      "position" : 4
    },
    {
      "token" : ",",
      "start_offset" : 8,
      "end_offset" : 9,
      "type" : "CN_CHAR",
      "position" : 5
    },
    {
      "token" : "对决",
      "start_offset" : 9,
      "end_offset" : 11,
      "type" : "CN_WORD",
      "position" : 6
    },
    {
      "token" : "@",
      "start_offset" : 11,
      "end_offset" : 12,
      "type" : "CN_CHAR",
      "position" : 7
    },
    {
      "token" : "甄子丹",
      "start_offset" : 12,
      "end_offset" : 15,
      "type" : "CN_WORD",
      "position" : 8
    },
    {
      "token" : "#",
      "start_offset" : 15,
      "end_offset" : 16,
      "type" : "CN_CHAR",
      "position" : 9
    },
    {
      "token" : "张",
      "start_offset" : 16,
      "end_offset" : 17,
      "type" : "CN_CHAR",
      "position" : 10
    },
    {
      "token" : "晋",
      "start_offset" : 17,
      "end_offset" : 18,
      "type" : "CN_WORD",
      "position" : 11
    },
    {
      "token" : "打到",
      "start_offset" : 18,
      "end_offset" : 20,
      "type" : "CN_WORD",
      "position" : 12
    },
    {
      "token" : "飞起",
      "start_offset" : 20,
      "end_offset" : 22,
      "type" : "CN_WORD",
      "position" : 13
    }
  ]
}
```

一、测试`match_phrase`，查询 `@巅峰`，6条文档，5条含有`巅峰`，2条还有 `@巅峰`，期望结果命中2条带有 `@巅峰`，的文档

```
curl -XPOST http://127.0.0.1:9222/ikindex3/fulltext2/_search?pretty  -d'
 {
     "query" : { "match_phrase" : { "content" : "巅峰" }},
     "highlight" : {
         "pre_tags" : ["<tag1", "<tag2"],
         "post_tags" : ["</tag1", "</tag2"],
         "fields" : {
             "content" : {}
         }
     }
}'
```

结果如下，与预期一致

```
{
  "took" : 119,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "failed" : 0
  },
  "hits" : {
    "total" : 2,
    "max_score" : 0.6810639,
    "hits" : [
      {
        "_index" : "ikindex3",
        "_type" : "fulltext2",
        "_id" : "4",
        "_score" : 0.6810639,
        "_source" : {
          "content" : "#中西拳术@巅峰。"
        },
        "highlight" : {
          "content" : [
            "#中西拳术<tag1@</tag1<tag1巅峰</tag1。"
          ]
        }
      },
      {
        "_index" : "ikindex3",
        "_type" : "fulltext2",
        "_id" : "2",
        "_score" : 0.39150736,
        "_source" : {
          "content" : "叶问遇到了“棘手”的对手，《叶问3》功夫升级 中西拳术@巅峰对决甄子丹张晋打到飞起"
        },
        "highlight" : {
          "content" : [
            "叶问遇到了“棘手”的对手，《叶问3》功夫升级 中西拳术<tag1@</tag1<tag1巅峰</tag1对决甄子丹张晋打到飞起"
          ]
        }
      }
    ]
  }
}
```

二、测试`match_phrase`，查询 `$中西`，预期一条符合，结果如下（与预期相符）：

```
curl -XPOST http://127.0.0.1:9222/ikindex3/fulltext2/_search?pretty  -d'
 {
     "query" : { "match_phrase" : { "content" : "$中西" }},
     "highlight" : {
         "pre_tags" : ["<tag1", "<tag2"],
         "post_tags" : ["</tag1", "</tag2"],
         "fields" : {
             "content" : {}
         }
     }
}'

{
  "took" : 9,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "failed" : 0
  },
  "hits" : {
    "total" : 1,
    "max_score" : 0.98793286,
    "hits" : [
      {
        "_index" : "ikindex3",
        "_type" : "fulltext2",
        "_id" : "6",
        "_score" : 0.98793286,
        "_source" : {
          "content" : "$中西拳术。巅峰，对决@甄子丹#张晋打到飞起"
        },
        "highlight" : {
          "content" : [
            "<tag1$</tag1<tag1中西</tag1拳术。巅峰，对决@甄子丹#张晋打到飞起"
          ]
        }
      }
    ]
  }
}
```

三、测试`match_phrase`，查询`巅峰，`，预期一条符合，结果如下（与预期相符）：

```
curl -XPOST http://127.0.0.1:9222/ikindex3/fulltext2/_search?pretty  -d'
 {
     "query" : { "match_phrase" : { "content" : "巅峰，" }},
     "highlight" : {
         "pre_tags" : ["<tag1", "<tag2"],
         "post_tags" : ["</tag1", "</tag2"],
         "fields" : {
             "content" : {}
         }
     }
}'

{
  "took" : 7,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "failed" : 0
  },
  "hits" : {
    "total" : 1,
    "max_score" : 0.77182573,
    "hits" : [
      {
        "_index" : "ikindex3",
        "_type" : "fulltext2",
        "_id" : "6",
        "_score" : 0.77182573,
        "_source" : {
          "content" : "$中西拳术。巅峰，对决@甄子丹#张晋打到飞起"
        },
        "highlight" : {
          "content" : [
            "$中西拳术。<tag1巅峰</tag1<tag1，</tag1对决@甄子丹#张晋打到飞起"
          ]
        }
      }
    ]
  }
}

测试英文逗号，同样命中，超出预期

curl -XPOST http://127.0.0.1:9222/ikindex3/fulltext2/_search?pretty  -d'
 {
     "query" : { "match_phrase" : { "content" : "巅峰," }},
     "highlight" : {
         "pre_tags" : ["<tag1", "<tag2"],
         "post_tags" : ["</tag1", "</tag2"],
         "fields" : {
             "content" : {}
         }
     }
}'

{
  "took" : 7,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "failed" : 0
  },
  "hits" : {
    "total" : 1,
    "max_score" : 0.77182573,
    "hits" : [
      {
        "_index" : "ikindex3",
        "_type" : "fulltext2",
        "_id" : "6",
        "_score" : 0.77182573,
        "_source" : {
          "content" : "$中西拳术。巅峰，对决@甄子丹#张晋打到飞起"
        },
        "highlight" : {
          "content" : [
            "$中西拳术。<tag1巅峰</tag1<tag1，</tag1对决@甄子丹#张晋打到飞起"
          ]
        }
      }
    ]
  }
}
```

四、测试`match_phrase`，查询`巅峰。`，预期一条符合，结果如下（与预期相符）：

```
curl -XPOST http://127.0.0.1:9222/ikindex3/fulltext2/_search?pretty  -d'
 {
     "query" : { "match_phrase" : { "content" : "巅峰。" }},
     "highlight" : {
         "pre_tags" : ["<tag1", "<tag2"],
         "post_tags" : ["</tag1", "</tag2"],
         "fields" : {
             "content" : {}
         }
     }
}'

命中

{
  "took" : 6,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "failed" : 0
  },
  "hits" : {
    "total" : 1,
    "max_score" : 1.1100999,
    "hits" : [
      {
        "_index" : "ikindex3",
        "_type" : "fulltext2",
        "_id" : "4",
        "_score" : 1.1100999,
        "_source" : {
          "content" : "#中西拳术@巅峰。"
        },
        "highlight" : {
          "content" : [
            "#中西拳术@<tag1巅峰</tag1<tag1。</tag1"
          ]
        }
      }
    ]
  }
}

测试英文句号,没有结果命中

curl -XPOST http://127.0.0.1:9222/ikindex3/fulltext2/_search?pretty  -d'
 {
     "query" : { "match_phrase" : { "content" : "巅峰." }},
     "highlight" : {
         "pre_tags" : ["<tag1", "<tag2"],
         "post_tags" : ["</tag1", "</tag2"],
         "fields" : {
             "content" : {}
         }
     }
}'

{
  "took" : 7,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "failed" : 0
  },
  "hits" : {
    "total" : 0,
    "max_score" : null,
    "hits" : [ ]
  }
}
```

结论

`match_phrase`，1、可以命中带有特殊符号的短语、词组。2、特殊符号有大小写的区分

