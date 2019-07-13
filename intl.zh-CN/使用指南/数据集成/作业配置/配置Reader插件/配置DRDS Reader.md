# 配置DRDS Reader {#concept_kvr_2xh_p2b .concept}

DRDS Reader插件实现了从DRDS（分布式RDS）读取数据。在底层实现上，DRDS Reader通过JDBC连接远程DRDS数据库，并执行相应的SQL语句，从DRDS库中选取数据。

DRDS的插件目前仅适配了MySQL引擎的场景，DRDS是一套分布式MySQL数据库，并且大部分通信协议遵守MySQL使用场景。

简而言之，DRDS Reader通过JDBC连接器连接至远程的DRDS数据库，根据您配置的信息生成查询SQL语句，发送至远程DRDS数据库，执行该SQL语句并返回结果。然后使用数据同步自定义的数据类型拼装为抽象的数据集，传递给下游Writer处理。

对于您配置的table、column、where等信息，DRDS Reader将其拼接为SQL语句发送至DRDS数据库。不同于普通的MySQL数据库，DRDS作为分布式数据库系统，无法适配所有MySQL的协议，包括复杂的Join等语句，DRDS暂时无法支持。

DRDS Reader支持大部分DRDS类型，但也存在个别类型没有支持的情况，请注意检查您的类型 。

DRDS Reader针对DRDS类型的转换列表，如下所示。

|类型分类|DRDS数据类型|
|:---|:-------|
|整数类|INT、TINYINT、SMALLINT、MEDIUMINT和BIGINT|
|浮点类|FLOAT、DOUBLE和DECIMAL|
|字符串类|VARCHAR、CHAR、TINYTEXT、TEXT、MEDIUMTEXT和LONGTEXT|
|日期时间类|DATE、DATETIME、TIMESTAMP、TIME和YEAR|
|布尔类|BIT和BOOL|
|二进制类|TINYBLOB、MEDIUMBLOB、BLOB、LONGBLOB和VARBINARY|

## 参数说明 {#section_jn2_gqh_p2b .section}

|参数|描述|必选|默认值|
|:-|:-|:-|:--|
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
|where|筛选条件，DRDS Reader根据指定的column、table、where条件拼接SQL，并根据这个SQL进行数据抽取。例如在测试时，可以将where条件指定实际业务场景，往往会选择当天的数据进行同步，可以将where条件指定为`STRTODATE(‘${bdp.system.bizdate}’, ‘%Y%m%d’) <= taday AND taday < DATEADD(STRTODATE(‘${bdp.system.bizdate}’, ‘%Y%m%d’), interval 1 day)`。 -   where条件可以有效地进行业务增量同步。
-   where条件不配置或者为空时，视作全表同步数据 。

 |否|无|

## 向导开发介绍 {#section_bp2_wsh_p2b .section}

1.  配置同步任务的数据来源和数据去向。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16221/15630066957672_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**数据源**|即上述参数说明中的datasource，通常填写您配置的数据源名称。|
    |**表**|即上述参数说明中的table。|
    |**数据过滤**|您将要同步数据的筛选条件，暂时不支持limit关键字过滤。SQL语法与选择的数据源一致。|
    |**切分键**|您可以将源数据表中某一列作为切分键，建议使用主键或有索引的列作为切分键，仅支持类型为整型的字段。 读取数据时，根据配置的字段进行数据分片，实现并发读取，可以提升数据同步效率。

**说明：** 切分键与数据同步中的选择来源有关，配置数据来源时才显示切分键配置项。

 |

2.  字段映射，即上述参数说明中的column。

    左侧的源头表字段和右侧的目标表字段为一一对应关系。单击**添加一行**可以增加单个字段。鼠标放至需要删除的字段上，即可单击**删除**图标进行删除 。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16221/15630066967673_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**同名映射**|单击**同名映射**，可以根据名称建立相应的映射关系，请注意匹配数据类型。|
    |**同行映射**|单击**同行映射**，可以在同行建立相应的映射关系，请注意匹配数据类型。|
    |**取消映射**|单击**取消映射**，可以取消建立的映射关系。|
    |**自动排版**|可以根据相应的规律自动排版。|
    |**手动编辑源表字段**|请手动编辑字段，一行表示一个字段，首尾空行会被采用，其他空行会被忽略。|
    |**添加一行**|添加一行的功能如下所示：     -   可以输入常量，输入的值需要使用英文单引号，如'abc'、'123'等。
    -   可以配合调度参数使用，如$\{bizdate\}等。
    -   可以输入关系数据库支持的函数，如now\(\)、count\(1\)等。
    -   如果您输入的值无法解析，则类型显示为未识别。
 |

