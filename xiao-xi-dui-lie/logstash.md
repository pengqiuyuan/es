ES 消费 KAFKA 数据

```
input {
        kafka {
            bootstrap_servers => "10.27.240.159:9092"
            topics => ["weibo"]
            auto_offset_reset => "earliest"
            codec => "json"
            group_id => "weibo_group_1"
        }
        kafka {
            bootstrap_servers => "10.27.240.159:9092"
            topics => ["weixin"]
            auto_offset_reset => "earliest"
            codec => "json"
            group_id => "weixin_group_1"
        }
        kafka {
            bootstrap_servers => "10.27.240.159:9092"
            topics => ["toutiao"]
            auto_offset_reset => "earliest"
            codec => "json"
            group_id => "toutiao_group_1"
        }
        kafka {
            bootstrap_servers => "10.27.240.159:9092"
            topics => ["baidu"]
            auto_offset_reset => "earliest"
            codec => "json"
            group_id => "baidu_group_1"
        }
        kafka {
            bootstrap_servers => "10.27.240.159:9092"
            topics => ["zhihu"]
            auto_offset_reset => "earliest"
            codec => "json"
            group_id => "zhihu_group_1"       
	}
        kafka {
            bootstrap_servers => "10.27.240.159:9092"
            topics => ["kejizixun"]
            auto_offset_reset => "earliest"
            codec => "json"
            group_id => "kejizixun_group_1"
        }
        kafka {
            bootstrap_servers => "10.27.240.159:9092"
            topics => ["sogouweixin"]
            auto_offset_reset => "earliest"
            codec => "json"
            group_id => "sogouweixin_group_1"
        }
}
filter {
    mutate {
         add_field => { "[@metadata][id]" => "%{id}"}
         add_field => { "[@metadata][index_name]" => "%{index_name}"}
         add_field => { "[@metadata][type_name]" => "%{type_name}"}
         remove_field => ["@timestamp","@version","index_name","type_name","id"]
    }
}
output {
	if [@metadata][index_name] == "weibo_articles_and_weiboers" {
		stdout { codec => rubydebug }
	}
	else if [@metadata][index_name] == "weixin_articles_and_weixiners" {
		stdout { codec => rubydebug }
	}
	else if [@metadata][index_name] == "toutiao_articles_and_users" {
		stdout { codec => rubydebug }
	}
	else if [@metadata][index_name] == "baidunews_news" {
		stdout { codec => rubydebug }
	}
	else if [@metadata][index_name] == "zhihu_questions" {
		stdout { codec => rubydebug }
	}
	else if [@metadata][index_name] == "tech_news" {
		stdout { codec => rubydebug }
	}
	else if [@metadata][index_name] == "sogou_weixin_articles" {
		stdout { codec => rubydebug }
	}
}
```



