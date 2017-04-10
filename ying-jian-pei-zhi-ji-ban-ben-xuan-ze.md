`15`、`30`、`90`台机器 `Data Client`

* [x] 内存 `32G`

```
$ cat /proc/meminfo |grep MemTotal
MemTotal:       32947548 kB
```

* [x] 磁盘 `1T SSD`

```
$ df -h
文件系统        容量  已用  可用 已用% 挂载点
udev             16G     0   16G    0% /dev
tmpfs           3.2G  4.4M  3.2G    1% /run
/dev/vda1        40G  5.0G   33G   14% /
tmpfs            16G  4.0K   16G    1% /dev/shm
tmpfs           5.0M     0  5.0M    0% /run/lock
tmpfs            16G     0   16G    0% /sys/fs/cgroup
/dev/vdb1      1008G   72M  957G    1% /mnt
tmpfs           3.2G     0  3.2G    0% /run/user/1000
```

* [x] CPU

逻辑CPU个数：`4`，物理CPU个数：`1`

```
$ cat /proc/cpuinfo | grep name | cut -f2 -d: | uniq -c 
4  Intel(R) Xeon(R) CPU E5-2680 v3 @ 2.50GHz
cat /proc/cpuinfo | grep "physical id" | sort | uniq | wc -l
1
$ cat /proc/cpuinfo |grep "model name" && cat /proc/cpuinfo |grep "physical id"
model name    : Intel(R) Xeon(R) CPU E5-2680 v3 @ 2.50GHz
model name    : Intel(R) Xeon(R) CPU E5-2680 v3 @ 2.50GHz
model name    : Intel(R) Xeon(R) CPU E5-2680 v3 @ 2.50GHz
model name    : Intel(R) Xeon(R) CPU E5-2680 v3 @ 2.50GHz
physical id    : 0
physical id    : 0
physical id    : 0
physical id    : 0
```

* [x] 操作系统版本 `Ubuntu 16.04`

```
$  head -n 1 /etc/issue
Ubuntu 16.04.2 LTS \n \l
$ uname -a
Linux iZ2ze2q8du3j7164j0v6umZ 4.4.0-63-generic #84-Ubuntu SMP Wed Feb 1 17:20:32 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux
```

* [x] 版本统一 `elk`，`elasticsearch v5.3.0`、`kibana v5.3.0`、`logtash v5.3.0`

`Lucene 6.x` ，磁盘空间少一半；索引时间少一半；查询性能提升`25%`

`Sliced Scroll`类型 并发进行数据遍历

`Shrink  API` ，`elasticsearch`索引的`shard`数是固定的，设置好了之后不能修改，如果发现`shard`太多或者太少的问题，那么我们就可以想象成这样一种场景，在写入压力非常大的收集阶段，设置足够多的索引，充分利用`shard`的并行写能力，索引写完之后收缩成更少的`shard`，提高查询性能。

`Rollover API`  首先创建一个`logs-0001` 的索引，它有一个别名是 `logs_write`, 然后我们给这个 `logs_write` 创建了一个 `rollover` 规则，即这个索引文档不超过 `1000` 个或者最多保存 `7` 天的数据，超过会自动切换别名到`logs-0002`, 你也可以设置索引的 `setting` 、 `mapping` 等参数 , 剩下的 `es` 会自动帮你处理。这个特性对于存放日志数据的场景是极为友好的。

`Reindex`

```
curl -XPOST http://localhost:9222/_reindex?slices=5 -d '
{
  "source": {
    "remote": {
      "host": "http://10.171.101.99:9200"
    },
    "index": "weixiners",
    "size": 50000
  },
  "dest": {
    "index": "weixiners-test",
    "type": "weixiner－test"
  },
  "script": {
    "inline": "ctx._source.uid = ctx._source.remove(\"_id\"); ctx._source.score = 1.0"
  }
}'
```

`restclient`，`5.0`里面提供了第一个`Java`原生的`REST`客户端`SDK`，相比之前的`TransportClient`，版本依赖绑定，集群升级麻烦，不支持跨`Java`版本的调用等问题，新的基于`HTTP`协议的客户端对`Elasticsearch`的依赖解耦，没有`jar`包冲突，提供了集群节点自动发现、日志处理、节点请求失败自动进行请求轮询，充分发挥`Elasticsearch`的高可用能力，并且性能不相上下

数据结构：`half_float`、`Text`和`Keyword`

