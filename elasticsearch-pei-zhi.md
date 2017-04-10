`Elasticsearch`配置 ，`ansible` 管理

`master` 节点

```
- hosts: elasticsearch_master_nodes
  become: yes
  roles:
    - { role: elasticsearch, es_instance_name: "node",
    es_config: {
        cluster.name: "tarantula",
        discovery.zen.ping.unicast.hosts: "node01, node02, node03,node04,node05,node06,node07,node08,node09,node10,node11,node12,node13,node14,node15", 
        network.host: "_eth0_, _local_",
        http.port: 9222,
        transport.tcp.port: 9333,
        node.data: false,
        node.master: true,
        bootstrap.memory_lock: true,
        discovery.zen.minimum_master_nodes: 2,
        gateway.recover_after_nodes: 2,
        action.destructive_requires_name: true,
        indices.breaker.total.limit: 70%,
        indices.breaker.fielddata.limit: 25%,
        indices.breaker.request.limit: 40%,
        indices.fielddata.cache.size: 20%,
        indices.queries.cache.size: 40%,
        indices.memory.index_buffer_size: 10%
        }
    }
  vars:
    es_templates: false
    es_scripts: true
    es_java_install: true
    es_major_version: "5.x"
    es_version: "5.3.0"
    es_heap_size: "4g"
    es_api_port: 9222
    es_max_map_count: 262144
    es_max_open_files: 512000   
    es_pid_dir: "/mnt/run/elasticsearch"
    es_data_dirs: "/mnt/lib/elasticsearch"
    es_log_dir: "/mnt/log/elasticsearch"
```

`master` && `data` 节点

```
- hosts: elasticsearch_master_data_nodes
  become: yes
  roles:
    - { role: elasticsearch, es_instance_name: "node",
    es_config: {
        cluster.name: "tarantula",
        discovery.zen.ping.unicast.hosts: "node01, node02, node03,node04,node05,node06,node07,node08,node09,node10,node11,node12,node13,node14,node15",
        network.host: "_eth0_, _local_",
        http.port: 9222,
        transport.tcp.port: 9333,
        node.data: true,
        node.master: true,
        bootstrap.memory_lock: true,
        discovery.zen.minimum_master_nodes: 2,
        gateway.recover_after_nodes: 2,
        action.destructive_requires_name: true,
        indices.breaker.total.limit: 70%,
        indices.breaker.fielddata.limit: 25%,
        indices.breaker.request.limit: 40%,
        indices.fielddata.cache.size: 20%,
        indices.queries.cache.size: 40%,
        indices.memory.index_buffer_size: 10%
        }
    }
  vars:
    es_templates: false
    es_scripts: true
    es_java_install: true
    es_major_version: "5.x"
    es_version: "5.3.0"
    es_heap_size: "16g"
    es_api_port: 9222
    es_max_map_count: 262144
    es_max_open_files: 512000
    es_pid_dir: "/mnt/run/elasticsearch"
    es_data_dirs: "/mnt/lib/elasticsearch"
    es_log_dir: "/mnt/log/elasticsearch"
```

`date` 节点

```
- hosts: elasticsearch_data_nodes
  become: yes
  roles:
    - { role: elasticsearch, es_instance_name: "node",
    es_config: {
        cluster.name: "tarantula",
        discovery.zen.ping.unicast.hosts: "node01, node02, node03,node04,node05,node06,node07,node08,node09,node10,node11,node12,node13,node14,node15",
        network.host: "_eth0_, _local_",
        http.port: 9222,
        transport.tcp.port: 9333,
        node.data: true,
        node.master: false,
        bootstrap.memory_lock: true,
        discovery.zen.minimum_master_nodes: 2,
        gateway.recover_after_nodes: 2,
        action.destructive_requires_name: true,
        indices.breaker.total.limit: 70%,
        indices.breaker.fielddata.limit: 25%,
        indices.breaker.request.limit: 40%,
        indices.fielddata.cache.size: 20%,
        indices.queries.cache.size: 40%,
        indices.memory.index_buffer_size: 10%
        } 
    }
  vars:
    es_templates: false
    es_scripts: true
    es_java_install: true
    es_major_version: "5.x"
    es_version: "5.3.0"
    es_heap_size: "16g"
    es_api_port: 9222
    es_max_map_count: 262144
    es_max_open_files: 512000
    es_pid_dir: "/mnt/run/elasticsearch"
    es_data_dirs: "/mnt/lib/elasticsearch"
    es_log_dir: "/mnt/log/elasticsearch"
```

`client` 节点

```
- hosts: elasticsearch_client_nodes
  become: yes
  roles:
    - { role: elasticsearch, es_instance_name: "node",
    es_config: {
        cluster.name: "tarantula",
        discovery.zen.ping.unicast.hosts: "node01, node02, node03,node04,node05,node06,node07,node08,node09,node10,node11,node12,node13,node14,node15",        
        network.host: "_eth0_, _local_",
        http.port: 9222,
        transport.tcp.port: 9333,
        node.data: false,
        node.master: false,
        bootstrap.memory_lock: true,
        discovery.zen.minimum_master_nodes: 2,
        gateway.recover_after_nodes: 2,
        action.destructive_requires_name: true,
        indices.breaker.total.limit: 70%,
        indices.breaker.fielddata.limit: 25%,
        indices.breaker.request.limit: 40%,
        indices.fielddata.cache.size: 20%,
        indices.queries.cache.size: 40%,
        indices.memory.index_buffer_size: 10%
        } 
    }
  vars:
    es_templates: false
    es_scripts: true
    es_java_install: false
    es_major_version: "5.x"
    es_version: "5.3.0"
    es_heap_size: "16g"
    es_api_port: 9222
    es_max_map_count: 262144
    es_max_open_files: 512000
    es_pid_dir: "/mnt/run/elasticsearch"
    es_data_dirs: "/mnt/lib/elasticsearch"
    es_log_dir: "/mnt/log/elasticsearch"
```



