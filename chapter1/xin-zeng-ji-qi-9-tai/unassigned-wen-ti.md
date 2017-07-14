UNASSIGNED 问题

```
GET _cat/shards/weixin*?h=index,shard,prirep,state,unassigned.reason

weixin_articles_and_weixiners 0 p STARTED
weixin_articles_and_weixiners 1 r UNASSIGNED ALLOCATION_FAILED
```

解决

```
curl -XPOST 'http://127.0.0.1:9222/_cluster/reroute?pretty&retry_failed=true' -d '{
    "commands" : [
        {
          "allocate_replica" : {
                "index" : "weixin_articles_and_weixiners", "shard" : 19,
                "node" : "内网IP地址"
          }
        }
    ]
 }'
 
 
cancle:取消node_1在my_index索引的第0个分片
allocate:将my_index索引上未分配的第0个分片分配给node_2
move:将my_index索引在node_2的第1块分片移动到node_1上
 
{"cancel" : {"index" : "my_index","shard" : 0,"node" : "node_1"}},  
{"allocate_replica" : {"index" : "my_index","shard" : 0,"node" : "node_2"}},  
{"move" : {"index" : "my_index","shard" : 1,"from_node" : "node_2","to_node" : "node_1"}} 
```

---

[elasticsearch 5x 手动控制分片分布](http://blog.csdn.net/coderLuo/article/details/72824801)

[elasticsearch 运维管理优化处理记录](https://jevic.github.io/2017/01/23/elk-yunwei/)

[分配改变](http://cwiki.apachecn.org/pages/viewpage.action?pageId=4260787)

[mongodb 和 Elasticsearch集群部署](http://ishield.cn/article/36)







