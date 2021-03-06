# 文本分类测试一

使用 `Hanlp` 与 `FastText` 完成微博文本分类

**实验结果：**

`1600` 条语料集，随机 `1500` 条作为训练集，`100` 条作为验证集、测试集，得到 `90.1%` 的精确度。

```text
admindeiMac:fastText admin$ ./fasttext supervised -input weibo1.txt -output weibo  -lr 1.0 -epoch 35 -wordNgrams 2 -bucket 200000 -dim 50 -loss hs
Read 0M words
Number of words:  10751
Number of labels: 34
admindeiMac:fastText admin$ ./fasttext test weibo.bin weibo2.txt 
N    101
P@1    0.901
R@1    0.457
```

语料集截图![](../.gitbook/assets/11111.png)NLP 关键词、短语提取后截图![](../.gitbook/assets/22222.png)

随机抽取（验证集）一

原数据

```text
新闻内容（主分类） 音乐MV（次分类） //@L浪漫的旭日东升M://@午夜的红裙子://@L浪漫的旭日东升M://@午夜的红裙子://@L浪漫的旭日东升M://@午夜的红裙子: //@L浪漫的旭日东升M 转 // #天天快报# 《【聆听音乐世界】乌兰托娅的《遇上你是咱俩的缘》真是天籁之音啊，好听极了》乌兰托娅的《遇上你是咱俩的缘》真是天籁之音啊，好听极了. O网页链接 L乌兰托娅的《遇上你是咱俩的缘》真是天籁之音... ​​​​
```

