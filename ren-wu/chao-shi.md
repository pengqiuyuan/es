请求 Es 时间过长 Nginx 超时

```
11:01:35.347 [SpringJobSchedulerFactoryBean_Worker-6] INFO  com.stq.schedual.words.WordsBase - 词包【微博子任务】统计调度结束-----【weibo_actualVolume异常】：3
org.elasticsearch.client.ResponseException: GET http://服务器IP:9999/weibo_articles_and_weiboers/weibo_articles_and_weiboer/_search?pretty=true: HTTP/1.1 504 Gateway Time-out
<html>
<head><title>504 Gateway Time-out</title></head>
<body bgcolor="white">
<center><h1>504 Gateway Time-out</h1></center>
<hr><center>nginx/1.10.3 (Ubuntu)</center>
</body>
</html>

    at org.elasticsearch.client.RestClient$1.completed(RestClient.java:354)
    at org.elasticsearch.client.RestClient$1.completed(RestClient.java:343)
    at org.apache.http.concurrent.BasicFuture.completed(BasicFuture.java:119)
    at org.apache.http.impl.nio.client.DefaultClientExchangeHandlerImpl.responseCompleted(DefaultClientExchangeHandlerImpl.java:177)
    at org.apache.http.nio.protocol.HttpAsyncRequestExecutor.processResponse(HttpAsyncRequestExecutor.java:436)
    at org.apache.http.nio.protocol.HttpAsyncRequestExecutor.inputReady(HttpAsyncRequestExecutor.java:326)
    at org.apache.http.impl.nio.DefaultNHttpClientConnection.consumeInput(DefaultNHttpClientConnection.java:265)
    at org.apache.http.impl.nio.client.InternalIODispatch.onInputReady(InternalIODispatch.java:81)
    at org.apache.http.impl.nio.client.InternalIODispatch.onInputReady(InternalIODispatch.java:39)
    at org.apache.http.impl.nio.reactor.AbstractIODispatch.inputReady(AbstractIODispatch.java:114)
    at org.apache.http.impl.nio.reactor.BaseIOReactor.readable(BaseIOReactor.java:162)
    at org.apache.http.impl.nio.reactor.AbstractIOReactor.processEvent(AbstractIOReactor.java:337)
    at org.apache.http.impl.nio.reactor.AbstractIOReactor.processEvents(AbstractIOReactor.java:315)
    at org.apache.http.impl.nio.reactor.AbstractIOReactor.execute(AbstractIOReactor.java:276)
    at org.apache.http.impl.nio.reactor.BaseIOReactor.execute(BaseIOReactor.java:104)
    at org.apache.http.impl.nio.reactor.AbstractMultiworkerIOReactor$Worker.run(AbstractMultiworkerIOReactor.java:588)
    at java.lang.Thread.run(Thread.java:745)
```

```
server
{   
    listen 9999;
    server_name localhost;
    location / {
        proxy_redirect off;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_pass http://服务器IP:端口;
        proxy_read_timeout 300;
        fastcgi_read_timeout 600;
    }
}
```



