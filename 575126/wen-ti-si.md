`Parent/Child` 关系文档

**解决问题：**

类似于`nested model`，可以关联两个实体。不同在于，`nested object`中所有的实体必须存在同一个文档中，而在 `parent-child`中，`parent` 和 `children` 可以是完全分开的文档。

可以用一个实体关联多个相关实体，是一对多的关系。

**限制条件：**

简单讲，仅支持在同一索引中的文档。[官网说明](https://www.elastic.co/guide/en/elasticsearch/guide/current/parent-child.html)

`Elasticsearch` 在 `parent` 和 `child` 之间维护了一个 `map`，由于这个 `map` 的作用，查询时的 `join` 操作非常迅速。但是这也产生了一个局限：`parent` 文档和他所有的 `child` 文档必须在同一个 `shard` 上，不能跨 `shard`。

**使用代价：**

[官网说明](https://www.elastic.co/guide/en/elasticsearch/guide/current/parent-child-performance.html#_global_ordinals_and_latency)

`Parent/Child`  的搜索性能比等效的 `Nested Query` 慢五到十倍。

`Parent/Child`  使用 [全局序数](https://www.elastic.co/guide/cn/elasticsearch/guide/current/preload-fielddata.html#global-ordinals) 来加速文档间的 `join`，当索引变更时，全局序数要重建。

父文档越多，那么全局序数的重建时间就越长。父子关系更适合于父文档少、子文档多的情况。

`joins` 越多，性能越差。

`parents` 文档的`_id`字段存储在内存中。

**综上所述**：在尝试 `parent-child`关系前考虑其他类型的关系技术。

Elasticsearch 6.0 以后，打算彻底移除 Type （这个 `_type`）

参考一：[Removal of Mapping Types](https://www.elastic.co/blog/elasticsearch-6-0-0-alpha1-released)

参考二：[Indices, types, and parent / child: current status and upcoming changes in Elasticsearch](https://www.elastic.co/blog/index-type-parent-child-join-now-future-in-elasticsearch)

`Types` 将被删除。因为之前的 `Parent/Child`与 `Types` 是紧密耦合的，因此需要修改。

添加新的功能，`"typeless parent/child fields" called "join fields"`。

参考 Relates [\#24317](https://github.com/elastic/elasticsearch/pull/24317)

