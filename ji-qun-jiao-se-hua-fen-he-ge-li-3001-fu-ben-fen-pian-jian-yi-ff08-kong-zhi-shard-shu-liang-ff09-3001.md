# 集群角色划分和隔离、 副本分片建议（控制shard数量）、容量的规划

集群角色划分和隔离、 副本分片建议（控制 `shard`数量）、容量的规划

角色分离的原因：

1. 然而对于一个规模较大，用户较多的集群，`master`和`client`在一些极端使用情况下可能会有性能瓶颈甚至内存溢出，从而使得共存的`data node`故障。
2. `data node`的故障恢复涉及到数据的迁移，对集群资源有一定消耗，容易造成数据写入延迟或者查询减慢。

角色分离的好处：

1. 如果将`master`和`client`独立出来，一旦出现问题，重启后几乎是瞬间就恢复的，对用户几乎没有任何影响。
2. 另外将这些角色独立出来的以后，也将对应的计算资源消耗从`data node`剥离出来，更容易掌握`data node`资源消耗与写入量和查询量之间的联系。
3. 故障点定位更加容易。

`master` 节点 `4`核`8G`

`data` 节点 `4`核`32G`

`client` 节点 `4`核`32G`

`Master node`机器配置可以比较低，3台4`core`的虚拟机，内存8GB就足够了

`Client node`的配置取决于仅仅用于查询，还是说还要作为数据`bulk`的统一入口。如果只用于查询，配置和`master node`类似足够。 如果用作写入入口，那么最好也用`8core, 32g`内存的机器。

`Master`和`client node`对于磁盘`IO`都没有要求，无需`SSD`。

`15+5`台 `3`（`master`&&`data`或者单独`master`） `2client 15 data 1replicas`

`30+5` 台 `3`（`master`&&`data`或者单独`master`）`2client 30 data 1replicas`

`90+5` 台 `3`（`master`&&`data`或者单独`master`） `2client 90 data 1replicas`

数据不增长的情况，单个shard尽量控制在`100GB`以内，比如`2TB`左右的索引，20个`shard`，1 `replica`比较合适。 但为了避免写入热点，尽量`pri+replica`是`data node`的整数倍。 比如你有30个`data node`，可以考虑 15 `shard` + 1 `replica`，总共30个`shard`，均匀分布到每一个`node`。这样对于~~**写入量大**~~的索引，写入压力可以均匀分布在每一个`data node`。

`shards` 、`replicas` 在 `mapping` 根据不同的索引设置

`100 G` 以内使用默认的 `5`个`shards` `1`个`replicas`

`1T` 以内使用`15`个`shards` 1个`replicas`

`1T` 以上使用`45`个`shards` 1个`replicas`

