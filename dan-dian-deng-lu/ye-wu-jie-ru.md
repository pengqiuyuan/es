##### 业务接入（支持跨域）

* [x] 只需要关心**两个**跳转页面（登录、注销）和**一个**验证 `jwttoken` 有效性接口即可。
* [x] `http://login.idatage.com/t` 提供 sso 服务

| 模块 | 说明 |
| :---: | :---: |
| 单点登录-登录 | 提供登录的入口 |
| 单点登录-登出 | 提供注销的入口 |
| 单点登录-登录状态 | 提供登录状态校验/登录信息查询的服务 |

**一、登录地址:**

`GET` `http://login.idatage.com/t/login?redirect=业务地址`

`参数` `redirect 必填`

**二、登出地址:**

`GET` `http://login.idatage.com/t/logout?redirect=业务地址`

`参数` `redirect 必填`

**三、登录状态验证接口：**

`GET` `http://login.idatage.com/t/validate?jwttoken=eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiI1IiwiaWF0IjoxNTIxMTAyMzA5fQ.V1R6uzgUsPMs-gBo1BYaYKV6V8stDY5hFDKL9kvIXlQ`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：`jwttoken` 加密签名，[具体参考](http://blog.leapoahead.com/2015/09/06/understanding-jwt/)



`response` ：`ttl` 为查询 `jwttoken` 的剩余有效时间

```
jwttoken 认证成功

{
	"code": 200,
	"data": {
		"company": "数太奇",
		"fullname": "彭秋源",
		"id": 101,
		"mail": "pengqiuyuanfj@gmail.com",
		"password": "",
		"phone": "18610314682",
		"position": "开发",
		"registerdate": 1527155804000,
		"registerway": "测试使用",
		"status": "1",
		"wechat": "18610314682"
	},
	"message": "JWT-TOKEN 有效"
}


jwttoken 认证失败

{
    "code": 400,
    "data": "",
    "message": "JWT-TOKEN 无效"
}
```

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

**五、根据 ids 获取用户信息：**

`POST` `http://login.idatage.com/t/findUserByIds`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
ids 必填。数组
```

`BODY` 体：

```
[26, 101]
```


`response` ：

```

[{
		"company": "",
		"fullname": "",
		"id": 26,
		"mail": "202XXXX@qq.com",
		"password": "",
		"phone": "18210XXXXXX",
		"position": "",
		"registerdate": 1521524679000,
		"registerway": "",
		"status": "1",
		"wechat": ""
	},
	{
		"company": "XXX",
		"fullname": "XXX",
		"id": 101,
		"mail": "peXXXX@gmail.com",
		"password": "",
		"phone": "18XXXX",
		"position": "开发",
		"registerdate": 1527155804000,
		"registerway": "测试使用",
		"status": "1",
		"wechat": "1861XXXX2"
	}
]
```



