# 配置SQL Server Reader {#concept_bgv_5qq_p2b .concept}

本文将为您介绍SQL Server Reader支持的数据类型、字段映射和数据源等参数及配置示例。

SQL Server Reader插件从SQL Server读取数据。在底层实现上，SQL Server Reader通过JDBC连接远程SQL Server数据库，并执行相应的SQL语句，从SQL Server库中读取数据。

SQL Server Reader通过JDBC连接器连接至远程的SQL Server数据库，根据您配置的信息生成查询SQL语句，发送至远程SQL Server数据库，执行该SQL并返回结果。然后使用数据同步自定义的数据类型拼装为抽象的数据集，传递给下游Writer处理。

-   对于您配置的table、column和where等信息，SQL Server Reader将其拼接为SQL语句发送至SQL Server数据库。
-   对于您配置的querySql信息，SQL Server直接将其发送至SQL Server数据库。

SQL Server Reader支持大部分SQL Server类型，但也存在部分类型没有支持的情况，请注意检查您的数据类型。

SQL Server Reader针对SQL Server的类型转换列表，如下所示。

|类型分类|SQL Server数据类型|
|:---|:-------------|
|整数类|BIGINT、INT、SMALLINT和TINYINT|
|浮点类|FLOAT、DECIMAL、REAL和NUMERIC|
|字符串类|CHAR、NCHAR、NTEXT、NVARCHAR、TEXT、VARCHAR、NVARCHAR（MAX）和VARCHAR（MAX）|
|日期时间类|DATE、DATETIME和TIME|
|布尔型|BIT|
|二进制类|BINARY、VARBINARY、VARBINARY（MAX）和TIMESTAMP|

## 参数说明 {#section_jn2_gqh_p2b .section}

|参数|描述|必选|默认值|
|:-|:-|:-|:--|
|datasource|数据源名称，脚本模式支持添加数据源，此配置项填写的内容必须要与添加的数据源名称保持一致。|是|无|
|table|选取的需要同步的表名称，一个作业只能支持一个表同步。|是|无|
|column|所配置的表中需要同步的列名集合，使用JSON的数组描述字段信息 。默认使用所有列配置，例如\[ \* \]。 -   支持列裁剪，即列可以挑选部分列进行导出。
-   支持列换序，即列可以不按照表schema信息顺序进行导出。
-   支持常量配置，您需要按照MySQL SQL语法格式，例如`["id", "table","1", "'mingya.wmy'", "'null'", "to_char(a+1)", "2.3" , "true"]`。
    -   id为普通列名。
    -   table为包含保留字的列名。
    -   1为整型数字常量。
    -   'mingya.wmy'为字符串常量（注意需要加上一对单引号）。
    -   'null'为字符串。
    -   to\_char\(a + 1\)为函数表达式。
    -   2.3为浮点数。
    -   true为布尔值。
-   column必须显示指定同步的列集合，不允许为空。

 |是|无|
|splitPk|SQL Server Reader进行数据抽取时，如果指定splitPk，表示您希望使用splitPk代表的字段进行数据分片。数据同步系统因此会启动并发任务进行数据同步，这样可以提高数据同步的效能。 -   推荐splitPk用户使用表主键，因为表主键通常情况下比较均匀，因此切分出来的分片也不容易出现数据热点。
-   目前splitPk仅支持整型数据切分，不支持字符串、浮点、日期等其他类型 。如果您指定其他非支持类型，SQL Server Reader将报错。

 |否|无|
|where|筛选条件，SQL Server Reader根据指定的column、table和where条件拼接SQL，并根据该SQL进行数据抽取。例如在测试时，可以将where条件指定为limit 10。在实际业务场景中，往往会选择当天的数据进行同步，将where条件指定为`gmt_create > $bizdate`。 -   where条件可以有效地进行业务增量同步。
-   where条件为空，视作同步全表所有的信息。

 |否|无|
|querySql|使用格式：`"querysql" : "查询statement",`在部分业务场景中，where配置项不足以描述所筛选的条件，您可以通过该配置型来自定义筛选SQL。当配置此项后，数据同步系统就会忽略tables、columns配置项，直接使用这项配置的内容对数据进行筛选，例如需要进行多表join后同步数据，使用`select a,b from table_a join table_b on table_a.id = table_b.id`。当您配置querySql时，SQL Server Reader直接忽略column、table和where条件的配置。|否|无|
|fetchSize|该配置项定义了插件和数据库服务器端每次批量数据获取条数，该值决定了数据集成和服务器端的网络交互次数，能够提升数据抽取性能。 **说明：** fetchSize值过大（\>2048）可能造成数据同步进程OOM。

 |否|1024|

## 向导开发介绍 {#section_bp2_wsh_p2b .section}

1.  选择数据源。

    配置同步任务的数据来源和数据去向。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16232/15633611727861_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**数据源**|即上述参数说明中的datasource，通常填写您配置的数据源名称。|
    |**表**|即上述参数说明中的table，选择需要同步的表。|
    |**数据过滤**|您将要同步数据的筛选条件，暂时不支持limit关键字过滤。SQL语法与选择的数据源一致。|
    |**切分键**|您可以将源数据表中某一列作为切分键，建议使用主键或有索引的列作为切分键。|

