# Nodejs

`Nodejs`连接`elasticsearch`

[官网文档参考](https://www.elastic.co/guide/en/elasticsearch/client/javascript-api/current/auth-reference.html)

```text
var client = new elasticsearch.Client({
  host: 'https://user:password@my-site.com:9200'
})
```

```text
var client = new elasticsearch.Client({
  host: 'https://user:password@my-site.com:9200'
})

client.count({
  index: 'zhihu_questions'
}, function (error, response) {
  var count = response.count;
});
```

