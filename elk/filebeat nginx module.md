filebeat我们有很多方式收集日志
我们常用的做法是把日志当作log，进行一些简单匹配之后，输出到logstash （之后在logstash进行grok分割成指定字段存到es） 或者 es中
频繁的写grok 正则匹配是很累的工作

所以filebeat提供了更简单的方式：** module **

看一下官网描述


Filebeat provides a set of pre-built modules that you can use to rapidly implement and deploy a log monitoring solution, complete with sample dashboards and data visualizations (when available), in about 5 minutes. These modules support common log formats, such as Nginx, Apache2, and MySQL, and can be run by issuing a simple command.

具体模块链接：
https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-modules.html