`NLP` 文本处理（[关键词提取](http://www.hankcs.com/nlp/textrank-algorithm-to-extract-the-keywords-java-implementation.html)和[短语提取](http://www.hankcs.com/nlp/extraction-and-identification-of-mutual-information-about-the-phrase-based-on-information-entropy.html)）

```text
__label__新闻内容 __label__音乐MV 乌兰托娅 遇上 旭日东升 快报 聆听 音乐 真是 世界 浪漫 天籁 乌兰托娅遇上 浪漫旭日东升 旭日东升红裙子 红裙子浪漫 世界乌兰托娅 好听乌兰托娅 旭日东升快报 网页链接 链接乌兰托娅 遇上真是
```

运行、结果（打分最高的10个标签）\_\_label\_\_新闻内容，\_\_label\_\_音乐MV

```text
    测试程序
    @Test
    public void test0() throws IOException, ParseException {    
        JFastText jft = new JFastText();
        jft.loadModel("/Users/admin/pqy/github/fastText/weibo.bin");
        String text = "乌兰托娅 遇上 旭日东升 快报 聆听 音乐 真是 世界 浪漫 天籁 乌兰托娅遇上 浪漫旭日东升 旭日东升红裙子 红裙子浪漫 世界乌兰托娅 好听乌兰托娅 旭日东升快报 网页链接 链接乌兰托娅 遇上真是";
        List<ProbLabel> probLabels = jft.predictProba(text,10);
        System.out.println(probLabels);
        for (ProbLabel pro : probLabels) {
            System.out.println("标签："+pro.label+"，打分："+Math.exp(pro.logProb));
        }
    }

    打印结果
    [logProb = -1.138458, label = __label__新闻内容, logProb = -1.751769, label = __label__音乐MV, logProb = -2.136085, label = __label__投诉声明, logProb = -2.564820, label = __label__用户新闻评价, logProb = -2.703368, label = __label__求助, logProb = -2.760699, label = __label__法制新闻, logProb = -3.018030, label = __label__官方声明, logProb = -3.311314, label = __label__明星推广, logProb = -3.329727, label = __label__用户提及, logProb = -3.573750, label = __label__政策解读]
    标签：__label__新闻内容，打分：0.32031252065101967
    标签：__label__音乐MV，打分：0.17346685969750258
    标签：__label__投诉声明，打分：0.1181164169463739
    标签：__label__用户新闻评价，打分：0.07693304254447338
    标签：__label__求助，打分：0.06697953279371761
    标签：__label__法制新闻，打分：0.06324754073837206
    标签：__label__官方声明，打分：0.04889744337313992
    标签：__label__明星推广，打分：0.036468227841489294
    标签：__label__用户提及，打分：0.03580287173068947
    标签：__label__政策解读，打分：0.02805046641759324
```

随机抽取（验证集）二

原数据

```text
营销内容（主分类） 活动推广（次分类） 进去点下载vx登入，再回链接进去后点【送祝福领红包】活动期间新号第一次两个包，老号每天都可以领一个红包，包有大有小全看脸！秒推！破零专属 一定要重新返回链接点送祝福，不然就是券不是红包居家撸包必备良品 //@宝宝分享菌 O网页链接进去链接下载天天快报，vx登录不用注册，返回链接直接领取红包，活动期间每天一个 ​​​​
```

`NLP` 文本处理（[关键词提取](http://www.hankcs.com/nlp/textrank-algorithm-to-extract-the-keywords-java-implementation.html)和[短语提取](http://www.hankcs.com/nlp/extraction-and-identification-of-mutual-information-about-the-phrase-based-on-information-entropy.html)）

```text
__label__营销内容 __label__活动推广 红包 链接 返回 祝福 进去 期间 活动 vx 必备 注册 一定重新 不用注册 分享网页 包有大全看 宝宝分享 居家必备 必备良品 接点祝福 活动期间 登录不用
```

运行、结果（打分最高的10个标签）\_\_label\_\_营销内容，\_\_label\_\_活动推广

```text
    测试程序
    @Test
    public void test0() throws IOException, ParseException {    
        JFastText jft = new JFastText();
        jft.loadModel("/Users/admin/pqy/github/fastText/weibo.bin");
        String text = "红包 链接 返回 祝福 进去 期间 活动 vx 必备 注册 一定重新 不用注册 分享网页 包有大全看 宝宝分享 居家必备 必备良品 接点祝福 活动期间 登录不用";
        List<ProbLabel> probLabels = jft.predictProba(text,10);
        System.out.println(probLabels);
        for (ProbLabel pro : probLabels) {
            System.out.println("标签："+pro.label+"，打分："+Math.exp(pro.logProb));
        }
    }

    打印结果
    [logProb = -0.779592, label = __label__营销内容, logProb = -0.949014, label = __label__活动推广, logProb = -2.716111, label = __label__品牌推广, logProb = -3.673375, label = __label__新闻内容, logProb = -3.952675, label = __label__投诉声明, logProb = -4.203053, label = __label__求助上访, logProb = -4.833073, label = __label__用户主动提及, logProb = -5.305556, label = __label__平台入口, logProb = -5.484654, label = __label__用户评价, logProb = -6.006136, label = __label__产品推广]
    标签：__label__营销内容，打分：0.4585929527198938
    标签：__label__活动推广，打分：0.38712255811929297
    标签：__label__品牌推广，打分：0.06613141226821419
    标签：__label__新闻内容，打分：0.025390640608013566
    标签：__label__投诉声明，打分：0.019203266855028347
    标签：__label__求助上访，打分：0.014949858046225568
    标签：__label__用户主动提及，打分：0.007962015248943197
    标签：__label__平台入口，打分：0.004963938402973328
    标签：__label__用户评价，打分：0.004149970929360042
    标签：__label__产品推广，打分：0.002463589267595421
```

随机抽取（验证集）三

原数据

```text
新闻内容（主分类） 新闻内容（次分类） 果粉的世界我们不懂 // #天天快报# 《【瞰云南】惊艳 云南第一家Apple全球直营店在昆明开业》  惊艳   云南第一家Apple全球直营店在昆明开业 O网页链接 ​​​​
```

`NLP` 文本处理（[关键词提取](http://www.hankcs.com/nlp/textrank-algorithm-to-extract-the-keywords-java-implementation.html)和[短语提取](http://www.hankcs.com/nlp/extraction-and-identification-of-mutual-information-about-the-phrase-based-on-information-entropy.html)）

```text
__label__新闻内容 __label__新闻内容 云南 惊艳 直营店 昆明 开业 Apple 全球 快报 世界 不懂 不懂快报 世界不懂 云南全球 云南惊艳 全球直营店 开业网页 快报云南 惊艳云南 昆明开业 果粉世界
```

运行、结果（打分最高的10个标签）\_\_label\_\_新闻内容，\_\_label\_\_营销内容

```text
    测试程序
    @Test
    public void test0() throws IOException, ParseException {    
        JFastText jft = new JFastText();
        jft.loadModel("/Users/admin/pqy/github/fastText/weibo.bin");
        String text = "云南 惊艳 直营店 昆明 开业 Apple 全球 快报 世界 不懂 不懂快报 世界不懂 云南全球 云南惊艳 全球直营店 开业网页 快报云南 惊艳云南 昆明开业 果粉世界";
        List<ProbLabel> probLabels = jft.predictProba(text,10);
        System.out.println(probLabels);
        for (ProbLabel pro : probLabels) {
            System.out.println("标签："+pro.label+"，打分："+Math.exp(pro.logProb));
        }
    }
    打印结果
    [logProb = -0.476273, label = __label__新闻内容, logProb = -2.745898, label = __label__营销内容, logProb = -3.164738, label = __label__知识性内容, logProb = -3.624013, label = __label__行业文章, logProb = -3.636667, label = __label__求助上访, logProb = -3.671238, label = __label__其他, logProb = -3.789606, label = __label__活动推广, logProb = -4.027542, label = __label__娱乐新闻, logProb = -4.039658, label = __label__新闻评价, logProb = -4.079453, label = __label__用户主动提及]
    标签：__label__新闻内容，打分：0.621093752236202
    标签：__label__营销内容，打分：0.064190646636016
    标签：__label__知识性内容，打分：0.042225205908758626
    标签：__label__行业文章，打分：0.026675414391655997
    标签：__label__求助上访，打分：0.02633999494054075
    标签：__label__其他，打分：0.025444950977320926
    标签：__label__活动推广，打分：0.02260450413933793
    标签：__label__娱乐新闻，打分：0.01781807095900549
    标签：__label__新闻评价，打分：0.017603498949053154
    标签：__label__用户主动提及，打分：0.016916708643830082
```

随机抽取（验证集）四

原数据

```text
新闻内容（主分类） 明星八卦（次分类） 转发微博 //@我的澎湃 转 // #天天快报# 《高清：真人秀女星海滩打球 丰腴身材辣眼睛》 O网页链接 ​​​​
```

`NLP` 文本处理（[关键词提取](http://www.hankcs.com/nlp/textrank-algorithm-to-extract-the-keywords-java-implementation.html)和[短语提取](http://www.hankcs.com/nlp/extraction-and-identification-of-mutual-information-about-the-phrase-based-on-information-entropy.html)）

```text
__label__新闻内容 __label__明星八卦 丰腴 真人秀 女星 打球 海滩 身材 高清 快报 眼睛 网页 丰腴身材 女星海滩 微博快报 快报高清 打球丰腴 海滩打球 真人秀女星 眼睛网页 网页链接 身材眼睛
```

运行、结果（打分最高的10个标签）\_\_label\_\_新闻内容，\_\_label\_\_用户主动提及

```text
    测试程序
    @Test
    public void test0() throws IOException, ParseException {    
        JFastText jft = new JFastText();
        jft.loadModel("/Users/admin/pqy/github/fastText/weibo.bin");
        String text = "丰腴 真人秀 女星 打球 海滩 身材 高清 快报 眼睛 网页 丰腴身材 女星海滩 微博快报 快报高清 打球丰腴 海滩打球 真人秀女星 眼睛网页 网页链接 身材眼睛";
        List<ProbLabel> probLabels = jft.predictProba(text,10);
        System.out.println(probLabels);
        for (ProbLabel pro : probLabels) {
            System.out.println("标签："+pro.label+"，打分："+Math.exp(pro.logProb));
        }
    }

    打印结果
    [logProb = -1.227689, label = __label__新闻内容, logProb = -1.751610, label = __label__用户主动提及, logProb = -2.611454, label = __label__营销内容, logProb = -2.705132, label = __label__知识性内容, logProb = -2.707546, label = __label__平台入口, logProb = -3.051701, label = __label__行业文章, logProb = -3.081810, label = __label__娱乐新闻, logProb = -3.147120, label = __label__其他, logProb = -3.468003, label = __label__新闻评价, logProb = -3.548918, label = __label__活动推广]
    标签：__label__新闻内容，打分：0.292968768966334
    标签：__label__用户主动提及，打分：0.17349446817388692
    标签：__label__营销内容，打分：0.07342771900058004
    标签：__label__知识性内容，打分：0.06686152892037624
    标签：__label__平台入口，打分：0.06670027293226938
    标签：__label__行业文章，打分：0.04727845462376656
    标签：__label__娱乐新闻，打分：0.04587614574467157
    标签：__label__其他，打分：0.04297572917160248
    标签：__label__新闻评价，打分：0.031179232381571866
    标签：__label__活动推广，打分：0.028755743137451696
```

随机抽取（验证集）五

原数据

```text
用户主动提及（主分类） 用户评价（次分类） 天天快报是诈骗网站，请大家一定要小心！就在刚才我在qq上看新闻，屏幕边上弹出一个小红包。于是我就好奇的点了下，然后上面提示我下载天天快报注册就送新手红包。好吧，我下载了之后根本没有红包。之后在该网站右上，如图2！之后让我填写手机，发验证。呵呵！不用我说你们懂得 2海城市 ​​​​
```

`NLP` 文本处理（[关键词提取](http://www.hankcs.com/nlp/textrank-algorithm-to-extract-the-keywords-java-implementation.html)和[短语提取](http://www.hankcs.com/nlp/extraction-and-identification-of-mutual-information-about-the-phrase-based-on-information-entropy.html)）

```text
__label__用户主动提及 __label__用户评价 红包 网站 快报 之后 下载 刚才 小心 qq 验证 手机 一定小心 上面提示 下载之后 下载快报 不用懂得 之后填写 之后根本 之后网站 填写手机 屏幕边上
```

运行、结果（打分最高的10个标签）\_\_label\_\_营销内容，\_\_label\_\_活动推广

```text
    测试程序
    @Test
    public void test0() throws IOException, ParseException {    
        JFastText jft = new JFastText();
        jft.loadModel("/Users/admin/pqy/github/fastText/weibo.bin");
        String text = "红包 网站 快报 之后 下载 刚才 小心 qq 验证 手机 一定小心 上面提示 下载之后 下载快报 不用懂得 之后填写 之后根本 之后网站 填写手机 屏幕边上";
        List<ProbLabel> probLabels = jft.predictProba(text,10);
        System.out.println(probLabels);
        for (ProbLabel pro : probLabels) {
            System.out.println("标签："+pro.label+"，打分："+Math.exp(pro.logProb));
        }
    }

    打印结果
    [logProb = -0.870515, label = __label__营销内容, logProb = -1.518276, label = __label__活动推广, logProb = -2.088133, label = __label__品牌推广, logProb = -3.060270, label = __label__新闻内容, logProb = -3.126143, label = __label__行业文章, logProb = -3.304752, label = __label__话题推广, logProb = -3.398077, label = __label__用户主动提及, logProb = -3.584448, label = __label__产品推广, logProb = -4.149024, label = __label__用户评价, logProb = -4.992616, label = __label__投诉声明]
    标签：__label__营销内容，打分：0.41873564972797755
    标签：__label__活动推广，打分：0.21908922444082563
    标签：__label__品牌推广，打分：0.12391829296383723
    标签：__label__新闻内容，打分：0.046875022745786143
    标签：__label__行业文章，打分：0.04388676426104315
    标签：__label__话题推广，打分：0.036708319030945194
    标签：__label__用户主动提及，打分：0.033437500160464366
    标签：__label__产品推广，打分：0.02775199297917488
    标签：__label__用户评价，打分：0.015779817437454362
    标签：__label__投诉声明，打分：0.0067878829419828176
```

