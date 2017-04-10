版本升级

1、自动升级集群

修改`ansible` `playbook`中 `es_version: "5.2.2"` =&gt; `es_version: "5.3.0"`，集群升级

执行 `ansible-playbook -s elasticsearch.yml`

2、手动升级 

利用 `ansible all -s -m raw ''`

```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.3.0.deb
sha1sum elasticsearch-5.3.0.deb 
sudo dpkg -i elasticsearch-5.3.0.deb
```



