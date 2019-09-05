# 配置TSDB Writer {#concept_645306 .concept}

TSDB Writer插件实现了将数据点写入阿里巴巴自主研究的TSDB数据库。

时间序列数据库（Time Series Database , 简称TSDB）是一种高性能、低成本、稳定可靠的在线时序数据库服务。提供高效读写、高压缩比存储、时序数据插值及聚合计算，广泛应用于物联网（IoT）设备监控系统 、企业能源管理系统（EMS）、生产安全监控系统和电力检测系统等行业场景。

TSDB提供百万级时序数据秒级写入、高压缩比低成本存储、预降采样、插值和多维聚合计算、查询结果可视化功能。TSDB可以解决由于设备采集点数量大、数据采集频率高造成的存储成本高、写入和查询分析效率低等问题。

目前仅支持脚本模式配置方式，更多详情请参见[时序时空数据库](https://help.aliyun.com/document_detail/55652.html)文档。

## 实现原理 {#section_792_evr_e29 .section}

TSDB Writer通过HTTP连接TSDB实例，并通过`/api/put`接口将数据点写入。

## 约束限制 {#section_udo_vgf_tuu .section}

目前仅支持兼容TSDB 2.4.x及以上版本。

## 支持的数据类型 {#section_pcb_k1t_kcz .section}

|类型分类|数据集成column配置类型|TSDB数据类型|
|----|--------------|--------|
|字符串|STRING|TSDB数据点序列化字符串，包括TIMESTAMP、METRIC、TAGS和VALUE。|

## 参数说明 {#section_exm_21k_fvl .section}

|数据源|参数|描述|是否必选|默认值|
|---|--|--|----|---|
|公共参数|sourceDbType|数据源的类型。|否|TSDB **说明：** 目前支持TSDB和RDB两个取值。其中，TSDB包括OpenTSDB、InfluxDB、Prometheus和TimeScale 。RDB包括MySQL、Oracle、PostgreSQL、DRDS等。

 |
|数据源为TSDB|endpoint|TSDB的HTTP连接地址。|是，格式为`http://IP:Port`。|无|
|batchSize|每次批量写入数据的条数。|否，数据类型为INT，需要确保大于0。|100|
|maxRetryTime|失败后重试的次数。|否，数据类型为INT，需要确保大于1。|3|
|ignoreWriteError|如果设置为true，则忽略写入错误，继续写入。如果多次重试后仍写入失败，则终止写入任务。|否，数据类型为BOOL。|false|
|数据源为RDB|endpoint|TSDB的HTTP连接地址。|是，格式为`http://IP:Port`。|无|
|column|关系型数据库中表的字段名。|是|无 **说明：** 此处的字段顺序，需要和 Reader插件中配置的column字段的顺序保持一致。

 |
|columnType|关系型数据库中表字段，映射到TSDB中的类型。支持的类型如下所示： -   timestamp：该字段为时间戳。
-   tag：该字段为tag。
-   metric\_num：该Metric的value是数值类型。
-   metric\_string：该Metric的value是字符串类型。

 |是|无 **说明：** 此处的字段顺序，需要和 Reader插件中配置的column字段的顺序保持一致。

 |
|batchSize|每次批量写入数据的条数。|否，数据类型为INT，需要确保大于0。|100|

## 向导开发介绍 {#section_spr_tcv_x24 .section}

暂不支持向导模式开发。

## 脚本开发介绍 {#section_zei_h6k_izg .section}

配置一个同步数据至TSDB的作业。

``` {#codeblock_o35_st2_z2z}
```json
{
    "order": {
        "hops": [
            {
                "from": "Reader",
                "to": "Writer"
            }
        ]
    },
    "setting": {
        "errorLimit": {
            "record": "0"
        },
        "speed": {
            "concurrent": 1,
            "throttle": true
        }
    },
    "steps": [
        {
            "category": "reader",
            "name": "Reader",
            "parameter": {},
            "stepType": ""
        },
        {
            "category": "writer",
            "name": "Writer",
            "parameter": {
                "endpoint": "http://localhost:8242",
                "sourceDbType": "RDB",
                "batchSize": 256,
                "column": [
                    "name",
                    "type",
                    "create_time",
                    "price"
                ],
                "columnType": [
                    "tag",
                    "tag",
                    "timestamp",
                    "metric_num"
                ]
            },
            "stepType": "tsdb"
        }
    ],
    "type": "job",
    "version": "2.0"
}
```
```

## 性能报告 {#section_m17_ebx_br7 .section}

-   性能数据特征
    -   Metric：指定一个Metric为m。
    -   tagkv：前4个tagkv全排列，形成`10*20*100*100=2,000,000`条时间线，最后IP对应2,000,000条时间线，从1开始自增。

        |tag\_k|tag\_v|
        |------|------|
        |zone|z1~z10|
        |cluster|c1~c20|
        |group|g1~100|
        |app|a1~a100|
        |ip|ip1~ip2,000,000|

    -   value：度量值为\[1, 100\]区间内的随机值。
    -   interval：采集周期为10秒，持续摄入3小时，总数据量为`3*60*60/10*2,000,000=2,160,000,000`个数据点。
-   性能测试结果

    |通道数|数据集成速度（Rec/s）|数据集成流量（MB/s）|
    |---|-------------|------------|
    |1|129,753|15.45|
    |2|284,953|33.70|
    |3|385,868|45.71|


