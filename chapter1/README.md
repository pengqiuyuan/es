# 集群的部署

* [x] 使用分布式配置管理工具`ansible`来做集群的部署

集群的初始部署，配置批量更改，集群版本升级，重启故障结点（快捷和安全）

如果ES集群规模比较大，那么部署ES实例将会成为一个比较繁琐和麻烦的事情，如果后期涉及到集群的参数修改或者调优，那么修改配置文件也将是一个头疼的问题

官方提供了三个工具：`Puppet`、`Chef`和`ansible`

`Ubuntu 16.04`

```text
[vpn]
node01 vpn_ip=10.0.0.1 ansible_host=77.222.52.211
node02 vpn_ip=10.0.0.2 ansible_host=77.222.52.212
node03 vpn_ip=10.0.0.3 ansible_host=77.222.52.213
node04 vpn_ip=10.0.0.4 ansible_host=77.222.52.214
node05 vpn_ip=10.0.0.5 ansible_host=77.222.52.215
node06 vpn_ip=10.0.0.6 ansible_host=77.222.52.216
node07 vpn_ip=10.0.0.7 ansible_host=77.222.52.217
node08 vpn_ip=10.0.0.8 ansible_host=77.222.52.218
node09 vpn_ip=10.0.0.9 ansible_host=77.222.52.219
node10 vpn_ip=10.0.0.10 ansible_host=77.222.52.220
node11 vpn_ip=10.0.0.11 ansible_host=77.222.52.221
node12 vpn_ip=10.0.0.12 ansible_host=77.222.52.222
node13 vpn_ip=10.0.0.13 ansible_host=77.222.52.223
node14 vpn_ip=10.0.0.14 ansible_host=77.222.52.224
node15 vpn_ip=10.0.0.15 ansible_host=77.222.52.225


[removevpn]

[elasticsearch_master_nodes]

[elasticsearch_master_data_nodes]
node03
node04
node05

[elasticsearch_data_nodes]
node06
node07
node08
node09
node10
node11
node12
node13
node14
node15

[elasticsearch_client_nodes]
node01
node02
```

在`node01 10.0.0.1`上安装`ansible`

```text
$ sudo apt-get install software-properties-common
$ sudo apt-add-repository ppa:ansible/ansible
$ sudo apt-get update
$ sudo apt-get install ansible
```

安装`git`

```text
$ sudo apt-get install git
```

克隆`ansible-tinc-elasticsearch`此项目`hosts、platbook`文件已配置好，已下是解释：

```text
$ git clone https://github.com/thisismitch/ansible-tinc-elasticsearch.git
```

项目在`/home/idatage`下，`/home/idatage/ansible-tinc-elasticsearch/hosts`文件：

```text
cd /home/idatage/ansible-tinc-elasticsearch
vi ./hosts
```

保存`hosts`，十五台机器`vpn_ip`为内网`ip`，`ansible_host`为公网`ip`，`hosts`文件修改完后记得执行

`ansible-playbook -s site.yml`

`ansible`配置私钥用来免密码登录：

```text
sudo ssh-keygen   #非root用户使用，ssh-keygen
ssh-copy-id idatage@77.222.52.211
ssh-copy-id idatage@77.222.52.212
ssh-copy-id idatage@77.222.52.213
ssh-copy-id idatage@77.222.52.214
ssh-copy-id idatage@77.222.52.215
ssh-copy-id idatage@77.222.52.216
ssh-copy-id idatage@77.222.52.217
ssh-copy-id idatage@77.222.52.218
ssh-copy-id idatage@77.222.52.219
ssh-copy-id idatage@77.222.52.220
ssh-copy-id idatage@77.222.52.221
ssh-copy-id idatage@77.222.52.222
ssh-copy-id idatage@77.222.52.223
ssh-copy-id idatage@77.222.52.224
ssh-copy-id idatage@77.222.52.225
```

