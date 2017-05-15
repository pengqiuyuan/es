ES 消费 KAFKA 数据

```
input {
        kafka {
            bootstrap_servers => "127.0.0.1:9092"
            topics => ["test1"]
            auto_offset_reset => "earliest"
        }
}
filter {
    json {
        source => "message"
    }
    split {
        field => "index_message"
    }
    mutate {
        rename => [
            "[index_message][id]", "id",
            "[index_message][intro]", "intro",
            "[index_message][categories]", "categories",
            "[index_message][tags]", "tags",
            "[index_message][updated_at]", "updated_at",
            "[index_message][username]", "username",
            "[index_message][name]", "name",
            "[index_message][sentiment]", "sentiment",
            "[index_message][trtl_tags]", "trtl_tags"
        ]
         add_field => { "[@metadata][id]" => "%{id}"}
         add_field => { "[@metadata][index_name]" => "%{index_name}"}
         add_field => { "[@metadata][type_name]" => "%{type_name}"}
         remove_field => ["headers","@timestamp","host","@version","message","index_message","index_name","type_name","id"]
    }
}
output {
        stdout {codec => rubydebug}
        elasticsearch {
            hosts => ["127.0.0.1:9222"]
            index => "%{[@metadata][index_name]}"
            workers => 1
            document_type => "%{[@metadata][type_name]}"
            document_id => "%{[@metadata][id]}"
            template_overwrite => false
        }
}
```



