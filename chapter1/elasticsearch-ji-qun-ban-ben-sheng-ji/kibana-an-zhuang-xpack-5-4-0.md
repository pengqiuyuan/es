遇到的问题，使用 nginx ，然后修改 自带的 kibana用户密码，访问 127.0.0.1 出现页面重定向过多。

安装 `xpack`

```
idatage@iZ2ze2q8du3j7164j0v6umZ:~$ sudo /usr/share/kibana/bin/kibana-plugin install file:///home/idatage/download/x-pack-5.4.0.zip
Attempting to transfer from file:///home/idatage/download/x-pack-5.4.0.zip
Transferring 161505245 bytes....................
Transfer complete
Retrieving metadata from plugin archive
Extracting plugin archive
Extraction complete
Optimizing and caching browser bundles...
Plugin installation complete
```

启动、停止、查看状态

```
sudo service kibana start
sudo service kibana stop
sudo service kibana status
```

使用 nginx 代理

1. 注意不用修改 `/etc/kibana/kibana.yml` 中的 `server.basePath`

  修改 `elasticsearch.url:"http://localhost:9222"`

2. 修改 `nginx` ，`/etc/nginx/sites-available/default`

  ```
    location / {
        proxy_pass http://localhost:5601;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
  ```
3. 检查 `sudo nginx -t` 、重启 `sudo nginx -s reload`

4. 访问 `127.0.0.1` 页面跳转到 `kibana` 登录界面



