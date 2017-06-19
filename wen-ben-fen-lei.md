使用 `Hanlp` 与 `FastText` 完成微博文本分类

**实验结果：**

`1600` 条语料集，随机 `1500` 条作为训练集，`100` 条作为验证集、测试集，得到 `90.1%` 的精确度。

```
admindeiMac:fastText admin$ ./fasttext supervised -input weibo1.txt -output weibo  -lr 1.0 -epoch 35 -wordNgrams 2 -bucket 200000 -dim 50 -loss hs
Read 0M words
Number of words:  10751
Number of labels: 34
admindeiMac:fastText admin$ ./fasttext test weibo.bin weibo2.txt 
N	101
P@1	0.901
R@1	0.457
```

随机抽取一

原数据

```
新闻内容（主分类） 音乐MV（次分类） //@L浪漫的旭日东升M://@午夜的红裙子://@L浪漫的旭日东升M://@午夜的红裙子://@L浪漫的旭日东升M://@午夜的红裙子: //@L浪漫的旭日东升M 转 // #天天快报# 《【聆听音乐世界】乌兰托娅的《遇上你是咱俩的缘》真是天籁之音啊，好听极了》乌兰托娅的《遇上你是咱俩的缘》真是天籁之音啊，好听极了. O网页链接 L乌兰托娅的《遇上你是咱俩的缘》真是天籁之音... ​​​​
```

`NLP` 文本处理（[关键词提取](http://www.hankcs.com/nlp/textrank-algorithm-to-extract-the-keywords-java-implementation.html)和[短语提取](http://www.hankcs.com/nlp/extraction-and-identification-of-mutual-information-about-the-phrase-based-on-information-entropy.html)）

```
__label__新闻内容 __label__音乐MV 乌兰托娅 遇上 旭日东升 快报 聆听 音乐 真是 世界 浪漫 天籁 乌兰托娅遇上 浪漫旭日东升 旭日东升红裙子 红裙子浪漫 世界乌兰托娅 好听乌兰托娅 旭日东升快报 网页链接 链接乌兰托娅 遇上真是
```

运行、结果（打分最高的10个标签）

```
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



