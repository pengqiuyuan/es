# 映射与模板

映射与模板

删除模板

`curl -XDELETE http://127.0.0.1:9222/_template/`

调整副本

```text
curl -XPUT localhost:9222/weixin_articles_and_weixiners/_settings -d '{
    "index" : {
        "number_of_replicas" : "0"
    }
}'
```

调整`refresh`时间

```text
curl -XPUT localhost:9222/weixin_articles_and_weixiners/_settings -d '{
    "index" : {
        "refresh_interval" : "300s"
    }
}'
```

增加`flush`间隔

```text
curl -XPUT localhost:9222/weixin_articles_and_weixiners/_settings -d '{
    "index" : {
        "translog.flush_threshold_size" : "1g"
    }
}'
```

