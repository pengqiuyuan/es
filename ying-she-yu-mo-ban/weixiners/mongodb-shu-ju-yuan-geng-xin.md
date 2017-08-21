[`mongo-connector` 文档](https://github.com/mongodb-labs/mongo-connector/wiki/Configuration-Options)

`config.json` 模式，`mongo-connector -c weixin.json`

```
{
    "mainAddress": "127.0.0.1:6717",
    "authentication": {
          "adminUsername": "用户名",
          "password": "密码"
    },
    "namespaces": {
        "include": ["wechat-dev.weixiners"],
        "mapping": {
          "wechat-dev.weixiners": "weixiners.weixiner"
        }
    },
    "docManagers": [
      {
        "docManager": "elastic2_doc_manager",
        "targetURL": "用户名:密码@node01:9222",
        "autoCommitInterval":0,
        "bulkSize":3000,
        "args": {
          "meta_index_name": "mongodb_weixiners",
          "meta_type": "mongodb_weixiners"
        }
      }
    ]
}
```



