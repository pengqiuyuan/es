**打包**

```
mvn clean package -Dmaven.test.skip=true
```

**启动**

```
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

```
nohup java -Xms256m -Xmx256m -jar -Dspring.profiles.active=idatage target/sso-1.0.jar  > nohup_idatage.out &

nohup java -Xms256m -Xmx256m -jar -Dspring.profiles.active=qy target/sso-1.0.jar  > nohup_qy.out &


```



