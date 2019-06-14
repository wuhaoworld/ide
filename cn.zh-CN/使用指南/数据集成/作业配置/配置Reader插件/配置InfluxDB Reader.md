# 配置InfluxDB Reader {#concept_627914 .concept}

InfluxDB是由InfluxData开发的开源时序型数据库，它由Go写成，致力于高性能地查询与存储时序型数据。InfluxDB Reader插件实现了从InfluxDB读取数据。

目前InfluxDB Reader仅支持脚本模式配置，更多详情请参见[InfluxDB](https://www.influxdata.com/)。

## 实现原理 {#section_til_uw3_otp .section}

在底层实现上，InfluxDB Reader通过Java Client，将SQL查询请求发送到InfluxDB实例，扫描出指定的数据点。整个同步的过程通过Database、Metric和时间段进行切分，组合为一个迁移Task。

## 约束限制 {#section_vut_gc0_kkx .section}

-   指定起止时间会被自动转为整点时刻，例如2019-4-18的`[3:35, 4:55)`，会被转为`[3:00, 4:00)`。
-   目前仅支持兼容InfluxDB 0.9及以上版本。

## 支持的数据类型 {#section_dfx_w6m_n3h .section}

|类型分类|数据集成column配置类型|TSDB数据类型|
|----|--------------|--------|
|字符串|string|TSDB数据点序列化字符串，包括timestamp、metric、tags和value。|

## 参数说明 {#section_z81_5ee_hus .section}

|参数|描述|是否必选|默认值|
|--|--|----|---|
|endpoint|InfluxDB的HTTP连接地址。|是，格式为`http://IP:Port。`|无|
|database|指定InfluxDB的数据库。|是|无|
|username|用于连接InfluxDB的账号。|是|无|
|password|用于连接InfluxDB的密码。|是|无|
|column|数据迁移任务需要迁移的Metric列表。|是|无|
|beginDateTime|和endDateTime配合使用，用于指定哪个时间段内的数据点需要被迁移。|是，格式为`yyyyMMddHHmmss`。|无 **说明：** 指定起止时间会自动忽略分钟和秒，转为整点时刻。例如2019-4-18的`[3:35, 4:55)`会被转为`[3:00, 4:00)`。

 |
|endDateTime|和beginDateTime配合使用，用于指定哪个时间段内的数据点需要被迁移。|是，格式为`yyyyMMddHHmmss`。|无 **说明：** 指定起止时间会自动忽略分钟和秒，转为整点时刻。例如2019-4-18的`[3:35, 4:55)`会被转为`[3:00, 4:00)`。

 |

## 向导开发介绍 {#section_7p3_u7l_ovg .section}

暂不支持向导模式开发。

## 脚本开发介绍 {#section_6yr_67x_zsx .section}

配置一个从InfluxDB数据库同步的作业。

``` {#codeblock_dwi_qoe_77l}
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
                "endpoint": "http://host:8086",
                "database": "",
                "username": "",
                "password": "",
                "column": [
                    "xc"
                ],
                "endDateTime": "20190515180000",
                "beginDateTime": "20190515170000"
            },
            "stepType": "influxdb"
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

