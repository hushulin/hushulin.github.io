
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
通过composer
``composer require league/fractal``

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
