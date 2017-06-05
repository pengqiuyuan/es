安装 `xpack 5.4.0`

集群第一次安装 xpack 需要执行完全群集重新启动。升级时, 通常可以执行滚动升级。

执行全集群重启升级的过程如下：

1. **停止** `logstash indexer` **端，停止数据写入 **`es`

   ```js
   sudo docker-compose stop
   ```

2. **禁用分片分配**

   当你关闭一个节点时，分配进程在等待一分钟之后开始将此节点上的分片复制到其它节点中，会造成很多浪费的I/O。这可以在节点关闭前通过禁用分片分配来避免：

   ```js
   curl -XPUT http://127.0.0.1:9222/_cluster/settings -d '{
     "transient" : {
       "cluster.routing.allocation.enable" : "none"
     }
   }'

   curl -XGET http://127.0.0.1:9222/_cluster/settings?pretty
   ```

3. **执行同步冲刷**

   你可以愉快地继续索引在升级。但是，如果你临时地关闭一些非不要的索引库以及执行一次[同步冲刷](../../Indices_APIs/Flush/Synced_Flush.md)请求可以帮助你快速恢复分片：

   ```js
   curl -XPOST http://127.0.0.1:9222/_flush/synced?pretty
   ```

   同步冲刷请求是一个”尽力而为“的操作。它可能会因为一些正在进行的索引操作而失败，但是如果有必要你可以反复的执行它，这是安全的。

4. **停止所有节点**

   在集群的所有节点上停掉 Elasticsearch 服务。

   ```js
   ansible all -s -m raw -a 'service node_elasticsearch stop'
   ```

5. **安装 xpack 插件**

   ```js
   #在node01（安装ansible的机器）上执行

   ansible all -s -m raw -a 'mkdir /home/idatage/download && mkdir /home/idatage/plugins'

   # copy x-pack-5.4.0.zip 到每一台待安装的机器

   ansible all -s -m copy -a 'src=/home/idatage/download/x-pack-5.4.0.zip dest=/home/idatage/download/x-pack-5.4.0.zip'

   #修改 /usr/share/elasticsearch/bin/elasticsearch-plugin ansible安装es节点为ES_ENV_FILE="/etc/default/node_elasticsearch"

   ansible all -s -m copy -a 'src=/usr/share/elasticsearch/bin/elasticsearch-plugin dest=/usr/share/elasticsearch/bin/elasticsearch-plugin'

   #ssh 的方式登录每一台机器安装 xpack

   sudo /usr/share/elasticsearch/bin/elasticsearch-plugin install file:///home/idatage/download/x-pack-5.4.0.zip

   #在node01（安装ansible的机器）上执行，特殊：替换自己编译的 x-pack-5.4.0.jar

   ansible all -s -m copy -a 'src=/home/idatage/plugins/x-pack-5.4.0.jar dest=/usr/share/elasticsearch/plugins/x-pack/x-pack-5.4.0.jar'
   ```

