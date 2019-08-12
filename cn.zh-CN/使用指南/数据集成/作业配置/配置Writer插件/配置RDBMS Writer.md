# 配置RDBMS Writer {#concept_e12_jyt_q2b .concept}

本文为您介绍RDBMS Writer支持的数据类型、写入方式、字段映射和数据源等参数及配置示例。

RDBMS Writer插件实现了写入数据至RDBMS主库的目的表的功能。在底层实现上，RDBMS Writer通过DataX框架获取Reader生成的协议数据，通过JDBC连接远程RDBMS数据库，并执行相应的`insert into...`的SQL语句，将数据写入RDBMS。RDBMS Writer是一个通用的关系数据库写插件，您可以通过注册数据库驱动等方式，增加任意多样的关系数据库写支持。

RDBMS Writer面向ETL开发工程师，通过RDBMS Writer从数仓导入数据至RDBMS。同时RDBMS Writer也可以作为数据迁移工具，为数据库管理员等用户提供服务。

## 类型转换 {#section_7nf_x56_2qg .section}

目前RDBMS Writer支持数字、字符等大部分通用的关系数据库类型，但也存在部分类型没有支持的情况，请注意检查您的数据类型。

## 参数说明 {#section_0ok_thu_r3t .section}

|参数|描述|是否必选|默认值|
|:-|:-|:---|:--|
|jdbcUrl|描述的是到对端数据库的JDBC连接信息，JDBCUrl按照RDBMS官方规范，并可填写连接附件控制信息。请注意不同的数据库JDBC的格式是不同的，DataX会根据具体jdbc的格式选择合适的数据库驱动完成数据读取。 -   DM格式：`jdbc:dm://ip:port/database`
-   DB2格式：`jdbc:db2://ip:port/database`
-   PPAS格式：`jdbc:edb://ip:port/database`

 |是|无|
|username|数据源的用户名。|是|无|
|password|数据源指定用户名的密码。|是|无|
|table|目标表名称，如果表的schema信息和上述配置username不一致，请使用schema.table的格式填写table信息。|是|无|
|column|所配置的表中需要同步的列名集合。以英文逗号（,）进行分隔。 **说明：** 建议您不要使用默认列情况。

 |是|无|
|preSql|执行数据同步任务之前率先执行的SQL语句，目前只允许执行一条SQL语句，例如清除旧数据。 **说明：** 当有多条SQL语句时，不支持事务。

 |否|无|
|postSql|执行数据同步任务之后执行的SQL语句，目前只允许执行一条SQL语句，例如加上某一个时间戳。 **说明：** 当有多条SQL语句时，不支持事务。

 |否|无|
|batchSize|一次性批量提交的记录数大小，该值可以极大减少数据集成与PostgreSQL的网络交互次数，并提升整体吞吐量。但是该值设置过大可能会造成数据集成运行进程OOM情况。|否|1024|

## 功能说明 {#section_vhx_qk5_q2b .section}

配置一个写入RDBMS的作业。

``` {#codeblock_xev_moz_0tl}
{
    "job": {
        "setting": {
            "speed": {
                "channel": 1
            }
        },
        "content": [
            {
                "reader": {
                    "name": "streamreader",
                    "parameter": {
                        "column": [
                            {
                                "value": "DataX",
                                "type": "string"
                            },
                            {
                                "value": 19880808,
                                "type": "long"
                            },
                            {
                                "value": "1988-08-08 08:08:08",
                                "type": "date"
                            },
                            {
                                "value": true,
                                "type": "bool"
                            },
                            {
                                "value": "test",
                                "type": "bytes"
                            }
                        ],
                        "sliceRecordCount": 1000
                    }
                },
                "writer": {
                    "name": "RDBMS Writer",
                    "parameter": {
                        "connection": [
                            {
                                "jdbcUrl": "jdbc:dm://ip:port/database",
                                "table": [
                                    "table"
                                ]
                            }
                        ],
                        "username": "username",
                        "password": "password",
                        "table": "table",
                        "column": [
                            "*"
                        ],
                        "preSql": [
                            "delete from XXX;"
                        ]
                    }
                }
            }
        ]
    }
}
```

RDBMS Writer增加新的数据库支持的操作如下。

1.  进入RDBMS Writer对应目录，这里$\{DATAX\_HOME\}为DataX主目录，即$\{DATAX\_HOME\}/plugin/writer/RDBMS Writer。
2.  在RDBMS Writer插件目录下有plugin.json配置文件，在此文件中注册您具体的数据库驱动，具体放在drivers数组中。RDBMS Writer插件在任务执行时，会动态选择合适的数据库驱动连接数据库。

    ``` {#codeblock_z7j_16r_w5x}
    {
        "name": "RDBMS Writer",
        "class": "com.alibaba.datax.plugin.reader.RDBMS Writer.RDBMS Writer",
        "description": "useScene: prod. mechanism: Jdbc connection using the database, execute select sql, retrieve data from the ResultSet. warn: The more you know about the database, the less problems you encounter.",
        "developer": "alibaba",
        "drivers": [
            "dm.jdbc.driver.DmDriver",
            "com.ibm.db2.jcc.DB2Driver",
            "com.sybase.jdbc3.jdbc.SybDriver",
            "com.edb.Driver"
        ]
    }
    ```

3.  在RDBMS Writer插件目录下有libs子目录，您需要将您具体的数据库驱动放到libs目录下。

    ``` {#codeblock_ste_w1e_wbb}
    $tree
    .
    |-- libs
    |   |-- Dm7JdbcDriver16.jar
    |   |-- commons-collections-3.0.jar
    |   |-- commons-io-2.4.jar
    |   |-- commons-lang3-3.3.2.jar
    |   |-- commons-math3-3.1.1.jar
    |   |-- datax-common-0.0.1-SNAPSHOT.jar
    |   |-- datax-service-face-1.0.23-20160120.024328-1.jar
    |   |-- db2jcc4.jar
    |   |-- druid-1.0.15.jar
    |   |-- edb-jdbc16.jar
    |   |-- fastjson-1.1.46.sec01.jar
    |   |-- guava-r05.jar
    |   |-- hamcrest-core-1.3.jar
    |   |-- jconn3-1.0.0-SNAPSHOT.jar
    |   |-- logback-classic-1.0.13.jar
    |   |-- logback-core-1.0.13.jar
    |   |-- plugin-rdbms-util-0.0.1-SNAPSHOT.jar
    |   `-- slf4j-api-1.7.10.jar
    |-- plugin.json
    |-- plugin_job_template.json
    `-- RDBMS Writer-0.0.1-SNAPSHOT.jar
    ```


