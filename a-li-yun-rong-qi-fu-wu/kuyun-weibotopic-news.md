# kuyun-weiboTopic-news

appCM

```text
ifengapp:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/news:latest'
  entrypoint:
    - node
    - startcm.js
    - '--name=ifeng_app'
  restart: always
  environment:
    - NODE_PREFIX=/usr/local
    - NODE_SOURCE=/usr/src/node
    - BASE_APKS=bash libgcc libstdc++ openssl ca-certificates
    - BUILD_APKS=git curl wget bzip2 tar make gcc clang g++ python linux-headers paxctl binutils-gold autoconf bison zlib-dev openssl-dev
    - NODE_CONFIG_FLAGS=--shared-openssl
  labels:
    aliyun.scale: '1'
ifengsite:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/news:latest'
  entrypoint:
    - node
    - startcm.js
    - '--name=ifeng_site'
  restart: always
  environment:
    - NODE_PREFIX=/usr/local
    - NODE_SOURCE=/usr/src/node
    - BASE_APKS=bash libgcc libstdc++ openssl ca-certificates
    - BUILD_APKS=git curl wget bzip2 tar make gcc clang g++ python linux-headers paxctl binutils-gold autoconf bison zlib-dev openssl-dev
    - NODE_CONFIG_FLAGS=--shared-openssl
  labels:
    aliyun.scale: '1'
neteasesite:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/news:latest'
  entrypoint:
    - node
    - startcm.js
    - '--name=netease_site'
  restart: always
  environment:
    - NODE_PREFIX=/usr/local
    - NODE_SOURCE=/usr/src/node
    - BASE_APKS=bash libgcc libstdc++ openssl ca-certificates
    - BUILD_APKS=git curl wget bzip2 tar make gcc clang g++ python linux-headers paxctl binutils-gold autoconf bison zlib-dev openssl-dev
    - NODE_CONFIG_FLAGS=--shared-openssl
  labels:
    aliyun.scale: '1'
neteaseapp:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/news:latest'
  entrypoint:
    - node
    - startcm.js
    - '--name=netease_app'
  restart: always
  environment:
    - NODE_PREFIX=/usr/local
    - NODE_SOURCE=/usr/src/node
    - BASE_APKS=bash libgcc libstdc++ openssl ca-certificates
    - BUILD_APKS=git curl wget bzip2 tar make gcc clang g++ python linux-headers paxctl binutils-gold autoconf bison zlib-dev openssl-dev
    - NODE_CONFIG_FLAGS=--shared-openssl
  labels:
    aliyun.scale: '1'
sinaapp:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/news:latest'
  entrypoint:
    - node
    - startcm.js
    - '--name=sina_app'
  restart: always
  environment:
    - NODE_PREFIX=/usr/local
    - NODE_SOURCE=/usr/src/node
    - BASE_APKS=bash libgcc libstdc++ openssl ca-certificates
    - BUILD_APKS=git curl wget bzip2 tar make gcc clang g++ python linux-headers paxctl binutils-gold autoconf bison zlib-dev openssl-dev
    - NODE_CONFIG_FLAGS=--shared-openssl
  labels:
    aliyun.scale: '1'
sinasite:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/news:latest'
  entrypoint:
    - node
    - startcm.js
    - '--name=sina_site'
  restart: always
  environment:
    - NODE_PREFIX=/usr/local
    - NODE_SOURCE=/usr/src/node
    - BASE_APKS=bash libgcc libstdc++ openssl ca-certificates
    - BUILD_APKS=git curl wget bzip2 tar make gcc clang g++ python linux-headers paxctl binutils-gold autoconf bison zlib-dev openssl-dev
    - NODE_CONFIG_FLAGS=--shared-openssl
  labels:
    aliyun.scale: '1'
tencentapp:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/news:latest'
  entrypoint:
    - node
    - startcm.js
    - '--name=tencent_app'
  restart: always
  environment:
    - NODE_PREFIX=/usr/local
    - NODE_SOURCE=/usr/src/node
    - BASE_APKS=bash libgcc libstdc++ openssl ca-certificates
    - BUILD_APKS=git curl wget bzip2 tar make gcc clang g++ python linux-headers paxctl binutils-gold autoconf bison zlib-dev openssl-dev
    - NODE_CONFIG_FLAGS=--shared-openssl
  labels:
    aliyun.scale: '1'
tencentsite:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/news:latest'
  entrypoint:
    - node
    - startcm.js
    - '--name=tencent_site'
  restart: always
  environment:
    - NODE_PREFIX=/usr/local
    - NODE_SOURCE=/usr/src/node
    - BASE_APKS=bash libgcc libstdc++ openssl ca-certificates
    - BUILD_APKS=git curl wget bzip2 tar make gcc clang g++ python linux-headers paxctl binutils-gold autoconf bison zlib-dev openssl-dev
    - NODE_CONFIG_FLAGS=--shared-openssl
  labels:
    aliyun.scale: '1'
tianapp:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/news:latest'
  entrypoint:
    - node
    - startcm.js
    - '--name=tian_app'
  restart: always
  environment:
    - NODE_PREFIX=/usr/local
    - NODE_SOURCE=/usr/src/node
    - BASE_APKS=bash libgcc libstdc++ openssl ca-certificates
    - BUILD_APKS=git curl wget bzip2 tar make gcc clang g++ python linux-headers paxctl binutils-gold autoconf bison zlib-dev openssl-dev
    - NODE_CONFIG_FLAGS=--shared-openssl
  labels:
    aliyun.scale: '1'
yidianapp:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/news:latest'
  entrypoint:
    - node
    - startcm.js
    - '--name=yidian_app'
  restart: always
  environment:
    - NODE_PREFIX=/usr/local
    - NODE_SOURCE=/usr/src/node
    - BASE_APKS=bash libgcc libstdc++ openssl ca-certificates
    - BUILD_APKS=git curl wget bzip2 tar make gcc clang g++ python linux-headers paxctl binutils-gold autoconf bison zlib-dev openssl-dev
    - NODE_CONFIG_FLAGS=--shared-openssl
  labels:
    aliyun.scale: '1'
sohuapp:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/news:latest'
  entrypoint:
    - node
    - startcm.js
    - '--name=sohu_app'
  restart: always
  environment:
    - NODE_PREFIX=/usr/local
    - NODE_SOURCE=/usr/src/node
    - BASE_APKS=bash libgcc libstdc++ openssl ca-certificates
    - BUILD_APKS=git curl wget bzip2 tar make gcc clang g++ python linux-headers paxctl binutils-gold autoconf bison zlib-dev openssl-dev
    - NODE_CONFIG_FLAGS=--shared-openssl
  labels:
    aliyun.scale: '1'
toutiaoapp:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/news:latest'
  entrypoint:
    - node
    - startcm.js
    - '--name=toutiao_app'
  restart: always
  environment:
    - NODE_PREFIX=/usr/local
    - NODE_SOURCE=/usr/src/node
    - BASE_APKS=bash libgcc libstdc++ openssl ca-certificates
    - BUILD_APKS=git curl wget bzip2 tar make gcc clang g++ python linux-headers paxctl binutils-gold autoconf bison zlib-dev openssl-dev
    - NODE_CONFIG_FLAGS=--shared-openssl
  labels:
    aliyun.scale: '1'
sohusite:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/news:latest'
  entrypoint:
    - node
    - startcm.js
    - '--name=sohu_site'
  restart: always
  environment:
    - NODE_PREFIX=/usr/local
    - NODE_SOURCE=/usr/src/node
    - BASE_APKS=bash libgcc libstdc++ openssl ca-certificates
    - BUILD_APKS=git curl wget bzip2 tar make gcc clang g++ python linux-headers paxctl binutils-gold autoconf bison zlib-dev openssl-dev
    - NODE_CONFIG_FLAGS=--shared-openssl
  labels:
    aliyun.scale: '1'
```

