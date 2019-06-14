# 配置Prometheus Reader {#concept_645201 .concept}

Prometheus是时间序列数据库，由SoundCloud开发并维护，是Google BorgMon监控系统的开源版本。Prometheus Reader插件实现了从Prometheus读取数据。

目前Prometheus Reader仅支持脚本模式配置方式。

## 实现原理 {#section_jkl_wwm_k4q .section}

在底层实现上，Prometheus Reader通过HTTP请求连接到Prometheus实例，用`/api/v1/query_range`接口获取原始数据点。整个同步的过程通过Metric和时间段进行切分，组合为一个迁移Task。

## 约束限制 {#section_17c_4cu_mfr .section}

-   指定起止时间会被自动转为整点时刻，例如2019-4-18的`[3:35, 4:55)`，会被转为`[3:00, 4:00)`。
-   目前仅支持兼容Prometheus 2.9.x版本。
-   时间上切分的粒度，默认只有10s。

    `/api/v1/query_range`接口对查询的数据点数量有所限制。如果查询的时间范围过大，会报 `exceeded maximum resolution of 11,000 points per timeseries`的异常。因此插件中默认选择10s作为查询的切分粒度。即使原始数据点的存储粒度为毫秒级，也只会查询出10,000个数据点，可满足 `/api/v1/query_range`接口的限制。


## 支持的数据类型 {#section_thk_j53_8th .section}

|类型分类|数据集成column配置类型|TSDB数据类型|
|----|--------------|--------|
|字符串|string|TSDB数据点序列化字符串，包括timestamp、metric、tags和value。|

## 参数说明 {#section_6av_3m6_143 .section}

|参数|描述|是否必选|默认值|
|--|--|----|---|
|endpoint|Prometheus的HTTP连接地址。|是，格式为`http://IP:Port`。|无|
|column|数据迁移任务需要迁移的Metric列表。|是|无|
|beginDateTime|和endDateTime配合使用，用于指定哪个时间段内的数据点需要被迁移。|是，格式为`yyyyMMddHHmmss`。|无 **说明：** 指定起止时间会自动忽略分钟和秒，转为整点时刻。例如2019-4-18的`[3:35, 4:55)`会被转为`[3:00, 4:00)`。

 |
|endDateTime|和beginDateTime配合使用，用于指定哪个时间段内的数据点需要被迁移。|是，格式为`yyyyMMddHHmmss`。|无 **说明：** 指定起止时间会自动忽略分钟和秒，转为整点时刻。例如2019-4-18的`[3:35, 4:55)`会被转为`[3:00, 4:00)`。

 |

## 向导开发介绍 {#section_yn6_b0v_mg6 .section}

暂不支持向导模式开发。

## 脚本开发介绍 {#section_bll_tk4_243 .section}

配置一个从Prometheus数据库同步的作业。

``` {#codeblock_j29_cg5_s0y}
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
                "endpoint": "http://localhost:9090",
                "column": [
                    "up"
                ],
                "beginDateTime": "20190520150000",
                "endDateTime": "20190520160000"
            },
            "stepType": "prometheus"
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

## 性能测试报告 {#section_xru_yqf_br0 .section}

|通道数|数据集成速度（Rec/s）|数据集成流量（MB/s）|
|---|-------------|------------|
|1|45,000|5.36|
|2|55,384|6.60|
|3|60,000|7.15|

