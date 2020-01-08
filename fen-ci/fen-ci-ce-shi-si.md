# 分词测试四

```text
curl  -u 用户:密码 -XPUT http://127.0.0.1:9222/ikindex2


curl -u 用户:密码 -XPOST http://127.0.0.1:9222/ikindex2/fulltext2/_mapping -d'
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

curl -u 用户:密码 -XPOST http://127.0.0.1:9222/ikindex2/fulltext2/1 -d'
{
"content": "习近平主席将迎接金砖国家及受邀国领导人并集体合影"
}'

curl -u 用户:密码 -XPOST http://127.0.0.1:9222/ikindex2/fulltext2/2 -d'
{
"content": "全景报道金砖国家工商论坛等重要活动"
}'

curl -u 用户:密码 -XPOST http://127.0.0.1:9222/ikindex2/fulltext2/_search?pretty  -d'
 {
     "query" : { "match_phrase" : { "content" : "金砖国家工商" }},
     "highlight" : {
         "pre_tags" : ["<tag1", "<tag2"],
         "post_tags" : ["</tag1", "</tag2"],
         "fields" : {
             "content" : {}
         }
     }
}'


curl -u 用户:密码  'http://127.0.0.1:9222/ikindex2/_analyze?analyzer=ik_max_word&pretty=true' -d '
{
    "text":"全景报道金砖国家工商论坛等重要活动"
}'


curl -u 用户:密码  'http://127.0.0.1:9222/ikindex2/_analyze?analyzer=ik_max_word&pretty=true' -d '
{
    "text":"习近平主席将迎接金砖国家及受邀国领导人并集体合影"
}'
```

