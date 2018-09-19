**一**、MCI 自动报告导出

`POST` `http://127.0.0.1/stq/api/v1/poi/downUgmWordReportByJsonDate`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
caseNum 必填，数值类型，根据案件数据量提供指定模板 20、50、100、150 ，4种。
jsonData 必填项，json字符串。
	titleName 日报名称
	journalNum 日报期数
```

`BODY` 体：

```
{
	"caseNum": 150,
	"jsonData": {
		"titleName": "UGM日报",
		"journalNum": 1,
		"titleDate": "2018年8月21日",
		"summary": "8月21日9时至17时30分，调查组对我区八宝山街道、苹果园街道、五里坨街道、金顶街街道、八角街道、鲁谷社区、古城街道等6类43个实地考察点位进行检查,检查发现问题132个（其中涉及安全环境工作组13个，城市家园80个，人文环境34个，社会环境2个，市场环境3个），涉及责任单位10家（详见附件1、附件2）。",
		"h1": {
			"total": "785",
			"notAccord": "18.18%",
			"accord": "81.82%",
			"notAccordNum": "123",
			"accordNum": "666",
			"content": [{
					"street": "八宝山街道",
					"category": [{
						"name": "超市",
						"total": "22",
						"notAccord": "18.18%",
						"accord": "81.82%",
						"notAccordNum": "4",
						"accordNum": "18"
					}, {
						"name": "社区",
						"total": "22",
						"notAccord": "18.18%",
						"accord": "81.82%",
						"notAccordNum": "4",
						"accordNum": "18"
					}, {
						"name": "社区综合文化服务中心",
						"total": "22",
						"notAccord": "18.18%",
						"accord": "81.82%",
						"notAccordNum": "4",
						"accordNum": "18"
					}]
				},
				{
					"street": "八角街道",
					"category": [{
						"name": "宾馆饭店",
						"total": "22",
						"notAccord": "18.18%",
						"accord": "81.82%",
						"notAccordNum": "4",
						"accordNum": "18"
					}, {
						"name": "超市",
						"total": "22",
						"notAccord": "18.18%",
						"accord": "81.82%",
						"notAccordNum": "4",
						"accordNum": "18"
					}, {
						"name": "医院",
						"total": "22",
						"notAccord": "18.18%",
						"accord": "81.82%",
						"notAccordNum": "4",
						"accordNum": "18"
					}]
				}
			]
		},
		"h2": [{
				"num": "1",
				"code": "281",
				"street": "八宝山街道",
				"category": "超市",
				"spotName": "北京永辉超市有限公司石景山分公司",
				"indexName": "Ⅱ-26城市规划建设",
				"testProject": "Ⅲ-57无障碍设施",
				"testContent": "是否设有轮椅通道、扶手、缘石坡道等无障碍设施",
				"problem": "没有设置无障碍设施",
				"result": "不符合",
				"responsibilityUnit": "区商务委",
				"workingGroup": "城市家园专项工作组",
				"image": "https://user-images.githubusercontent.com/4953205/45670903-98cdb600-bb56-11e8-8f93-a3f71a06aab9.png"
			},

			{
				"num": "2",
				"code": "281",
				"street": "八宝山街道",
				"category": "超市",
				"spotName": "北京永辉超市有限公司石景山分公司",
				"indexName": "Ⅱ-26城市规划建设",
				"testProject": "Ⅲ-57无障碍设施",
				"testContent": "是否设有轮椅通道、扶手、缘石坡道等无障碍设施",
				"problem": "没有设置无障碍设施",
				"result": "不符合",
				"responsibilityUnit": "区商务委",
				"workingGroup": "城市家园专项工作组",
				"image": "https://user-images.githubusercontent.com/4953205/45670903-98cdb600-bb56-11e8-8f93-a3f71a06aab9.png"
			},

			{
				"num": "3",
				"code": "282",
				"street": "八宝山街道111",
				"category": "超市",
				"spotName": "北京永辉超市有限公司石景山分公司",
				"indexName": "Ⅱ-26城市规划建设",
				"testProject": "Ⅲ-57无障碍设施",
				"testContent": "是否设有轮椅通道、扶手、缘石坡道等无障碍设施",
				"problem": "没有设置无障碍设施",
				"result": "不符合",
				"responsibilityUnit": "区商务委",
				"workingGroup": "城市家园专项工作组",
				"image": "https://user-images.githubusercontent.com/4953205/45670903-98cdb600-bb56-11e8-8f93-a3f71a06aab9.png"
			}
		]
	}
}
```

`response` 返回提示信息

```
成功：
{
	"msPath": "https://narnia.oss-cn-beijing.aliyuncs.com/UGMæ¥æ¥/20180919105141913/UGMæ¥æ¥ï¼2018å¹´8æ21æ¥ï¼.docx?Expires=1852685503&OSSAccessKeyId=LTAIARWAKGUIqkn6&Signature=gkBJed1pATs7auMmZcBh8Z/nLAI=",
	"message": "任务执行成功"
}

失败：1、检查输入body体 jsonData 是否包含。2、检查 value 是否含有 null 值。

{
    "msPath": "",
    "message": "任务执行错误"
}
```



