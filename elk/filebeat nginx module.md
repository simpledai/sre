filebeat我们有很多方式收集日志
我们常用的做法是把日志当作log，进行一些简单匹配之后，输出到logstash （之后在logstash进行grok分割成指定字段存到es） 或者 es中
频繁的写grok 正则匹配是很累的工作

所以filebeat提供了更简单的方式：** module **

看一下官网描述

Filebeat provides a set of pre-built modules that you can use to rapidly implement and deploy a log monitoring solution, complete with sample dashboards and data visualizations (when available), in about 5 minutes. These modules support common log formats, such as Nginx, Apache2, and MySQL, and can be run by issuing a simple command.

具体模块链接：
https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-modules.html

我们拿nginx 模快来说：
https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-modules-quickstart.html

1.查看filebeat开启了哪些模块
	./filebeat modules list 

2.开启具体模块
	./filebeat modules enable nginx

3. 设置初识化环境
	./filebeat setup -e


4. 设置模块的具体参数及收取路径
   cd /opt/filebeat/modules.d
   vim nginx.yml 

```- module: nginx
  # Access logs
  access:
    enabled: true

    # Set custom paths for the log files. If left empty,
    # Filebeat will choose the paths depending on your OS.
    var.paths: ["/usr/local/openresty/nginx/logs/*_access.log*"]

  error:
    enabled: false
    var.paths: ["/usr/local/openresty/nginx/logs/www.cbibank.com_error.log*"]
    # Set custom paths for the log files. If left empty,
    # Filebeat will choose the paths depending on your OS.
    #var.paths:

```

5.设置filebeat主配置文件

[root@ip-10-1-4-11 filebeat]# cat nginx-access.yml 
filebeat.inputs:
setup.template.settings:
  index.number_of_shards: 2

filebeat.config.modules:
    path: ${path.config}/modules.d/*.yml
    reload.enabled: true
output.elasticsearch:
    hosts: ["10.2.12.31:9200","10.2.12.32:9200","10.2.12.33:9200"]
setup.kibana:
  host: "10.1.1.21:5601"
      


6.之后启动filebeat


### 注意点1：

但是这里我们要注意一个问题，我们如果是自定义的nginx日志格式呢？
答案：会有一定机率出现匹配错误，并且kibana不能很好显示，所以我们就用nginx默认日志格式就好
我们使用的日志格式是：

```shell
    log_format main '$remote_addr - $remote_user [$time_local] '
                       '"$request" $status $bytes_sent '
                       '"$http_referer" "$http_user_agent" "$gzip_ratio"'
                       '"$http_x_forwarded_for" "$http_x_real_forwarded_for"';
```

### 注意点2:
如果我们如果使用上面的filebeat主配置文件，那么你的index name 就是 filebeat-7.3.2-2020.04.17-000001 这种格式的
不建议改这个index名称，原因如下













