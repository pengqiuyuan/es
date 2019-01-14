打包部署


```
生成环境

mvn clean package -Dmaven.test.skip=true

java -Xms4g -Xmx4g -jar -Dserver.port=8081 target/tarzan.jar
```

```
测试环境

mvn clean package -Dmaven.test.skip=true

java -Xms4g -Xmx4g -jar -Dserver.port=8081 target/tarzan.jar
```



mvn spring-boot:run -Dspring-boot.run.arguments=--server.port=8082
