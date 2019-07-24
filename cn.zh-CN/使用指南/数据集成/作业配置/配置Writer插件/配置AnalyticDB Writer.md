# 配置AnalyticDB Writer {#concept_bft_jyk_q2b .concept}

本文将为您介绍AnalyticDB Writer支持的数据源、数据类型、字段映射、参数配置以及一个完整的导入数据操作示例。

数据集成通过实时导入的方式将数据导入AnalyticDB中，要求您必须提前在AnalyticDB中创建好实时表（普通表）。实时导入方式效率高，且流程简单。

如果数据源来源是RDS for SQLServer，详细的导入操作，请参见[使用数据集成迁移](https://help.aliyun.com/document_detail/98790.html)。

开始配置AnalyticDB Writer插件前，请首先配置好数据源，详情请参见[配置AnalyticDB数据源](cn.zh-CN/使用指南/数据集成/数据源配置/配置AnalyticDB数据源.md#)。

AnalyticDB Writer针对AnalyticDB类型的转换列表，如下所示。

|类型|AnalyticDB数据类型|
|:-|:-------------|
|整数类|INT、TINYINT、SMALLINT、BIGINT|
|浮点类|FLOAT和DOUBLE|
|字符串类|VARCHAR|
|日期时间类|DATE和TIMESTAMP|
|布尔类|BOOLEAN|

## 参数说明 {#section_b4m_w61_htc .section}

|参数|描述|必选|默认值|
|:-|:-|:-|:--|
|连接url|AnalyticDB连接信息，格式为Address:Port。|是|无|
|数据库|AnalyticDB的数据库名称。|是|无|
|Access Id|AnalyticDB对应的AccessKey Id。|是|无|
|Access Key|AnalyticDB对应的AccessKey Secret。|是|无|
|datasource|数据源名称，脚本模式支持添加数据源，此配置项填写的内容必须与添加的数据源名称保持一致。|是|无|
|table|目标表的表名称。|是|无|
|partition|目标表的分区名称，当目标表为普通表，需要指定该字段。|否|无|
|writeMode|Insert模式，在主键冲突情况下新的记录会覆盖旧的记录。|是|无|
|column|目的表字段列表，可以为\["\*"\]，或者具体的字段列表，例如\["a", "b", "c"\]。|是|无|
|suffix|AnalyticDB url配置项的格式为`ip:port`，此部分为您定制的连接串，是可选参数（请参见MySQL支持的JDBC控制参数）。实际在AnalyticDB数据库访问时，会变成JDBC数据库连接串。例如配置suffix为`autoReconnect=true&failOverReadOnly=false&maxReconnects=10`。|否|无|
|batchSize|AnalyticDB提交数据写的批量条数，当writeMode为insert时，该值才会生效。|writeMode为insert时，为必选。|无|
|bufferSize|DataX数据收集缓冲区大小，缓冲区的目的是积累一个较大的Buffer，源头的数据首先进入到此Buffer中进行排序，排序完成后再提交到AnalyticDB。排序是根据AnalyticDB的分区列模式进行的，排序的目的是数据顺序对AnalyticDB服务端更友好（出于性能考虑）。 BufferSize缓冲区中的数据会经过batchSize批量提交到ADB中，通常需要设置bufferSize为batchSize数量的多倍。当writeMode为insert时，该值才会生效。

 |writeMode为insert时，为必选。|默认不配置不开启此功能。|

## 向导开发介绍 {#section_bp2_wsh_p2b .section}

1.  选择数据源。

    配置同步任务的**数据来源**和**数据去向**。

    ![选择数据源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16239/15639674647998_zh-CN.png)

    |配置项|说明|
    |:--|:-|
    |**数据源**|选择ADS，系统将自动关联[配置AnalyticDB数据源](https://help.aliyun.com/document_detail/100590.html)时设置的数据源名称。|
    |**表**|选择AnalyticDB中的一张表，将Reader数据库中的数据同步至该表中。|
    |**导入模式**|根据AnalyticDB中表的更新方式设置导入模式，包括**批量导入**和**实时导入**。 **说明：** 批量导入不支持从非MaxCompute数据源批量导入数据至AnalyticDB。请配置两个同步任务，先将数据导入MaxCompute，再批量导入AnalyticDB。

 |
    |**导入规则**|     -   **写入前清理已有数据**：导数据之前，清空表或者分区的所有数据，相当于`insert overwrite`。
    -   **写入前保留已有数据**：导数据之前，不清理任何数据，每次运行数据都是追加进去的，相当于`insert into`。
 |
    |**一级分区**|默认，不可修改。|

2.  字段映射，即上述参数说明中的column。

    左侧的源头表字段和右侧的目标表字段为一一对应的关系。单击**添加一行**可以增加单个字段，鼠标放至需要删除的字段上，即可单击**删除**图标进行删除。

    ![字段映射](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16239/15639674658002_zh-CN.png)

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

    ![通道控制](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16221/15639674657675_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**任务期望最大并发数**|数据同步任务内，可以从源并行读取或并行写入数据存储端的最大线程数。向导模式通过界面化配置并发数，指定任务所使用的并行度。|
    |**同步速率**|设置同步速率可以保护读取端数据库，以避免抽取速度过大，给源库造成太大的压力。同步速率建议限流，结合源库的配置，请合理配置抽取速率。|
    |**错误记录数**|错误记录数，表示脏数据的最大容忍条数。|
    |**任务资源组**|任务运行的机器，如果任务数比较多，使用默认资源组出现等待资源的情况，建议购买独享数据集成资源或添加自定义资源组，详情请参见[DataWorks独享资源](../../../../cn.zh-CN/产品定价/预付费（包年包月）/DataWorks独享资源.md#)和[新增任务资源](cn.zh-CN/使用指南/数据集成/常见配置/新增任务资源.md#)。|


## 脚本开发介绍 {#section_cp2_wsh_p2b .section}

``` {#codeblock_0jz_dsp_oac}
{
    "type":"job",
    "version":"2.0",
    "steps":[ //下面是关于Writer的模板，您可以查找相应数据源的写插件文档。
        {
            "stepType":"stream",
            "parameter":{
            "name":"Reader",
            "category":"reader"
        },
        {
            "stepType":"ads",//插件名。
            "parameter":{
                "partition":"",//目标表的分区名称。
                "datasource":"",//数据源。
                "column":[//字段。
                     "id"
                ],
                "writeMode":"insert",//写入模式。
                "batchSize":"256",//一次性批量提交的记录数大小。
                "table":"",//表名
                "overWrite":"true"//AnalyticDB写入是否覆盖当前写入的表，true为覆盖写入，false为不覆盖。（追加）写入。当 writeMode 为 Load 时，该值才会生效。
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

