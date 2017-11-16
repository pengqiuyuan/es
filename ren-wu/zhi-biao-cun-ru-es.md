```
curl -XPUT http://127.0.0.1:9200/cibao_index

curl -XPUT http://127.0.0.1:9200/_template/cibao_index -d '
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
          "type": "double"
        },
        "weibo_actualVolume": {
          "type": "float"
        },
        "weibo_exposure": {
          "type": "double"
        },
        "weibo_interactive": {
          "type": "double"
        },
        "weibo_forwardDepth": {
          "type": "float"
        },
        "weibo_account": {
          "type": "float"
        },
        "weibo_commentCount": {
          "type": "double"
        },
        "weibo_upCount": {
          "type": "double"
        },
        "weibo_repostCount": {
          "type": "double"
        }

        ,
        "weixin_volume": {
          "type": "double"
        },
        "weixin_actualVolume": {
          "type": "float"
        },
        "weixin_readCount": {
          "type": "double"
        },
        "weixin_upCount": {
          "type": "double"
        },
        "weixin_readArticleCount": {
          "type": "double"
        },
        "weixin_account": {
          "type": "float"
        }

        ,
        "tieba_recoveryCount": {
          "type": "double"
        },
        "tieba_actualVolume": {
          "type": "float"
        },
        "tieba_account": {
          "type": "float"
        }

        ,
        "tieba_actualVolume": {
          "type": "float"
        },
        "tieba_account": {
          "type": "float"
        }

        ,
        "zhihuquestions_questionsCount": {
          "type": "float"
        },
        "zhihuquestions_followCount": {
          "type": "float"
        },
        "zhihuquestions_seeCount": {
          "type": "double"
        },
        "zhihuquestions_answerCount": {
          "type": "float"
        },
        "zhihuquestions_actualVolume": {
          "type": "float"
        },
        "zhihuquestions_account": {
          "type": "float"
        }

        ,
        "tianya_clicksCount": {
          "type": "double"
        },
        "tianya_answerCount": {
          "type": "float"
        },
        "tianya_actualVolume": {
          "type": "float"
        },
        "tianya_account": {
          "type": "float"
        }

        ,
        "toutiao_followCount": {
          "type": "float"
        },
        "toutiao_fansCount": {
          "type": "float"
        },
        "toutiao_readCount": {
          "type": "float"
        },
        "toutiao_commentCount": {
          "type": "float"
        },
        "toutiao_upCount": {
          "type": "float"
        },
        "toutiao_stepCount": {
          "type": "float"
        },
        "toutiao_actualVolume": {
          "type": "float"
        },
        "toutiao_account": {
          "type": "float"
        }

        ,
        "zixun_upCount": {
          "type": "float"
        },
        "zixun_collectionCount": {
          "type": "float"
        },
        "zixun_commentCount": {
          "type": "float"
        },
        "zixun_seeCount": {
          "type": "float"
        },
        "zixun_actualVolume": {
          "type": "float"
        },
        "zixun_account": {
          "type": "float"
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
        weiboList.add("weibo_commentCount");//评
        weiboList.add("weibo_upCount");//点赞
        weiboList.add("weibo_repostCount");//转

        weixinList.add("weixin_volume");//总文章量
        weixinList.add("weixin_actualVolume");//实际文章量
        weixinList.add("weixin_readCount");//总阅读数
        weixinList.add("weixin_upCount");//总点赞量
        weixinList.add("weixin_readArticleCount");//有阅读的文章数量
        weixinList.add("weixin_account");//帐号提及量

        tiebaList.add("tieba_recoveryCount");//回复数
        tiebaList.add("tieba_actualVolume");//实际声量
        tiebaList.add("tieba_account");//帐号提及量

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

```
curl -u -XPUT http://127.0.0.1:9200/cibao_coefficient


curl -u -XPUT http://127.0.0.1:9200/_template/cibao_coefficient -d '
{
  "template": "cibao_coefficient*",
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
      "properties": {
      	"type": {
          "type": "keyword"
        },
        "key": {
          "format": "strict_date_optional_time||epoch_millis",
          "type": "date"
        },
        "value": {
          "type": "double"
        }
      }
    }
  }
}'
```



