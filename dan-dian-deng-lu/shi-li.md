**四、跨域示例**

```
业务A : http://test1.idatage.com/protected-resource
业务B : http://test1.qyconsulting.cn/protected-resource
SSO :  http://login.idatage.com/t/login

登录（跨域同时登录）：
第一步、访问业务B -> 页面跳转至 http://login.idatage.com/t/login?redirect=http://test1.qyconsulting.cn/protected-resource
第二步、输入账号密码（可注册） -> 跳转至业务B测试页面 
第三步、访问业务A -> 页面跳转至业务A测试页面，不需要登录

注销（跨域同时注销）：
第一步：点击业务B测试页面里的Logout按钮 -> 页面跳转至重新登录页面
第二步：刷新业务A已登录的测试页面 -> 页面同时跳转至重新登录页面


```



