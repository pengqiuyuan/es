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

```
mvn spring-boot:run -Drun.jvmArguments='-Dserver.port=8085'
mvn spring-boot:run -Dspring-boot.run.arguments=--server.port=8082
```

```
mvn install
mvn -pl ruoyi-admin clean test -Dtest=com.ruoyi.project.Ttest#test

https://stackoverflow.com/questions/41092200/run-mvn-spring-bootrun-from-parent-module



mvn -pl my-app -am spring-boot:run

mvn -pl ruoyi-admin -am  spring-boot:run -Dspring-boot.run.arguments=--server.port=8080

https://stackoverflow.com/questions/43752986/run-test-cases-of-particular-module-in-multi-module-project-using-maven

 mvn spring-boot:run -Dspring-boot.run.arguments=--server.port=8080
 
  mvn clean test -DfailIfNoTests=false  -Dtest=com.ruoyi.project.Ttest#test
  
  
  mvn clean test -Dtest=Ttest#test -DfailIfNoTests=false
  
```

```
public class ShiroUtils
{

    @Before
    public static Subject getSubject()
    {
        DefaultSecurityManager defaultSecurityManager = new DefaultSecurityManager();
        SecurityUtils.setSecurityManager(defaultSecurityManager);
        return SecurityUtils.getSubject();
    }
}
```






