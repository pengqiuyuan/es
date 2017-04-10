`elasticsearch-analysis-ik` 分词

`medcl：https://github.com/medcl/elasticsearch-analysis-ik`

`oopsdata: https://github.com/OopsData/elasticsearch-analysis-ik`

源代码

```
if(ub == Character.UnicodeBlock.CJK_UNIFIED_IDEOGRAPHS  
                    || ub == Character.UnicodeBlock.CJK_COMPATIBILITY_IDEOGRAPHS  
                    || ub == Character.UnicodeBlock.CJK_UNIFIED_IDEOGRAPHS_EXTENSION_A){
                              //目前已知的中文字符UTF-8集合
                              return CHAR_CHINESE;
}
```

更新代码

`https://github.com/OopsData/elasticsearch-analysis-ik/commit/356b3eebdec3e617b392ca4a842cf422054920b1`

```
if (ub == Character.UnicodeBlock.CJK_UNIFIED_IDEOGRAPHS || ub == Character.UnicodeBlock.BASIC_LATIN
                    || ub == Character.UnicodeBlock.CJK_COMPATIBILITY_IDEOGRAPHS
                    || ub == Character.UnicodeBlock.CJK_UNIFIED_IDEOGRAPHS_EXTENSION_A
                    || ub == Character.UnicodeBlock.GENERAL_PUNCTUATION
                    || ub == Character.UnicodeBlock.CJK_SYMBOLS_AND_PUNCTUATION
                    || ub == Character.UnicodeBlock.HALFWIDTH_AND_FULLWIDTH_FORMS) {
                //目前已知的中文字符UTF-8集合
                return CHAR_CHINESE;

            }
```

打包

```
git clone https://github.com/OopsData/elasticsearch-analysis-ik
git pull
git checkout tags/v5.3.0
mvn package
```

`target` 目录下的`zip`文件就是我们需要的

copy and unzip`target/releases/elasticsearch-analysis-ik-{version}.zip 到 your-es-root/plugins/ik`

集群手动安装`ik`插件

上传到安装`ansible` 的`client`节点`scp ./elasticsearch-analysis-ik-5.3.0.zip idatage@10.0.0.1:/home/idatage/plugins`

```
ansible all -s -m copy -a 'src=/home/idatage/plugins/elasticsearch-analysis-ik-5.3.0.zip dest=/usr/share/elasticsearch/elasticsearch-analysis-ik-5.3.0.zip'
ansible all -s -m raw -a 'ls /usr/share/elasticsearch'
ansible all -s -m raw -a 'apt-get install unzip'
ansible all -s -m raw -a 'unzip /usr/share/elasticsearch/elasticsearch-analysis-ik-5.3.0.zip -d /usr/share/elasticsearch/plugins/ik'
ansible all -s -m raw -a 'ls /usr/share/elasticsearch/plugins/ik'
```

之后重启新安装`ik`的节点

`elasticsearch`实例的`restart、start、stop`，`node_elasticsearch.service`中的`node`为`ansible playbook`中定义的名称`es_instance_name: "node"`

```
systemctl restart node_elasticsearch.service
systemctl start node_elasticsearch.service
systemctl stop node_elasticsearch.service
systemctl status node_elasticsearch.service
```

或者

```
service node_elasticsearch restart
service node_elasticsearch start
service node_elasticsearch stop
service node_elasticsearch status
```

分词的验证

```
curl -XPOST 'http://localhost:9222/weixiners/_analyze?analyzer=ik_max_word&text=%e4%b8%ad%e5%8d%8e%e4%ba%ba%e6%b0%91%e5%85%b1%e5%92%8c%e5%9b%bd%e5%9b%bd%e6%ad%8c&pretty'
```

```
curl -XPOST 'http://localhost:9222/weixiners/_analyze?analyzer=ik_smart&text=%e4%b8%ad%e5%8d%8e%e4%ba%ba%e6%b0%91%e5%85%b1%e5%92%8c%e5%9b%bd%e5%9b%bd%e6%ad%8c&pretty'
```



