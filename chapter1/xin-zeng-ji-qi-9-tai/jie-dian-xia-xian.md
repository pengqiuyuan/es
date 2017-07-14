`15` 台 `ES` 服务器节点下线

```
curl -XPUT http://127.0.0.1:9222/_cluster/settings -d '{
  "transient" : {
    "cluster.routing.allocation.exclude._name" : "node16-node,node17-node,node18-node,node19-node,node20-node,node21-node,node22-node,node23-node,node24-node,node25-node,node26-node,node27-node,node28-node,node29-node,node30-node"
  }
}'

curl -XGET http://127.0.0.1:9222/_cluster/settings?pretty
```



