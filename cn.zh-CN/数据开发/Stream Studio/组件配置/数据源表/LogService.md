# LogService {#concept_dsw_xls_wgb .concept}

日志服务（LogService，简称LOG/原SLS）是针对实时数据的一站式服务，无需开发即可完成数据采集、消费、投递以及查询分析等功能，帮助提升运维、运营效率，建立DT时代海量日志处理能力。

日志服务本身是流数据存储，实时计算可以将其作为流式数据输入。更多信息请参见[创建日志服务LOG源表](../../../../cn.zh-CN/Flink SQL开发指南/Flink SQL/DDL语句/创建数据源表/创建日志服务 LOG源表.md#)。

日志服务的数据格式和JSON一致，示例如下。

``` {#codeblock_2na_spo_9w2}
{
    "a": 1000,
    "b": 1234,
    "c": "li"
}
```

## 配置面板说明 {#section_q13_zpf_xgb .section}

|参数|注释说明|备注|
|--|----|--|
|血缘表名（任务唯一）|任务中表的唯一标志，不能与任务中其它血缘表重名。|无|
|列定义|要读取的LogService内容字段和属性字段列表。|无|
|消费端点信息|消费端点信息。|[服务入口](../../../../cn.zh-CN/API 参考/服务入口.md#)|
|accessId|对应SQL中with参数accessId。|无|
|accessKey|对应SQL中with参数accessKey。|无|
|项目|读取的LogService项目。|无|
|LogStore|项目下的具体的LogStore。|无|
|消费组名|消费组名。|您可以自定义消费组名（无固定格式）|
|消费日志开始的时间点|消费日志开始的时间点。|无|
|消费客户端心跳间隔时间|消费客户端心跳间隔时间，单位ms，为可选项。|无|
|读取最大尝试次数|可以尝试读取的最大次数。|无|
|调试开关|如果打开调试开关，会打印出解析异常的日志。|无|

## 类型映射 {#section_jyd_jqf_xgb .section}

日志服务和实时计算字段类型对应关系，建议您使用该对应关系进行DDL声明。

|日志服务字段类型|实时计算字段类型|
|--------|--------|
|STRING|VARCHAR|

## 属性字段 {#section_pnf_qqf_xgb .section}

目前默认支持三个属性字段的获取，也支持其他自定义写入的字段。

|字段名|注释说明|
|---|----|
|`__source__`|消息源|
|`__topic__`|消息主题|
|`__timestamp__`|日志时间|

**说明：** 

-   LogService暂不支持MAP类型的数据。
-   字段顺序支持无序（建议字段顺序和表中定义一致）。
-   输入数据源为JSON形式时，注意定义分隔符，并且需要采用内置函数分析JSON\_VALUE，否则就会解析失败，报错如下。

    ``` {#codeblock_5sc_pp6_7i2}
    2017-12-25 15:24:43,467 WARN [Topology-0 (1/1)] com.alibaba.blink.streaming.connectors.common.source.parse.DefaultSourceCollector - Field missing error, table column number: 3, data column number: 3, data filed number: 1, data: [{"lg_order_code":"LP00000005","activity_code":"TEST_CODE1","occur_time":"2017-12-10 00:00:01"}]
    ```

-   batchGetSize设置不能超过1,000，否则会报错。
-   batchGetSize指明的是logGroup获取的数量。如果单条logItem的大小和batchGetSize都很大，可能会导致频繁的GC，此时需要调小该参数。