appnews

```text
appnews:
  restart: always
  environment:
    - NODE_PREFIX=/usr/local
    - NODE_SOURCE=/usr/src/node
    - BASE_APKS=bash libgcc libstdc++ openssl ca-certificates
    - >-
      BUILD_APKS=git curl wget bzip2 tar make gcc clang g++ python linux-headers
      paxctl binutils-gold autoconf bison zlib-dev openssl-dev
    - NODE_CONFIG_FLAGS=--shared-openssl
  memswap_limit: 0
  labels:
    aliyun.scale: '1'
  entrypoint:
    - node
    - startlst.js
  shm_size: 0
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/news:latest'
  memswap_reservation: 0
  kernel_memory: 0
  mem_limit: 0
```

appnw

```text
appnw:
  restart: always
  environment:
    - NODE_PREFIX=/usr/local
    - NODE_SOURCE=/usr/src/node
    - BASE_APKS=bash libgcc libstdc++ openssl ca-certificates
    - >-
      BUILD_APKS=git curl wget bzip2 tar make gcc clang g++ python linux-headers
      paxctl binutils-gold autoconf bison zlib-dev openssl-dev
    - NODE_CONFIG_FLAGS=--shared-openssl
  memswap_limit: 0
  labels:
    aliyun.scale: '1'
  entrypoint:
    - node
    - startnw.js
  shm_size: 0
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/news:latest'
  memswap_reservation: 0
  kernel_memory: 0
  mem_limit: 0
```

kuyun

```text
kuyunRank:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/kuyunrank:latest'
  mem_limit: 0
  environment:
    - LANG=C.UTF-8
    - JAVA_HOME=/usr/lib/jvm/java-1.8-openjdk
  kernel_memory: 0
  memswap_reservation: 0
  restart: always
  entrypoint:
    - java
    - '-jar'
    - crawled_kuyunrank.jar
  shm_size: 0
  memswap_limit: 0
  labels:
    aliyun.scale: '1'
```

weibo-topic

```text
topicrank:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/weibo:topic'
  command:
    - bin/cron_topic_rank_local.sh
  restart: always
  environment:
    - NPM_CONFIG_LOGLEVEL=info
  cpu_shares: 20
  labels:
    aliyun.scale: '3'
  entrypoint:
    - bin/cron_topic_rank_local.sh
  memswap_limit: 0
  shm_size: 0
  memswap_reservation: 0
  kernel_memory: 0
  name: topicrank
topicstar:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/weibo:topic'
  command:
    - bin/run_topic_stat_local.sh
  restart: always
  environment:
    - NPM_CONFIG_LOGLEVEL=info
  cpu_shares: 20
  labels:
    aliyun.global: 'true'
```

