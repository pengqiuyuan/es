HTTP POST 请求数据写入 KAFKA 队列

```
input {
    http {
        host => "127.0.0.1"
        port => "8082"
        codec => "json"
        response_headers => {
            "Content-Type" => "application/json"
        }
    }
}
output {
    kafka {
        bootstrap_servers => "127.0.0.1:9092"
        topic_id => "test1"
        codec => "json"
    }
    stdout {codec => rubydebug}
}
```



