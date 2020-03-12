---
layout: logstash
title: 使用logstash采集日志
date: 2020-03-12 10:56:34
tags:
---
在生成环境中收集线上多台服务器错误日志

# PHP java 中配置

### PHP 

  `php的错误信息使用函数`[set-error-handler(callable $error_handler [, int $error_types = E_ALL | E_STRICT ])](https://www.php.net/manual/zh/function.set-error-handler.php)
  `php的框架经常会使用monolog 这个第三个包做日志处理`

### Java

 `Java 主流的框架使用的是log4j2包`

# 日志格式

 `使用Json格式处理`

# 存储中间件

 `如果日志只有一个地方消费,使用redis。多消费使用kafka。redis的性能要好于kafka`

# logstash 采集日志

[logstash](https://www.elastic.co/cn/products/logstash) 可以采集，处理，转换日志 
[filebeat]