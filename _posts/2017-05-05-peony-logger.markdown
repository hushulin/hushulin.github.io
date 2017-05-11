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

# 附录JavaScript源代码实现
```js
(function (factory) {
	if (typeof define === 'function' && define.amd) {
		define(['jquery'], factory);
	} else if (typeof exports === 'object') {
		factory(require('jquery'));
	} else {
		factory(jQuery);
	}
})(function ($) {
	'use strict';

	var $window = $(window),
		$document = $(document);

	var console = window.console || { log: function () {} };

	function isNumber(n) {
		return typeof n === 'number';
	}

	function isUndefined(n) {
		return typeof n === 'undefined';
	}

	function toArray(obj, offset) {
		var args = [];

		if (isNumber(offset)) { // It's necessary for IE8
			args.push(offset);
		}

		return args.slice.apply(obj, args);
	}
	
	// 类
	function PeonyLogger($container , $options) {

		this.$event_id_key = "event_id";
		this.$event_data_key = "event_data";
		this.$decollator = "&&";
		this.$url = "/peony_logger.php";

		this.$container = $container;

		if ( $options ) {

			this.id = $options[this.$event_id_key];

			if ( $.isArray($options[this.$event_data_key]) ) {
				this.data = $options[this.$event_data_key].join(this.$decollator);
			} else {
				this.data = $options[this.$event_data_key];
			}

		} else {

			this.id = this.$container.attr(this.$event_id_key);
			this.data = this.$container.attr(this.$event_data_key);
		}
		
		this.$container.on('click' , $.proxy(this.write , this));
	}
	
	// 原型 业务逻辑 
	PeonyLogger.prototype = {

		constructor: PeonyLogger,

		write: function (event) {

			var data = new FormData();

			data.append(this.$event_id_key, this.id);
			data.append(this.$event_data_key, this.data);

			var xhr = new XMLHttpRequest();
			xhr.withCredentials = true;

			xhr.addEventListener("readystatechange", function () {
				if (this.readyState === 4) {
					console.log(this.responseText);
				}
			});

			xhr.open("POST", this.$url);
			xhr.setRequestHeader("cache-control", "no-cache");
			xhr.send(data);

		}
	};

	// Save the other 
	PeonyLogger.other = $.fn.peony_logger;

	// Register as jQuery plugin
	$.fn.peony_logger = function (options) {
		var args = toArray(arguments, 1),
			result;

		this.each(function () {

			var $this = $(this),
				data = $this.data('peony_logger'),
				fn;

			if (!data) {
				$this.data('peony_logger', (data = new PeonyLogger($this, options)));
			}

			if (typeof options === 'string' && $.isFunction((fn = data[options]))) {
				result = fn.apply(data, args);
			}
		});

		return isUndefined(result) ? this : result;
	};

	$.fn.peony_logger.noConflict = function () {
		$.fn.peony_logger = PeonyLogger.other;
		return this;
	};

});
```