# 配置MySQL Writer {#concept_ynf_pzm_q2b .concept}

本文将为您介绍MySQL Writer支持的数据类型、字段映射和数据源等参数及配置示例。

MySQL Writer插件实现了写入数据至MySQL数据库目标表的功能。在底层实现上， MySQL Writer通过JDBC连接远程MySQL数据库，并执行相应的`insert into`或`replace into`语句，将数据写入MySQL。数据库本身采用InnoDB引擎，以将数据分批次提交入库。

**说明：** 

-   开始配置MySQL Writer插件前，请首先配置好数据源，详情请参见[配置MySQL数据源](intl.zh-CN/使用指南/数据集成/数据源配置/配置MySQL数据源.md#)。
-   目前MySQL Writer暂不支持MySQL 8.0及以上版本。

MySQL Writer作为数据迁移工具，为数据库管理员等用户提供服务。根据您配置的writeMode，通过数据同步框架获取Reader生成的协议数据。

**说明：** 整个任务必须具备`insert/replace into`的权限。您可以根据配置任务时，在preSql和postSql中指定的语句，判断是否需要其他权限。

## 类型转换列表 {#section_f5g_g1n_q2b .section}

目前MySQL Writer支持大部分MySQL类型，但也存在个别类型没有支持的情况，请注意检查您的数据类型。

MySQL Writer针对MySQL类型的转换列表，如下所示。

|类型分类|MySQL数据类型|
|:---|:--------|
|整数类|INT、TINYINT、SMALLINT、MEDIUMINT、BIGINT和YEAR|
|浮点类|FLOAT、DOUBLE和DECIMAL|
|字符串类|VARCHAR、CHAR、TINYTEXT、TEXT、MEDIUMTEXT和LONGTEXT|
|日期时间类|DATE、DATETIME、TIMESTAMP和TIME|
|布尔型|BOOL|
|二进制类|TINYBLOB、MEDIUMBLOB、BLOB、LONGBLOB和VARBINARY|

## 参数说明 {#section_jn2_gqh_p2b .section}

|参数|描述|必选|默认值|
|:-|:-|:-|:--|
|datasource|数据源名称，脚本模式支持添加数据源，此配置项填写的内容必须与添加的数据源名称保持一致。|是|无|
|table|选取的需要同步的表名称。|是|无|
|writeMode|选择导入模式，可以支持insert into、on duplicate key update和replace into三种方式。 -   insert into：当主键/唯一性索引冲突时会写不进去冲突的行，以脏数据的形式体现。
-   on duplicate key update：没有遇到主键/唯一性索引冲突时，与`insert into`行为一致。冲突时会用新行替换已经指定的字段的语句，写入数据至MySQL。
-   replace into：没有遇到主键/唯一性索引冲突时，与`insert into`行为一致。冲突时会先删除原有行，再插入新行。即新行会替换原有行的所有字段。

 |否|insert|
|column|目标表需要写入数据的字段，字段之间用英文所逗号分隔，例如`"column": ["id", "name", "age"]`。如果要依次写入全部列，使用\*表示， 例如`"column": ["*"]`。|是|无|
|preSql|执行数据同步任务之前率先执行的SQL语句。目前向导模式仅允许执行一条SQL语句，脚本模式可以支持多条SQL语句，例如清除旧数据。 **说明：** 当有多条SQL语句时，不支持事务。

 |否|无|
|postSql|执行数据同步任务之后执行的SQL语句，目前向导模式仅允许执行一条SQL语句，脚本模式可以支持多条SQL语句，例如加上某一个时间戳。 **说明：** 当有多条SQL语句时，不支持事务。

 |否|无|
|batchSize|一次性批量提交的记录数大小，该值可以极大减少数据同步系统与MySQL的网络交互次数，并提升整体吞吐量。如果该值设置过大，会导致数据同步运行进程OOM异常。|否|1,024|

## 向导开发介绍 {#section_bp2_wsh_p2b .section}

1.  选择数据源。

    配置同步任务的**数据来源**和**数据去向**。

    ![选择数据源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16250/15638582278183_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**数据源**|即上述参数说明中的datasource，通常填写您配置的数据源名称。|
    |**表**|即上述参数说明中的table。|
    |**导入前准备语句**|即上述参数说明中的preSql，输入执行数据同步任务之前率先执行的SQL语句。|
    |**导入后完成语句**|即上述参数说明中的postSql，输入执行数据同步任务之后执行的SQL语句。|
    |**主键冲突**|即上述参数说明中的writeMode，可以选择需要的导入模式。|

2.  字段映射，即上述参数说明中的column。

    左侧的源头表字段和右侧的目标表字段为一一对应的关系。单击**添加一行**可以增加单个字段，将鼠标放至需要删除的字段上，即可单击**删除**按钮进行删除。

    ![字段映射](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16227/15638582277782_zh-CN.png)

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

    ![通道控制](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16221/15638582277675_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**任务期望最大并发数**|数据同步任务内，可以从源并行读取或并行写入数据存储端的最大线程数。向导模式通过界面化配置并发数，指定任务所使用的并行度。|
    |**同步速率**|设置同步速率可以保护读取端数据库，以避免抽取速度过大，给源库造成太大的压力。同步速率建议限流，结合源库的配置，请合理配置抽取速率。|
    |**错误记录数**|错误记录数，表示脏数据的最大容忍条数。|
    |**任务资源组**|任务运行的机器，如果任务数比较多，使用默认资源组出现等待资源的情况，建议购买独享数据集成资源或添加自定义资源组，详情请参见[DataWorks独享资源](../../../../intl.zh-CN/产品定价/预付费（包年包月）/DataWorks独享资源.md#)和[新增任务资源](intl.zh-CN/使用指南/数据集成/常见配置/新增任务资源.md#)。|


## 脚本开发介绍 {#section_cp2_wsh_p2b .section}

脚本配置样例如下，详情请参见上述参数说明。

``` {#codeblock_fh9_5bp_qa5 .language-json}
{
    "type":"job",
    "version":"2.0",//版本号。
    "steps":[ //下面是关于Writer的模板，您可以查找相应数据源的写插件文档。
        {
            "stepType":"stream",
            "parameter":{},
            "name":"Reader",
            "category":"reader"
        },
        {
            "stepType":"mysql",//插件名。
            "parameter":{
                "postSql":[],//导入后的准备语句。
                "datasource":"",//数据源。
                "column":[//列名。
                    "id",
                    "value"
                ],
                "writeMode":"insert",//写入模式。
                "batchSize":1024,//一次性批量提交的记录数大小。
                "table":"",//表名。
                "preSql":[]//导入前的准备语句。
            },
            "name":"Writer",
            "category":"writer"
        }
    ],
    "setting":{
        "errorLimit":{//错误记录数。
            "record":"0"
        },
        "speed":{
            "throttle":false,//是否限流。
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

