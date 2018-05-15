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
	"startDate": "2017-01-01",
	"endDate": "2017-12-31",
	"category": "tw",
	"pageSize": "10"
}
```

`response` Es查询有保存计算指标

`Twitter`

```
{
	"tw": [{
			"doc_count": 596,
			"key": "GOPTaxScam"
		},
		{
			"doc_count": 459,
			"key": "TaxReform"
		},
		{
			"doc_count": 286,
			"key": "taxreform"
		},
		{
			"doc_count": 236,
			"key": "TaxCutsandJobsAct"
		},
		{
			"doc_count": 209,
			"key": "NetNeutrality"
		},
		{
			"doc_count": 164,
			"key": "GetCovered"
		},
		{
			"doc_count": 123,
			"key": "Christmas"
		},
		{
			"doc_count": 123,
			"key": "MerryChristmas"
		},
		{
			"doc_count": 117,
			"key": "CHIP"
		},
		{
			"doc_count": 98,
			"key": "DreamActNow"
		}
	],
	"message": "任务成功"
}
```



