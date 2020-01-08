# crawler-group-05

**tianya**

```text
channel:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/tianya:latest'
  command:
    - ts-node
    - scripts/channel.js
  restart: always
  environment:
    - NPM_CONFIG_LOGLEVEL=info
  labels:
    aliyun.scale: '1'
plate:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/tianya:latest'
  command:
    - ts-node
    - index.js
  restart: always
  environment:
    - NPM_CONFIG_LOGLEVEL=info
  labels:
    aliyun.scale: '3'
post:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/tianya:latest'
  command:
    - ts-node
    - post.js
  restart: always
  environment:
    - NPM_CONFIG_LOGLEVEL=info
  labels:
   aliyun.scale: '6'
```

