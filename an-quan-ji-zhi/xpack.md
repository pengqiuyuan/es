```
ansible all -s -m copy -a 'src=/home/idatage/plugins/peng-qiuyuan-a8b6beab-10ff-480f-9eff-7295efd58242-v5.json dest=/tmp/peng-qiuyuan-a8b6beab-10ff-480f-9eff-7295efd58242-v5.json'
ansible all -s -m raw -a 'ls /tmp'
```

`x-pack`

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



