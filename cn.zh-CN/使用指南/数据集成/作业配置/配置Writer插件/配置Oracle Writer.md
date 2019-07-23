# 配置Oracle Writer {#concept_dzy_j2n_q2b .concept}

本文将为您介绍Oracle Writer支持的数据类型、写入方式、字段映射和数据源等参数及配置示例。

Oracle Writer插件实现了写入数据到Oracle主库的目标表的功能。在底层实现上，Oracle Writer通过JDBC连接远程Oracle数据库，并执行相应的`insert into...`SQL语句，将数据写入Oracle。

**说明：** 开始配置Oracle Writer插件前，请首先配置好数据源，详情请参见[配置Oracle数据源](intl.zh-CN/使用指南/数据集成/数据源配置/配置Oracle数据源.md#)。

Oracle Writer面向ETL开发工程师，使用Oracle Writer从数仓导入数据至Oracle。同时Oracle Writer也可以作为数据迁移工具，为数据库管理员等用户提供服务。

Oracle Writer通过数据同步框架获取Reader生成的协议数据，然后通过JDBC连接远程Oracle数据库，并执行相应的SQL语句，将数据写入Oracle。

## 类型转换列表 {#section_h4p_w2n_q2b .section}

Oracle Writer支持大部分Oracle类型，但也存在个别类型没有支持的情况，请注意检查您的数据类型。

Oracle Writer针对Oracle类型的转换列表，如下所示。

|类型分类|Oracle数据类型|
|:---|:---------|
|整数类|NUMBER、RAWID、INTEGER、INT和SMALLINT|
|浮点类|NUMERIC、DECIMAL、FLOAT、DOUBLE PRECISIOON和REAL|
|字符串类|LONG、CHAR、NCHAR、VARCHAR、VARCHAR2、NVARCHAR2、CLOB、NCLOB、CHARACTER、CHARACTER VARYING、CHAR VARYING、NATIONAL CHARACTER、NATIONAL CHAR、NATIONAL CHARACTER VARYING、NATIONAL CHAR VARYING和NCHAR VARYING|
|日期时间类|TIMESTAMP和DATE|
|布尔型|BIT和BOOL|
|二进制类|BLOB、BFILE、RAW和LONG RAW|

## 参数说明 {#section_jn2_gqh_p2b .section}

|参数|描述|是否必选|默认值|
|:-|:-|:---|:--|
|datasource|数据源名称，脚本模式支持添加数据源，此配置项填写的内容必须要与添加的数据源名称保持一致。|是|无|
|table|目标表名称，如果表的schema信息和上述配置username不一致，请使用schema.table的格式填写table信息。|是|无|
|writeMode|选择导入模式，可以支持insert into、on duplicate key update和replace into三种方式。 -   insert into：当主键/唯一性索引冲突时会写不进去冲突的行，以脏数据的形式体现。
-   on duplicate key update：没有遇到主键/唯一性索引冲突时，与`insert into`行为一致。冲突时会用新行替换已经指定的字段的语句，写入数据至MySQL。
-   replace into：没有遇到主键/唯一性索引冲突时，与`insert into`行为一致。冲突时会先删除原有行，再插入新行。即新行会替换原有行的所有字段。

 |否|insert|
|column|目标表需要写入数据的字段，字段之间用英文逗号分隔。例如`"column": ["id”,”name”,”age”]`。如果要依次写入全部列，使用\*表示。例如`"column":["*"]`。|是|无|
|preSql|执行数据同步任务之前率先执行的SQL语句。目前向导模式仅允许执行一条SQL语句，脚本模式可以支持多条SQL语句，例如清除旧数据。|否|无|
|postSql|执行数据同步任务之后执行的SQL语句。目前向导模式仅允许执行一条SQL语句，脚本模式可以支持多条SQL语句，例如加上某一个时间戳。|否|无|
|batchSize|一次性批量提交的记录数大小，该值可以极大减少数据同步系统与MySQL的网络交互次数，并提升整体吞吐量。如果该值设置过大，会导致数据同步运行进程OOM异常。|否|1,024|

## 向导开发介绍 {#section_bp2_wsh_p2b .section}

1.  选择数据源。

    配置同步任务的**数据来源**和**数据去向**。

    ![选择数据源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16251/15638559248194_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**数据源**|即上述参数说明中的datasource，通常填写您配置的数据源名称。|
    |**表**|即上述参数说明中的table。|
    |**导入前准备语句**|即上述参数说明中的preSql，输入执行数据同步任务之前率先执行的SQL语句。|
    |**导入后完成语句**|即上述参数说明中的postSql，输入执行数据同步任务之后执行的SQL语句。|
    |**主键冲突**|即上述参数说明中的writeMode，可以选择需要的导入模式。|

2.  字段映射，即上述参数说明中的column。

    左侧的源头表字段和右侧的目标表字段为一一对应关系。单击**添加一行**可以增加单个字段，鼠标放至需要删除的字段上，即可单击**删除**图标进行删除。

    ![字段映射](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16227/15638559247782_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**同名映射**|单击**同名映射**，可以根据名称建立相应的映射关系，请注意匹配数据类型。|
    |**同行映射**|单击**同行映射**，可以在同行建立相应的映射关系，请注意匹配数据类型。|
    |**取消映射**|单击**取消映射**，可以取消建立的映射关系。|
    |**自动排版**|可以根据相应的规律自动排版。|
    |**手动编辑源表字段**|请手动编辑字段，一行表示一个字段，首尾空行会被采用，其他空行会被忽略。|
    |**添加一行**|     -   可以输入常量，输入的值需要使用英文单引号，如'abc'、'123'等。
    -   可以配合调度参数使用，如$\{bizdate\}等。
    -   可以输入关系数据库支持的函数，如now\(\)、count\(1\)等。
    -   如果您输入的值无法解析，则类型显示为未识别。
 |

3.  通道控制。

    ![通道控制](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16221/15638559247675_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**任务期望最大并发数**|数据同步任务内，可以从源并行读取或并行写入数据存储端的最大线程数。向导模式通过界面化配置并发数，指定任务所使用的并行度。|
    |**同步速率**|设置同步速率可以保护读取端数据库，以避免抽取速度过大，给源库造成太大的压力。同步速率建议限流，结合源库的配置，请合理配置抽取速率。|
    |**错误记录数**|错误记录数，表示脏数据的最大容忍条数。|
    |**任务资源组**|任务运行的机器，如果任务数比较多，使用默认资源组出现等待资源的情况，建议购买独享数据集成资源或添加自定义资源组，详情请参见[DataWorks独享资源](../../../../intl.zh-CN/产品定价/预付费（包年包月）/DataWorks独享资源.md#)和[新增任务资源](intl.zh-CN/使用指南/数据集成/常见配置/新增任务资源.md#)。|


## 脚本开发介绍 {#section_cp2_wsh_p2b .section}

配置一个写入Oracle的作业。

``` {#codeblock_xkd_wv2_u4h}
{
    "type":"job",
    "version":"2.0",//版本号。
    "steps":[
        { //下面是关于Writer的模板，您可以查找相应数据源的写插件文档。
            "stepType":"stream",
            "parameter":{},
            "name":"Reader",
            "category":"reader"
        },
        {
            "stepType":"oracle",//插件名。
            "parameter":{
                "postSql":[],//执行数据同步任务之后执行的SQL语句。
                "datasource":"",
                "session":[],//数据库连接会话参数。
                "column":[//字段。
                    "id",
                    "name"
                ],
                "encoding":"UTF-8",//编码格式。
                "batchSize":1024,//一次性批量提交的记录数大小。
                "table":"",//表名。
                "preSql":[]//执行数据同步任务之前执行的SQL语句。
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
            "concurrent":1,//并发数。
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

