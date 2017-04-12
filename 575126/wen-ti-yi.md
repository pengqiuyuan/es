出错过程还原，解析时间戳类型（秒级）

`mapping`

```
curl -XPOST http://localhost:9222/ikindex/fulltext/_mapping -d'
 {
     "fulltext": {
         "properties": {
             "crawled_at": {
            "format": "strict_date_optional_time||epoch_millis",
            "type": "date"
             }
         }
     }
 }'
```

插入一条数据

```
curl -XPUT http://127.0.0.1:9222/ikindex/fulltext/1 -d '
{
    "crawled_at": 1491979523.6475554
}'
```

报错

```
{"error":{"root_cause":[{"type":"mapper_parsing_exception","reason":"failed to parse [crawled_at]"}],"type":"mapper_parsing_exception","reason":"failed to parse [crawled_at]","caused_by":{"type":"illegal_argument_exception","reason":"Invalid format: \"1491979523.6475554\" is malformed at \"979523.6475554\""}},"status":400}
```

原因

`elasticsearch` 支持的`时间戳`日期类型是`Long`。范围是 `Long.MIN_VALUE` 到 `Long.MAX_VALUE`。传入的是秒级别的时间戳

`"crawled_at": 1491979523.6475554`，为`double`类型。

避免`es`插入数据失败，建议插入数据时，时间戳统一为毫秒级别。

[官方文档一](https://www.elastic.co/guide/en/elasticsearch/reference/current/mapping-date-format.html#strict-date-time)

[官方文档二](https://www.elastic.co/guide/en/elasticsearch/reference/current/date.html)

