ES 慢查询添加日志

为了排查 `node15 OOM` 的原因，是否为聚合查询导致。

```
curl -u 用户名:密码 -XPUT http://127.0.0.1:9200/weibo/_settings -d'
{
    "index.search.slowlog.threshold.query.warn": "13s",
    "index.search.slowlog.threshold.query.info": "5s",
    "index.search.slowlog.threshold.fetch.warn": "2s",
    "index.search.slowlog.threshold.fetch.info": "800ms"
}'

curl -u 用户名:密码 -XPUT http://127.0.0.1:9222/weixin/_settings -d'
{
    "index.search.slowlog.threshold.query.warn": "13s",
    "index.search.slowlog.threshold.query.info": "5s",
    "index.search.slowlog.threshold.fetch.warn": "2s",
    "index.search.slowlog.threshold.fetch.info": "800ms"
}'
```



