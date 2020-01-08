# weibo-weixin

微博

```text
weiboer-star:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/weibo:master'
  entrypoint:
    - coffee
    - weiboer_star_syncer.coffee
  restart: always
  environment:
    - NPM_CONFIG_LOGLEVEL=info
  cpu_shares: 20
  labels:
    aliyun.scale: '4'
weiboer-top:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/weibo:master'
  entrypoint:
    - coffee
    - weiboer_top_syncer.coffee
  restart: always
  environment:
    - NPM_CONFIG_LOGLEVEL=info
  cpu_shares: 20
  labels:
    aliyun.scale: '4'
main:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/weibo:master'
  restart: always
  environment:
    - NPM_CONFIG_LOGLEVEL=info
  labels:
    aliyun.scale: '5'
  entrypoint:
    - coffee
    - starters/main.coffee
  cpu_shares: 20
add:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/weibo:master'
  restart: always
  environment:
    - NPM_CONFIG_LOGLEVEL=info
  labels:
    aliyun.scale: '5'
  entrypoint:
    - coffee
    - stat_tools/weibo_article_add_topics.coffee
  cpu_shares: 20
level:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/weibo:master'
  restart: always
  environment:
    - NPM_CONFIG_LOGLEVEL=info
  labels:
    aliyun.scale: '10'
  entrypoint:
    - coffee
    - stat_tools/cal_repost_level.coffee
  cpu_shares: 20
log:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/weibo:master'
  restart: always
  environment:
    - NPM_CONFIG_LOGLEVEL=info
  labels:
    aliyun.scale: '3'
  entrypoint:
    - coffee
    - weiboer_log_syncer.coffee
  cpu_shares: 20
task:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/weibo:master'
  entrypoint:
    - coffee
    - stat_tools/narnia_task_crawler.coffee
  restart: always
  environment:
    - NPM_CONFIG_LOGLEVEL=info
  mem_limit: 209715200
  cpu_shares: 20
  labels:
    aliyun.scale: '10'
weiboer-syncer:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/weibo:master'
  entrypoint:
    - coffee
    - weiboer_syncer.coffee
  restart: always
  environment:
    - NPM_CONFIG_LOGLEVEL=info
  cpu_shares: 20
  labels:
    aliyun.global: 'true'
```

微信

```text
newrank:
  image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/weixin:latest'
  entrypoint:
    - node
    - main/scripts/crawl_newrank.js
  restart: always
  environment:
    - NPM_CONFIG_LOGLEVEL=info
  labels:
    aliyun.global: 'true'
# content:
#   image: 'registry.cn-hangzhou.aliyuncs.com/shutaiqi/weixin:latest'
#   entrypoint:
#     - node
#     - main/scripts/crawl_server.js
#   restart: always
#   environment:
#     - NPM_CONFIG_LOGLEVEL=info
#   labels:
#     aliyun.global: 'true'
```

