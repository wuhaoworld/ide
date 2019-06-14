# 配置OpenTSDB Reader {#concept_644823 .concept}

OpenTSDB是主要由Yahoo维护、可扩展、分布式的时序数据库，OpenTSDB Reader插件实现了从OpenTSDB读取数据。

OpenTSDB与阿里巴巴自研TSDB的关系与区别，请参见[相比OpenTSDB优势](https://help.aliyun.com/document_detail/113368.html)。

目前OpenTSDB Reader仅支持脚本模式配置方式。

## 实现原理 {#section_shv_qhe_0sz .section}

在底层实现上，OpenTSDB Reader通过HTTP请求连接到OpenTSDB实例，用`/api/config`接口获取其底层存储HBase的连接信息。然后通过AsyncHBase框架连接HBase，以Scan的方式将数据点扫描出来。整个同步的过程通过Database、Metric和时间段进行切分，即某个Metric在某一个小时内的数据迁移，组合成一个迁移Task。

## 约束限制 {#section_j5v_b0a_f0o .section}

-   指定起止时间会被自动转为整点时刻，例如2019-4-18的`[3:35, 4:55)`，会被转为`[3:00, 4:00)`。
-   目前仅支持兼容OpenTSDB 2.3.x版本。
-   不可直接使用`/api/query`查询获取数据点，需要连接OpenTSDB的底层存储。

    因为通过OpenTSDB的HTTP接口（`/api/query`）读取数据，在数据量较大的情况下，会导致OpenTSDB的异步框架报CallBack过多的异常。所以通过连接底层HBase存储，以Scan的方式扫描数据点，可避免此问题。且通过指定Metric和时间范围，可顺序扫描HBase表，提高查询效率。


## 支持的数据类型 {#section_37q_tdb_de2 .section}

|类型分类|数据集成column配置类型|TSDB数据类型|
|----|--------------|--------|
|字符串|string|TSDB数据点序列化字符串，包括timestamp、metric、tags和value。|

## 参数说明 {#section_ixo_c5e_wuz .section}

|参数|描述|是否必选|默认值|
|--|--|----|---|
|endpoint|OpenTSDB的HTTP连接地址。|是，格式为`http://IP:Port`。|无|
|column|数据迁移任务需要迁移的Metric列表。|是|无|
|beginDateTime|和endDateTime配合使用，用于指定哪个时间段内的数据点需要被迁移。|是，格式为`yyyyMMddHHmmss`。|无 **说明：** 指定起止时间会自动忽略分钟和秒，转为整点时刻。例如2019-4-18的`[3:35, 4:55)`会被转为`[3:00, 4:00)`。

 |
|endDateTime|和beginDateTime配合使用，用于指定哪个时间段内的数据点需要被迁移。|是，格式为`yyyyMMddHHmmss`。|无 **说明：** 指定起止时间会自动忽略分钟和秒，转为整点时刻。例如2019-4-18的`[3:35, 4:55)`会被转为`[3:00, 4:00)`。

 |

## 向导开发介绍 {#section_fav_usi_ede .section}

暂不支持向导模式开发。

## 脚本开发介绍 {#section_np9_xbg_wws .section}

配置一个从OpenTSDB数据库同步抽取数据到本地的作业。

``` {#codeblock_uiz_jim_0n9}
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
            "parameter": {
                "endpoint": "http://host:4242",
                "column": [
                    "xc"
                ],
                "beginDateTime": "20190101000000",
                "endDateTime": "20190101030000"
            },
            "stepType": "opentsdb"
        },
        {
            "category": "writer",
            "name": "Writer",
            "parameter": {},
            "stepType": ""
        }
    ],
    "type": "job",
    "version": "2.0"
}
```
```

## 性能报告 {#section_67i_3o6_0ql .section}

-   性能数据特征

    从Metric、时间线、Value和采集周期四个方面进行描述。

    -   Metric：指定一个Metric为m。
    -   tagkv：前四个tagkv全排列，形成`10*20*100*100=2,000,000`条时间线，最后IP对应2,000,000条时间线，从1开始自增。

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
    |1|215,428|25.65|
    |2|424,994|50.60|
    |3|603,132|71.81|


