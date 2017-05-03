HTTP POST 请求数据写入 KAFKA 队列

```js
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
	if [index_name] == "weibo_articles_and_weiboers"{
		kafka {
			bootstrap_servers => "127.0.0.1:9092"
			topic_id => "weibo_articles_and_weiboers"
			codec => "json"
		}
		stdout {codec => rubydebug}
	}	
	else if [index_name] == "weixin_articles_and_weixiners"{
		kafka {
			bootstrap_servers => "127.0.0.1:9092"
			topic_id => "weixin_articles_and_weixiners"
			codec => "json"
		}
		stdout {codec => rubydebug}
	}
	else if [index_name] == "toutiao_articles_and_users"{
		kafka {
			bootstrap_servers => "127.0.0.1:9092"
			topic_id => "toutiao_articles_and_users"
			codec => "json"
		}
		stdout {codec => rubydebug}
	}
	else if [index_name] == "baidunews_news"{
		kafka {
			bootstrap_servers => "127.0.0.1:9092"
			topic_id => "baidunews_news"
			codec => "json"
		}
		stdout {codec => rubydebug}
	}
	else if [index_name] == "zhihu_questions"{
		kafka {
			bootstrap_servers => "127.0.0.1:9092"
			topic_id => "zhihu_questions"
			codec => "json"
		}
		stdout {codec => rubydebug}
	}
	else if [index_name] == "test"{
		kafka {
			bootstrap_servers => "127.0.0.1:9092"
			topic_id => "test"
			codec => "json"
		}
		stdout {codec => rubydebug}
	}
}
```



