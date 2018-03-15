##### 业务接入

| 模块 | 说明 |
| :---: | :---: |
| 单点登录-登录 | 提供登录的入口 |
| 单点登录-登出 | 提供注销的入口 |
| 单点登录-登录状态 | 提供登录状态校验/登录信息查询的服务 |
| 单点登录-数据库 | 存储用户账户信息 |
| 单点登录-缓存 | 存储用户的登录信息，使用Redis |

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

`response`

```
jwttoken 认证成功

{
    "code": 200,
    "data": {
        "mail": "pengqiuyuanfj@gmail.com",
        "phone": "13654255565",
        "id": 5,
        "ttl": 86228,
        "registerDate": 1520325613000,
        "status": "1"
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



