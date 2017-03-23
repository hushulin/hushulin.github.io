
# Fractal
Fractal 为复合数据输出提供一个展示和转化层，类似作用于 RESTful APIs，并且在 JSON 中工作得很好。Fractal 可以认为是你的应用程序中 JSON/YAML/等等的视图层。
当构建API时，人们最常规的做法是单纯的从数据库查找出数据传递给json_encode()。这对于“简单的”APIs可能是可行的，但是如果它们对外提供服务，或者被移动应用调用，那么它很快将会引发不一致的输出问题。

# 目标
- 在源数据与输出层之间，提供一个保护中间层，以致于数据结构发生变化时不会影响用户
- 系统的数据转换，避免了foreach() 和 对数据的布尔值判断
- 为复合数据结构内置了（嵌入，嵌套，切面加载）等关联关系
- 内置标准的 HAL 和 JSON-API 序列化，并且支持自定义序列化
- 为类似小数据量和大数据量，支持数据分页
- 在简单的API中，轻松应对微妙复杂的输出数据

这个包遵循PHP的 PSR-1, PSR-2 和 PSR-4规范。如果你发现有遵循漏洞，请通过pull request发一个补丁上来。

# 安装
## 通过composer

{% highlight php %}
composer require league/fractal
{% endhighlight php %}

很多现代PHP框架都会默认的包含 Composer autoloader ，但是还是请您再次确保下列文件包含进来
{% highlight php %}
<?php

// Include the Composer autoloader
require 'vendor/autoload.php';

{% endhighlight php %}
## 单独安装
如果没有使用composer 你也可以单独安装 Fractal ,用下面代码注册自动加载函数:
{% highlight php %}
spl_autoload_register(function ($class) {
    $prefix = 'League\\Fractal\\';
    $base_dir = __DIR__ . '/src/';
    $len = strlen($prefix);
    if (strncmp($prefix, $class, $len) !== 0) {
        // no, move to the next registered autoloader
        return;
    }
    $relative_class = substr($class, $len);
    $file = $base_dir . str_replace('\\', '/', $relative_class) . '.php';
    if (file_exists($file)) {
        require $file;
    }
});
{% endhighlight php %}
或者，使用其他兼容PSR-4 规范的加载器。

# 简单例子
为简单起见，这个例程我们把所有代码放在一个文件里。在你的实际应用程序中，你可以把实例化，初始化放到应用启动过程中，或者你采用了IOC容器，交给容器去实例化初始化。把数据收集、JSON转化都单独放入不同的代码部分。
{% highlight php %}
<?php
use League\Fractal\Manager;
use League\Fractal\Resource\Collection;

// Create a top level instance somewhere
$fractal = new Manager();

// Get data from some sort of source
// Most PHP extensions for SQL engines return everything as a string, historically
// for performance reasons. We will fix this later, but this array represents that.
$books = [
	[
		'id' => '1',
		'title' => 'Hogfather',
		'yr' => '1998',
		'author_name' => 'Philip K Dick',
		'author_email' => 'philip@example.org',
	],
	[
		'id' => '2',
		'title' => 'Game Of Kill Everyone',
		'yr' => '2014',
		'author_name' => 'George R. R. Satan',
		'author_email' => 'george@example.org',
	]
];

// Pass this array (collection) into a resource, which will also have a "Transformer"
// This "Transformer" can be a callback or a new instance of a Transformer object
// We type hint for array, because each item in the $books var is an array
$resource = new Collection($books, function(array $book) {
    return [
        'id'      => (int) $book['id'],
        'title'   => $book['title'],
        'year'    => (int) $book['yr'],
        'author'  => [
        	'name'  => $book['author_name'],
        	'email' => $book['author_email'],
        ],
        'links'   => [
            [
                'rel' => 'self',
                'uri' => '/books/'.$book['id'],
            ]
        ]
    ];
});

// Turn that into a structured array (handy for XML views or auto-YAML converting)
$array = $fractal->createData($resource)->toArray();

// Turn all of that into a JSON string
echo $fractal->createData($resource)->toJson();

// Outputs: {"data":[{"id":1,"title":"Hogfather","year":1998,"author":{"name":"Philip K Dick","email":"philip@example.org"}},{"id":2,"title":"Game Of Kill Everyone","year":2014,"author":{"name":"George R. R. Satan","email":"george@example.org"}}]}
{% endhighlight php %}
值得注意的是，相对于直接使用``Transformers``,回调函数也是一个非常好的替代方案。回调函数能使你复用``Transformers``并且保持你的应用程序控制器层轻量级。

# 环境要求
支持以下PHP版本和HHVM
- PHP 5.4
- PHP 5.5
- PHP 5.6
- PHP 7.0
- PHP 7.1
- HHVM

# 协议许可
MIT License (MIT)
