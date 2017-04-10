基于 `nginx` 的简单安全配置

* [x] 修改 `elasticsearch` `http`（`9222`） 和 transport （`9333`）默认端口

* [x] `nginx` 安装（安装在`node01 client`节点）,`ufw` 开启`80`、`22`端口

```
[vpn]
node01 vpn_ip=10.0.0.1 ansible_host=77.222.52.211
node02 vpn_ip=10.0.0.2 ansible_host=77.222.52.212
[elasticsearch_client_nodes]
node01
node02
```

`sudo apt-get -y install nginx`

如果`80`端口被占用，执行`sudo fuser -k 80/tcp`

安装目录在 `/etc/nginx`

启动：`sudo nginx`

检查：`sudo nginx -t`

修改配置重启：`sudo nginx -s reload`

查看nginx日志：`/var/log/nginx`

修改配置目录：`/etc/nginx/sites-available/default` 文件

```
        location /x/{
                proxy_set_header    Host $http_host;
                proxy_set_header    X-Real-IP   $remote_addr;
                proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_redirect off;
                proxy_pass http://127.0.0.1:9222/;
        }
        location /y/{
                proxy_set_header    Host $http_host;
                proxy_set_header    X-Real-IP   $remote_addr;
                proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_redirect off;
                proxy_pass  http://127.0.0.1:9100/;
        }
        location /z/{
                proxy_set_header    Host $http_host;
                proxy_set_header    X-Real-IP   $remote_addr;
                proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_redirect off;
                proxy_pass  http://127.0.0.1:8000/;
        }
```

* [x] 登录权限

安装`htpasswd`，确认是否存在，`which htpasswd`

`sudo apt-get -y install apache2-utils`

生成`passfile`文件，

`sudo htpasswd -c -d /etc/nginx/conf.d/pass_file xxxx`

修改配置目录：`/etc/nginx/sites-available/default`文件，添加

```
auth_basic "Protected Elasticsearch";
auth_basic_user_file /etc/nginx/conf.d/pass_file;
```



