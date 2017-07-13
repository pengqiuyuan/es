第一步、`ROOT` 用户挂载 `SSD`，[参考](https://help.aliyun.com/document_detail/25426.html?spm=5176.doc25446.2.4.5NxhED)

```
sudo fdisk -l 
fdisk /dev/vdb 对数据盘进行分区。根据提示，依次输入 n，p，1，两次回车，wq，分区就开始了。
fdisk -l 
mkfs.ext3 /dev/vdb1
echo /dev/vdb1 /mnt ext3 defaults 0 0 >> /etc/fstab
cat /etc/fstab
mount /dev/vdb1 /mnt
df -h

后四条
echo /dev/vdb1 /mnt ext3 defaults 0 0 >> /etc/fstab && cat /etc/fstab && mount /dev/vdb1 /mnt && df -h
```

第二步、登录`9`台新机器，创建 `idatage` 用户，`root` 权限

创建用户`sudo adduser idatage`

添加`root`权限`sudo vim /etc/sudoers`

`idatage ALL=NOPASSWD:ALL`

第三步、`ROOT` 用户配置私钥免密码登录，[参考](/chapter1.md)

第四步、修改 `hosts` 文件，[参考](/chapter1.md)

第五步、执行 `ansible-playbook -s site.yml`

第六步、执行 `ansible all -m ping` 检查

第七步、修改系统配置，[参考](/system-pei-zhi.md)

```
ansible all -s -m raw -a '
grep "* - nofile 512000" /etc/security/limits.conf || echo "* - nofile 512000" >> /etc/security/limits.conf
grep "elasticsearch - nproc unlimited" /etc/security/limits.conf || echo "elasticsearch - nproc unlimited" >> /etc/security/limits.conf
grep "fs.file-max = 1024000" /etc/sysctl.conf || echo "fs.file-max = 1024000" >> /etc/sysctl.conf
grep "vm.max_map_count = 262144" /etc/sysctl.conf || echo "vm.max_map_count = 262144" >> /etc/sysctl.conf
grep "vm.swappiness = 1" /etc/sysctl.conf || echo "vm.swappiness = 1" >> /etc/sysctl.conf #禁用 swapping
sysctl -p'
```

第八步、修改 `ansible` 配置文集 `elasticsearch.yml` ，主要两个方面，修改 `discovery.zen.ping.unicast.hosts` 和 添加新的 `elasticsearch_data_nodes`

```

```

第九步、跳转到 `node07`，停止数据写入 `Elasticsearch`、停止 `Logstash`

```
sudo docker-compose stop
```

第十步、刷新段文件到磁盘、停止分片自动分配

```
curl -XPOST http://127.0.0.1:9222/_flush/synced?pretty

curl -XPUT http://127.0.0.1:9222/_cluster/settings -d '{
  "transient" : {
    "cluster.routing.allocation.enable" : "none"
  }
}'
```

第十一步、手动停止集群

```
ansible all -s -m raw -a 'service node_elasticsearch stop'
```

第十二步、执行 `ansible` 的 `elasticsearch.yml `，等待节点全部启动，等待新增完毕。`xpack` 会被自动删除，后面机器全部启动后需要重新安装 `xpack` 和部分集群安装 `IK`

```
ansible-playbook -s elasticsearch.yml
```



