11

```
安装（ ssh node* 手动一台一台安装）

ansible all -s -m raw -a 'mkdir /home/idatage/download && mkdir /home/idatage/plugins'

ansible all -s -m copy -a 'src=/home/idatage/download/x-pack-5.3.0.zip dest=/home/idatage/download/x-pack-5.3.0.zip'

修改 /usr/share/elasticsearch/bin/elasticsearch-plugin
ansible all -s -m copy -a 'src=/usr/share/elasticsearch/bin/elasticsearch-plugin dest=/usr/share/elasticsearch/bin/elasticsearch-plugin'

/usr/share/elasticsearch/bin/elasticsearch-plugin install file:///home/dev/idatage/x-pack-5.4.0.zip

特殊：删除原来的 x-pack-5.4.0.jar
ansible all -s -m raw -a 'rm -rf /usr/share/elasticsearch/plugins/x-pack/x-pack-5.4.0.jar'
ansible all -s -m raw -a 'ls /usr/share/elasticsearch/plugins/x-pack/'

特殊：替换自己编译的 x-pack-5.4.0.jar
ansible all -s -m copy -a 'src=/home/idatage/licenseVerifier/x-pack-5.4.0.jar dest=/usr/share/elasticsearch/plugins/x-pack/x-pack-5.4.0.jar'
启动（测试环境）
```



