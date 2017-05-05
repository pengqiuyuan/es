**POST 请求写入数据到 `kafka`**

`POST` `http://127.0.0.1/api/v1/pa`

`HEADERS`：`"Content-Type" => "application/json"`

`BODY` 体参数说明：

```
index_name：索引名称（字符串）
type_name：分片名称（字符串）
index_message：消息体（数组、集合），消息体内的每一个对象都有 id（字符串）、index_name、 type_name 参数。
```

```js

```

**`logstash` 消费`kafka`中的数据到 `elasticsearch`**

```
input {
        kafka {
            bootstrap_servers => "127.0.0.1:9092"
            topics => ["weibo"]
            auto_offset_reset => "earliest"
            codec => "json"
        }
        kafka {
            bootstrap_servers => "127.0.0.1:9092"
            topics => ["weixin"]
            auto_offset_reset => "earliest"
            codec => "json"
        }
        kafka {
            bootstrap_servers => "127.0.0.1:9092"
            topics => ["toutiao"]
            auto_offset_reset => "earliest"
            codec => "json"
        }
        kafka {
            bootstrap_servers => "127.0.0.1:9092"
            topics => ["baidu"]
            auto_offset_reset => "earliest"
            codec => "json"
        }
        kafka {
            bootstrap_servers => "127.0.0.1:9092"
            topics => ["zhihu"]
            auto_offset_reset => "earliest"
            codec => "json"
        }
        kafka {
            bootstrap_servers => "127.0.0.1:9092"
            topics => ["kejizixun"]
            auto_offset_reset => "earliest"
            codec => "json"
        }
}
#filter {
#    mutate {
#         add_field => { "[@metadata][index_name]" => "test"}
#        add_field => { "[@metadata][type_name]" => "test"}
#         remove_field => ["headers","@timestamp","host","@version","message","index_message","index_name","type_name","id"]
#    }
#}
output {
        stdout {codec => rubydebug}
#        elasticsearch {
#            hosts => ["127.0.0.1:9222"]
#            index => "%{[@metadata][index_name]}"
#            workers => 1
#            document_type => "%{[@metadata][type_name]}"
#            template_overwrite => false
#        }
}
```



