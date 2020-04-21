
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

