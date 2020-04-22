watcher is an Elasticsearch feature that you can use to create actions based on conditions, which are periodically evaluated using queries on your data. Watches are helpful for analyzing mission-critical and business-critical streaming data. For example, you might watch application logs for performance outages or audit access logs for security threats.


https://www.elastic.co/guide/en/kibana/7.3/watcher-ui.html

https://www.elastic.co/guide/en/kibana/7.3/watcher-ui.html#watcher-create-threshold-alert


通过帮助手册我们可以看到我们可以创建两种类型的watcher
一种是比较简单的叫做 threshold watch （入门级的watch）
还有一种是advanced watch （高级的）

简单的太简单，甚至不能处理一些查询字段的关键字报警的操作，我们直接来用advanced watch


一个advanced watch 实际上是使用的  ** PUT watch API **
https://www.elastic.co/guide/en/elasticsearch/reference/7.3/watcher-api-put-watch.html



