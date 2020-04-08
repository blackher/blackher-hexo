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
  `php的框架经常会使用monolog做日志处理`
  `以上都可以将日志打入存储中间件`

### Java

 `Java 主流的框架使用的是log4j2包,当然可以打入存储中间件`

# 日志格式

 `使用Json格式处理`

# 存储中间件

 `如果日志只有一个地方消费,使用redis。多消费使用kafka。redis的性能要好于kafka`

# logstash 采集日志

[logstash](https://www.elastic.co/cn/products/logstash) 可以采集，处理，转换日志 
[filebeat](https://www.elastic.co/cn/products/filebeat) 简单文件采集

### 读取中间件

``` bash
  input{ #读取中间件
     redis {
        host => "host"
        port => "port"
        db => 'db'
        data_type => "list" #redis数据类型
        key => 'key' #redis key
        batch_count => 1 #这个值是指从队列中读取数据时，一次读取多少
        type => 'redis_type' #指日志的type 下面
      }
      kafka {
        bootstrap_servers => "127.0.0.1:9092" #kafka服务器地址
        topics => "topic"
        batch_size => 5
        codec => "json" #写入的时候使用json编码，
        group_id => "group_id" 
        consumer_threads => 1
        decorate_events => true #此属性会将当前topic、offset、group、partition等信息也带到message中
        type =>'kafka_type'
   
  }
  ouput{
      if [type] == "redis_key"{
        elasticsearch { #读取到elasticsearch
          hosts => ['127.0.0.01:9200']
          index => 'dev-api-error-record-%{+YYYY.MM.dd}' #按照日期读取到不通的index上
          }
        }
      if [type] == "kafka_type"{
        file { #读取到file
          path =>'/path/%{type}-%{+YYYY.MM.dd}.txt' #路径
        }

  }
  
```
`logstash 还可以使用很多的存储中间件 更多的功能:正则匹配，文件格式预处理等等`
`启动logstash 的时候可以加上 --config.reload.automatic 自动检测配置文件的变动和自动重新加载配置文件`
# 总结
`项目的日志按照json格式--->中间件(redis/kafka...) --->logstah(采集处理分发) --->储存地点`
`还可以结合elasearch+grafna 结合做报警提示，下次在做这个总结(还有promethus 监控)`         