# Kafka {#concept_yxg_5ls_wgb .concept}

实时计算Kafka源表声明基于云栖社区的kafka版本实现。Kafka源表数据解析流程为Kafka Source Table \> UDTF \> Flink \> SINK，从Kakfa读入的数据均为VARBINARY（二进制）格式。读入的每条数据，都需要用UDTF将其解析为格式化数据。

更多详情请参见[创建消息队列Kafka源表](../../../../cn.zh-CN/Flink SQL开发指南/Flink SQL/DDL语句/创建数据源表/创建消息队列 Kafka源表.md#)。

## 配置面板说明 {#section_rqt_j4f_xgb .section}

|参数|注释说明|备注|
|--|----|--|
|血缘表名|任务中表的唯一标志，不能与任务中其他血缘表重名。|无。|
|定义列|定义要读取的kafka字段列表。|kafka的列定义必须依次为messageKey varbinary、message varbinary、topic varchar、partition int和offset bigint，顺序不可更改。|
|kafka对应版本|kafka对应版本。|无。|
|读取的单个topic|读取的单个topic。|可选项包括kafka08、kafka09、kafka10和kafka11。|
|读取一批topic的表达式|读取一批topic的表达式。|无。|
|启动位点|启动位点。| -   EARLISET从kafka最早分区开始读取数据。
-   Group\_OFFSETS根据Group读取数据。
-   LATEST从kafka最新位点开始读取数据。
-   TIMESTAMP从指定的时间点开始读取数据（kafk010、kafka011支持）。

 |
|定时检查是否有新分区产生|检查是否有新分区产生的时间间隔，单位为ms。|无。|
|group.id|消费组的ID。|可选。|
|zk链接地址|zk链接地址。|适用于kafka08。|
|kafka集群地址|kafka集群地址。|适用于kafka09、kafka10和kafka11。|
|添加扩展参数|添加kafka支持的可选配置项。|无。|

## 可选扩展参数 {#section_mvf_n4f_xgb .section}

-   kafka08

    ``` {#codeblock_y8p_g00_ika}
    "consumer.id","socket.timeout.ms","fetch.message.max.bytes","num.consumer.fetchers","auto.commit.enable","auto.commit.interval.ms","queued.max.message.chunks", "rebalance.max.retries","fetch.min.bytes","fetch.wait.max.ms","rebalance.backoff.ms","refresh.leader.backoff.ms","auto.offset.reset","consumer.timeout.ms","exclude.internal.topics","partition.assignment.strategy","client.id","zookeeper.session.timeout.ms","zookeeper.connection.timeout.ms","zookeeper.sync.time.ms","offsets.storage","offsets.channel.backoff.ms","offsets.channel.socket.timeout.ms","offsets.commit.max.retries","dual.commit.enabled","partition.assignment.strategy","socket.receive.buffer.bytes","fetch.min.bytes"
    ```

-   [kafka09](https://kafka.apache.org/0110/documentation.html#consumerconfigs)
-   [kafka010](https://kafka.apache.org/090/documentation.html#newconsumerconfigs)
-   [kafka011](https://kafka.apache.org/0102/documentation.html#newconsumerconfigs)

## kafka版本对应关系 {#section_qql_fpf_xgb .section}

|type|kafka版本|
|----|-------|
|kafka08|0.8.22|
|kafka09|0.9.0.1|
|kafka010|0.10.2.1|
|kafka011|0.11.0.2|

