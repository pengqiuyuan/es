二、**获取热门话题 TopN**

`POST` `http://127.0.0.1/stq/api/v1/rowlet/findTopNTopics`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
startDate为起始时间（含），必填。
endDate为结束时间（不含），必填。
category为数据源 tw、fb，必填
pageSize，必填。获取多少条
```

`BODY` 体：

```
twitter

{
	"startDate": "2016-10-09",
	"endDate": "2017-12-10",
	"category": "tw",
	"pageSize": "10"
}

```

`response` Es查询有保存计算指标

`Twitter`

```
{
	"tw": [{
			"doc_count": 5018,
			"key": "Trumpcare"
		},
		{
			"doc_count": 3859,
			"key": "ACA"
		},
		{
			"doc_count": 2519,
			"key": "TaxReform"
		},
		{
			"doc_count": 2487,
			"key": "TrumpCare"
		},
		{
			"doc_count": 2084,
			"key": "Obamacare"
		},
		{
			"doc_count": 1909,
			"key": "ProtectOurCare"
		},
		{
			"doc_count": 1812,
			"key": "DACA"
		},
		{
			"doc_count": 1653,
			"key": "taxreform"
		},
		{
			"doc_count": 1557,
			"key": "GOPTaxScam"
		},
		{
			"doc_count": 1529,
			"key": "AHCA"
		}
	],
	"message": "任务成功"
}
```



