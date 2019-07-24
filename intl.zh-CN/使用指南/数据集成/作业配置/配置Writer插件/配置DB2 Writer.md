# 配置DB2 Writer {#concept_prk_khl_q2b .concept}

本文为您介绍DB2 Writer支持的数据类型、字段映射和数据源等参数及配置示例。

DB2 Writer插件为您提供写入数据至DB2数据库的目标表的功能。在底层实现上，DB2 Writer通过JDBC连接远程DB2数据库，执行相应的`insert into`语句，将数据写入DB2，内部会分批次提交入库。

DB2 Writer面向ETL开发工程师，使用DB2 Writer从数仓导入数据至DB2。同时DB2 Writer可以作为数据迁移工具，为数据库管理员等用户提供服务。

DB2 Writer通过数据同步框架获取Reader生成的协议数据，通过`insert into`（当主键/唯一性索引冲突时，冲突的行会写不进去）语句，写入数据至DB2。另外出于性能考虑采用了`PreparedStatement + Batch`，并且设置了`rewriteBatchedStatements=true`，将数据缓冲到线程上下文Buffer中，当Buffer累计到预定阈值时，才发起写入请求。

**说明：** 整个任务至少需要具备`insert into`的权限，是否需要其他权限，取决于您配置任务时在preSql和postSql中指定的语句。

DB2 Writer支持大部分DB2类型，但也存在个别没有支持的情况，请注意检查您的数据类型。

DB2 Writer针对DB2类型的转换列表，如下所示。

|类型分类|DB2数据类型|
|:---|:------|
|整数类|SMALLINT|
|浮点类|DECIMAL、REAL和DOUBLE|
|字符串类|CHAR、CHARACTER、VARCHAR、GRAPHIC、VARGRAPHIC、LONG VARCHAR、CLOB、LONG VARGRAPHIC和DBCLOB|
|日期时间类|DATE、TIME和TIMESTAMP|
|布尔类|—|
|二进制类|BLOB|

## 参数说明 {#section_jn2_gqh_p2b .section}

|参数|描述|必选|默认值|
|:-|:-|:-|:--|
|jdbcUrl|描述的是到DB2数据库的JDBC连接信息，jdbcUrl按照DB2官方规范，DB2格式为jdbc:db2://ip:port/database，并可以填写连接附件控制信息。|是|无|
|username|数据源的用户名 。|是|无|
|password|数据源指定用户名的密码 。|是|无|
|table|所选取的需要同步的表 。|是|无|
|column|目标表需要写入数据的字段，字段之间用英文逗号分隔。例如："column": \["id", "name", "age"\]。如果要依次写入全部列，使用（\*）表示。例如"column": \["\*"\]。|是|无|
|preSql|执行数据同步任务之前率先执行的SQL语句，目前仅允许执行一条SQL语句，例如清除旧数据。|否|无|
|postSql|执行数据同步任务之后执行的SQL语句，目前向导模式仅允许执行一条SQL语句，脚本模式可以支持多条SQL语句，例如加上某一个时间戳。|否|无|
|batchSize|一次性批量提交的记录数大小，该值可以极大减少数据同步系统与MySQL的网络交互次数，并提升整体吞吐量。如果该值设置过大，会导致数据同步运行进程OOM异常。|否|1,024|

## 向导开发介绍 {#section_bp2_wsh_p2b .section}

暂不支持向导开发模式。

## 脚本开发介绍 {#section_cp2_wsh_p2b .section}

配置一个写入DB2的数据同步作业。

``` {#codeblock_xp9_v1g_nda}
{
    "type":"job",
    "version":"2.0",//版本号
    "steps":[
        { //下面是关于Writer的模板，您可以查找相应数据源的写插件文档。
            "stepType":"stream",
            "parameter":{},
            "name":"Reader",
            "category":"reader"
        },
        {
            "stepType":"db2",//插件名。
            "parameter":{
                "postSql":[],//执行数据同步任务之前率先执行的SQL语句。
                "password":"",//密
                "jdbcUrl":"jdbc:db2://ip:port/database",//DB2数据库的JDBC连接信息。
                "column":[
                    "id"
                ],
                "batchSize":1024,//一次性批量提交的记录数大小。
                "table":"",//表名。
                "username":"",//用户名。
                "preSql":[]//执行数据同步任务之后执行的SQL语句。
            },
            "name":"Writer",
            "category":"writer"
        }
    ],
    "setting":{
        "errorLimit":{
            "record":"0"//错误记录数。
        },
        "speed":{
            "throttle":false,//false代表不限流，下面的限流的速度不生效，true代表限流。
            "concurrent":1,//作业并发数。
        }
    },
    "order":{
        "hops":[
            {
                "from":"Reader",
                "to":"Writer"
            }
        ]
    }
}
```