2.  字段映射，即上述参数说明中的column。

    左侧的源头表字段和右侧的目标表字段为一一对应关系。单击**添加一行**可以增加单个字段，鼠标放至需要删除的字段上，即可单击**删除**图标进行删除。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16231/15633611727846_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**同名映射**|单击**同名映射**，可以根据名称建立相应的映射关系，请注意匹配数据类型。|
    |**同行映射**|单击**同行映射**，可以在同行建立相应的映射关系，请注意匹配数据类型。|
    |**取消映射**|单击**取消映射**，可以取消建立的映射关系。|
    |**自动排版**|可以根据相应的规律自动排版。|
    |**手动编辑源表字段**|请手动编辑字段，一行表示一个字段，首尾空行会被采用，其他空行会被忽略。|
    |**添加一行**|     -   可以输入常量，输入的值需要使用英文单引号，如’abc’、’123’等。
    -   可以配合调度参数使用，如$\{bizdate\}等。
    -   可以输入关系数据库支持的函数，如now\(\)、count\(1\)等。
    -   如果您输入的值无法解析，则类型显示为未识别。
 |

3.  通道控制。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16221/15633611727675_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**任务期望最大并发数**|数据同步任务内，可以从源并行读取或并行写入数据存储端的最大线程数。向导模式通过界面化配置并发数，指定任务所使用的并行度。|
    |**同步速率**|设置同步速率可以保护读取端数据库，以避免抽取速度过大，给源库造成太大的压力。同步速率建议限流，结合源库的配置，请合理配置抽取速率。|
    |**错误记录数**|错误记录数，表示脏数据的最大容忍条数。|
    |**任务资源组**|任务运行的机器，如果任务数比较多，使用默认资源组出现等待资源的情况，建议购买独享数据集成资源或添加自定义资源组，详情请参见[DataWorks独享资源](../../../../intl.zh-CN/产品定价/预付费（包年包月）/DataWorks独享资源.md#)和[新增任务资源](intl.zh-CN/使用指南/数据集成/常见配置/新增任务资源.md#)。|


## 脚本开发介绍 {#section_cp2_wsh_p2b .section}

配置一个从SQL Server数据库同步抽取数据的作业。

``` {#codeblock_j50_wov_v4o .language-json}
{
    "type":"job",
    "version":"2.0",//版本号。
    "steps":[
        {
            "stepType":"sqlserver",//插件名。
            "parameter":{
                "datasource":"",//数据源。
                "column":[//字段。
                    "id",
                    "name"
                ],
                "where":"",//筛选条件。
                "splitPk":"",//如果指定splitPk，表示您希望使用splitPk代表的字段进行数据分片。
                "table":""//数据表。
            },
            "name":"Reader",
            "category":"reader"
        },
        {//下面是关于Writer的模板，您可以查找相应的写插件文档。
            "stepType":"stream",
            "parameter":{},
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

如果您想使用querySql查询，Reader部分脚本代码示例如下（SQL Server数据源是sql\_server\_source，待查询的表是dbo.test\_table，待查询的列是name）。

``` {#codeblock_22c_yhl_9xa .language-json}
{
    "stepType": "sqlserver",
    "parameter": {
        "querySql": "select name from dbo.test_table",
        "datasource": "sql_server_source",
        "column": [
            "name"
        ],
        "where": "",
        "splitPk": "id"
    },
    "name": "Reader",
    "category": "reader"
},
```

## 补充说明 {#section_htd_3th_p2b .section}

-   主备同步数据恢复问题

    主备同步问题指SQL Server使用主从灾备，备库从主库不间断通过binlog恢复数据。由于主备数据同步存在一定的时间差，特别在于某些特定情况，例如网络延迟等问题，导致备库同步恢复的数据与主库有较大差别，从备库同步的数据不是一份当前时间的完整镜像。

-   一致性约束

    SQL Server在数据存储划分中属于RDBMS系统，对外可以提供强一致性数据查询接口。例如一次同步任务启动运行过程中，当该库存在其他数据写入方写入数据时，由于数据库本身的快照特性，SQL Server Reader完全不会获取到写入的更新数据。

    上述是在SQL Server Reader单线程模型下数据同步一致性的特性，SQL Server Reader可以根据您配置的信息使用并发数据抽取，因此不能严格保证数据一致性。

    当SQL Server Reader根据splitPk进行数据切分后，会先后启动多个并发任务完成数据同步。多个并发任务相互之间不属于同一个读事务，同时多个并发任务存在时间间隔，因此这份数据并不是完整的、一致的数据快照信息。

    针对多线程的一致性快照需求，目前在技术上无法实现，只能从工程角度解决。工程化的方式存在取舍，在此提供以下解决思路，您可以根据自身情况进行选择。

    -   使用单线程同步，即不再进行数据切片。缺点是速度比较慢，但是能够很好保证一致性。
    -   关闭其他数据写入方，保证当前数据为静态数据，例如锁表、关闭备库同步等。缺点是可能影响在线业务。
-   数据库编码问题

    SQL Server Reader底层使用JDBC进行数据抽取，JDBC天然适配各类编码，并在底层进行了编码转换。因此SQL Server Reader不需您指定编码，可以自动获取编码并转码。

-   增量数据同步

    SQL Server Reader使用JDBC SELECT语句完成数据抽取工作，因此可以使用`SELECT…WHERE…`进行增量数据抽取，有以下几种方式：

    -   数据库在线应用写入数据库时，填充modify字段为更改时间戳，包括新增、更新、删除（逻辑删除）。对于该类应用，SQL Server Reader只需要where条件后跟上一同步阶段时间戳即可。
    -   对于新增流水型数据，SQL Server Reader在where条件后跟上一阶段最大自增ID即可。
    对于业务上无字段区分新增、修改数据的情况，SQL Server Reader无法进行增量数据同步，只能同步全量数据。

-   SQL安全性

    SQL Server Reader提供querySql语句交给您自己实现SELECT抽取语句，SQL Server Reader本身对querySql不进行任何安全性校验。


