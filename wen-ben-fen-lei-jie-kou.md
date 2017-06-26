文本分类提供两个接口服务

**POST 请求（获取单条文本的主、次分类）**

`POST` `http://127.0.0.1/stq/api/v1/fa/fasttext/one`

`HEADERS`：`"Content-Type" => "text/plain;application/json"`

`BODY` 体参数说明：文本内容为一条字符串

```
"爸爸节，我用这种方式来度过：“每一百个新出生的婴儿中，就有一个可能患自闭症”。他（她）们生活在孤寂中，他们的父母用极大的耐心和爱，苦苦陪伴孩子成长。他们都是来自星星的孩子，他们需要我们的爱。谢谢给力的哈雷兄弟们，谢谢每一位支持的朋友。"
```

`response` 请求成功（逗号左边为主分类，右边为此分类）

```
新闻内容,新闻内容
```

`response` 数据写入队列失败（有一条消息写入失败就会触发。返回 `false` 的 场景是 `web server` 与 `kafka` 连接断开）

```
{
  "success" : "false"
}
```

`logstash`** 消费**`kafka`**中的数据到 **`elasticsearch`

```
...
```

从 `kafka` 队列中读取的数据，两条符合预期（`index_name`、`type_name`、`id`会在`logstash filter`中处理后移除，保存或者更新数据到 `es`）

```
{
          "author_name" => "乒乓网1"
}
{
          "author_name" => "乒乓网2"
}
```



