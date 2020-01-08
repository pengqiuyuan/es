# 问题五

Logstash 更新数据到 Elasticsearch，版本冲突

```text
version conflict, current version [2340] is different than the one provided [2339]
```

```text
15:56:50.027 [[main]>worker5] WARN  logstash.outputs.elasticsearch - Failed action. {:status=>409, :action=>["update", {:_id=>"a99c020aab6641a489f3b368a042c418", :_index=>"news_comments", :_type=>"news_comments", :_routing=>nil, :_retry_on_conflict=>1}, %{host} %{message}], :response=>{"update"=>{"_index"=>"news_comments", "_type"=>"news_comments", "_id"=>"a99c020aab6641a489f3b368a042c418", "status"=>409, "error"=>{"type"=>"version_conflict_engine_exception", "reason"=>"[news_comments][a99c020aab6641a489f3b368a042c418]: version conflict, current version [2340] is different than the one provided [2339]", "index_uuid"=>"fUG7RIRsSOeeNrld77Qypg", "shard"=>"8", "index"=>"news_comments"}}}}
```

[Elasticsearch 并发更新问题](https://my.oschina.net/zhuguowei/blog/486250)

[Elasticsearch 并发冲突问题](http://www.jianshu.com/p/7a3652bae8a4)

[Logstash version\_type](https://www.elastic.co/guide/en/logstash/current/plugins-outputs-elasticsearch.html#plugins-outputs-elasticsearch-version_type)

```text
doc_as_upsert => true
action => "update"
```

