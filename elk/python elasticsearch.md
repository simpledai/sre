**连接ES的信息**


    
    pip install elasticsearch
    ES_list = ["18.177.57.232:9200","18.177.57.232:9201","18.177.57.232:9202"]
    from elasticsearch import Elasticsearch
    
    es = Elasticsearch(
        ES_list,
        # 启动前嗅探es集群服务器
        sniff_on_start=True,
        # es集群服务器结点连接异常时是否刷新es节点信息
        sniff_on_connection_fail=True,
        # 每60秒刷新节点信息
        sniffer_timeout=60
    )
    print(type(es))
     


es的API 手册
https://elasticsearch-py.readthedocs.io/en/master/api.html#elasticsearch

我们看到有很多模块，我们最常用的无非也就几个，比如：
search(**kwargs)
Returns results matching a query.

https://www.elastic.co/guide/en/elasticsearch/reference/master/search-search.html

