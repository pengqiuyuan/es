版本升级

1、自动升级集群

备份

```
ansible all -s -m raw -a 'cp -r /usr/share/elasticsearch /usr/share/elasticsearch5.3.0'
ansible all -s -m raw -a 'ls /usr/share/'
```

修改`ansible` `playbook`中 `es_version: "5.3.0"` =&gt; `es_version: "5.4.0"`，集群升级

执行 `ansible-playbook -s elasticsearch.yml`

升级`es`

```
mkdir download && cd /home/idatage/download

wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.4.0.deb
sha1sum elasticsearch-5.4.0.deb
sudo dpkg -i elasticsearch-5.4.0.deb

ansible all -s -m raw -a 'mkdir /home/idatage/download'
ansible all -s -m copy -a 'src=/home/idatage/download/elasticsearch-5.4.0.deb dest=/home/idatage/download/elasticsearch-5.4.0.deb'
ansible all -s -m raw -a 'sha1sum /home/idatage/download/elasticsearch-5.4.0.deb'
ansible all -s -m raw -a 'sudo dpkg -i /home/idatage/download/elasticsearch-5.4.0.deb'
```

升级 `ik`

```
移除之前手动安装的 ik v5.3.0
ansible all -s -m raw -a 'rm -rf /usr/share/elasticsearch/plugins/ik'
本地打包修改过得 ik v5.4.0，上传服务器
```

```
ansible all -s -m copy -a 'src=/home/idatage/plugins/elasticsearch-analysis-ik-5.4.0.zip dest=/usr/share/elasticsearch/elasticsearch-analysis-ik-5.4.0.zip'
ansible all -s -m raw -a 'ls /usr/share/elasticsearch'
ansible all -s -m raw -a 'apt-get install unzip'
ansible all -s -m raw -a 'unzip /usr/share/elasticsearch/elasticsearch-analysis-ik-5.4.0.zip -d /usr/share/elasticsearch/plugins/ik'
ansible all -s -m raw -a 'ls /usr/share/elasticsearch/plugins/ik'
```

升级 `xpack`

```
先移除
ansible all -s -m raw -a '/usr/share/elasticsearch/bin/elasticsearch-plugin remove x-pack'

安装（ ssh node* 手动一台一台安装）
ansible all -s -m copy -a 'src=/home/idatage/download/x-pack-5.4.0.zip dest=/home/idatage/download/x-pack-5.4.0.zip'
/usr/share/elasticsearch/bin/elasticsearch-plugin install file:///home/dev/download/x-pack-5.4.0.zip

特殊：删除原来的 x-pack-5.4.0.jar
ansible all -s -m raw -a 'rm -rf /usr/share/elasticsearch/plugins/x-pack/x-pack-5.4.0.jar'
ansible all -s -m raw -a 'ls /usr/share/elasticsearch/plugins/x-pack/'

特殊：替换自己编译的 x-pack-5.4.0.jar
ansible all -s -m copy -a 'src=/home/idatage/licenseVerifier/x-pack-5.4.0.jar dest=/usr/share/elasticsearch/plugins/x-pack/x-pack-5.4.0.jar'
```

启动（测试环境）

```
ansible all -s -m raw -a 'service node_elasticsearch start'

查看日志
ansible all -s -m raw -a 'tail -100 /mnt/log/elasticsearch/*/test.log'
```

升级 `kibana`

```
先移除
/usr/share/kibana/bin/kibana-plugin remove x-pack

安装
/usr/share/kibana/bin/kibana-plugin install file:///home/idatage/download/x-pack-5.4.0.zip
```

2、手动升级

利用 `ansible all -s -m raw ''`

```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.3.0.deb
sha1sum elasticsearch-5.3.0.deb 
sudo dpkg -i elasticsearch-5.3.0.deb
```