执行命令`ansible all -m ping`结果如下：

```text
$ ansible all -m ping
node02 | SUCCESS => {
"changed": false,
"ping": "pong"
}
node01 | SUCCESS => {
"changed": false,
"ping": "pong"
}
node03 | SUCCESS => {
"changed": false,
"ping": "pong"
}
```

`sity.yml`文件

```text
---

- hosts: vpn
  become: yes
  roles:
    - tinc

- hosts: removevpn
  become: yes
  roles:
    - tinc-remove
```

执行命令`ansible-playbook -s site.yml`成功结果：

```text
PLAY RECAP *********************************************************************
node01 : ok=18 changed=15 unreachable=0 failed=0
node02 : ok=18 changed=15 unreachable=0 failed=0
node03 : ok=18 changed=15 unreachable=0 failed=0
```

安装`ansible`的主机`1`执行如下命令，`-s su`权限，修改系统配置（`System`配置后面介绍），

`/home/idatage/ansible-tinc-elasticsearch`

```text
ansible all -s -m raw -a '
grep "* - nofile 512000" /etc/security/limits.conf || echo "* - nofile 512000" >> /etc/security/limits.conf
grep "elasticsearch - nproc unlimited" /etc/security/limits.conf || echo "elasticsearch - nproc unlimited" >> /etc/security/limits.conf
grep "fs.file-max = 1024000" /etc/sysctl.conf || echo "fs.file-max = 1024000" >> /etc/sysctl.conf
grep "vm.max_map_count = 262144" /etc/sysctl.conf || echo "vm.max_map_count = 262144" >> /etc/sysctl.conf
grep "vm.swappiness = 1" /etc/sysctl.conf || echo "vm.swappiness = 1" >> /etc/sysctl.conf #禁用 swapping
sysctl -p'
```

成功如下：

```text
$ ansible all -s -m raw -a '
> grep "* - nofile 512000" /etc/security/limits.conf || echo "* - nofile 512000" >> /etc/security/limits.conf
> grep "elasticsearch - nproc unlimited" /etc/security/limits.conf || echo "elasticsearch - nproc unlimited" >> /etc/security/limits.conf
> grep "fs.file-max = 1024000" /etc/sysctl.conf || echo "fs.file-max = 1024000" >> /etc/sysctl.conf
> grep "vm.max_map_count = 262144" /etc/sysctl.conf || echo "vm.max_map_count = 262144" >> /etc/sysctl.conf
> grep "vm.swappiness = 1" /etc/sysctl.conf || echo "vm.swappiness = 1" >> /etc/sysctl.conf #禁用 swapping
> sysctl -p'
node01 | SUCCESS | rc=0 >>
* - nofile 512000
elasticsearch - nproc unlimited
fs.file-max = 1024000
vm.max_map_count = 262144
vm.swappiness = 1
vm.swappiness = 0
net.ipv4.neigh.default.gc_stale_time = 120
net.ipv4.conf.all.rp_filter = 0
net.ipv4.conf.default.rp_filter = 0
net.ipv4.conf.default.arp_announce = 2
net.ipv4.conf.lo.arp_announce = 2
net.ipv4.conf.all.arp_announce = 2
net.ipv4.tcp_max_tw_buckets = 5000
net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_max_syn_backlog = 1024
net.ipv4.tcp_synack_retries = 2
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1
fs.file-max = 1024000
vm.max_map_count = 262144
vm.swappiness = 1
Shared connection to 10.0.0.1 closed.
```

`elasticsearch.yml`文件，`ansible playbook`用来完成集群的初始部署、配置

