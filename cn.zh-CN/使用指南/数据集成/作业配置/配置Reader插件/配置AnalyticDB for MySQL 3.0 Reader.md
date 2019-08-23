# 配置AnalyticDB for MySQL 3.0 Reader {#concept_261553 .concept}

本文将为您介绍AnalyticDB for MySQL 3.0 Reader支持的数据类型、字段映射和数据源等参数及配置示例。

AnalyticDB for MySQL 3.0 Reader插件实现了从AnalyticDB for MySQL 3.0读取数据。在底层实现上，AnalyticDB for MySQL 3.0 Reader通过JDBC连接远程AnalyticDB for MySQL 3.0数据库，并执行相应的SQL语句，从AnalyticDB for MySQL 3.0库中读取数据。

## 数据类型转换 {#section_u26_mcc_bmz .section}

AnalyticDB for MySQL 3.0 Reader针对AnalyticDB for MySQL 3.0类型的转换列表，如下表所示。

|类型分类|AnalyticDB for MySQL 3.0类型|
|----|--------------------------|
|整数类|INT、INTEGER、TINYINT、SMALLINT和BIGINT|
|浮点类|FLOAT、DOUBLE和DECIMAL|
|字符串类|VARCHAR|
|日期时间类|DATE、DATETIME、TIMESTAMP和TIME|
|布尔类|BOOLEAN|

## 参数说明 {#section_hmf_zcs_dm0 .section}

|参数|描述|是否必选|默认值|
|--|--|----|---|
|datasource|数据源名称，脚本模式支持添加数据源，此配置项填写的内容必须要与添加的数据源名称保持一致。|是|无|
|table|所选取的需要同步的表。|是|无|
|column|所配置的表中需要同步的列名集合，使用JSON的数组描述字段信息，默认使用所有列配置，例如\[ \* \]。 -   支持列裁剪，即列可以挑选部分列进行导出。
-   支持列换序，即列可以不按照表组织结构信息的顺序进行导出。
-   支持常量配置，您需要按照MySQL的语法格式，例如`[“id”, “`table`“, “1”, “‘bazhen.csy’”, “null”, “to_char(a + 1)”, “2.3” , “true”]`。
    -   id为普通列名。
    -   table包含保留的列名。
    -   1为整型数字常量。
    -   bazhen.csy为字符串常量。
    -   null为空指针。
    -   to\_char\(a + 1\)为计算字符串长度函数表达式。
    -   2.3为浮点数。
    -   true为布尔值。
-   column必须显示您指定同步的列集合，不允许为空 。

 |是|无|
|splitPk|AnalyticDB for MySQL 3.0 Reader进行数据抽取时，如果指定splitPk，表示您希望使用splitPk代表的字段进行数据分片，数据同步因此会启动并发任务进行数据同步，提高数据同步的效能。 -   推荐splitPk用户使用表主键，因为表主键通常情况下比较均匀，因此切分出来的分片也不容易出现数据热点。
-   目前splitPk仅支持整型数据切分，不支持字符串、浮点和日期等其他类型 。如果您指定其他非支持类型，忽略splitPk功能，使用单通道进行同步。
-   如果不填写splitPk，包括不提供splitPk或者splitPk值为空，数据同步视作使用单通道同步该表数据 。

 |否|无|
|where|筛选条件，在实际业务场景中，往往会选择当天的数据进行同步，将where条件指定为`gmt_create>$bizdate`。 -   where条件可以有效地进行业务增量同步。如果不填写where语句，包括不提供where的key或value，数据同步均视作同步全量数据。
-   不可以将where条件指定为limit 10，这不符合MySQL SQL WHERE子句约束。

 |否|无|

## 向导开发介绍 {#section_9xw_odj_u25 .section}

1.  选择数据源。

    配置同步任务的**数据来源**和**数据去向**。

    ![选择数据源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1462970/156652988057150_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**数据源**|即上述参数说明中的datasource，通常填写您配置的数据源名称。|
    |**表**|即上述参数说明中的table。|
    |**数据过滤**|您将要同步数据的筛选条件，暂时不支持limit关键字过滤。SQL语法与选择的数据源一致。|
    |**切分键**|您可以将源数据表中某一列作为切分键，建议使用主键或有索引的列作为切分键，仅支持类型为整型的字段。 读取数据时，根据配置的字段进行数据分片，实现并发读取，可以提升数据同步效率。

**说明：** 切分键与数据同步中的选择来源有关，配置数据来源时才显示切分键配置项。

 |

2.  字段映射，即上述参数说明中的column。

    左侧的源头表字段和右侧的目标表字段为一一对应关系。单击**添加一行**可以增加单个字段，鼠标放至需要删除的字段上，即可单击**删除**图标进行删除 。

    ![字段映射](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1462970/156652988057152_zh-CN.png)

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

    ![通道控制](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16221/15665298817675_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**任务期望最大并发数**|数据同步任务内，可以从源并行读取或并行写入数据存储端的最大线程数。向导模式通过界面化配置并发数，指定任务所使用的并行度。|
    |**同步速率**|设置同步速率可以保护读取端数据库，以避免抽取速度过大，给源库造成太大的压力。同步速率建议限流，结合源库的配置，请合理配置抽取速率。|
    |**错误记录数**|错误记录数，表示脏数据的最大容忍条数。|
    |**任务资源组**|任务运行的机器，如果任务数比较多，使用默认资源组出现等待资源的情况，建议购买独享数据集成资源或添加自定义资源组，详情请参见[DataWorks独享资源](../../../../cn.zh-CN/产品定价/包年包月/DataWorks独享资源.md#)和[新增任务资源](cn.zh-CN/使用指南/数据集成/常见配置/新增任务资源.md#)。|


## 脚本开发介绍 {#section_xki_zlm_a5k .section}

脚本配置示例如下，详情请参见上述参数说明。

``` {#codeblock_bl2_ruf_xf5}
{
    "type": "job",
    "steps": [
        { 
            "stepType": "analyticdb_for_mysql", //插件名。
            "parameter": {
                "column": [ //列名。
                    "id",
                    "value",
                    "table"
                ],
                "connection": [
                    {
                        "datasource": "xxx", //数据源。
                        "table": [ //表名。
                            "xxx"
                        ]
                    }
                ],
                "where": "", //过滤条件。
                "splitPk": "", //切分键。
                "encoding": "UTF-8" //编码格式。
            },
            "name": "Reader",
            "category": "reader"
        },
        { //下面是关于writer的模板，您可以查找相应的写插件文档。
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
            "record": "0" //同步过程中的错误记录限制数。
        },
        "speed": {
            "concurrent": 2, //任务记录数。
            "throttle": false //false代表不限流，下面的限流的速度不生效，true代表限流。
        }
    }
}
```

