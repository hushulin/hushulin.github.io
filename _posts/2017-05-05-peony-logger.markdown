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
1. 引用demo代码 '<script type="text/javascript" src="./log4javascript.js"></script>'
2. 注意，该插件依赖jQuery，扩展jQuery插件


# 快速使用
## PHP
`peony_logger($event_id,$event_data);`
## JavaScript
`$('button').peony_logger({event_id:1001,event_data:[1,2,3,4]});`


# 参数说明
event_id

integer

事件ID,如点赞事件ID 为 1001 发公号事件ID 为 2001