```javascript
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
        gateway.expected_nodes: 15,
        gateway.recover_after_nodes: 15,
        action.destructive_requires_name: true,
        indices.breaker.total.limit: 70%,
        indices.breaker.fielddata.limit: 24%,
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
    es_version: "5.4.0"
    es_heap_size: "4g"
    es_api_port: 9222
    es_max_map_count: 262144
    es_max_open_files: 512000   
    es_pid_dir: "/mnt/run/elasticsearch"
    es_data_dirs: "/mnt/lib/elasticsearch"
    es_log_dir: "/mnt/log/elasticsearch"
#    es_enable_xpack: true
#    es_xpack_license: "{{ lookup('file', '/tmp/peng-qiuyuan-a8b6beab-10ff-480f-9eff-7295efd58242-v5.json')  }}"
#    es_xpack_features:
#      - monitoring

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
        gateway.expected_nodes: 15,
        gateway.recover_after_nodes: 15,
        action.destructive_requires_name: true,
        indices.breaker.total.limit: 70%,
        indices.breaker.fielddata.limit: 24%,
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
    es_version: "5.4.0"
    es_heap_size: "16g"
    es_api_port: 9222
    es_max_map_count: 262144
    es_max_open_files: 512000
    es_pid_dir: "/mnt/run/elasticsearch"
    es_data_dirs: "/mnt/lib/elasticsearch"
    es_log_dir: "/mnt/log/elasticsearch"
#    es_enable_xpack: true
#    es_xpack_license: "{{ lookup('file', '/tmp/peng-qiuyuan-a8b6beab-10ff-480f-9eff-7295efd58242-v5.json')  }}"
#    es_xpack_features:
#      - monitoring

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
        gateway.expected_nodes: 15,
        gateway.recover_after_nodes: 15,
        action.destructive_requires_name: true,
        indices.breaker.total.limit: 70%,
        indices.breaker.fielddata.limit: 24%,
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
    es_version: "5.4.0"
    es_heap_size: "16g"
    es_api_port: 9222
    es_max_map_count: 262144
    es_max_open_files: 512000
    es_pid_dir: "/mnt/run/elasticsearch"
    es_data_dirs: "/mnt/lib/elasticsearch"
    es_log_dir: "/mnt/log/elasticsearch"
#    es_enable_xpack: true
#    es_xpack_license: "{{ lookup('file', '/tmp/peng-qiuyuan-a8b6beab-10ff-480f-9eff-7295efd58242-v5.json')  }}"
#    es_xpack_features:
#      - monitoring

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
    gateway.expected_nodes: 15,
        gateway.recover_after_nodes: 15,
        action.destructive_requires_name: true,
        indices.breaker.total.limit: 70%,
        indices.breaker.fielddata.limit: 24%,
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
    es_version: "5.4.0"
    es_heap_size: "16g"
    es_api_port: 9222
    es_max_map_count: 262144
    es_max_open_files: 512000
    es_pid_dir: "/mnt/run/elasticsearch"
    es_data_dirs: "/mnt/lib/elasticsearch"
    es_log_dir: "/mnt/log/elasticsearch"
#    es_enable_xpack: true
#    es_xpack_license: "{{ lookup('file', '/tmp/peng-qiuyuan-a8b6beab-10ff-480f-9eff-7295efd58242-v5.json')  }}"
#    es_xpack_features:
#      - monitoring
```

执行`ansible-playbook elasticsearch.yml`，成功如下：

```text
TASK [elasticsearch : Update Native Roles] *************************************

PLAY RECAP *********************************************************************
node01 : ok=48 changed=0 unreachable=0 failed=0
node02 : ok=49 changed=7 unreachable=0 failed=0
node03 : ok=46 changed=1 unreachable=0 failed=0
```

`elasticsearch`实例的`restart、start、stop`，`node_elasticsearch.service`中的`node`为上面`playbook`中定义的名称

`es_instance_name: "node"`

```text
systemctl restart node_elasticsearch.service
systemctl start node_elasticsearch.service
systemctl stop node_elasticsearch.service
systemctl status node_elasticsearch.service
```

```text
service node_elasticsearch restart
service node_elasticsearch start
service node_elasticsearch stop
service node_elasticsearch status
```

