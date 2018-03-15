**四、跨域示例**

```
业务A : http://test1.idatage.com/protected-resource
业务B : http://test1.qyconsulting.cn/protected-resource
SSO :  http://login.idatage.com/t/login

第一步、访问业务B -> 页面跳转至 http://login.idatage.com/t/login?redirect=http://test1.qyconsulting.cn/protected-resource
第二步、输入账号密码（可注册） -> 跳转至业务B测试页面 
第二步、访问业务A -> 页面跳转至业务A测试页面，不需要登录
```



