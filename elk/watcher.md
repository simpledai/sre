watcher is an Elasticsearch feature that you can use to create actions based on conditions, which are periodically evaluated using queries on your data. Watches are helpful for analyzing mission-critical and business-critical streaming data. For example, you might watch application logs for performance outages or audit access logs for security threats.

https://www.elastic.co/guide/en/elasticsearch/reference/7.3/watcher-api.html
https://www.elastic.co/guide/en/kibana/7.3/watcher-ui.html

https://www.elastic.co/guide/en/kibana/7.3/watcher-ui.html#watcher-create-threshold-alert

一个watch是如何工作的：
The alerting features provide an API for creating, managing and testing watches.
A watch describes a single alert and can contain multiple notification actions


A watch is constructed from four simple building blocks:
一个watch 是由以下几个部分组成的：

1.Schedule
A schedule for running a query and checking the condition.

2.Query
The query to run as input to the condition. Watches support the full Elasticsearch query language, including aggregations.

3.Condition
A condition that determines whether or not to execute the actions. You can use simple conditions (always true), or use scripting for more sophisticated scenarios.

4.Actions
One or more actions, such as sending email, pushing data to 3rd party systems through a webhook, or indexing the results of the query.

A full history of all watches is maintained in an Elasticsearch index. 
This history keeps track of each time a watch is triggered and records the results from the query, ** whether the condition was met, and what actions were taken. **
最后所有watch的记录都会被记录到一个index中，不论是否匹配规则




通过帮助手册我们可以看到我们可以创建两种类型的watcher
一种是比较简单的叫做 threshold watch （入门级的watch）
还有一种是advanced watch （高级的）


简单的太简单，甚至不能处理一些查询字段的关键字报警的操作，我们直接来用advanced watch


一个advanced watch 实际上是使用的  ** PUT watch API **
https://www.elastic.co/guide/en/elasticsearch/reference/7.3/watcher-api-put-watch.html

删除一个watcher
DELETE _watcher/watch/log_error_watch

禁用一个watcher
PUT _watcher/watch/my-watch?active=false

创建一个watcher
PUT _watcher/watch/test
{
  "trigger" : {
    "schedule" : { "interval" : "60s" } 
  },
  "input" : {
    "search" : {
      "request" : {
        "indices" : [
          "pr-corporbank-*"
        ],
        "body" : {
          "query" : {
            "bool" : {
              "must" : {
                "match": {
                   "Level": "error"
                }
              },
              "filter" : {
                "range": {
                  "@timestamp": {
                    "from": "{{ctx.trigger.scheduled_time}}||-5m",
                    "to": "{{ctx.trigger.triggered_time}}"
                  }
                }
              }
            }
          }
        }
      }
    }
  },
  "condition" : {
    "compare" : { "ctx.payload.hits.total" : { "gt" : 0 }}
  },
  "actions" : {
    "email_admin" : {
      "email" : {
        "to" : "dailiang@new4g.cn",
        "subject" : "pr-coprbank hit error message"
      }
    }
  }
}

但是发邮件之前需要在xpack设置一下邮箱相关
可以参考
https://www.elastic.co/guide/en/elasticsearch/reference/7.3/actions-email.html#configuring-email
 
Watcher can send email using any SMTP email service.