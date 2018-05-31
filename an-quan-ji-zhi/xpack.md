```
ansible all -s -m copy -a 'src=/home/idatage/plugins/peng-qiuyuan-a8b6beab-10ff-480f-9eff-7295efd58242-v5.json dest=/tmp/peng-qiuyuan-a8b6beab-10ff-480f-9eff-7295efd58242-v5.json'
ansible all -s -m raw -a 'ls /tmp'
```

[反编译工具](https://github.com/deathmarine/Luyten)：本地打包 `mvn clean install`

`x-pack`重新编译 `LicenseVerifier.java`，`license`验证永远返回 `true`

```
package org.elasticsearch.license;

public class LicenseVerifier
{
    public static boolean verifyLicense(final License license, final byte[] encryptedPublicKeyData) {
        return true;
    }

    public static boolean verifyLicense(final License license) {
        return true;
    }
}
```

本地编译

```
javac -encoding UTF-8 -cp ./x-pack-5.3.0.jar  LicenseVerifier.java
```

本地替换 `LicenseVerifier.class`、打包

```
jar cvf x-pack-5.3.0.jar .
```

上传替换 `es`  的 `x-pack-5.3.0.jar`

```
scp ./x-pack-5.3.0.jar root@127.0.0.1:/root/licenseVerifier
```

`ansible`目录 `/home/dev/ansible-tinc-elasticsearch`

```
ansible all -s -m copy -a 'src=/root/licenseVerifier/x-pack-5.3.0.jar dest=/usr/share/elasticsearch/plugins/x-pack/x-pack-5.3.0.jar'
```

重启集群

```
ansible all -s -m raw -a 'service node_elasticsearch restart'

ansible all -s -m raw -a 'tail -100 /mnt/log/elasticsearch/*/test.log'
```

```
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
```

```
curl -XGET -u elastic:changeme 'http://127.0.0.1:9222/_xpack/license'
```

卸载

```
/usr/share/elasticsearch/bin/elasticsearch-plugin remove x-pack

/usr/share/kibana/bin/kibana-plugin remove x-pack

ansible all -s -m raw -a '/usr/share/elasticsearch/bin/elasticsearch-plugin remove x-pack'
```

安装

```
/usr/share/elasticsearch/bin/elasticsearch-plugin install file:///root/x-pack-5.3.0.zip

/usr/share/kibana/bin/kibana-plugin install file:///root/x-pack-5.3.0.zip
```



