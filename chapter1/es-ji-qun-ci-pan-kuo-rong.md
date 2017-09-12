```
ansible all -s -m raw -a 'service node_elasticsearch stop'

ansible all -s -m raw -a 'tail -50 /mnt/log/elasticsearch/node*-node/tarantula.log'
```

[文档](https://help.aliyun.com/document_detail/25452.html?spm=5176.2020520101.0.0.6029e411FEqeGg)

`Linux` 扩容数据盘，需要从阿里云控制台重启机器，之后再重新挂载`SSD`磁盘。

步骤

```
df -H
umount /dev/vdb1
df -H

fdisk -l
fdisk /dev/vdb

d n p 1 回车 回车 wq

df -h
umount /dev/vdb1

e2fsck -f /dev/vdb1
resize2fs /dev/vdb1

mount /dev/vdb1  /mnt
df -h


ansible all -s -m raw -a 'df -h'
```



