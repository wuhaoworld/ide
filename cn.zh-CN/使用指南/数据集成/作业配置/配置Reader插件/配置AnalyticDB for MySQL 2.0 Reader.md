# 配置AnalyticDB for MySQL 2.0 Reader {#concept_261553 .concept}

本文将为您介绍AnalyticDB for MySQL 2.0 Reader支持的数据类型、字段映射和数据源等参数及配置示例。

AnalyticDB for MySQL 2.0 Reader插件实现了从AnalyticDB for MySQL 2.0读取数据。在底层实现上，AnalyticDB for MySQL 2.0 Reader通过JDBC连接远程AnalyticDB for MySQL 2.0数据库，并根据AnalyticDB for MySQL 2.0的推荐分页大小，执行相应的SQL语句，从AnalyticDB for MySQL 2.0库中分批读取数据。

## 数据类型转换 {#section_u26_mcc_bmz .section}

|AnalyticDB for MySQL 2.0类型|DataX类型|MaxCompute类型|
|--------------------------|-------|------------|
|BIGINT|LONG|BIGINT|
|TINYINT|LONG|INT|
|TIMESTAMP|DATE|DATETIME|
|VARCHAR|STRING|STRING|
|SMALLINT|LONG|INT|
|INT|LONG|INT|
|FLOAT|STRING|DOUBLE|
|DOUBLE|STRING|DOUBLE|
|DATE|DATE|DATETIME|
|TIME|DATE|DATETIME|

**说明：** 不支持multivalue，会直接异常退出。

## 使用限制 {#section_yj7_ohb_ja8 .section}

当前版本，在大批量数据导出并且配置较低的机器上，会出现超时的情况。

-   当前mode=Select时，上限为30万行。
-   当前​mode=ODPS时，上限为1亿行。
-   50列以上为AnalyticDB for MySQL 2.0本身的限制，需要联系AnalyticDB for MySQL 2.0的管理员进行手动调整。
-   Java版本需要1.8及以上，编译转码`native2ascii LocalStrings.properties > LocalStrings_zh_CN.properties`。

## 参数说明 {#section_hmf_zcs_dm0 .section}

|参数|描述|是否必选|默认值|
|--|--|----|---|
|table|需要导出的表的名称。|是|无|
|column|列名，如果没有，则为全部。|否|\*|
|limit|限制导出的记录数。|否|无|
|where|where条件，方便添加筛选条件，此处的String会被直接作为SQL条件添加到查询语句中，例如`where id < 100`。|否|无|
|mode|目前支持Select和ODPS2种导入类型。 -   Select：使用limit分页。
-   ODPS：使用ODPS DUMP来导出数据，需要有ODPS的访问权限。

 |否|Select|
|odps.accessKey|当mode=ODPS时必填，AnalyticDB for MySQL 2.0访问ODPS使用的云账号AccessKey，需要有Describe、Create、Select、Alter、Update和Drop权限。|否|无|
|odps.accessId|当mode=ODPS时必填，AnalyticDB for MySQL 2.0访问ODPS使用的云账号AccessID，需要有Describe、Create、Select、Alter、Update和Drop权限。|否|无|
|odps.odpsServer|当mode=ODPS时必填，ODPS API地址。|否|无|
|odps.tunnelServer|当mode=ODPS时必填，ODPS Tunnel地址。|否|无|
|odps.project|当mode=ODPS时必填，ODPS Project名称。|否|无|
|odps.accountType|当mode=ODPS时生效，ODPS访问账号类型。|否|aliyun|

## 配置文件示例 {#section_xki_zlm_a5k .section}

``` {#codeblock_bl2_ruf_xf5}
{
    "type": "job",
    "steps": [
        {
            "stepType": "ads",
            "parameter": {
                "datasource": "ads_demo",
                "table": "th_test",
                "column": [
                    "id",
                    "testtinyint",
                    "testbigint",
                    "testdate",
                    "testtime",
                    "testtimestamp",
                    "testvarchar",
                    "testdouble",
                    "testfloat"
                ],
                "odps": {
                    "accessId": "*********",
                    "accessKey": "*********",
                    "account": "*********@aliyun.com",
                    "odpsServer": " http://service.cn.maxcompute.aliyun-inc.com/api",
                    "tunnelServer": "http://dt.cn-shanghai.maxcompute.aliyun-inc.com",
                    "accountType": "aliyun",
                    "project": "odps_test"
                },
                "mode": "ODPS"
            },
            "name": "Reader",
            "category": "reader"
        },
        {
            "stepType": "stream",
            "parameter": {},
            "name": "Writer",
            "category": "writer"
        }
    ],
    "version": "2.0",
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
            "record": ""
        },
        "speed": {
            "concurrent": 2,
            "throttle": false,
        }
    }
}
```

