baidunews

```
baidunews:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/baidunews:latest'
  entrypoint:
    - node
    - main/index.js
  restart: always
  environment:
    - NPM_CONFIG_LOGLEVEL=info
  labels:
    aliyun.scale: '10'
```

toutiaohao

```
toutiao:
  restart: always
  environment:
    - LANG=C.UTF-8
    - GPG_KEY=97FC712E4C024BBEA48A61ED3A5CA953F73C700D
  memswap_limit: 0
  labels:
    aliyun.global: 'true'
  entrypoint:
    - python3
    - headlineFetcher_domain.py
  shm_size: 0
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/toutiaohao:latest'
  memswap_reservation: 0
  kernel_memory: 0
  mem_limit: 0
```

zhihu

```
zhihu-question:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/zhihu:latest'
  entrypoint:
    - ts-node
    - index.js
    - questions-latest
  restart: always
  environment:
    - NPM_CONFIG_LOGLEVEL=info
  mem_limit: 209715200
  cpu_shares: 10
  labels:
    aliyun.global: 'true'
```



