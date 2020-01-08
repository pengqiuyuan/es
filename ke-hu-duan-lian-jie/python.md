# Python

`Python`连接`elasticsearch`

[官网文档参考](http://elasticsearch-py.readthedocs.io/en/master/index.html?highlight=auth)

```text
es = Elasticsearch(
    ['localhost', 'otherhost'],
    http_auth=('user', 'secret'),
    port=443
)
```

