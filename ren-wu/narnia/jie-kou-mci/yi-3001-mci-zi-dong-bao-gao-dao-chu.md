**一**、MCI 自动报告导出

`POST` `http://127.0.0.1/stq/api/v1/poi/downMciReportByJsonDate`

`HEADERS`：`"Content-Type" => "application/json"`

`参数说明`：

```
jsonData 必填项，json字符串。
```

`BODY` 体：

```
{
    "jsonData": {
        "titleDate": "2017年12月",
        "summary": "根据媒体融合传播效果指数（MCI）监测系统数据显示，【电视】媒体融合传播效果指数整体优于【报纸】媒体。其中，【央视】融合传播效果指数（MCI）达52.0，位居各类媒体首位。【中央电视台新闻频道】、【人民日报】、【中央电视台财经频道】位列11月媒体融合传播效果指数（MCI）综合排名前三名。",
        "h1": {
            "h1_p1_content1": "2017年11月，【电视】媒体融合传播效果指数整体优于【报纸】媒体。其中，【央视】融合传播效果指数（MCI）达52.0，位居各类媒体首位。",
            "allType": [
                {
                    "rank": "1",
                    "mediaType": "电视-央视",
                    "totalInType": "94.2",
                    "highestTotalInType": "94.2",
                    "lowestTotalInType": "94.2"
                },
                {
                    "rank": "1",
                    "mediaType": "电视-央视",
                    "totalInType": "94.2",
                    "highestTotalInType": "94.2",
                    "lowestTotalInType": "94.2"
                }
            ],
            "h1_p2_content1": "11月，各类媒体融合传播效果指数（MCI）综合排名中，【中央电视台新闻频道】、【人民日报】、【中央电视台财经频道】位居前三。其中，位居首位的【中央电视台新闻频道】MCI得分为94.2。",
            "totalTop10": [
                {
                    "rank": "1",
                    "mediaName": "中央电视台新闻频道",
                    "total": "94.2",
                    "mediaType": "电视-央视"
                },
                {
                    "rank": "1",
                    "mediaName": "中央电视台新闻频道",
                    "total": "94.2",
                    "mediaType": "电视-央视"
                }
            ]
        },
        "h2": {
            "h2_content1": "2017年11月，电视媒体融合传播效果指数（MCI）为39.5，低于该指数的媒体共有28家。媒体融合传播效果指数最高的3家媒体为【中央电视台新闻频道】、【中央电视台财经频道】、【中央电视台中文国际频道】，其中位居首位的【中央电视台新闻频道】MCI得分为94.2",
            "h2_p1_content1": "2017年11月，央视融合传播效果指数（MCI）为52.0，与电视媒体MCI相比高出31.6%。央视中低于电视媒体MCI的共有5家媒体。央视融合传播效果指数最高的3家媒体是【新闻频道】、【财经频道】、【中文国际频道】，其中位居首位的【新闻频道】MCI得分为94.2。",
            "yangshiTop10": [
                {
                    "rank": "1",
                    "mediaName": "中央电视台新闻频道",
                    "spread": "88.7",
                    "leadPower": "88.7",
                    "influence": "88.7",
                    "trust": "88.7",
                    "total": "88.7"
                },
                {
                    "rank": "1",
                    "mediaName": "中央电视台新闻频道",
                    "spread": "88.7",
                    "leadPower": "88.7",
                    "influence": "88.7",
                    "trust": "88.7",
                    "total": "88.7"
                }
            ],
            "h2_p2_content1": "2017年11月，卫视融合传播效果指数（MCI）为33.3，与电视媒体MCI相比低了15.7%。卫视中低于电视媒体MCI的共有22家媒体。卫视融合传播效果指数最高的3家媒体是【湖南卫视】、【山东卫视】、【河南卫视】，其中位居首位的【湖南卫视】MCI得分为60.6。",
            "weishiTop10": [
                {
                    "rank": "1",
                    "mediaName": "湖南卫视",
                    "spread": "80.4",
                    "leadPower": "80.4",
                    "influence": "80.4",
                    "trust": "80.4",
                    "total": "80.4"
                },
                {
                    "rank": "1",
                    "mediaName": "湖南卫视",
                    "spread": "80.4",
                    "leadPower": "80.4",
                    "influence": "80.4",
                    "trust": "80.4",
                    "total": "80.4"
                }
            ]
        },
        "h3": {
            "h3_content1": "2017年11月，报纸媒体融合传播效果指数（MCI）为28.1，低于该指数的媒体共有117家。媒体融合传播效果指数最高的3家媒体为【人民日报】、【参考消息】、【环球时报】，其中，位居首位的【人民日报】MCI得分为86.6。",
            "h3_p1_content1": "2017年11月，党政机关报融合传播效果指数（MCI）为52.0，与报纸媒体MCI相比高出31.6%。党政机关报中低于报纸媒体MCI的共有5家媒体。党政机关报融合传播效果指数最高的3家媒体是【新闻频道】、【财经频道】、【中文国际频道】，其中位居首位的【新闻频道】MCI得分为94.2。",
            "dangbaojiguanbaoTop10": [
                {
                    "rank": "1",
                    "mediaName": "中央电视台新闻频道",
                    "spread": "88.7",
                    "leadPower": "88.7",
                    "influence": "88.7",
                    "trust": "88.7",
                    "total": "88.7"
                },
                {
                    "rank": "1",
                    "mediaName": "中央电视台新闻频道",
                    "spread": "88.7",
                    "leadPower": "88.7",
                    "influence": "88.7",
                    "trust": "88.7",
                    "total": "88.7"
                }
            ],
            "h3_p2_content1": "2017年11月，都市报融合传播效果指数（MCI）为52.0，与报纸媒体MCI相比高出31.6%。都市报中低于报纸媒体MCI的共有5家媒体。都市报融合传播效果指数最高的3家媒体是【新闻频道】、【财经频道】、【中文国际频道】，其中位居首位的【新闻频道】MCI得分为94.2。",
            "dushibaoTop10": [
                {
                    "rank": "1",
                    "mediaName": "中央电视台新闻频道",
                    "spread": "88.5",
                    "leadPower": "88.5",
                    "influence": "88.5",
                    "trust": "88.5",
                    "total": "88.5"
                },
                {
                    "rank": "1",
                    "mediaName": "中央电视台新闻频道",
                    "spread": "88.5",
                    "leadPower": "88.5",
                    "influence": "88.5",
                    "trust": "88.5",
                    "total": "88.5"
                }
            ],
            "h3_p3_content1": "2017年11月，行业报融合传播效果指数（MCI）为52.0，与报纸媒体MCI相比高出31.6%。行业报中低于报纸媒体MCI的共有5家媒体。行业报融合传播效果指数最高的3家媒体是【新闻频道】、【财经频道】、【中文国际频道】，其中位居首位的【新闻频道】MCI得分为94.2。",
            "hangyebaoTop10": [
                {
                    "rank": "1",
                    "mediaName": "中央电视台新闻频道",
                    "spread": "89.8",
                    "leadPower": "89.8",
                    "influence": "89.8",
                    "trust": "89.8",
                    "total": "89.8"
                },
                {
                    "rank": "1",
                    "mediaName": "中央电视台新闻频道",
                    "spread": "89.8",
                    "leadPower": "89.8",
                    "influence": "89.8",
                    "trust": "89.8",
                    "total": "89.8"
                }
            ]
        },
        "h4": {
            "h4_content1": "2017年11月，报纸媒体融合传播效果指数（MCI）为28.1，低于该指数的媒体共有117家。媒体融合传播效果指数最高的3家媒体为【人民日报】、【参考消息】、【环球时报】，其中，位居首位的【人民日报】MCI得分为86.6。",
            "h4_p1_content1": "2017年11月，党政机关报融合传播效果指数（MCI）为52.0，与报纸媒体MCI相比高出31.6%。党政机关报中低于报纸媒体MCI的共有5家媒体。党政机关报融合传播效果指数最高的3家媒体是【新闻频道】、【财经频道】、【中文国际频道】，其中位居首位的【新闻频道】MCI得分为94.2。",
            "centerBroadTop10": [
                {
                    "rank": "1",
                    "mediaName": "centerBroadTop10",
                    "spread": "88.7",
                    "leadPower": "88.7",
                    "influence": "88.7",
                    "trust": "88.7",
                    "total": "88.7"
                },
                {
                    "rank": "1",
                    "mediaName": "centerBroadTop10",
                    "spread": "88.7",
                    "leadPower": "88.7",
                    "influence": "88.7",
                    "trust": "88.7",
                    "total": "88.7"
                }
            ],
            "h4_p2_content1": "2017年11月，都市报融合传播效果指数（MCI）为52.0，与报纸媒体MCI相比高出31.6%。都市报中低于报纸媒体MCI的共有5家媒体。都市报融合传播效果指数最高的3家媒体是【新闻频道】、【财经频道】、【中文国际频道】，其中位居首位的【新闻频道】MCI得分为94.2。",
            "privinceBroadTop10": [
                {
                    "rank": "1",
                    "mediaName": "privinceBroadTop10",
                    "spread": "88.5",
                    "leadPower": "88.5",
                    "influence": "88.5",
                    "trust": "88.5",
                    "total": "88.5"
                },
                {
                    "rank": "1",
                    "mediaName": "privinceBroadTop10",
                    "spread": "88.5",
                    "leadPower": "88.5",
                    "influence": "88.5",
                    "trust": "88.5",
                    "total": "88.5"
                }
            ],
            "h4_p3_content1": "2017年11月，行业报融合传播效果指数（MCI）为52.0，与报纸媒体MCI相比高出31.6%。行业报中低于报纸媒体MCI的共有5家媒体。行业报融合传播效果指数最高的3家媒体是【新闻频道】、【财经频道】、【中文国际频道】，其中位居首位的【新闻频道】MCI得分为94.2。",
            "cityBroadTop10": [
                {
                    "rank": "1",
                    "mediaName": "cityBroadTop10",
                    "spread": "89.8",
                    "leadPower": "89.8",
                    "influence": "89.8",
                    "trust": "89.8",
                    "total": "89.8"
                },
                {
                    "rank": "1",
                    "mediaName": "cityBroadTop10",
                    "spread": "89.8",
                    "leadPower": "89.8",
                    "influence": "89.8",
                    "trust": "89.8",
                    "total": "89.8"
                }
            ]
        },
        "h5": {
            "h5_p1_content1": "2017年11月，【电视】媒体融合传播效果指数整体优于【报纸】媒体。其中，【央视】融合传播效果指数（MCI）达52.0，位居各类媒体首位。",
            "tongxunsheTop2": [
                {
                    "rank": "1",
                    "mediaName": "tongxunsheTop2",
                    "spread": "89.8",
                    "leadPower": "89.8",
                    "influence": "89.8",
                    "trust": "89.8",
                    "total": "89.8"
                },
                {
                    "rank": "1",
                    "mediaName": "tongxunsheTop2",
                    "spread": "89.8",
                    "leadPower": "89.8",
                    "influence": "89.8",
                    "trust": "89.8",
                    "total": "89.8"
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
    "msPath": "https://narnia.oss-cn-beijing.aliyuncs.com/MCI%E4%B8%AD%E5%9B%BD%E5%AA%92%E4%BD%93%E8%9E%8D%E5%90%88%E4%BC%A0%E6%92%AD%E6%95%88%E6%9E%9C%E6%8C%87%E6%95%B0%E5%88%86%E6%9E%90%E6%8A%A5%E5%91%8A%EF%BC%882017%E5%B9%B412%E6%9C%88%EF%BC%89.docx?Expires=1516867676&OSSAccessKeyId=LTAIARWAKGUIqkn6&Signature=W5emkfLYcd3QXEQId%2BbZn7vLLGc%3D",
    "message": "任务执行成功"
}

失败：1、检查输入body体 jsonData 是否包含。2、检查 value 是否含有 null 值。

{
    "msPath": "",
    "message": "任务执行错误"
}
```



