**安装 **`kibana 5`

安装 `64 bit`：

```
wget https://artifacts.elastic.co/downloads/kibana/kibana-5.3.0-amd64.deb
sha1sum kibana-5.3.0-amd64.deb 
sudo dpkg -i kibana-5.3.0-amd64.deb
```

启动、停止、重启、状态

```
sudo service kibana start
sudo service kibana stop
sudo service kibana restart
sudo service kibana status
```

```
$ sudo service kibana status
● kibana.service - Kibana
   Loaded: loaded (/etc/systemd/system/kibana.service; disabled; vendor preset: enabled)
   Active: active (running) since 四 2017-04-13 10:10:17 CST; 3h 1min ago
 Main PID: 30796 (node)
   CGroup: /system.slice/kibana.service
           └─30796 /usr/share/kibana/bin/../node/bin/node --no-warnings /usr/share/kibana/bin/../src/cli -c /etc/kibana/kibana.yml
```

`home` 位置`/usr/share/kibana`

`config` 位置 `/etc/kibana`

---

`kibana 5 nginx`** 代理配置**

生成`passfile`文件，

`sudo htpasswd -c -d /etc/nginx/conf.d/pass_file_kibana5 xxxx`

配置 `nginx`，目录 `/etc/nginx/sites-available/default`

```
        location /kibana/ {
                proxy_pass http://127.0.0.1:5601;
                rewrite /kibana/(.*)$ /$1 break;
                proxy_set_header    Host $http_host;
                proxy_set_header    X-Real-IP   $remote_addr;
                proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
                auth_basic           "Restricted";
                auth_basic_user_file /etc/nginx/conf.d/pass_file_kibana5;
        }
```

> 注意：需要修改 `/etc/kibana/kibana.yml`

```
server.basePath:"/kibana"
elasticsearch.url:"http://localhost:9222"
```

浏览器访问：`http://127.0.0.1/kibana`

