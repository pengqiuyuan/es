#### 词包模块（单个监测项为一个词包计算子任务）

> **任务加载**

【1】词包任务主、次两张表创建（OneToMany 一对多）1-2小时，包括class的创建

```
stq_monitor_primary

id 主键
task_name 监测项任务名称
task_type 监测项任务分类。此监测项监测的数据源、微博（1）、微信（2）等等
excel_path 指标下载地址。当点击词包父任务页面的下载按钮时，首先根据主表 id 和 task_type 去 es或mongodb？ 获取对应指标文档，然后服务器生成excel文件
data_index 指标值（actualVolume，volume等等）。页面默认全部（除情感分析？），不可勾选。
data_index_name 指标值中文名称（实际声量，声量等等）。
cr_date 词包主任务生成时间
upd_date 词包主任务更新时间
status 词包主任务有效、无效。控制次表监测项任务的状态，停止对应的每个子任务。

stq_monitor_second

id 主键
primary_id 外键，stq_monitor_primary 表的主键
start_date 监测项任务起始时间
end_date 监测项任务结束时间
task_type 监测项任务分类。此监测项监测的数据源、微博（1）、微信（2）等等
key_word 监测项名称。如：三少爷的剑+电影+-测试1+-测试2+测试3+-测试4+中文加+-中文减||三少爷的剑+林更新||三少爷的剑+何润东||三少爷的剑+江一燕||三少爷的剑+蒋梦婕
cr_date 词包次任务生成时间
upd_date 词包次任务更新时间
status 词包次任务的运行状态，0（子任务未开始），1（子任务进行中），2（子任务已完成，完成以后立即保存指标到es对应索引），3（此子任务计算出错）
```

【2】页面添加单个监测项任务。（保存词包主、次任务表），返回一组主任务ID到前端页面，指标结果通过传入主ID获取。

3个jsp页面，2个controller，2个service，2个dao，测试结果。预期一天

```
页面传入参数
1、监测项名称，页面输入框提示输入格式。“||”为或，“+”为包含，“+-”为不包含，如：三少爷的剑+电影+-测试1+-测试2+测试3+-测试4+中文加+-中文减||三少爷的剑+林更新||三少爷的剑+何润东||三少爷的剑+江一燕||三少爷的剑+蒋梦婕
2、监测项起始时间
3、监测项结束时间
4、类型（监测数据的来源，如：微博、微信等等）
同时保持任务到词包主、次两张表
返回数组展示在前端页面：如：[1,2,3]，如果，每多选一个类型，数组多一个值。

注意：没有指标可以勾选。这里在服务层处理好，数据源类型的不同，需要计算的指标也不一样。
```

【3】Excel批量添加监测项任务。（保存词包主、次任务表），返回父任务ID到前端页面，指标结果通过传入父ID获取。

一个jsp页面，一个controller的方法，一个service的方法，测试结果。预期半天

```
一、需要Excel 文件的模板，供使用者下载。Excel列包括：监测项名称、监测起始时间、监测结束时间、数据源类型

二、页面传入参数
1、上传文件
2、选择类型（监测数据的来源，如：微博、微信等等）
同时保持任务到词包主、次两张表
返回数组展示在前端页面：如：[1,2,3]，如果，每多选一个类型，数组多一个值。

注意：没有指标可以勾选。这里在服务层处理好，数据源类型的不同，需要计算的指标也不一样。
```

【4】API ，客户端提交监测项任务集合，返回父任务ID。（保存词包主、次任务表），返回主任务ID到前端页面，指标结果通过传入（主ID+type）获取。

一个方法，预期半天。

```
request 
keyword:如：三少爷的剑+电影+-测试1+-测试2+测试3+-测试4+中文加+-中文减||三少爷的剑+林更新||三少爷的剑+何润东||三少爷的剑+江一燕||三少爷的剑+蒋梦婕
type：微博（1）、微信（2）等等

{
    "taskList": [
        {
            "keyword": "1",
            "startDate": "2017-01-01",
            "endDate": "2017-01-02"
        },
        {
            "keyword": "1",
            "startDate": "2017-01-01",
            "endDate": "2017-01-02"
        }
    ],
    "type": "1,2,3,4"
}

response
primaryId：客户端获取指标的唯一ID
[
    {
        "primaryId": "1",
        "type": "1"
    },
    {
        "primaryId": "2",
        "type": "2"
    }
]
```

> **任务处理（计算）**

【1】微博

实际声量，声量，互动量，转发深度（取最大值），原发提及占比，评论贡献比，点赞贡献比，二级及以上转发占比，三级及以上转发占比，**曝光量、独立账号占比，正面情绪占比，中立情绪占比，负面情绪占比，口碑值**

【2】微信

实际声量，声量，阅读量，点赞量，统计占比，**正面情绪占比，中立情绪占比，负面情绪占比，口碑值**

【3】百度新闻

【4】百度贴吧

【5】头条

【6】知乎问答

【7】天涯

> **指标保存**

【1】单个监测项任务计算结果的保存（Es或者mongodb）。每条文档都有，词包父ID ，词包子ID，起始日期、结束日期，指标属于类别（微博、微信等等）

> **结果取出**

【1】词包父任务页面，通过ID查询任务，点击下载，导出多个监测项Excel文件  
【2】API ，客户端提交任务词包父ID，返回指标结果  
【3】API ，客户端通过传入参数，词包监测项名称、起始日期、结束日期、类别（微博、微信等等），返回指标结果

> 生产环境配置

JDK8+、Mysql、mongodb、Jetty、Nginx



彭秋源：计算、公共模块的封装（指标计算、任务调度、Es相关、Demo例子）

何新彪：与mongo（或者es？）交互的部分，这部分比较重要，客户端直接获取数据的来源。

任务加载模块

#### 统计计算模块

#### 原文导出模块