6. **启动集群**

   如果你有专门的master节点（在节点配置中设置`node.master`为`true`且`node.data`为`false`），先启动他们是一个好的主意。在处理数据节点之前等待它们形成一个集群并选举出一个主节点。你可以通过查看日志来检查进度。

   一旦对方发现了[最小的主节点数](../../Modules/Discovery/Zen_Discovery.md#master-election)，它们将在集群中选举主节点。从这时开始，就可以使用[\_cat/health](../../cat_APIs/cat_health.md)与[\_cat/nodes](../../cat_APIs/cat_nodes.md)API来监控节点加入集群：

   ```js
   # 先启动 master node

   ansible node03,node04,node05 -s -m raw -a 'service node_elasticsearch start'

   # 再启动 data node

   ansible node01,node02,node06,node07,node08,node09,node10,node11,node12,node13,node14,node15 -s -m raw -a 'service node_elasticsearch start'

   #查看集群状态

   curl -u elastic:changeme -XGET http://127.0.0.1:9222/_cat/health?v

   #查看节点

   curl -u elastic:changeme -XGET http://127.0.0.1:9222/_cat/nodes?v

   #查看 _xpack 的 license 为 trial

   curl -XGET -u elastic:changeme 'http://127.0.0.1:9222/_xpack/license'

   #更新 _xpack 的 license

   curl -XPUT -u elastic:changeme 'http://127.0.0.1:9222/_xpack/license' -d '
   {
     "license" : {
       "uid" : "9fa06f95-cc9b-480c-a11d-c7dd01c6ebcd",
       "type" : "platinum",
       "issue_date_in_millis" : 1483689705479,
       "expiry_date_in_millis" : 3580889705000,
       "max_nodes" : 1000,
       "issued_to" : "app-es",
       "issuer" : "ice leng",
       "signature" : "AAAAAgAAAA3wtFyCv7w82WuX+xfEAAABmC9ZN0hjZDBGYnVyRXpCOW5Bb3FjZDAxOWpSbTVoMVZwUzRxVk1PSmkxaktJRVl5MUYvUWh3bHZVUTllbXNPbzBUemtnbWpBbmlWRmRZb25KNFlBR2x0TXc2K2p1Y1VtMG1UQU9TRGZVSGRwaEJGUjE3bXd3LzRqZ05iLzRteWFNekdxRGpIYlFwYkJiNUs0U1hTVlJKNVlXekMrSlVUdFIvV0FNeWdOYnlESDc3MWhlY3hSQmdKSjJ2ZTcvYlBFOHhPQlV3ZHdDQ0tHcG5uOElCaDJ4K1hob29xSG85N0kvTWV3THhlQk9NL01VMFRjNDZpZEVXeUtUMXIyMlIveFpJUkk2WUdveEZaME9XWitGUi9WNTZVQW1FMG1DenhZU0ZmeXlZakVEMjZFT2NvOWxpZGlqVmlHNC8rWVVUYzMwRGVySHpIdURzKzFiRDl4TmM1TUp2VTBOUlJZUlAyV0ZVL2kvVk10L0NsbXNFYVZwT3NSU082dFNNa2prQ0ZsclZ4NTltbU1CVE5lR09Bck93V2J1Y3c9PQAAAQCYj3myHoaDvxR/jzfmPSlCcnnUdcf91IrmHc2vkI8vYcy5yJ3f/aedNKRihwIpJ7uy0CDDZEclKhM9cQroDL80nmAX398LPQS96vDtrNBKtkGLJcQObVnkQG/ZG9FyLWZbFaFw4WYYAi+wY1USj0psVd6izr93DlWh0YQtd1rfIW/rAmkt9lgHegAbpMfhq2aVb1ESiZdhNBWtWz0AuYD8ED14idjuyl78N87azxj6RsGyH/v3BP9ObHmsjcA0TEeq1+ehvqFykmAppnx+EOtgjEiqxDTNsctPfoMaBpovFxSJDV49uA9JGYRbVOqk8UC3fdwurKVGa6uV1LlrP7Ij"
     }
   }'

   #修改 elastic 初始密码

   curl -XPUT -u elastic '127.0.0.1:9222/_xpack/security/user/elastic/_password' -d '{
     "password" : "自己的密码"
   }'
   ```

   ```
   使用这些API来检查所有节点已经成功地加入到集群。
   ```

7. **等待状态**`yellow`

   一旦节点加入了集群，他将开始恢复本地存储的分片数据。刚开始[\_cat/health](../../cat_APIs/cat_health.md)会返回`status`为`red`，这表示还有主分片未分配完成。

   一旦本地存储的分片恢复完成，`status`将会变成`yellow`，这表示所有主分片已恢复，但是副本分片没有分配。这是我们预料到的，因为分片分配被我们之前禁用了。

8. **重新打开分片分配**

   延迟副本分片的分配，直到所有节点都加入了集群且完成了本地分片数据的分配。从这时开始，所有节点都已在集群中，重新打开分片分配是安全的：

   ```js
    PUT _cluster/settings
    {
      "transient": {
        "cluster.routing.allocation.enable": "all"
      }
    }
   ```

   集群将开始分片副本到所有的数据节点。这是你可以安全的开始新增索引与执行搜索操作，但是如果你在分片恢复之前延迟这些操作将会使得恢复过程变得更快。

   你可以使用[\_cat/health](../../cat_APIs/cat_health.md)与[\_cat/revocery](../../cat_APIs/cat_recovery.md)API来监控进度：

   ```js
   curl -u 用户名:密码 -XGET http://127.0.0.1:9222/_cat/health?pretty

   curl -u 用户名:密码 -XGET http://127.0.0.1:9222/_cat/nodes?pretty

   本地查询

   curl -i 用户名:密码@127.0.0.1:9200/weibo/_cat/nodes?pretty
   ```

   一旦`_cat/health`输出的`status`列变成`green`，所有主分片与副本分片都成功分配完成。



