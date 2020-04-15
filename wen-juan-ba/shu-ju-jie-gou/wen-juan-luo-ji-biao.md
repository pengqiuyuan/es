---
description: 逻辑表
---

# 问卷逻辑表

`逻辑表 wj_logic`

| `字段含义` | 字段名称 | 字段类型 | 解释 |
| :--- | :--- | :--- | :--- |
|  | Id |  | 主键id |
|  | surveys\_id |  | 问卷id |
|  | condition\_rpn |  | 条件表conditionCode的后缀表达式 |
|  | result\_type |  | 结果类型（1.跳转 2.显示 3.隐藏 -1.甄别 0.结束） |



`逻辑条件表 t_logic_condition`

| `字段含义` | 字段名称 | 字段类型 | 解释 |
| :--- | :--- | :--- | :--- |
|  | Id |  | 主键id |
|  | logic\_id |  | 逻辑表id |
|  | condition\_code |  | 条件表标识，需保证对于每个逻辑表都是唯一的 |
|  | title\_code |  | 题目唯一标识（暂定题目序号） |
|  | match\_method |  | 匹配方式（1.精准匹配 2.模糊匹配 3.模糊不匹配） |
|  | option\_rpn |  | 选项标识的后缀表达式 |

`逻辑结果表 t_logic_result`

| `字段含义` | 字段名称 | 字段类型 | 解释 |
| :--- | :--- | :--- | :--- |
|  | Id |  | 主键id |
|  | logic\_id |  | 逻辑表id |
|  | title\_code |  | 题目唯一标识（暂定题目序号） |
|  | option\_ids |  | 选项id数组，仅结果类型为显示或隐藏时生效 |

```text
后缀表达式：可以实现复杂的逻辑，比如a/b中选一个且c/d中选一个，就可以表示为"a b | c d | &"
不需要括号，解析成数组后用一个栈就可以进行运算				

示例中表达式内容其实是空格分隔的数组，如有需要改成逗号分隔也可以				

单选、多选题选项标识为形如1/2/3/4的数字，矩阵题标识为形如1.3/3.5/10.10的格式，级联题标识为形如3.2.1.5的格式				

可优化的地方：
其他：仅逻辑表有remark、create_by、create_time、update_by、update_time字段				
```

`示例一`

![](../../.gitbook/assets/image%20%282%29.png)

`示例二`

![](../../.gitbook/assets/image%20%281%29.png)

{% file src="../../.gitbook/assets/luo-ji-she-ji-1.xlsx" %}
