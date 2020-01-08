# Elasticsearch的停用词

**Elasticsearch的停用词**

有些词在文本中出现的频率非常高，但是对文本所携带的信息基本不产生影响。

英文：a、an、the、of

中文：的、了、着、是 、标点符号等

文本经过分词之后，停用词通常被过滤掉，不会被进行索引。

在检索的时候，用户的查询中如果含有停用词，检索系统也会将其过滤掉（因为用户输入的查询字符串也要进行分词处理）。

排除停用词可以加快建立索引的速度，减小索引库文件的大小。

[英文停用词](http://www.ranks.nl/stopwords)

[中文停用词](http://www.ranks.nl/stopwords/chinese-stopwords)

