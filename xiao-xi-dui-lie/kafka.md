挂载普通磁盘 ROOT 用户

```
fdisk -l 
fdisk /dev/vdc 对数据盘进行分区。根据提示，依次输入 n，p，1，两次回车，wq，分区就开始了。
fdisk -l 
mkfs.ext3 /dev/vdc1
echo /dev/vdc1 /kafka ext3 defaults 0 0 >> /etc/fstab
cat /etc/fstab
mkdir /kafka
mount /dev/vdc1 /kafka
df -h
```



