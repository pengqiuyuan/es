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

`home` 位置` /usr/share/kibana`

`config` 位置 `/etc/kibana`

---



