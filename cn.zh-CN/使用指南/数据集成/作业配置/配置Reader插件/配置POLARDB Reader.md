# 配置POLARDB Reader {#concept_ud2_vzb_5fb .concept}

本文将为您介绍POLARDB Reader支持的数据类型、字段映射和数据源等参数及配置示例。

POLARDB Reader插件通过JDBC连接器连接至远程的POLARDB数据库，根据您配置的信息生成查询SQL语句，发送至远程POLARDB数据库，执行该SQL语句并返回结果。然后使用数据同步自定义的数据类型将其拼装为抽象的数据集，传递给下游Writer处理。

在底层实现上，POLARDB Reader插件通过JDBC连接远程POLARDB数据库，并执行相应的SQL语句，从POLARDB库中读取数据。

POLARDB Reader插件支持读取表和视图。表字段可以依序指定全部列、指定部分列、调整列顺序、指定常量字段和配置POLARDB的函数，例如now\(\)等。

## 类型转换列表 {#section_ny3_4fr_5fb .section}

POLARDB Reader针对POLARDB类型的转换列表，如下所示。

|类型分类|POLARDB数据类型|
|:---|:----------|
|整数类|INT、TINYINT、SMALLINT、MEDIUMINT和BIGINT|
|浮点类|FLOAT、DOUBLE和DECIMAL|
|字符串类|VARCHAR、CHAR、TINYTEXT、TEXT、MEDIUMTEXT和LONGTEXT|
|日期时间类|DATE、DATETIME、TIMESTAMP、TIME和YEAR|
|布尔型|BIT和BOOL|
|二进制类|TINYBLOB、MEDIUMBLOB、BLOB、LONGBLOB和VARBINARY|

**说明：** 

-   除上述罗列字段类型外，其它类型均不支持。
-   POLARDB Reader插件将tinyint\(1\)视作整型。

## 参数说明 {#section_vpb_wfr_5fb .section}

|参数|描述|必选|默认值|
|:-|:-|:-|:--|
|datasource|数据源名称，脚本模式支持添加数据源，此配置项填写的内容必须要与添加的数据源名称保持一致。|是|无|
|table|选取的需要同步的表名称。|是|无|
|column|所配置的表中需要同步的列名集合，使用JSON的数组描述字段信息 。默认使用所有列配置，例如\[\*\]。 -   支持列裁剪，即列可以挑选部分列进行导出。
-   支持列换序，即列可以不按照表Schema信息顺序进行导出。
-   支持常量配置，您需要按照SQL语法格式，例如`["id", "table","1","'mingya.wmy'","'null'", "to_char(a+1)","2.3","true"]`。
    -   id为普通列名。
    -   table为包含保留字的列名。
    -   1为整型数字常量。
    -   ‘mingya.wmy’为字符串常量（注意需要加上一对单引号）。
    -   'null'为字符串常量。
    -   to\_char\(a+1\)为计算字符串长度函数。
    -   2.3为浮点数。
    -   true为布尔值。
-   column必须显示指定同步的列集合，不允许为空。

 |是|无|
|splitPk|POLARDB Reader进行数据抽取时，如果指定splitPk，表示您希望使用splitPk代表的字段进行数据分片，数据同步因此会启动并发任务进行数据同步，从而提高数据同步的效能。 -   推荐splitPk用户使用表主键，因为表主键通常情况下比较均匀，因此切分出来的分片不容易出现数据热点。
-   目前splitPk仅支持整型数据切分，不支持字符串、浮点、日期等其他类型 。如果您指定其他非支持类型，忽略plitPk功能，使用单通道进行同步。
-   如果splitPk不填写，包括不提供splitPk或者splitPk值为空，数据同步视作使用单通道同步该表数据 。

 |否|无|
|where|筛选条件，在实际业务场景中，往往会选择当天的数据进行同步，将where条件指定为gmt\_create\>$bizdate。 -   where条件可以有效地进行业务增量同步。如果不填写where语句，包括不提供where的key或value，数据同步均视作同步全量数据。
-   将where条件指定为limit 10不符合WHERE子句约束，不建议使用。

 |否|无|
