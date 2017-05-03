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
        field => "indexMessage"
    }
    mutate {
        rename => [
            "[indexMessage][id]", "id",
            "[indexMessage][intro]", "intro",
            "[indexMessage][categories]", "categories",
            "[indexMessage][tags]", "tags",
            "[indexMessage][updated_at]", "updated_at",
            "[indexMessage][username]", "username",
            "[indexMessage][name]", "name",
            "[indexMessage][sentiment]", "sentiment",
            "[indexMessage][trtl_tags]", "trtl_tags"
        ]
         add_field => { "[@metadata][id]" => "%{id}"}
         add_field => { "[@metadata][index]" => "%{index}"}
         add_field => { "[@metadata][type]" => "%{type}"}
         remove_field => ["headers","@timestamp","host","@version","message","indexMessage","index","type","id"]
    }
}
output {
        stdout {codec => rubydebug}
        elasticsearch {
	        hosts => ["127.0.0.1:9222"]
	        index => "%{[@metadata][index]}"
	        workers => 1
	        document_type => "%{[@metadata][type]}"
	        document_id => "%{[@metadata][id]}"
	        template_overwrite => false
    	}
}
```



