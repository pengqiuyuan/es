**一**、MCI 自动报告导出

`POST` `http://127.0.0.1/stq/api/v1/poi/downGniReportByJsonDate`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
category 必填，字符串，目前只有 stq
jsonData 必填项，json字符串。
```

`BODY` 体：

```
{
	"category": "stq",
	"jsonData": {
		"titleDate": "2018年01月",
		"summary": "根据政务新媒体指数（GNI）监测系统数据显示，2018年01月，山东省青岛市文明办的政务新媒体指数（GNI）综合排名第一，得分69.4。省级精神文明办政务新媒体指数前三名为河南省文明办、山东省文明办、首都文明办，市级精神文明办政务新媒体指数前三名为山东省青岛市文明办、山东省临沂市文明办、山东省潍坊市文明办，区县精神文明办政务新媒体指数前三名为广东省肇庆市四会市文明办、河南省新乡市卫辉市文明办、宜兴文明办，基层精神文明办政务新媒体指数前三名为安定门街道文明办、上海市徐汇区虹梅社区文明办、崇文门外街道办事处文明办。",
		"h1": {
			"h1_p1_content1": "2018年01月，全国精神文明办政务新媒体指数综合排名中，山东省青岛市文明办、河南省文明办、山东省临沂市文明办位居前三。",
			"totalTop10": [{
					"mediaName": "山东省青岛市文明办",
					"total": "69.4",
					"mediaType": "市级"
				},
				{
					"mediaName": "河南省文明办",
					"total": "69.1",
					"mediaType": "省级"
				},
				{
					"mediaName": "山东省临沂市文明办",
					"total": "66.2",
					"mediaType": "市级"
				},
				{
					"mediaName": "山东省潍坊市文明办",
					"total": "64.2",
					"mediaType": "市级"
				},
				{
					"mediaName": "山东省文明办",
					"total": "63.3",
					"mediaType": "省级"
				},
				{
					"mediaName": "首都文明办",
					"total": "62.6",
					"mediaType": "省级"
				},
				{
					"mediaName": "四川省文明办",
					"total": "58.7",
					"mediaType": "省级"
				},
				{
					"mediaName": "广东省肇庆市文明办",
					"total": "58.3",
					"mediaType": "市级"
				},
				{
					"mediaName": "温州文明办",
					"total": "55.8",
					"mediaType": "市级"
				},
				{
					"mediaName": "河南省南阳市文明办",
					"total": "55",
					"mediaType": "市级"
				}
			]
		},
		"h2": {
			"h2_content1": "2018年01月，对全国31个（不含港澳台）省级行政区域的精神文明办政务新媒体影响力排名，河南省文明办、山东省文明办、首都文明办位居前三。",
			"provTop10": [{
					"mediaName": "河南省文明办",
					"activeScore": "76.2",
					"toExposeScore": "80",
					"toInteractScore": "71.2",
					"connectScore": "49.2",
					"total": "69.1"
				},
				{
					"mediaName": "山东省文明办",
					"activeScore": "63.7",
					"toExposeScore": "74.4",
					"toInteractScore": "69.1",
					"connectScore": "46.1",
					"total": "63.3"
				},
				{
					"mediaName": "首都文明办",
					"activeScore": "77.2",
					"toExposeScore": "68.9",
					"toInteractScore": "60.2",
					"connectScore": "44",
					"total": "62.6"
				},
				{
					"mediaName": "四川省文明办",
					"activeScore": "62.7",
					"toExposeScore": "50",
					"toInteractScore": "45.5",
					"connectScore": "76.8",
					"total": "58.7"
				},
				{
					"mediaName": "内蒙古自治区文明办",
					"activeScore": "54.7",
					"toExposeScore": "41.1",
					"toInteractScore": "24",
					"connectScore": "49.3",
					"total": "42.3"
				},
				{
					"mediaName": "湖南文明办",
					"activeScore": "53.3",
					"toExposeScore": "42.3",
					"toInteractScore": "26.1",
					"connectScore": "43.7",
					"total": "41.3"
				},
				{
					"mediaName": "上海市文明办",
					"activeScore": "45.3",
					"toExposeScore": "38",
					"toInteractScore": "33.8",
					"connectScore": "32.1",
					"total": "37.3"
				},
				{
					"mediaName": "河北文明办",
					"activeScore": "48.3",
					"toExposeScore": "35.7",
					"toInteractScore": "28.7",
					"connectScore": "11.9",
					"total": "31.1"
				},
				{
					"mediaName": "广东省文明办",
					"activeScore": "41.7",
					"toExposeScore": "49.3",
					"toInteractScore": "30.7",
					"connectScore": "0",
					"total": "30.4"
				},
				{
					"mediaName": "江西文明办",
					"activeScore": "51.5",
					"toExposeScore": "14.6",
					"toInteractScore": "13.8",
					"connectScore": "37.5",
					"total": "29.3"
				}
			]
		},
		"h3": {
			"h3_content1": "2018年01月，对全国市级行政区域的精神文明办政务新媒体影响力排名，山东省青岛市文明办、山东省临沂市文明办、山东省潍坊市文明办位居前三。",
			"cityTop10": [{
					"mediaName": "山东省青岛市文明办",
					"activeScore": "82.2",
					"toExposeScore": "76.1",
					"toInteractScore": "53.1",
					"connectScore": "66.3",
					"total": "69.4"
				},
				{
					"mediaName": "山东省临沂市文明办",
					"activeScore": "81.2",
					"toExposeScore": "76.8",
					"toInteractScore": "62.7",
					"connectScore": "44.1",
					"total": "66.2"
				},
				{
					"mediaName": "山东省潍坊市文明办",
					"activeScore": "81.9",
					"toExposeScore": "77.3",
					"toInteractScore": "63.4",
					"connectScore": "34.3",
					"total": "64.2"
				},
				{
					"mediaName": "广东省肇庆市文明办",
					"activeScore": "76.8",
					"toExposeScore": "69.4",
					"toInteractScore": "49",
					"connectScore": "38.2",
					"total": "58.3"
				},
				{
					"mediaName": "温州文明办",
					"activeScore": "71.2",
					"toExposeScore": "60.6",
					"toInteractScore": "49.5",
					"connectScore": "41.9",
					"total": "55.8"
				},
				{
					"mediaName": "河南省南阳市文明办",
					"activeScore": "78",
					"toExposeScore": "60.4",
					"toInteractScore": "35.3",
					"connectScore": "46.4",
					"total": "55"
				},
				{
					"mediaName": "广东省珠海市文明办",
					"activeScore": "70",
					"toExposeScore": "58.6",
					"toInteractScore": "45.4",
					"connectScore": "41.7",
					"total": "53.9"
				},
				{
					"mediaName": "合肥市文明办",
					"activeScore": "72.5",
					"toExposeScore": "66.4",
					"toInteractScore": "40.4",
					"connectScore": "32.3",
					"total": "52.9"
				},
				{
					"mediaName": "内蒙古包头市文明办",
					"activeScore": "71.8",
					"toExposeScore": "59.9",
					"toInteractScore": "38.1",
					"connectScore": "33.7",
					"total": "50.9"
				},
				{
					"mediaName": "陕西省西安市文明办",
					"activeScore": "58",
					"toExposeScore": "48.1",
					"toInteractScore": "32.7",
					"connectScore": "62.5",
					"total": "50.3"
				}
			]
		},
		"h4": {
			"h4_content1": "2018年01月，对全国区级行政区域的精神文明办政务新媒体影响力排名，广东省肇庆市四会市文明办、河南省新乡市卫辉市文明办、宜兴文明办位居前三。",
			"strictTop10": [{
					"mediaName": "广东省肇庆市四会市文明办",
					"activeScore": "72.3",
					"toExposeScore": "60.6",
					"toInteractScore": "42.6",
					"connectScore": "25.8",
					"total": "50.3"
				},
				{
					"mediaName": "河南省新乡市卫辉市文明办",
					"activeScore": "64.1",
					"toExposeScore": "46.3",
					"toInteractScore": "36.7",
					"connectScore": "32.2",
					"total": "44.8"
				},
				{
					"mediaName": "宜兴文明办",
					"activeScore": "61.1",
					"toExposeScore": "35.3",
					"toInteractScore": "37.5",
					"connectScore": "44.8",
					"total": "44.7"
				},
				{
					"mediaName": "诸暨文明办",
					"activeScore": "46.4",
					"toExposeScore": "43.2",
					"toInteractScore": "35.9",
					"connectScore": "37.5",
					"total": "40.8"
				},
				{
					"mediaName": "江阴文明办",
					"activeScore": "64.7",
					"toExposeScore": "37.9",
					"toInteractScore": "30.2",
					"connectScore": "23.7",
					"total": "39.1"
				},
				{
					"mediaName": "广东省佛山市三水区文明办",
					"activeScore": "64.9",
					"toExposeScore": "46.8",
					"toInteractScore": "25.7",
					"connectScore": "17.6",
					"total": "38.8"
				},
				{
					"mediaName": "长沙县文明办",
					"activeScore": "53.6",
					"toExposeScore": "30.1",
					"toInteractScore": "24.1",
					"connectScore": "46.8",
					"total": "38.7"
				},
				{
					"mediaName": "张家港文明办",
					"activeScore": "51.1",
					"toExposeScore": "37.8",
					"toInteractScore": "33.3",
					"connectScore": "30",
					"total": "38.1"
				},
				{
					"mediaName": "山东省威海市乳山市文明办",
					"activeScore": "54.8",
					"toExposeScore": "30.2",
					"toInteractScore": "26.5",
					"connectScore": "30.7",
					"total": "35.6"
				},
				{
					"mediaName": "含山县文明办",
					"activeScore": "51.3",
					"toExposeScore": "27.8",
					"toInteractScore": "19.8",
					"connectScore": "41",
					"total": "35"
				}
			]
		},
		"h5": {
			"h5_p1_content1": "2018年01月，对全国基层行政区域的精神文明办政务新媒体影响力排名，安定门街道文明办、上海市徐汇区虹梅社区文明办、崇文门外街道办事处文明办位居前三。",
			"h5_p2_content1": "更多数据请前往数太奇 · GNI政务新媒体指数监测平台查询: http://gni.idatage.com",
			"baseTop10": [{
					"mediaName": "安定门街道文明办",
					"activeScore": "29",
					"toExposeScore": "3.7",
					"toInteractScore": "1.4",
					"connectScore": "27.4",
					"total": "15.4"
				},
				{
					"mediaName": "上海市徐汇区虹梅社区文明办",
					"activeScore": "17.5",
					"toExposeScore": "25.8",
					"toInteractScore": "17.8",
					"connectScore": "0",
					"total": "15.3"
				},
				{
					"mediaName": "崇文门外街道办事处文明办",
					"activeScore": "20.9",
					"toExposeScore": "10.1",
					"toInteractScore": "2.6",
					"connectScore": "17.1",
					"total": "12.7"
				},
				{
					"mediaName": "广东省惠州市惠城区龙丰街道文明办",
					"activeScore": "28.4",
					"toExposeScore": "1.8",
					"toInteractScore": "0",
					"connectScore": "19.7",
					"total": "12.5"
				},
				{
					"mediaName": "长辛店镇文明办",
					"activeScore": "11.8",
					"toExposeScore": "23.7",
					"toInteractScore": "0",
					"connectScore": "9",
					"total": "11.2"
				},
				{
					"mediaName": "甘肃省白银市会宁县河畔镇文明办",
					"activeScore": "26.9",
					"toExposeScore": "1.1",
					"toInteractScore": "0",
					"connectScore": "14",
					"total": "10.5"
				},
				{
					"mediaName": "东直门街道文明办",
					"activeScore": "15.7",
					"toExposeScore": "4.1",
					"toInteractScore": "0",
					"connectScore": "21.5",
					"total": "10.3"
				},
				{
					"mediaName": "经济技术开发区文明办",
					"activeScore": "13.5",
					"toExposeScore": "3.3",
					"toInteractScore": "0",
					"connectScore": "12",
					"total": "7.2"
				},
				{
					"mediaName": "河南省新乡市凤凰山文明办",
					"activeScore": "21.2",
					"toExposeScore": "1.4",
					"toInteractScore": "0",
					"connectScore": "3.9",
					"total": "6.6"
				},
				{
					"mediaName": "河南省许昌市建安区文明办",
					"activeScore": "12.2",
					"toExposeScore": "3.7",
					"toInteractScore": "0",
					"connectScore": "3.9",
					"total": "4.9"
				}
			]
		}
	}
}
```

`response` 返回提示信息

```
成功：

{
    "msPath": "https://narnia.oss-cn-beijing.aliyuncs.com/stq/20180228181016636/GNI%E6%94%BF%E5%8A%A1%E6%96%B0%E5%AA%92%E4%BD%93%E6%8C%87%E6%95%B0%E5%88%86%E6%9E%90%E6%8A%A5%E5%91%8A%EF%BC%882018%E5%B9%B401%E6%9C%88%EF%BC%89.docx?Expires=1521640004&OSSAccessKeyId=LTAIARWAKGUIqkn6&Signature=f5h%2Btexh9za4bIdcGOmnaDhizW4%3D",
    "message": "任务执行成功"
}

失败：1、检查输入body体 jsonData 是否包含。2、检查 value 是否含有 null 值。

{
    "msPath": "",
    "message": "任务执行错误"
}
```