|querySql（高级模式，向导模式不提供）|在部分业务场景中，where配置项不足以描述所筛选的条件，您可以通过该配置型来自定义筛选SQL。当配置该项后，数据同步系统就会忽略column、table和where配置项，直接使用该项配置的内容对数据进行筛选。例如需要进行多表 join 后同步数据，使用`select a,b from table_a join table_b on table_a.id = table_b.id`。当您配置querySql时，POLARDB Reader直接忽略column、table和where条件的配置，querySql优先级大于table、column、where、splitPk选项。datasource会使用它解析出用户名和密码等信息。|否|无|
|singleOrMulti（只适合分库分表）|表示分库分表，向导模式转换成脚本模式会主动生成`“singleOrMulti”: “multi”`配置，但脚本模式不会自动生成，您需要手动添加。如果不添加该配置，则仅识别第1个数据源。 **说明：** 仅前端使用singleOrMulti，后端没有使用该参数判断分库分表。

 |是|multi|

## 向导开发介绍 {#section_jvk_sgr_5fb .section}

1.  选择数据源。

    配置同步任务的**数据来源**和**数据去向**。

    ![选择数据源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/62197/156681322932058_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**数据源**|即上述参数说明中的datasource，通常填写您配置的数据源名称。|
    |**表**|即上述参数说明中的table。|
    |**数据过滤**|您将要同步数据的筛选条件，暂时不支持limit关键字过滤。SQL语法与选择的数据源一致。|
    |**切分键**|您可以将源数据表中某一列作为切分键，建议使用主键或有索引的列作为切分键，仅支持类型为整型的字段。读取数据时，根据配置的字段进行数据分片，实现并发读取，可以提升数据同步效率。 **说明：** 切分键和数据同步中的选择来源有关，配置数据来源时才显示切分键配置项。

 |

2.  字段映射，即上述参数说明中的column。

    左侧的源头表字段和右侧的目标表字段为一一对应的关系。单击**添加一行**可以增加单个字段，将鼠标放至需要删除的字段上，即可单击**删除**按钮进行删除。

    ![字段映射](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/62209/156681322932015_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**同名映射**|单击**同名映射**，可以根据名称建立相应的映射关系，请注意匹配数据类型。|
    |**同行映射**|单击**同行映射**，可以在同行建立相应的映射关系，请注意匹配数据类型。|
    |**取消映射**|单击**取消映射**，可以取消建立的映射关系。|
    |**自动排版**|可以根据相应的规律自动排版。|

3.  通道控制。

    ![通道控制](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/62209/156681322932018_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**任务期望最大并发数**|数据同步任务内，可以从源并行读取或并行写入数据存储端的最大线程数。向导模式通过界面化配置并发数，指定任务所使用的并行度。|
    |**同步速率**|设置同步速率可以保护读取端数据库，以避免抽取速度过大，给源库造成太大的压力。同步速率建议限流，结合源库的配置，请合理配置抽取速率。|
    |**错误记录数**|错误记录数，表示脏数据的最大容忍条数。|
    |**任务资源组**|任务运行的机器，如果任务数比较多，使用默认资源组出现等待资源的情况，建议购买独享数据集成资源或添加自定义资源组，详情请参见[DataWorks独享资源](../../../../intl.zh-CN/产品定价/包年包月/DataWorks独享资源.md#)和[新增任务资源](intl.zh-CN/使用指南/数据集成/常见配置/新增任务资源.md#)。|


## 脚本开发介绍 {#section_vw5_p3r_5fb .section}

单库单表的脚本示例如下，详情请参见上述参数说明。

``` {#codeblock_fss_6eo_fdc .language-json}
{
    "type": "job",
    "steps": [
        {
            "parameter": {
                "datasource": "test_005",//数据源名。
                "column": [//源端列名。
                    "id",
                    "name",
                    "age",
                    "sex",
                    "salary",
                    "interest"
                ],
                "where": "id=1001",//过滤条件。
                "splitPk": "id",//切分键。
                "table": "polardb_person"//源端表名。
            },
            "name": "Reader",
            "category": "reader"
        },
        {
            "parameter": {}
    ],
    "version": "2.0",//版本号。
    "order": {
        "hops": [
            {
                "from": "Reader",
                "to": "Writer"
            }
        ]
    },
    "setting": {
        "errorLimit": {//错误记录数。
            "record": ""
        },
        "speed": {
            "concurrent": 6,//并发数。
            "throttle": false,//同步速率限流。
        }
    }
}
```

