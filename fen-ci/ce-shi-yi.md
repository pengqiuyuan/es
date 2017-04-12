`match` 测试

创建索引

`curl -XPUT http://127.0.0.1:9222/ikindex2`

设置 `mapping`

```
curl -XPOST http://127.0.0.1:9222/ikindex2/fulltext2/_mapping -d'
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

```
curl -XPOST http://127.0.0.1:9222/ikindex2/fulltext2/1 -d'
{
    "content": "1111111《叶问3》功夫升级 中西拳术巅峰对决甄子丹张晋打到飞起"
}'

curl -XPOST http://127.0.0.1:9222/ikindex2/fulltext2/2 -d'
{
    "content": "333333333333《叶问3》功夫升级 中西拳术@巅峰对决甄子丹张晋打到飞起"
}'

curl -XPOST http://127.0.0.1:9222/ikindex2/fulltext2/3 -d'
{
    "content": "中西拳术巅峰对决甄子丹张晋打到飞起"
}'

curl -XPOST http://127.0.0.1:9222/ikindex2/fulltext2/4 -d'
{
    "content": "#中西拳术@巅峰。"
}'

curl -XPOST http://127.0.0.1:9222/ikindex2/fulltext2/5 -d'
{
    "content": "#中西甄子丹张晋打到飞起"
}'
```

查询

```
curl -XPOST http://127.0.0.1:9222/ikindex2/fulltext2/_search?pretty  -d'
 {
     "query" : { "match" : { "content" : "@巅峰" }},
     "highlight" : {
         "pre_tags" : ["<tag1", "<tag2"],
         "post_tags" : ["</tag1", "</tag2"],
         "fields" : {
             "content" : {}
         }
     }
}'
```

结果，命中4个文档

```
{
  "took" : 26,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "failed" : 0
  },
  "hits" : {
    "total" : 4,
    "max_score" : 0.8854469,
    "hits" : [
      {
        "_index" : "ikindex2",
        "_type" : "fulltext2",
        "_id" : "4",
        "_score" : 0.8854469,
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
        "_index" : "ikindex2",
        "_type" : "fulltext2",
        "_id" : "3",
        "_score" : 0.8630463,
        "_source" : {
          "content" : "中西拳术巅峰对决甄子丹张晋打到飞起"
        },
        "highlight" : {
          "content" : [
            "中西拳术<tag1巅峰</tag1对决甄子丹张晋打到飞起"
          ]
        }
      },
      {
        "_index" : "ikindex2",
        "_type" : "fulltext2",
        "_id" : "1",
        "_score" : 0.8169973,
        "_source" : {
          "content" : "1111111《叶问3》功夫升级 中西拳术巅峰对决甄子丹张晋打到飞起"
        },
        "highlight" : {
          "content" : [
            "1111111《叶问3》功夫升级 中西拳术<tag1巅峰</tag1对决甄子丹张晋打到飞起"
          ]
        }
      },
      {
        "_index" : "ikindex2",
        "_type" : "fulltext2",
        "_id" : "2",
        "_score" : 0.58938235,
        "_source" : {
          "content" : "333333333333《叶问3》功夫升级 中西拳术@巅峰对决甄子丹张晋打到飞起"
        },
        "highlight" : {
          "content" : [
            "333333333333《叶问3》功夫升级 中西拳术<tag1@</tag1<tag1巅峰</tag1对决甄子丹张晋打到飞起"
          ]
        }
      }
    ]
  }
}
```

测试分词  `中西拳术@巅峰对决甄子丹#张晋打到飞起`，符号`#、@、。`都在

```
curl 'http://127.0.0.1:9222/ikindex2/_analyze?analyzer=ik_max_word&pretty=true' -d '
{
"text":"#中西拳术@巅峰。"
}'
```

```
{
  "tokens" : [
    {
      "token" : "#",
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
      "token" : "@",
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
      "token" : "。",
      "start_offset" : 8,
      "end_offset" : 9,
      "type" : "CN_CHAR",
      "position" : 9
    }
  ]
}
```



