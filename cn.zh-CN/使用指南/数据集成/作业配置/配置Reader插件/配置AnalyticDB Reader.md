# 配置AnalyticDB Reader {#concept_261553 .concept}

AnalyticDB Reader插件实现了从AnalyticDB读取数据。在底层实现上，AnalyticDB Reader通过JDBC连接远程AnalyticDB数据库，并根据AnalyticDB的推荐分页大小，执行相应的SQL语句，将数据从AnalyticDB库中分批Select出来。

## 数据类型转换 {#section_u26_mcc_bmz .section}

|AnalyticDB类型|DataX类型|MaxCompute类型|
|------------|-------|------------|
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
-   50列以上为AnalyticDB本身的限制，需要联系AnalyticDB的管理员进行手动调整。
-   Java版本需要1.8及以上，编译转码native2ascii LocalStrings.properties \> LocalStrings\_zh\_CN.properties。

## 参数说明 {#section_hmf_zcs_dm0 .section}

|参数|描述|是否必选|默认值|
|--|--|----|---|
|address|AnalyticDB数据库地址及端口号，例如 127.0.0.1:9999。|是|无|
|username|AnalyticDB数据库访问用户名，通常为对应云账号的AccessID。|是|无|
|password|AnalyticDB数据库访问密码，通常为云账号的AccesssKey。|是|无|
|schema|AnalyticDB数据库名称（即schema）。|是|无|
|table|需要导出的表的名称。|是|无|
|column|列名，如果没有，则为全部。|否|\*|
|limit|限制导出的记录数。|否|无|
|where|where条件，方便添加筛选条件，这里的String会被直接作为SQL条件添加到查询语句中，例如`where id < 100`。|否|无|
|mode|导入类型，目前支持两种类型。 -   Select：使用limit分页。
-   ODPS：使用ODPS DUMP来导出数据，需要有ODPS的访问权限。

 |否|Select|
|odps.accessKey|当mode=ODPS时必填，AnalyticDB访问ODPS使用的云账号AccessKey，需要有Describe、Create、Select、Alter、Update和Drop权限。|否|无|
|odps.accessId|当mode=ODPS时必填，AnalyticDB访问ODPS使用的云账号AccessID，需要有Describe、Create、Select、Alter、Update和Drop权限。|否|无|
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
                "address": "100.81.***.*",
                "port": "9999",
                "username": "*********",
                "password": "*********",
                "datasource": "ads_demo",
                "schema": "ads_test",
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
            "dmu": 1
        }
    }
}
```

