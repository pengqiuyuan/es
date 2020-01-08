---
description: 问卷表
---

# 问卷表

`问卷表 wj_surveys`

| 字段含义 | 字段名称 | 数据类型 |
| :--- | :--- | :--- |
| 问卷ID | id |  |
| 标题 | title |  |
| 副标题 | subtitle |  |
| 欢迎语 | welcome |  |
| 结束语 | closing |  |
| 页头 | header |  |
| 页脚 | footer |  |
| 描述 | description |  |
| 状态 | status |  |
| 标识符 | identifier |  |
| 星标 | is\_star |  |
| 投放渠道 | channel |  |
| 分页显示数组 | pages | 数组 |
| 逻辑数组 | logics | 数组 |

`问卷吧 surveys`

```text
{ 
    "_id" : ObjectId("566e6cdbeb0e5bf0cb000008"), 
    "_type" : "Survey", 
    "access_control_setting" : {
        "times_for_one_computer" : NumberInt(-1), 
        "has_captcha" : false, 
        "ip_restrictions" : [

        ], 
        "password_control" : {
            "password_type" : NumberInt(-1), 
            "single_password" : "", 
            "password_list" : [

            ], 
            "username_password_list" : [

            ]
        }
    }, 
    "browser_extension_promotable" : false, 
    "browser_extension_promote_info" : {
        "reward_scheme_id" : "", 
        "filters" : [
            {
                "key_words" : "[\"\"]", 
                "url" : ""
            }
        ]
    }, 
    "closing" : "调查问卷结束语", 
    "created_at" : ISODate("2015-12-14T07:16:43.350+0000"), 
    "delta" : true, 
    "description" : "调查问卷描述", 
    "email_promotable" : true, 
    "email_promote_info" : {
        "email_amount" : "500", 
        "reward_scheme_id" : "56720965eb0e5b331300000b", 
        "promote_email_count" : NumberInt(9500)
    }, 
    "filters" : [

    ], 
    "footer" : "", 
    "header" : "", 
    "is_star" : false, 
    "logic_control" : [
        {
            "rule_type" : NumberInt(2), 
            "conditions" : [
                {
                    "question_id" : "566e7251eb0e5bf0cb00001a", 
                    "answer" : [
                        NumberLong(1854666238619514)
                    ], 
                    "fuzzy" : false
                }
            ], 
            "result" : [
                "566e7278eb0e5ba29a00001c", 
                "566e72c9eb0e5be452000003", 
                "566e72eaeb0e5bf0cb00001c", 
                "566e734ceb0e5ba29a00001e"
            ]
        }, 
        {
            "rule_type" : NumberInt(2), 
            "conditions" : [
                {
                    "question_id" : "566e7251eb0e5bf0cb00001a", 
                    "answer" : [
                        NumberLong(380670120608105)
                    ], 
                    "fuzzy" : false
                }
            ], 
            "result" : [
                "566e7278eb0e5ba29a00001c", 
                "566e72c9eb0e5be452000003", 
                "566e72eaeb0e5bf0cb00001c", 
                "566e734ceb0e5ba29a00001e", 
                "566e736aeb0e5ba29a00001f"
            ]
        }, 
        {
            "rule_type" : NumberInt(2), 
            "conditions" : [
                {
                    "question_id" : "566e739deb0e5ba29a000021", 
                    "answer" : [
                        NumberLong(8547245017589994)
                    ], 
                    "fuzzy" : false
                }
            ], 
            "result" : [
                "566e73d4eb0e5bf0cb00001d", 
                "566e73f3eb0e5ba29a000022", 
                "566e740aeb0e5ba29a000023", 
                "566e742feb0e5be452000004", 
                "566e745feb0e5ba29a000024"
            ]
        }, 
        {
            "rule_type" : NumberInt(2), 
            "conditions" : [
                {
                    "question_id" : "566e74b9eb0e5ba29a000025", 
                    "answer" : [
                        NumberLong(7825620020073737)
                    ], 
                    "fuzzy" : false
                }
            ], 
            "result" : [
                "566e74dceb0e5be452000006", 
                "566e7576eb0e5b956e000002"
            ]
        }, 
        {
            "rule_type" : NumberInt(2), 
            "conditions" : [
                {
                    "question_id" : "566e75deeb0e5be452000007", 
                    "answer" : [
                        NumberLong(20869101363300), 
                        NumberLong(5650176260594513)
                    ], 
                    "fuzzy" : true
                }
            ], 
            "result" : [
                "566e7600eb0e5b956e000005", 
                "566e761deb0e5b956e000006"
            ]
        }, 
        {
            "rule_type" : NumberInt(0), 
            "conditions" : [
                {
                    "question_id" : "566e6d02eb0e5ba29a00000a", 
                    "answer" : [
                        NumberLong(6864711565642462), 
                        NumberLong(1135592729641177), 
                        NumberLong(2291585636031517), 
                        NumberLong(18651376635410504)
                    ], 
                    "fuzzy" : true
                }
            ], 
            "result" : null
        }, 
        {
            "rule_type" : NumberInt(0), 
            "conditions" : [
                {
                    "question_id" : "566e6d25eb0e5b17de000009", 
                    "answer" : [
                        NumberLong(1000963831277897), 
                        NumberLong(9090675728955636), 
                        NumberLong(9905365176865078), 
                        NumberLong(19760159837217480)
                    ], 
                    "fuzzy" : true
                }
            ], 
            "result" : null
        }
    ], 
    "max_num_per_ip" : NumberInt(10), 
    "open_red_pack" : true, 
    "pages" : [
        {
            "name" : "new page", 
            "questions" : [
                "566e6d02eb0e5ba29a00000a", 
                "566e6d25eb0e5b17de000009", 
                "566e6d60eb0e5ba29a00000b", 
                "566e6d9beb0e5b17de00000c"
            ]
        }, 
        {
            "name" : "new page", 
            "questions" : [
                "566e6dc2eb0e5b17de00000d", 
                "566e6df3eb0e5b17de00000f", 
                "566e6e4beb0e5b17de000010"
            ]
        }, 
        {
            "name" : "new page", 
            "questions" : [
                "566e6e87eb0e5b17de000012", 
                "566e6eafeb0e5b17de000013", 
                "566e6f7ceb0e5bf0cb00000d", 
                "566e6f9aeb0e5ba29a00000d"
            ]
        }, 
        {
            "name" : "new page", 
            "questions" : [
                "566e6fc2eb0e5b17de000015", 
                "566e6fd9eb0e5b17de000016", 
                "566e701beb0e5b17de000019", 
                "566e7040eb0e5ba29a000012", 
                "566e7058eb0e5bf0cb00000f"
            ]
        }, 
        {
            "name" : "new page", 
            "questions" : [
                "566e706eeb0e5ba29a000014", 
                "566e7099eb0e5ba29a000015", 
                "566e70deeb0e5bf0cb000012", 
                "566e70f2eb0e5ba29a000016"
            ]
        }, 
        {
            "name" : "new page", 
            "questions" : [
                "566e7111eb0e5ba29a000017", 
                "566e714aeb0e5ba29a000018", 
                "566e7164eb0e5ba29a000019", 
                "566e7197eb0e5bf0cb000015", 
                "566e71aceb0e5bf0cb000016"
            ]
        }, 
        {
            "name" : "new page", 
            "questions" : [
                "566e71c9eb0e5bf0cb000018", 
                "566e7251eb0e5bf0cb00001a", 
                "566e7278eb0e5ba29a00001c", 
                "566e72c9eb0e5be452000003"
            ]
        }, 
        {
            "name" : "new page", 
            "questions" : [
                "566e72eaeb0e5bf0cb00001c", 
                "566e734ceb0e5ba29a00001e", 
                "566e736aeb0e5ba29a00001f"
            ]
        }, 
        {
            "name" : "new page", 
            "questions" : [
                "566e737feb0e5ba29a000020", 
                "566e739deb0e5ba29a000021", 
                "566e73d4eb0e5bf0cb00001d", 
                "566e73f3eb0e5ba29a000022"
            ]
        }, 
        {
            "name" : "new page", 
            "questions" : [
                "566e740aeb0e5ba29a000023", 
                "566e742feb0e5be452000004", 
                "566e745feb0e5ba29a000024", 
                "566e747beb0e5bf0cb00001e"
            ]
        }, 
        {
            "name" : "new page", 
            "questions" : [
                "566e74b9eb0e5ba29a000025", 
                "566e74dceb0e5be452000006", 
                "566e7576eb0e5b956e000002"
            ]
        }, 
        {
            "name" : "new page", 
            "questions" : [
                "566e758feb0e5b956e000004"
            ]
        }, 
        {
            "name" : "new page", 
            "questions" : [
                "566e75deeb0e5be452000007", 
                "566e7600eb0e5b956e000005", 
                "566e761deb0e5b956e000006", 
                "566e764feb0e5be45200000b"
            ]
        }, 
        {
            "name" : "new page", 
            "questions" : [
                "566e7669eb0e5be45200000c", 
                "566e768deb0e5ba29a000028", 
                "566e76a1eb0e5be45200000e", 
                "566e76bceb0e5ba29a000029"
            ]
        }, 
        {
            "name" : "new page", 
            "questions" : [
                "566e76cfeb0e5be45200000f", 
                "566e76e4eb0e5be452000010", 
                "566e7705eb0e5ba29a00002b", 
                "566e772deb0e5ba29a00002c"
            ]
        }, 
        {
            "name" : "new page", 
            "questions" : [
                "566e7744eb0e5ba29a00002d", 
                "566e775feb0e5b956e000007", 
                "566e77d6eb0e5ba29a00002e", 
                "566e7801eb0e5ba29a00002f"
            ]
        }, 
        {
            "name" : "new page", 
            "questions" : [
                "566e7820eb0e5ba29a000030", 
                "566e8129eb0e5bcb91000006"
            ]
        }
    ], 
    "publish_result" : false, 
    "quality_control_questions_ids" : [

    ], 
    "quality_control_questions_type" : NumberInt(0), 
    "quillme_hot" : false, 
    "quillme_promotable" : true, 
    "quillme_promote_info" : {
        "reward_scheme_id" : "56720965eb0e5b331300000b"
    }, 
    "quillme_promote_reward_type" : NumberInt(32), 
    "quota" : {
        "rules" : [
            {
                "conditions" : [
                    {
                        "condition_type" : NumberInt(1), 
                        "name" : "566e6d02eb0e5ba29a00000a", 
                        "value" : [
                            NumberLong(6864711565642462)
                        ], 
                        "fuzzy" : false
                    }
                ], 
                "amount" : NumberInt(50), 
                "finished_count" : NumberInt(160), 
                "submitted_count" : NumberInt(160)
            }, 
            {
                "amount" : NumberInt(200), 
                "conditions" : [
                    {
                        "condition_type" : NumberInt(1), 
                        "name" : "566e6d02eb0e5ba29a00000a", 
                        "value" : [
                            NumberLong(1135592729641177)
                        ], 
                        "fuzzy" : false
                    }
                ], 
                "finished_count" : NumberInt(369), 
                "submitted_count" : NumberInt(369)
            }, 
            {
                "amount" : NumberInt(250), 
                "conditions" : [
                    {
                        "condition_type" : NumberInt(1), 
                        "name" : "566e6d02eb0e5ba29a00000a", 
                        "value" : [
                            NumberLong(2291585636031517)
                        ], 
                        "fuzzy" : false
                    }
                ], 
                "finished_count" : NumberInt(293), 
                "submitted_count" : NumberInt(293)
            }, 
            {
                "amount" : NumberInt(250), 
                "conditions" : [
                    {
                        "condition_type" : NumberInt(1), 
                        "name" : "566e6d02eb0e5ba29a00000a", 
                        "value" : [
                            NumberLong(4259473617868921)
                        ], 
                        "fuzzy" : false
                    }
                ], 
                "finished_count" : NumberInt(249), 
                "submitted_count" : NumberInt(249)
            }, 
            {
                "amount" : NumberInt(250), 
                "conditions" : [
                    {
                        "condition_type" : NumberInt(1), 
                        "name" : "566e6d02eb0e5ba29a00000a", 
                        "value" : [
                            NumberLong(18651376635410504)
                        ], 
                        "fuzzy" : false
                    }
                ], 
                "finished_count" : NumberInt(290), 
                "submitted_count" : NumberInt(290)
            }, 
            {
                "amount" : NumberInt(50), 
                "conditions" : [
                    {
                        "condition_type" : NumberInt(1), 
                        "name" : "566e6d25eb0e5b17de000009", 
                        "value" : [
                            NumberLong(3397086550866415)
                        ], 
                        "fuzzy" : false
                    }
                ], 
                "finished_count" : NumberInt(31), 
                "submitted_count" : NumberInt(31)
            }, 
            {
                "amount" : NumberInt(150), 
                "conditions" : [
                    {
                        "condition_type" : NumberInt(1), 
                        "name" : "566e6d25eb0e5b17de000009", 
                        "value" : [
                            NumberLong(1000963831277897)
                        ], 
                        "fuzzy" : false
                    }
                ], 
                "finished_count" : NumberInt(148), 
                "submitted_count" : NumberInt(148)
            }, 
            {
                "amount" : NumberInt(200), 
                "conditions" : [
                    {
                        "condition_type" : NumberInt(1), 
                        "name" : "566e6d25eb0e5b17de000009", 
                        "value" : [
                            NumberLong(9090675728955636)
                        ], 
                        "fuzzy" : false
                    }
                ], 
                "finished_count" : NumberInt(283), 
                "submitted_count" : NumberInt(283)
            }, 
            {
                "amount" : NumberInt(300), 
                "conditions" : [
                    {
                        "condition_type" : NumberInt(1), 
                        "name" : "566e6d25eb0e5b17de000009", 
                        "value" : [
                            NumberLong(9905365176865078)
                        ], 
                        "fuzzy" : false
                    }
                ], 
                "finished_count" : NumberInt(416), 
                "submitted_count" : NumberInt(416)
            }, 
            {
                "amount" : NumberInt(300), 
                "conditions" : [
                    {
                        "condition_type" : NumberInt(1), 
                        "name" : "566e6d25eb0e5b17de000009", 
                        "value" : [
                            NumberLong(19760159837217480)
                        ], 
                        "fuzzy" : false
                    }
                ], 
                "finished_count" : NumberInt(483), 
                "submitted_count" : NumberInt(483)
            }
        ], 
        "is_exclusive" : true, 
        "quota_satisfied" : false, 
        "finished_count" : NumberInt(1361), 
        "submitted_count" : NumberInt(1361)
    }, 
    "sample_attributes_for_promote" : [

    ], 
    "sms_promotable" : false, 
    "sms_promote_info" : {
        "sms_amount" : "0", 
        "reward_scheme_id" : "", 
        "promote_sms_count" : NumberInt(0)
    }, 
    "spread_point" : NumberInt(0), 
    "star" : false, 
    "status" : NumberInt(1), 
    "style_setting" : {
        "style_sheet_name" : "", 
        "has_progress_bar" : true, 
        "has_question_number" : true, 
        "is_one_question_per_page" : false, 
        "has_advertisement" : true, 
        "has_oopsdata_link" : true, 
        "redirect_link" : "", 
        "allow_pageup" : false, 
        "allow_replay" : false, 
        "show_estimated_time" : true
    }, 
    "subtitle" : "", 
    "title" : "2016年的消费会更“给力”吗？", 
    "updated_at" : ISODate("2015-12-22T05:26:18.832+0000"), 
    "user_id" : ObjectId("519c2c58eb0e5b6355000034"), 
    "wechart_promotable" : true, 
    "wechart_promote_info" : {
        "reward_scheme_id" : "56720965eb0e5b331300000b"
    }, 
    "weibo_promotable" : false, 
    "weibo_promote_info" : {
        "text" : "", 
        "image" : "", 
        "video" : "", 
        "audio" : "", 
        "reward_scheme_id" : ""
    }, 
    "welcome" : "<p class=\"MsoNormal\">\n\t亲爱的朋友：\n</p>\n<p class=\"MsoNormal\">\n\t<span>&nbsp;&nbsp;&nbsp;\n2016</span>年是“十三五”规划的开启之年，这让我们对新的一年充满了期待。<span>2016</span>年，您认为消费会更“给力”吗？您的回答，将对我们研究<span>2016</span>年消费趋势具有重要的参考意义。\n</p>\n<p class=\"MsoNormal\" style=\"text-indent:21.75pt;\">\n\t《小康》杂志社收集您的真实想法，也将如实反映您的真实意愿。\n</p>\n<p class=\"MsoNormal\" style=\"text-indent:21.75pt;\">\n\t感谢您的参与！\n</p>\n<p class=\"MsoNormal\" align=\"right\" style=\"text-align:right;text-indent:21.75pt;\">\n\t求是《小康》杂志社\n</p>\n<p class=\"MsoNormal\" align=\"right\" style=\"text-align:right;text-indent:21.75pt;\">\n\t<span>2015</span>年<span>12</span>月\n</p>"
}
```

