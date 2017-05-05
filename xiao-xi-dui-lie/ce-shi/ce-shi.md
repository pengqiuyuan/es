HTTP POST 请求数据写入 ES

```
input {
    http {
        host => "127.0.0.1"
        port => "8082"
        codec => "json"
        response_headers => {
            "Content-Type" => "application/json
        }
  }
}
filter {
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
    }

    mutate {
        add_field => { "[@metadata][id]" => "%{id}"}
        add_field => { "[@metadata][index]" => "%{index}"}
        add_field => { "[@metadata][type]" => "%{type}"}
        remove_field => ["headers","@timestamp","host","@version","indexMessage"]
    }
}
output {
    elasticsearch {
        hosts => ["127.0.0.1:9222"]
        index => "%{[@metadata][index]}"
        workers => 1
        document_type => "%{[@metadata][type]}"
        document_id => "%{[@metadata][id]}"
        template_overwrite => false
    }
    stdout {codec => rubydebug}
}
```



