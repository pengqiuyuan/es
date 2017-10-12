```
curl -XPUT http://127.0.0.1:9222/cibao_index

curl -XPUT http://127.0.0.1:9222/_template/cibao_index -d '
{
  "template": "cibao_index*",
  "settings": {
    "refresh_interval": "60s",
    "number_of_replicas": "1",
    "number_of_shards": "15"
  },
  "mappings": {
    "_default_": {
      "_all": {
        "enabled": true
      },
      "_source": {
        "enabled": true
      },
      "dynamic_templates": [
        {
          "message_field": {
            "match": "message",
            "match_mapping_type": "string",
            "mapping": {
              "type": "text"
            }
          }
        },
        {
          "string_fields": {
            "match": "*",
            "match_mapping_type": "string",
            "mapping": {
              "type": "keyword"
            }
          }
        },
        {
          "double_fields": {
            "match": "*",
            "match_mapping_type": "double",
            "mapping": {
              "type": "double"
            }
          }
        },
        {
          "byte_fields": {
            "match": "*",
            "match_mapping_type": "byte",
            "mapping": {
              "type": "byte"
            }
          }
        },
        {
          "short_fields": {
            "match": "*",
            "match_mapping_type": "short",
            "mapping": {
              "type": "short"
            }
          }
        },
        {
          "integer_fields": {
            "match": "*",
            "match_mapping_type": "integer",
            "mapping": {
              "type": "integer"
            }
          }
        },
        {
          "long_fields": {
            "match": "*",
            "match_mapping_type": "long",
            "mapping": {
              "type": "long"
            }
          }
        },
        {
          "date_fields": {
            "match": "*",
            "match_mapping_type": "date",
            "mapping": {
              "type": "date"
            }
          }
        }
      ],
      "properties": {
        "startDate": {
          "format": "strict_date_optional_time||epoch_millis",
          "type": "date"
        },
        "endDate": {
          "format": "strict_date_optional_time||epoch_millis",
          "type": "date"
        },
        "updateDate": {
          "format": "strict_date_optional_time||epoch_millis",
          "type": "date"
        },
        "startDateString": {
          "type": "keyword"
        },
        "endDateString": {
          "type": "keyword"
        },
        "updateDateString": {
          "type": "keyword"
        },
        "keywords": {
          "type": "keyword"
        },
        "source": {
          "type": "keyword",
          "ignore_above": 256
        },
        "weibo_volume": {
          "type": "long"
        },
        "weibo_actualVolume": {
          "type": "integer"
        },
        "weibo_exposure": {
          "type": "long"
        },
        "weibo_interactive": {
          "type": "long"
        },
        "weibo_forwardDepth": {
          "type": "integer"
        }

        ,
        "weixin_volume": {
          "type": "long"
        },
        "weixin_actualVolume": {
          "type": "integer"
        },
        "weixin_readCount": {
          "type": "long"
        },
        "weixin_upCount": {
          "type": "long"
        },
        "weixin_readArticleCount": {
          "type": "long"
        }

        ,
        "tieba_recoveryCount": {
          "type": "long"
        }

        ,
        "baidunews_volume": {
          "type": "long"
        }

        ,
        "zhihuquestions_questionsCount": {
          "type": "integer"
        },
        "zhihuquestions_followCount": {
          "type": "integer"
        },
        "zhihuquestions_seeCount": {
          "type": "long"
        },
        "zhihuquestions_answerCount": {
          "type": "integer"
        }

        ,
        "tianya_clicksCount": {
          "type": "long"
        },
        "tianya_answerCount": {
          "type": "integer"
        }

        ,
        "toutiao_followCount": {
          "type": "integer"
        },
        "toutiao_fansCount": {
          "type": "integer"
        },
        "toutiao_readCount": {
          "type": "integer"
        },
        "toutiao_commentCount": {
          "type": "integer"
        },
        "toutiao_upCount": {
          "type": "integer"
        },
        "toutiao_stepCount": {
          "type": "integer"
        }

        ,
        "zixun_upCount": {
          "type": "integer"
        },
        "zixun_collectionCount": {
          "type": "integer"
        },
        "zixun_commentCount": {
          "type": "integer"
        },
        "zixun_seeCount": {
          "type": "integer"
        }

      }
    }
  }
}'
```

```
    static{
        weiboList.add("weibo_volume");//声量
        weiboList.add("weibo_actualVolume");//实际声量
        weiboList.add("weibo_exposure");//曝光量
        weiboList.add("weibo_interactive");//互动量
        weiboList.add("weibo_forwardDepth");//转发深度
        weiboList.add("weibo_account");//帐号提及量
        
        weixinList.add("weixin_volume");//总文章量
        weixinList.add("weixin_actualVolume");//实际文章量
        weixinList.add("weixin_readCount");//总阅读数
        weixinList.add("weixin_upCount");//总点赞量
        weixinList.add("weixin_readArticleCount");//有阅读的文章数量
        weixinList.add("weixin_account");//帐号提及量

        tiebaList.add("tieba_recoveryCount");//回复数
        tiebaList.add("tieba_actualVolume");//实际声量
        tiebaList.add("tieba_account");//帐号提及量

        baidunewsList.add("baidunews_volume");//声量
        baidunewsList.add("baidunews_actualVolume");//实际声量
        baidunewsList.add("baidunews_account");//帐号提及量

        zhihuquestionsList.add("zhihuquestions_questionsCount");//问题数
        zhihuquestionsList.add("zhihuquestions_followCount");//关注人数
        zhihuquestionsList.add("zhihuquestions_seeCount");//查看人数
        zhihuquestionsList.add("zhihuquestions_answerCount");//回答人数
        zhihuquestionsList.add("zhihuquestions_actualVolume");//实际声量
        zhihuquestionsList.add("zhihuquestions_account");//帐号提及量

        tianyaList.add("tianya_clicksCount");//帖子点击数
        tianyaList.add("tianya_answerCount");//贴子回复数
        tianyaList.add("tianya_actualVolume");//实际声量
        tianyaList.add("tianya_account");//帐号提及量

        toutiaoList.add("toutiao_followCount");//关注量
        toutiaoList.add("toutiao_fansCount");//粉丝量
        toutiaoList.add("toutiao_readCount");//阅读量
        toutiaoList.add("toutiao_commentCount");//评论量
        toutiaoList.add("toutiao_upCount");//点赞量
        toutiaoList.add("toutiao_stepCount");//踩量
        toutiaoList.add("toutiao_actualVolume");//实际声量
        toutiaoList.add("toutiao_account");//帐号提及量

        zixunList.add("zixun_upCount");//点赞量
        zixunList.add("zixun_collectionCount");//收藏量
        zixunList.add("zixun_commentCount");//评论量
        zixunList.add("zixun_seeCount");//浏览量
        zixunList.add("zixun_actualVolume");//实际声量
        zixunList.add("zixun_account");//帐号提及量
    }
```



