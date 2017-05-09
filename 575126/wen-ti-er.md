磁盘空间不足

`No space left on device`

```
idatage@iZ2ze2q8du3j7164j0v6uoZ:/var/lib/docker$ sudo df -h
Filesystem      Size  Used Avail Use% Mounted on
udev             16G     0   16G   0% /dev
tmpfs           3.2G  4.5M  3.2G   1% /run
/dev/vda1        40G   39G     0 100% /
tmpfs            16G     0   16G   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs            16G     0   16G   0% /sys/fs/cgroup
/dev/vdb1      1008G  842M  956G   1% /mnt
tmpfs           3.2G     0  3.2G   0% /run/user/1001
tmpfs           3.2G     0  3.2G   0% /run/user/1000
```

系统盘被写满 ，原因 `27G	./volumes`，`docker`的默认挂载目录（`/var/lib/docker/volumes`），大部分是`kafka`导致

```
/dev/vda1        40G     0   39G   100% /
```

```
idatage@iZ2ze2q8du3j7164j0v6uoZ:/var/lib/docker$ sudo du -h --max-depth=1 |sort 
100K	./network
108K	./swarm
15M	./image
20K	./plugins
27G	./volumes
33G	.
4.0K	./tmp
4.0K	./trust
52K	./containers
5.6G	./aufs
```

常用命令

`sudo du -h --max-depth=1 |grep [TG] |sort`**   **\#查找上`G`和`T`的目录并排序

`sudo du -sh`** **   \#统计当前目录的大小，以直观方式展现

`sudo du -h --max-depth=1 |grep 'G' |sort`**` `  **\#查看上`G`目录并排序

`sudo du -h --max-depth=1 |sort`    \#查看当前目录下所有一级子目录文件夹大小 并排序

`sudo du -h --max-depth=1 |grep [TG] |sort -nr`**` `**  \#倒序排

`sudo df -h`

`sudo du -h`

`sudo du -h /var/lib/docker/volumes`

