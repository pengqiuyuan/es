第一步、登录`15`台新机器，创建 `idatage` 用户，`root` 权限

创建用户`sudo adduser idatage`

添加`root`权限`sudo vim /etc/sudoers`

`idatage ALL=NOPASSWD:ALL`

第二步、修改 `hosts` 文件，[参考](/chapter1.md)

第三步、配置私钥免密码登录，[参考](/chapter1.md)

第四部、挂载 `SSD`，[参考](https://help.aliyun.com/document_detail/25426.html?spm=5176.doc25446.2.4.5NxhED)

```
sudo fdisk -l 
fdisk /dev/vdb 对数据盘进行分区。根据提示，依次输入 n，p，1，两次回车，wq，分区就开始了。
fdisk -l 
mkfs.ext3 /dev/vdb1
echo /dev/vdb1 /mnt ext3 defaults 0 0 >> /etc/fstab
cat /etc/fstab
mount /dev/vdb1 /mnt
df -h
```

第五步、执行 `ansible-playbook -s site.yml`

第六步、修改系统配置，[参考](/system-pei-zhi.md)

