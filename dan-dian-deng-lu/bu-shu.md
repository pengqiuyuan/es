# 部署

**打包**

```text
mvn clean package -Dmaven.test.skip=true
```

**启动**

```text
java -Xms256m -Xmx256m -jar -Dspring.profiles.active=idatage target/sso-1.0.jar

nohup java -Xms256m -Xmx256m -jar -Dspring.profiles.active=idatage target/sso-1.0.jar  > nohup_idatage.out &

mvn spring-boot:run -Drun.profiles=idatage

-------

java -Xms256m -Xmx256m -jar -Dspring.profiles.active=qy target/sso-1.0.jar

nohup java -Xms256m -Xmx256m -jar -Dspring.profiles.active=qy target/sso-1.0.jar  > nohup_qy.out &

mvn spring-boot:run -Drun.profiles=qy

-------
mvn spring-boot:run -Drun.profiles=dev
```

```text
mvn clean package -Dmaven.test.skip=true

nohup java -Xms256m -Xmx256m -jar -Dspring.profiles.active=idatage target/sso-1.0.jar  > nohup_idatage.out &

nohup java -Xms256m -Xmx256m -jar -Dspring.profiles.active=qy target/sso-1.0.jar  > nohup_qy.out &
```

**测试**

```text
mvn clean package -Dmaven.test.skip=true

nohup java -Xms32m -Xmx32m -jar -Dserver.port=8083 target/com.hellokoding.security-1.5.2.RELEASE.jar  > nohup_test1.out &
```

```text
mvn clean package -Dmaven.test.skip=true

nohup java -Xms32m -Xmx32m -jar -Dserver.port=8084 target/com.hellokoding.security-1.5.2.RELEASE.jar  > nohup_test2.out &
```

