第一步、登录`15`台新机器，创建 `idatage` 用户，`root` 权限

创建用户`sudo adduser idatage`

添加`root`权限`sudo vim /etc/sudoers`

`idatage ALL=NOPASSWD:ALL`

第二步、修改 `hosts` 文件，[参考](/chapter1.md)

第三步、配置私钥免密码登录，[参考](/chapter1.md)

第四部、挂载 `SSD`，参考



第五步、执行 `ansible-playbook -s site.yml`

第六步、修改系统配置，[参考](/system-pei-zhi.md)

