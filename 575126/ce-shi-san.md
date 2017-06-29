测试文档更新，`logstash` 添加 `output` 添加  `doc_as_upsert =>true` `action >"update"`，如：

```
output {
    if [@metadata][index_name] == "tieba_posts" {
        elasticsearch {
                hosts => ["127.0.0.1:9200"]
                index => "%{[@metadata][index_name]}"
                document_type => "%{[@metadata][type_name]}"
                document_id => "%{[@metadata][id]}"
                template_overwrite => false
                user => '用户名'
                password => '密码'
                doc_as_upsert => true
                action => "update"
            }
        }
}
```

希望结果：

* 文档不存在时，索引新文档

* 文档存在时（`_id` 判断），更新部分文档（爬虫上传的 `Body` 体内容）

测试结果：

