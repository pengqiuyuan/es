**POST 请求写入数据到 **`kafka`

`POST` `http://127.0.0.1/stq/api/v1/pa/toutiao/add`

`HEADERS`：`"Content-Type" => "application/json"`

`BODY` 体参数说明：List 集合、数组

```js
[
    {
      "id": "10",
      "index_name": "toutiao_articles_and_users",
      "type_name": "toutiao_articles_and_users",
      "avatar_img": "http://p3.pstatp.com/thumb/6427/6955928713",
      "name": "乒乓网"
      ...
    },
    {
      "id": "11",
      "index_name": "toutiao_articles_and_users",
      "type_name": "toutiao_articles_and_users",
      "avatar_img": "http://p3.pstatp.com/thumb/6427/6955928713",
      "name": "乒乓网"
      ...
    }
  ]
```

`logstash`** 消费**`kafka`**中的数据到 **`elasticsearch`

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
filter {
    mutate {
         add_field => { "[@metadata][index_name]" => "test"}         
     add_field => { "[@metadata][type_name]" => "test"}
         remove_field => ["@timestamp","@version","index_name","type_name","id"]
    }
}
output {
#        stdout {codec => rubydebug}
         elasticsearch {
            hosts => ["127.0.0.1:9222"]
#           index => "%{[@metadata][index_name]}"
            index => "test"
        workers => 1
            document_type => "%{[@metadata][type_name]}"
            template_overwrite => false
        }
}
```

从队列中读取的数据，两条符合预期（`index_name`、`type_name`、`id`会在`logstash filter`中处理后移除，保存数据到 `es`）

```
{
    "avatar_img" => "http://p3.pstatp.com/thumb/6427/6955928713",
          "name" => "乒乓网1"
}
{
    "avatar_img" => "http://p3.pstatp.com/thumb/6427/6955928713",
          "name" => "乒乓网2"
}
```



