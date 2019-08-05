# HBase {#concept_omw_cxf_xgb .concept}

本文将为您介绍实时计算云数据库HBase版维表的配置面板说明。

更多详情请参见[实时计算云数据库（HBase）维表](../../../../cn.zh-CN/Flink SQL开发指南/Flink SQL/DDL语句/创建数据维表/创建云数据库 HBase版维表.md#)。

## 配置面板说明 {#section_rjw_fxf_xgb .section}

|参数|注释说明|备注|
|--|----|--|
|血缘表名（任务唯一）|任务中表的唯一标志，不能与任务中其他血缘表重名。|无|
|表名|HBase表名。|无|
|数据同步|从元数据中心读取指定表名的元数据，帮助填充输出字段和其他元信息表单项。|无|
|列族名|列族名。|目前仅支持插入同一列族。|
|Rowkey字段名|指定输出字段中作为主键的字段。|无|
|HBase集群对应的ZooKeeper地址|HBase集群配置的ZooKeeper地址，以（,）分隔主机列表。|可以在hbase-site.xml文件中找到hbase.zookeeper.quorum相关配置。|
|HBase集群配置在zk上的路径|HBase集群配置在ZooKeeper的路径。|可以在hbase-site.xml文件中找到hbase.zookeeper.quorum的相关配置。|
|选择输出字段|要输出到HBase表的字段列表。|无|
|缓存策略|缓存策略。|包括None、LRU和ALL三种缓存策略。|
|缓存大小|缓存大小。|选择`LRU`缓存策略后，可以设置缓存大小。|
|缓存超时时间|缓存超时时间，单位为毫秒。| -   选择`LRU`缓存策略后，可以设置缓存失效的超时时间，默认不过期。
-   选择`ALL`策略，则为缓存reload的间隔时间，默认不重新加载。

 |
|更新时间黑名单|缓存策略选择`ALL`时启用。更新时间黑名单，防止在此时间内进行cache更新（例如双11场景）。|自定义输入格式如下所示： ``` {#codeblock_5a3_o05_aue}
2017-10-24 14:00 -> 2017-10-24 15:00, 2017-11-10 23:30 -> 2017-11-11 08:00
```

 用逗号（,）分隔多个黑名单，用箭头（-\>）分隔黑名单的起始结束时间。|
|cacheScanLimit|缓存策略选择`ALL`时启用。load全量HBase数据，服务端一次RPC返回给客户端的行数。|无|
|用户名|用户名。|无|
|密码|密码。|无|
|最大尝试次数|最大尝试次数。|默认10次。|
|partitionedJoin|设置为true后，会用joinKey进行分区，将数据分发到Join节点，提高缓存命中率。|可选，默认关闭。|
|shuffleEmptyKey|设置为true后，遇到空key会随机往下游进行shuffle，否则往0号下游发。|建议打开。|

## 说明 {#section_pmt_3xf_xgb .section}

-   声明维表时，必须要指名主键。维表JOIN的时候，ON的条件必须包含所有主键的等值条件，HBase中的主键即rowkey。
-   目前RDS和DRDS提供None（无缓存）、LRU（最近使用策略缓存）和ALL三种缓存策略。需要配置相关参数：缓存大小（cacheSizecacheTTLMs、cacheTTLMs和cacheReloadTimeBlackList）。
-   使用ALL Cache时，由于会进行异步Reload，需要给维表JOIN的节点增加内存，增加的内存大小为远程表数据量的2倍。

