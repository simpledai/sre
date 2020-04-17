filebeat我们有很多方式收集日志
我们常用的做法是把日志当作log，进行一些简单匹配之后，输出到logstash （之后在logstash进行grok分割） 或者 es中

