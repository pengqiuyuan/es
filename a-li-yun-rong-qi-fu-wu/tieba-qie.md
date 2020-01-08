# tieba-qie

qie

```text
qie:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/qie:latest'
  entrypoint:
    - python3
    - qie_domain.py
  restart: always
  labels:
    aliyun.scale: '1'
```

tieba

```text
tieba:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/tieba:latest'
  entrypoint:
    - python3
    - tieba_domain.py
  restart: always
  labels:
    aliyun.global: 'true'
```

