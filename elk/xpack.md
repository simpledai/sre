
https://www.elastic.co/guide/en/elasticsearch/reference/7.6/setup-xpack.html

X-Pack is an Elastic Stack extension that bundles security, alerting, monitoring, reporting, and graph capabilities into one easy-to-install package.

Prior to Elasticsearch 5.0.0, you had to install separate Shield, Watcher, and Marvel plugins to get the features that are bundled together in X-Pack.

With X-Pack, you no longer have to worry about whether or not you have the right version of each plugin,

just install the X-Pack for the Elasticsearch version you’re running)

X-Pack是Elastic技术栈的扩展，它集安全，提醒，监控，报表以及图标功能于一体。

在Elasticsearch 5.0之前，你必须单独安装Shield插件，还要配套Watcher, Marvel等插件，现在X-Pack把它们都整合到一块儿了

修改elasticsearch.yml 
```language
xpack.security.enabled

```

** 设置elasticsearch的用户名和密码 ** 

** es有很多build-in user ，就是内置用户 ** 

说明如下：
https://www.elastic.co/guide/en/elasticsearch/reference/7.6/built-in-users.html

elastic
A built-in superuser.
kibana
The user Kibana uses to connect and communicate with Elasticsearch.
logstash_system
The user Logstash uses when storing monitoring information in Elasticsearch.
beats_system
The user the Beats use when storing monitoring information in Elasticsearch.
apm_system
The user the APM server uses when storing monitoring information in Elasticsearch.
remote_monitoring_user
The user Metricbeat uses when collecting and storing monitoring information in Elasticsearch. It has the remote_monitoring_agent and remote_monitoring_collector built-in roles.


** 设置密码 **
密码我们可以通过交互式的方式查看
bin/elasticsearch-setup-passwords kibana

