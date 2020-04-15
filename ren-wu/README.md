# Narnia

```text
cibao_index： Es 保存计算指标索引 
stq_monitor_second： Mysql表 词包单条任务对应表 【作用类似于待执行的词包任务队列】。添加悲观锁，阻止其他事务读取相同实体，实现简单运行多个工程分布式取任务。

整体流程
1、从任务添加的成功的时刻起，词包新增调度器开始取出任务开始计算。（ivst、narnia、travel、common 4种任务类型的区分）
2、endDate 如果没有传，后台会判定这条任务为无限计算（mysql 保存 categoryDuration 为 1），开始每天定时更新（更新完成以后endDate会修改并记录为当天日期），每次更新的时候重新计算最近7天（暂时）的数据，保存到缓存。
3、endDate 如果有传，一般情况只计算一次然后保存到缓存，如果 endDate 的日期在7天内，后台也会定时更新，直到 endDate 不在最近7天的范围内，不再更新。

任务处理（每个调度器为多线程并发执行任务）
    词包新增调度器：单个线程每秒执行一次，一次去一条符合条件的任务（taskStatus 任务状态是否为0 未开始）
    词包更新调度器：单个线程每秒执行一次，一次去一条符合条件的任务（categoryUpDate 不等于当前日期，如：2017-11-03）
    微博系数计算调度器：每天凌晨更新一次微博系数 2014-01-01 到当前日期。微博统计计算时，取对应系数值，取最近7天的系数时，实时计算。
    原文导出调度器：单个线程每秒执行一次，一次去一条符合条件的任务
    统计计算调度器：单个线程每秒执行一次，一次去一条符合条件的任务
计算流程
    单条任务计算流程（微博...资讯）一次取出一条
        1、根据关键字、起始日期、结束日期（查询Es cibao_index 索引）判断此条任务是否已经计算过。计算过？返回。未计算过，继续执行代码块。
        2、开始计算指标，目前除了微博、微信账号提及量（10天或者30天一次Es查询）、微博曝光量（5天或者30天一次Es查询）的计算，其他指标都是一条聚合查询出一段时间的计算结果，保存下来（Es create 重复不覆盖）。
    单条任务更新流程，一次取出一条
        1、取出词包表里status=1、categoryUpDate=不等于今天，的待更新数据。如果这条任务为无限计算 categoryDuration 为 1（ivst、narnia、travel、common），重新计算最近7天（暂时）的数据，保存到 cibao_index。
        如果这条任务不为无限计算 categoryDuration 不为 1，判定 endDate 的日期是否在7天内，后台会定时更新，直到 endDate 不在最近7天的范围内，不再更新。
        2、更新词包任务不会判断任务是否计算过，会逐条取出任务计算。
```
