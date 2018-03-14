**打包**

```
mvn clean package -Dmaven.test.skip=true
```

**启动**

```
java -jar -Dspring.profiles.active=idatage target/sso-1.0.jar

mvn spring-boot:run -Drun.profiles=dev

mvn spring-boot:run -Drun.profiles=idatage

mvn spring-boot:run -Drun.profiles=qy

```





