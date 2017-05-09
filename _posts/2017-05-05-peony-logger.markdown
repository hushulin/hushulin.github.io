# 简述
1. 公司日志系统搭建与大数据平台Hadoop之上，采用成熟的Hadoop生态内的技术堆栈
2. 日志系统架构为 flume(ng) + hdfs + kafka(在建，实时分析) + storm(在建，实时分析) + mapreduce(离线分析)
3. 架构细节见astah图
4. 基于此背景，本文档详细描述各语言日志收集方法


# 安装
## PHP
1. 在helpers.php里直接复制demo代码
2. peony_logger 函数代码块


## JavaScript
1. 引用demo代码 `<script type="text/javascript" src="./log4javascript.js"></script>`
2. 注意，该插件依赖jQuery，扩展jQuery插件


# 快速使用
## PHP
`peony_logger($event_id,$event_data);`
## JavaScript
`$('button').peony_logger({event_id:1001,event_data:[1,2,3,4]});`


# 参数说明
> event_id

integer

事件ID,如点赞事件ID 为 1001 发公号事件ID 为 2001

> event_data

string 或者 array

记录该事件的日志信息，建议使用数组，如果使用字符串，则需要搞清楚当前程序正在使用哪种分割符

数组数据怎么传？

查询对应事件id的约定文档，按顺序传入数据，严格匹配文档约束字段

比如：

文档中描述


|事件ID | 事件描述 | 所需字段信息     |
|-------|:--------:|:----------------:|
|1001   | 点赞     | user_id , post_id|


则PHP的对应书写就是
`peony_logger(1001 , [1003 , 45]);`

其中 1003 是user_id 用户id

其中 45 是post_id 文章id