3.  通道控制。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16221/15630066967675_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**任务期望最大并发数**|数据同步任务内，可以从源并行读取或并行写入数据存储端的最大线程数。向导模式通过界面化配置并发数，指定任务所使用的并行度。|
    |**同步速率**|设置同步速率可以保护读取端数据库，以避免抽取速度过大，给源库造成太大的压力。同步速率建议限流，结合源库的配置，请合理配置抽取速率。|
    |**错误记录数**|错误记录数，表示脏数据的最大容忍条数。|
    |**任务资源组**|任务运行的机器，如果任务数比较多，使用默认资源组出现等待资源的情况，建议购买独享数据集成资源或添加自定义资源组，详情请参见[DataWorks独享资源](../../../../intl.zh-CN/产品定价/预付费（包年包月）/DataWorks独享资源.md#)和[新增任务资源](intl.zh-CN/使用指南/数据集成/常见配置/新增任务资源.md#)。|


## 脚本开发介绍 {#section_cp2_wsh_p2b .section}

配置一个从DRDS数据库同步抽取数据作业。

``` {#codeblock_igt_4qy_5s5}
{
    "type":"job",
    "version":"2.0",//版本号。
    "steps":[
        {
            "stepType":"drds",//插件名。
            "parameter":{
                "datasource":"",//数据源名。
                "column":[//列名。
                    "id",
                    "name"
                ],
                "where":"",//过滤条件。
                "table":"",//表名。
                "splitPk": ""//切分键。
            },
            "name":"Reader",
            "category":"reader"
        },
        {//此处以stream为例，如果您需要其他插件，可以查找相应的文档。
            "stepType":"stream",//插件名
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
}:"Writer"
            }
        ]
    }
}
```

## 补充说明 {#section_htd_3th_p2b .section}

-   一致性视图问题

    DRDS本身属于分布式数据库，对外无法提供一致性的多库多表视图。不同于MySQL等单库单表同步，DRDS Reader无法抽取同一个时间切片的分库分表快照信息，即DRDS Reader抽取底层不同的分表将获取不同的分表快照，无法保证强一致性。

-   数据库编码问题

    DRDS本身的编码设置非常灵活，包括指定编码到库、表、字段级别，甚至可以设置不同编码。优先级从高到低为字段、表、库、实例。建议您在库级别将编码统一设置为UTF-8。

    DRDS Reader底层使用JDBC进行数据抽取，JDBC天然适配各类编码，并在底层进行了编码转换。因此DRDS Reader不需要您指定编码，可以自动获取编码并转码。

    对于DRDS底层写入编码和其设定的编码不一致的混乱情况，DRDS Reader对此无法识别，也无法提供解决方案，这类情况的导出结果有可能为乱码。

-   增量数据同步

    DRDS Reader使用JDBC SELECT语句完成数据抽取工作，因此可以使用`SELECT…WHERE…`进行增量数据抽取，有以下几种方式：

    -   数据库在线应用写入数据库时，填充modify字段为更改时间戳，包括新增、更新、删除（逻辑删除）。对于这类应用，DRDS Reader只需要where条件后跟上一同步阶段时间戳即可。
    -   对于新增流水型数据，DRDS Reader在where条件后跟上一阶段最大自增ID即可。
    对于业务上无字段区分新增、修改数据的情况，DRDS Reader也无法进行增量数据同步，只能同步全量数据 。

-   SQL安全性

    DRDS Reader提供querySql语句交给您自己实现SELECT抽取语句，DRDS Reader本身对SQLQuery不进行任何安全性校验。


