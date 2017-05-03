ES 消费 KAFKA 数据

```
input {
    kafka {
        bootstrap_servers => "127.0.0.1:9092"
        topics => ["test1"]
        auto_offset_reset => "earliest"
    }
}
output {
    stdout {codec => rubydebug} #测试
}
```



