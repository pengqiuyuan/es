**七**、SPC 周、月报自动导出

`POST` `http://127.0.0.1/stq/api/v1/poi/downRowletWithSpcReportByJsonDate`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
category 必填，字符串
    week
    month
jsonData 必填项，json字符串。
```

`BODY` 体：

```
{
	"category": "week",
	"jsonData": {
		"titleName": "SPC美国社交媒体政治传播内容分析周报",
		"titleDate": "2018年第1周  1月1日—1月7日",
		"summary": "根据国际意见领袖社交媒体传播内容分析平台数据显示，2018年1月1日-1月7日国际意见领袖（正文简称：“IKOLs”）共发文10000条，与上月相比增加2%，其中Facebook 5500条，twitter 4500条。根据IKOLs影响力指数分析，本周 Facebook最具影响力IKOLs是Donald J. Trump、Barack Obama、Michael R. Pence、Ryan Zinke、Elaine Duke； 本周Twitter最具影响力IKOLs是Melania Trump、Karen Pence、James Mattis、Eric D. Hargan、Sonny Perdue。",
		"h1": {
			"h1_p1_content1": "根据IKOLs影响力指数分析， Facebook最具影响力IKOLs是Donald J. Trump、Barack Obama、Michael R. Pence、Ryan Zinke、Elaine Duke， Twitter IKOLs最具影响力的是Melania Trump、Karen Pence、James Mattis、Eric D. Hargan、Sonny Perdue。",
			"ikolsCount": {
				"tw": [{
						"key": "@Donald J. Trump",
						"value": "145",
						"job": "总统"
					},
					{
						"key": "@Donald J. Trump",
						"value": "145",
						"job": "总统"
					}
				],
				"fb": [{
						"key": "@Melania Trump",
						"value": "255",
						"job": "总统"
					},
					{
						"key": "@Melania Trump",
						"value": "255",
						"job": "总统"
					}
				]
			},
			"h1_p2_content1": "2018年第1周， Facebook发文量最多的IKOLs是Donald J. Trump、Barack Obama、Michael R. Pence、Elaine L. Chao、Scott Pruitt，IKOLs人均发文量是12条。 Twitter发文量最多的IKOLs是Melania Trump、Karen Pence、James Mattis、Mike Pompeo、Daniel Coats，IKOLs人均发文量是11条。",
			"articlesCount": {
				"tw": [{
						"key": "@Donald J. Trump",
						"value": "145",
						"job": "总统"
					},
					{
						"key": "@Donald J. Trump",
						"value": "145",
						"job": "总统"
					}
				],
				"fb": [{
						"key": "@Melania Trump",
						"value": "255",
						"job": "总统"
					},
					{
						"key": "@Melania Trump",
						"value": "255",
						"job": "总统"
					}
				]
			},
			"h1_p3_content1": "2018年第1周，Facebook发文转发量最高的IKOLs是Donald J. Trump、Barack Obama、Michael R. Pence、Ryan Zinke、Elaine Duke，IKOLs人均发文转发量是20。Twitter发文转发量最多的IKOLs是Melania Trump、Karen Pence、James Matti、Eric D. Hargan、Sonny Perdue，IKOLs人均发文转发量是20。",
			"repostCount": {
				"tw": [{
						"key": "@Donald J. Trump",
						"value": "145",
						"job": "总统"
					},
					{
						"key": "@Donald J. Trump",
						"value": "145",
						"job": "总统"
					}
				],
				"fb": [{
						"key": "@Melania Trump",
						"value": "255",
						"job": "总统"
					},
					{
						"key": "@Melania Trump",
						"value": "255",
						"job": "总统"
					}
				]
			},
			"h1_p4_content1": "2018年第1周，Facebook发文评论量最多的IKOLs是Donald J. Trump、Barack Obama、Michael R. Pence、Elaine L. Chao、Scott Pruitt，IKOLs人均发文评论量是40条。 Twitter发文评论量最多的IKOLs是Melania Trump、Karen Pence、James Mattis、Mike Pompeo、Daniel Coats，IKOLs人均发文评论量是45。",
			"commentCount": {
				"tw": [{
						"key": "@Donald J. Trump",
						"value": "145",
						"job": "总统"
					},
					{
						"key": "@Donald J. Trump",
						"value": "145",
						"job": "总统"
					}
				],
				"fb": [{
						"key": "@Melania Trump",
						"value": "255",
						"job": "总统"
					},
					{
						"key": "@Melania Trump",
						"value": "255",
						"job": "总统"
					}
				]
			},
			"h1_p5_content1": "2018年第1周，Facebook发文点赞量最高的IKOLs是Donald J. Trump、Barack Obama、Michael R. Pence、Ryan Zinke、Elaine Duke，IKOLs人均发文点赞量是500。 Twitter发文点赞量最多的IKOLs是Melania Trump、Karen Pence、James Matti、Eric D. Hargan、Sonny Perdue，IKOLs人均发文点赞量是500。",
			"upCount": {
				"tw": [{
						"key": "@Donald J. Trump",
						"value": "145",
						"job": "总统"
					},
					{
						"key": "@Donald J. Trump",
						"value": "145",
						"job": "总统"
					}
				],
				"fb": [{
						"key": "@Melania Trump",
						"value": "255",
						"job": "总统"
					},
					{
						"key": "@Melania Trump",
						"value": "255",
						"job": "总统"
					}
				]
			},
			"h1_p6_content1": "本周Facebook粉丝量最多的IKOLs是Donald J. Trump、Barack Obama、Michael R. Pence、John F. Kelly、David J. Shulkin，粉丝量分别是15901、15872、14981、13687和13465。Twitter粉丝量最多的IKOLs是Melania Trump、Karen Pence、James Mattis、Elaine L. Chao、Scott Pruitt，粉丝量分别是18761、18561、18091、17889、14243。",
			"fansCount": {
				"tw": [{
						"key": "@Donald J. Trump",
						"value": "145",
						"job": "总统"
					},
					{
						"key": "@Donald J. Trump",
						"value": "145",
						"job": "总统"
					}
				],
				"fb": [{
						"key": "@Melania Trump",
						"value": "255",
						"job": "总统"
					},
					{
						"key": "@Melania Trump",
						"value": "255",
						"job": "总统"
					}
				]
			},
			"h1_p7_content1": "本周Facebook新增粉丝量最多的IKOLs是Donald J. Trump、Barack Obama、Michael R. Pence、，分别增加了15901、15872、14981、14567和13456； Twitter新增粉丝量最多的IKOLs是Melania Trump、Karen Pence、James Mattis、Elaine L. Chao、Scott Pruitt，分别是18761、18561、18091、17889、14243。",
			"newsFansCount": {
				"tw": [{
						"key": "@Donald J. Trump",
						"value": "145",
						"job": "总统"
					},
					{
						"key": "@Donald J. Trump",
						"value": "145",
						"job": "总统"
					}
				],
				"fb": [{
						"key": "@Melania Trump",
						"value": "255",
						"job": "总统"
					},
					{
						"key": "@Melania Trump",
						"value": "255",
						"job": "总统"
					}
				]
			}
		},
		"h2": {
			"h2_p1_content1": "Facebook转发量最高的发文来自于First Lady Melania Trump、Mike Pence、Barack Obama、Al Franken、Bill Nelson（内容详见下表）。Twitter转发量最高的发文来自于First Lady Melania Trump、Mike Pence、Barack Obama、Ryan Zinke、Dan Coats（内容详见下表）。",
			"repostContent": {
				"tw": [{
						"name": "Chris Christie@govchristie",
						"date": "2017/12/11 13:34:30",
						"comment": "2389",
						"repost": "2389",
						"up": "2389",
						"content": "The effects of the hurricane season are still being felt throughout southern portions of the U.S. and in Puerto Rico, and residents still need our help. As Christmas and the New Year approach, I encourage people to lend time volunteering or providing financial support to those still reeling from the hurricanes.​"
					},
					{
						"name": "Chris Christie@govchristie",
						"date": "2017/12/11 13:34:30",
						"comment": "2389",
						"repost": "2389",
						"up": "2389",
						"content": "The effects of the hurricane season are still being felt throughout southern portions of the U.S. and in Puerto Rico, and residents still need our help. As Christmas and the New Year approach, I encourage people to lend time volunteering or providing financial support to those still reeling from the hurricanes.​"
					}
				],
				"fb": [{
						"name": "Chris Christie@govchristie",
						"date": "2017/12/11 13:34:30",
						"comment": "2389",
						"repost": "2389",
						"up": "2389",
						"content": "The effects of the hurricane season are still being felt throughout southern portions of the U.S. and in Puerto Rico, and residents still need our help. As Christmas and the New Year approach, I encourage people to lend time volunteering or providing financial support to those still reeling from the hurricanes.​"
					},
					{
						"name": "Chris Christie@govchristie",
						"date": "2017/12/11 13:34:30",
						"comment": "2389",
						"repost": "2389",
						"up": "2389",
						"content": "The effects of the hurricane season are still being felt throughout southern portions of the U.S. and in Puerto Rico, and residents still need our help. As Christmas and the New Year approach, I encourage people to lend time volunteering or providing financial support to those still reeling from the hurricanes.​"
					}
				]
			},
			"h2_p2_content1": "Facebook评论量最高的发文来自于 Asa Hutchinson、Ben Cardin、Chris Christie、Ryan Zinke、Dan Coats（内容详见下表）。Twitter评论量最高的发文来自于Charlie Baker 、Chris Murphy、Grassley Press、Ryan Zinke、Dan Coats（内容详见下表）.",
			"commentContent": {
				"tw": [{
						"name": "Chris Christie@govchristie",
						"date": "2017/12/11 13:34:30",
						"comment": "2389",
						"repost": "2389",
						"up": "2389",
						"content": "The effects of the hurricane season are still being felt throughout southern portions of the U.S. and in Puerto Rico, and residents still need our help. As Christmas and the New Year approach, I encourage people to lend time volunteering or providing financial support to those still reeling from the hurricanes.​"
					},
					{
						"name": "Chris Christie@govchristie",
						"date": "2017/12/11 13:34:30",
						"comment": "2389",
						"repost": "2389",
						"up": "2389",
						"content": "The effects of the hurricane season are still being felt throughout southern portions of the U.S. and in Puerto Rico, and residents still need our help. As Christmas and the New Year approach, I encourage people to lend time volunteering or providing financial support to those still reeling from the hurricanes.​"
					}
				],
				"fb": [{
						"name": "Chris Christie@govchristie",
						"date": "2017/12/11 13:34:30",
						"comment": "2389",
						"repost": "2389",
						"up": "2389",
						"content": "The effects of the hurricane season are still being felt throughout southern portions of the U.S. and in Puerto Rico, and residents still need our help. As Christmas and the New Year approach, I encourage people to lend time volunteering or providing financial support to those still reeling from the hurricanes.​"
					},
					{
						"name": "Chris Christie@govchristie",
						"date": "2017/12/11 13:34:30",
						"comment": "2389",
						"repost": "2389",
						"up": "2389",
						"content": "The effects of the hurricane season are still being felt throughout southern portions of the U.S. and in Puerto Rico, and residents still need our help. As Christmas and the New Year approach, I encourage people to lend time volunteering or providing financial support to those still reeling from the hurricanes.​"
					}
				]
			},
			"h2_p3_content1": "Facebook点赞量最高的发文来自于Asa Hutchinson、Ben Cardin、Chris Christie、Chris Murphy、Brian Sandoval （内容详见下表）。Twitte点赞量最高的发文来自于Charlie Baker 、Chris Murphy、 Grassley Press、Al Franken、Chris Christie、Brian Sandoval（内容详见下表）。",
			"upContent": {
				"tw": [{
						"name": "Chris Christie@govchristie",
						"date": "2017/12/11 13:34:30",
						"comment": "2389",
						"repost": "2389",
						"up": "2389",
						"content": "The effects of the hurricane season are still being felt throughout southern portions of the U.S. and in Puerto Rico, and residents still need our help. As Christmas and the New Year approach, I encourage people to lend time volunteering or providing financial support to those still reeling from the hurricanes.​"
					},
					{
						"name": "Chris Christie@govchristie",
						"date": "2017/12/11 13:34:30",
						"comment": "2389",
						"repost": "2389",
						"up": "2389",
						"content": "The effects of the hurricane season are still being felt throughout southern portions of the U.S. and in Puerto Rico, and residents still need our help. As Christmas and the New Year approach, I encourage people to lend time volunteering or providing financial support to those still reeling from the hurricanes.​"
					}
				],
				"fb": [{
						"name": "Chris Christie@govchristie",
						"date": "2017/12/11 13:34:30",
						"comment": "2389",
						"repost": "2389",
						"up": "2389",
						"content": "The effects of the hurricane season are still being felt throughout southern portions of the U.S. and in Puerto Rico, and residents still need our help. As Christmas and the New Year approach, I encourage people to lend time volunteering or providing financial support to those still reeling from the hurricanes.​"
					},
					{
						"name": "Chris Christie@govchristie",
						"date": "2017/12/11 13:34:30",
						"comment": "2389",
						"repost": "2389",
						"up": "2389",
						"content": "The effects of the hurricane season are still being felt throughout southern portions of the U.S. and in Puerto Rico, and residents still need our help. As Christmas and the New Year approach, I encourage people to lend time volunteering or providing financial support to those still reeling from the hurricanes.​"
					}
				]
			},
			"h2_p4_content1": "Facebook点赞量最高的发文来自于Asa Hutchinson、Ben Cardin、Chris Christie、Chris Murphy、Brian Sandoval （内容详见下表）。Twitte点赞量最高的发文来自于Charlie Baker 、Chris Murphy、 Grassley Press、Al Franken、Chris Christie、Brian Sandoval（内容详见下表）。",
			"topicRank": {
				"tw": [{
						"key": "1",
						"value": "AChristmasStoryLive"
					},
					{
						"key": "2",
						"value": "WWEClash"
					}
				]
			},
			"h2_p4_content2": "Facebook点赞量最高的发文来自于Asa Hutchinson、Ben Cardin、Chris Christie、Chris Murphy、Brian Sandoval （内容详见下表）。Twitte点赞量最高的发文来自于Charlie Baker 、Chris Murphy、 Grassley Press、Al Franken、Chris Christie、Brian Sandoval（内容详见下表）。",
			"topicContent": {
				"tw": [{
						"name": "Chris Christie@govchristie",
						"date": "2017/12/11 13:34:30",
						"comment": "2389",
						"repost": "2389",
						"up": "2389",
						"content": "The effects of the hurricane season are still being felt throughout southern portions of the U.S. and in Puerto Rico, and residents still need our help. As Christmas and the New Year approach, I encourage people to lend time volunteering or providing financial support to those still reeling from the hurricanes.​"
					},
					{
						"name": "Chris Christie@govchristie",
						"date": "2017/12/11 13:34:30",
						"comment": "2389",
						"repost": "2389",
						"up": "2389",
						"content": "The effects of the hurricane season are still being felt throughout southern portions of the U.S. and in Puerto Rico, and residents still need our help. As Christmas and the New Year approach, I encourage people to lend time volunteering or providing financial support to those still reeling from the hurricanes.​"
					}
				]
			}
		}
	}
}
```

`response` 返回提示信息

```
成功：

{
    "msPath": "https://narnia.oss-cn-beijing.aliyuncs.com/week/20180212174052910/SPC%E7%BE%8E%E5%9B%BD%E7%A4%BE%E4%BA%A4%E5%AA%92%E4%BD%93%E6%94%BF%E6%B2%BB%E4%BC%A0%E6%92%AD%E5%86%85%E5%AE%B9%E5%88%86%E6%9E%90%E5%91%A8%E6%8A%A5%EF%BC%882018%E5%B9%B4%E7%AC%AC1%E5%91%A8%20%201%E6%9C%881%E6%97%A5%E2%80%941%E6%9C%887%E6%97%A5%EF%BC%89.docx?Expires=1520255848&OSSAccessKeyId=LTAIARWAKGUIqkn6&Signature=hfhmKl99sNYqDTHtsufPyrSjDTM%3D",
    "message": "任务执行成功"
}

失败：1、检查输入body体 jsonData 是否包含。2、检查 value 是否含有 null 值。

{
    "msPath": "",
    "message": "任务执行错误"
}
```



