```
ansible all -s -m raw -a 'service node_elasticsearch stop'

ansible node15 -s -m raw -a 'tail -50 /mnt/log/elasticsearch/node*-node/tarantula.log'
```



