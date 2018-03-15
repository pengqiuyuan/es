**单点登录**

账户通过一次登录，即可在多个相关的系统之间来回访问。目前有`idatage.com` 、`qyconsulting.cn` 两个主域名，登录一次，`A.idatage.com` 和 `B.qyconsulting.cn` 就可不用再登录了。

**实现**

`JSON Web Token（JWT）+ COOKIE`

**设计**![](/assets/dandian1.png)

业务接入

| 模块 | 说明 |
| :---: | :---: |
| 单点登录-登录 | 提供登录的入口 |
| 单点登录-登出 | 提供注销的入口 |
| 单点登录-登录状态 | 提供登录状态校验/登录信息查询的服务 |

普通功能

| 模块 |
| :---: |
| 登录 |
| 注销 |
| 验证登录状态 |
| 忘记密码 |
| 邮件发送 |
| 修改密码 |

**登录时序图**

![](/assets/dandian2.png)

**登录状态校验**

![](/assets/dandian3.png)

**登出时序图**

![](/assets/dandian4.png)

**跨域登录（主域名已登录）**

![](/assets/dandian5.png)

**跨域登录（主域名未登录）**

![](/assets/dandian6.png)

