watcher is an Elasticsearch feature that you can use to create actions based on conditions, which are periodically evaluated using queries on your data. Watches are helpful for analyzing mission-critical and business-critical streaming data. For example, you might watch application logs for performance outages or audit access logs for security threats.


https://www.elastic.co/guide/en/kibana/7.3/watcher-ui.html

https://www.elastic.co/guide/en/kibana/7.3/watcher-ui.html#watcher-create-threshold-alert

一个watch是如何工作的：
The alerting features provide an API for creating, managing and testing watches.
A watch describes a single alert and can contain multiple notification actions


A watch is constructed from four simple building blocks:
一个watch 是由以下几个部分组成的：
Schedule
A schedule for running a query and checking the condition.
Query
The query to run as input to the condition. Watches support the full Elasticsearch query language, including aggregations.
Condition
A condition that determines whether or not to execute the actions. You can use simple conditions (always true), or use scripting for more sophisticated scenarios.
Actions
One or more actions, such as sending email, pushing data to 3rd party systems through a webhook, or indexing the results of the query.

通过帮助手册我们可以看到我们可以创建两种类型的watcher
一种是比较简单的叫做 threshold watch （入门级的watch）
还有一种是advanced watch （高级的）

简单的太简单，甚至不能处理一些查询字段的关键字报警的操作，我们直接来用advanced watch


一个advanced watch 实际上是使用的  ** PUT watch API **
https://www.elastic.co/guide/en/elasticsearch/reference/7.3/watcher-api-put-watch.html




 
