请求超时问题

```

00:15:14.041 [executor-9] ERROR org.quartz.core.ErrorLogger - Job (DEFAULT.wordsUpdateStatsMethod threw an exception.
org.quartz.SchedulerException: Job threw an unhandled exception.
	at org.quartz.core.JobRunShell.run(JobRunShell.java:224) ~[quartz-2.1.3.jar:na]
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149) [na:1.8.0_151]
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624) [na:1.8.0_151]
	at java.lang.Thread.run(Thread.java:748) [na:1.8.0_151]
Caused by: org.springframework.scheduling.quartz.JobMethodInvocationFailedException: Invocation of method 'schedual' on target class [class com.stq.schedual.words.WordsUpdateStatsScheduled] failed; nested exception is java.lang.RuntimeException: error while performing request
	at org.springframework.scheduling.quartz.MethodInvokingJobDetailFactoryBean$MethodInvokingJob.executeInternal(MethodInvokingJobDetailFactoryBean.java:266) ~[spring-context-support-4.2.4.RELEASE.jar:4.2.4.RELEASE]
	at org.springframework.scheduling.quartz.QuartzJobBean.execute(QuartzJobBean.java:75) ~[spring-context-support-4.2.4.RELEASE.jar:4.2.4.RELEASE]
	at org.quartz.core.JobRunShell.run(JobRunShell.java:213) ~[quartz-2.1.3.jar:na]
	... 3 common frames omitted
Caused by: java.lang.RuntimeException: error while performing request
	at org.elasticsearch.client.RestClient$SyncResponseListener.get(RestClient.java:681) ~[rest-5.4.0.jar:5.4.0]
	at org.elasticsearch.client.RestClient.performRequest(RestClient.java:219) ~[rest-5.4.0.jar:5.4.0]
	at org.elasticsearch.client.RestClient.performRequest(RestClient.java:191) ~[rest-5.4.0.jar:5.4.0]
	at com.stq.service.stq.words.weibo.WeiboStatsService.countPerdays(WeiboStatsService.java:193) ~[classes/:na]
	at com.stq.service.stq.words.weibo.WeiboStatsService.coefficient(WeiboStatsService.java:263) ~[classes/:na]
	at com.stq.service.stq.words.weibo.WeiboStatsService$$FastClassBySpringCGLIB$$6853de11.invoke(<generated>) ~[classes/:na]
	at org.springframework.cglib.proxy.MethodProxy.invoke(MethodProxy.java:204) ~[spring-core-4.2.4.RELEASE.jar:4.2.4.RELEASE]
	at org.springframework.aop.framework.CglibAopProxy$CglibMethodInvocation.invokeJoinpoint(CglibAopProxy.java:720) ~[spring-aop-4.2.4.RELEASE.jar:4.2.4.RELEASE]
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:157) ~[spring-aop-4.2.4.RELEASE.jar:4.2.4.RELEASE]
	at org.springframework.transaction.interceptor.TransactionInterceptor$1.proceedWithInvocation(TransactionInterceptor.java:99) ~[spring-tx-4.2.4.RELEASE.jar:4.2.4.RELEASE]
	at org.springframework.transaction.interceptor.TransactionAspectSupport.invokeWithinTransaction(TransactionAspectSupport.java:281) ~[spring-tx-4.2.4.RELEASE.jar:4.2.4.RELEASE]
	at org.springframework.transaction.interceptor.TransactionInterceptor.invoke(TransactionInterceptor.java:96) ~[spring-tx-4.2.4.RELEASE.jar:4.2.4.RELEASE]
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:179) ~[spring-aop-4.2.4.RELEASE.jar:4.2.4.RELEASE]
	at org.springframework.aop.framework.CglibAopProxy$DynamicAdvisedInterceptor.intercept(CglibAopProxy.java:655) ~[spring-aop-4.2.4.RELEASE.jar:4.2.4.RELEASE]
	at com.stq.service.stq.words.weibo.WeiboStatsService$$EnhancerBySpringCGLIB$$cd2f6450.coefficient(<generated>) ~[classes/:na]
	at com.stq.service.stq.words.WordsUpdateService.cibaoWeiboUpdate(WordsUpdateService.java:136) ~[classes/:na]
	at com.stq.service.stq.words.WordsUpdateService.getEsWord(WordsUpdateService.java:103) ~[classes/:na]
	at com.stq.service.stq.words.WordsUpdateService$$FastClassBySpringCGLIB$$854d966a.invoke(<generated>) ~[classes/:na]
	at org.springframework.cglib.proxy.MethodProxy.invoke(MethodProxy.java:204) ~[spring-core-4.2.4.RELEASE.jar:4.2.4.RELEASE]
	at org.springframework.aop.framework.CglibAopProxy$CglibMethodInvocation.invokeJoinpoint(CglibAopProxy.java:720) ~[spring-aop-4.2.4.RELEASE.jar:4.2.4.RELEASE]
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:157) ~[spring-aop-4.2.4.RELEASE.jar:4.2.4.RELEASE]
	at org.springframework.transaction.interceptor.TransactionInterceptor$1.proceedWithInvocation(TransactionInterceptor.java:99) ~[spring-tx-4.2.4.RELEASE.jar:4.2.4.RELEASE]
	at org.springframework.transaction.interceptor.TransactionAspectSupport.invokeWithinTransaction(TransactionAspectSupport.java:281) ~[spring-tx-4.2.4.RELEASE.jar:4.2.4.RELEASE]
	at org.springframework.transaction.interceptor.TransactionInterceptor.invoke(TransactionInterceptor.java:96) ~[spring-tx-4.2.4.RELEASE.jar:4.2.4.RELEASE]
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:179) ~[spring-aop-4.2.4.RELEASE.jar:4.2.4.RELEASE]
	at org.springframework.aop.framework.CglibAopProxy$DynamicAdvisedInterceptor.intercept(CglibAopProxy.java:655) ~[spring-aop-4.2.4.RELEASE.jar:4.2.4.RELEASE]
	at com.stq.service.stq.words.WordsUpdateService$$EnhancerBySpringCGLIB$$51ab1289.getEsWord(<generated>) ~[classes/:na]
	at com.stq.schedual.words.WordsUpdateStatsScheduled.schedual(WordsUpdateStatsScheduled.java:50) ~[classes/:na]
	at sun.reflect.GeneratedMethodAccessor62.invoke(Unknown Source) ~[na:na]
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43) ~[na:1.8.0_151]
	at java.lang.reflect.Method.invoke(Method.java:498) ~[na:1.8.0_151]
	at org.springframework.util.MethodInvoker.invoke(MethodInvoker.java:269) ~[spring-core-4.2.4.RELEASE.jar:4.2.4.RELEASE]
	at org.springframework.scheduling.quartz.MethodInvokingJobDetailFactoryBean$MethodInvokingJob.executeInternal(MethodInvokingJobDetailFactoryBean.java:257) ~[spring-context-support-4.2.4.RELEASE.jar:4.2.4.RELEASE]
	... 5 common frames omitted
Caused by: java.util.concurrent.TimeoutException: null
	at org.apache.http.nio.pool.AbstractNIOConnPool.processPendingRequest(AbstractNIOConnPool.java:364) ~[httpcore-nio-4.4.5.jar:4.4.5]
	at org.apache.http.nio.pool.AbstractNIOConnPool.processNextPendingRequest(AbstractNIOConnPool.java:344) ~[httpcore-nio-4.4.5.jar:4.4.5]
	at org.apache.http.nio.pool.AbstractNIOConnPool.release(AbstractNIOConnPool.java:318) ~[httpcore-nio-4.4.5.jar:4.4.5]
	at org.apache.http.impl.nio.conn.PoolingNHttpClientConnectionManager.releaseConnection(PoolingNHttpClientConnectionManager.java:303) ~[httpasyncclient-4.1.2.jar:4.1.2]
	at org.apache.http.impl.nio.client.AbstractClientExchangeHandler.releaseConnection(AbstractClientExchangeHandler.java:239) ~[httpasyncclient-4.1.2.jar:4.1.2]
	at org.apache.http.impl.nio.client.MainClientExec.responseCompleted(MainClientExec.java:387) ~[httpasyncclient-4.1.2.jar:4.1.2]
	at org.apache.http.impl.nio.client.DefaultClientExchangeHandlerImpl.responseCompleted(DefaultClientExchangeHandlerImpl.java:168) ~[httpasyncclient-4.1.2.jar:4.1.2]
	at org.apache.http.nio.protocol.HttpAsyncRequestExecutor.processResponse(HttpAsyncRequestExecutor.java:436) ~[httpcore-nio-4.4.5.jar:4.4.5]
	at org.apache.http.nio.protocol.HttpAsyncRequestExecutor.inputReady(HttpAsyncRequestExecutor.java:326) ~[httpcore-nio-4.4.5.jar:4.4.5]
	at org.apache.http.impl.nio.DefaultNHttpClientConnection.consumeInput(DefaultNHttpClientConnection.java:265) ~[httpcore-nio-4.4.5.jar:4.4.5]
	at org.apache.http.impl.nio.client.InternalIODispatch.onInputReady(InternalIODispatch.java:81) ~[httpasyncclient-4.1.2.jar:4.1.2]
	at org.apache.http.impl.nio.client.InternalIODispatch.onInputReady(InternalIODispatch.java:39) ~[httpasyncclient-4.1.2.jar:4.1.2]
	at org.apache.http.impl.nio.reactor.AbstractIODispatch.inputReady(AbstractIODispatch.java:114) ~[httpcore-nio-4.4.5.jar:4.4.5]
	at org.apache.http.impl.nio.reactor.BaseIOReactor.readable(BaseIOReactor.java:162) ~[httpcore-nio-4.4.5.jar:4.4.5]
	at org.apache.http.impl.nio.reactor.AbstractIOReactor.processEvent(AbstractIOReactor.java:337) ~[httpcore-nio-4.4.5.jar:4.4.5]
	at org.apache.http.impl.nio.reactor.AbstractIOReactor.processEvents(AbstractIOReactor.java:315) ~[httpcore-nio-4.4.5.jar:4.4.5]
	at org.apache.http.impl.nio.reactor.AbstractIOReactor.execute(AbstractIOReactor.java:276) ~[httpcore-nio-4.4.5.jar:4.4.5]
	at org.apache.http.impl.nio.reactor.BaseIOReactor.execute(BaseIOReactor.java:104) ~[httpcore-nio-4.4.5.jar:4.4.5]
	at org.apache.http.impl.nio.reactor.AbstractMultiworkerIOReactor$Worker.run(AbstractMultiworkerIOReactor.java:588) ~[httpcore-nio-4.4.5.jar:4.4.5]
	... 1 common frames omitted
	
```

解决办法

```
RestClientBuilder
setMaxConnPerRoute(120)  默认 10
setMaxConnTotal(140)  默认 30
```


[elasticsearch的RestClientAPI请求超时问题](http://blog.csdn.net/wangweislk/article/details/78839384)

[异步httpclient(httpasyncclient)的使用与总结](http://blog.csdn.net/ouyang111222/article/details/78884634)

[使用httpclient必须知道的参数设置及代码写法、存在的风险](http://jinnianshilongnian.iteye.com/blog/2089792)




