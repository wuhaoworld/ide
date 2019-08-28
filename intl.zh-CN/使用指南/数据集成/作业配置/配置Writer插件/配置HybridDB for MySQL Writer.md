# 配置HybridDB for MySQL Writer {#concept_rjl_j1c_5fb .concept}

本文将为您介绍HybridDB for MySQL Writer支持的数据类型、写入方式、字段映射和数据源等参数及配置示例。

HybridDB for MySQL Writer插件实现了写入数据至MySQL数据库目标表的功能。在底层实现上，HybridDB for MySQL Writer通过JDBC连接远程HybridDB for MySQL数据库，并执行相应的`insert into`或`replace into`语句，将数据写入HybridDB for MySQL。数据库本身采用InnoDB引擎，分批次提交数据入库。

**说明：** 开始配置HybridDB for MySQL Writer插件前，请首先配置好数据源，详情请参见[配置HybridDB for MySQL数据源](intl.zh-CN/使用指南/数据集成/数据源配置/配置HybridDB for MySQL数据源.md#)。

HybridDB for MySQL Writer面向数据开发工程师，通过HybridDB for MySQL Writer从数仓导入数据至HybridDB for MySQL。同时，HybridDB for MySQL Writer可以作为数据迁移工具，为数据库管理员等用户提供服务。HybridDB for MySQL Writer通过数据同步框架获取Reader生成的协议数据。

**说明：** 整个任务至少需要具备`insert into`的权限，是否需要其它权限，取决于您配置任务时在preSql和postSql中指定的语句。

## 类型转换列表 {#section_qqr_b4r_5fb .section}

目前HybridDB for MySQL Writer支持大部分HybridDB for MySQL类型，请注意检查您的数据类型。

HybridDB for MySQL Writer针对HybridDB for MySQL类型的转换列表，如下所示。

|类型分类|HybridDB for MySQL数据类型|
|:---|:---------------------|
|整数类|INT、TINYINT、SMALLINT、MEDIUMINT、BIGINT和YEAR|
|浮点类|FLOAT、DOUBLE和DECIMAL|
|字符串类|VARCHAR、CHAR、TINYTEXT、TEXT、MEDIUMTEXT和LONGTEXT|
|日期时间类|DATE、DATETIME、TIMESTAMP和TIME|
|布尔类|BOOL|
|二进制类|TINYBLOB、MEDIUMBLOB、BLOB、LONGBLOB和VARBINARY|

## 参数说明 {#section_vpb_wfr_5fb .section}

|参数|描述|必选|默认值|
|:-|:-|:-|:--|
|datasource|数据源名称，脚本模式支持添加数据源，此配置项填写的内容必须与添加的数据源名称保持一致。|是|无|
|table|选取的需要同步的表名称。|是|无|
|writeMode|选择导入模式，目前支持insert和replace两种方式。 -   replace into：没有遇到主键/唯一性索引冲突时，与insert into行为一致，冲突时会用新行替换原有行所有字段。
-   insert into：当主键/唯一性索引冲突时会写不进去冲突的行，以脏数据的形式体现。

 |否|insert|
|column|目标表需要写入数据的字段，字段之间用英文逗号分隔。例如`"column":["id","name","age"]`。如果要依次写入全部列，使用\*表示，例如`"column":["*"]`。|是|无|
|preSql|执行数据同步任务之前率先执行的SQL语句。目前向导模式仅允许执行一条SQL语句，脚本模式可以支持多条SQL语句，例如清除旧数据。|否|无|
|postSql|执行数据同步任务之后执行的SQL语句，目前向导模式仅允许执行一条SQL语句，脚本模式可以支持多条SQL语句，例如加上某一个时间戳。|否|无|
|batchSize|一次性批量提交的记录数大小，该值可以极大减少数据同步系统与HybridDB for MySQL的网络交互次数，并提升整体吞吐量。如果该值设置过大，会导致数据同步运行进程OOM异常。|否|1,024|

## 向导开发介绍 {#section_jvk_sgr_5fb .section}

1.  选择数据源。

    配置同步任务的**数据来源**和**数据去向**。

    ![选择数据源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/62205/156698830832039_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**数据源**|即上述参数说明中的datasource，通常选择您配置的数据源名称。|
    |**表**|即上述参数说明中的table。|
    |**导入前准备语句**|即上述参数说明中的preSql，输入执行数据同步任务之前率先执行的SQL语句。|
    |**导入后完成语句**|即上述参数说明中的postSql，输入执行数据同步任务之后执行的SQL语句。|
    |**主键冲突**|即上述参数说明中的writeMode，可以选择需要的导入模式。|

2.  字段映射，即上述参数说明中的column。

    左侧的源头表字段和右侧的目标表字段为一一对应关系。单击**添加一行**可以增加单个字段，鼠标放至需要删除的字段上，即可单击**删除**图标进行删除。

    ![字段映射](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/62205/156698830832041_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**同名映射**|单击**同名映射**，可以根据名称建立相应的映射关系，请注意匹配数据类型。|
    |**同行映射**|单击**同行映射**，可以在同行建立相应的映射关系，请注意匹配数据类型。|
    |**取消映射**|单击**取消映射**，可以取消建立的映射关系。|
    |**自动排版**|可以根据相应的规律自动排版。|

3.  通道控制。

    ![通道控制](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/62209/156698830832018_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**任务期望最大并发数**|数据同步任务内，可以从源并行读取或并行写入数据存储端的最大线程数。向导模式通过界面化配置并发数，指定任务所使用的并行度。|
    |**同步速率**|设置同步速率可以保护读取端数据库，以避免抽取速度过大，给源库造成太大的压力。同步速率建议限流，结合源库的配置，请合理配置抽取速率。|
    |**错误记录数**|错误记录数，表示脏数据的最大容忍条数。|
    |**任务资源组**|任务运行的机器，如果任务数比较多，使用默认资源组出现等待资源的情况，建议购买独享数据集成资源或添加自定义资源组，详情请参见[DataWorks独享资源](../../../../intl.zh-CN/产品定价/包年包月/DataWorks独享资源.md#)和[新增任务资源](intl.zh-CN/使用指南/数据集成/常见配置/新增任务资源.md#)。|

    96811


## 脚本开发介绍 {#section_vw5_p3r_5fb .section}

脚本配置示例如下，详情请参见上述参数说明。

``` {#codeblock_55z_6uv_8cr}
{
    "type": "job",
    "steps": [
        {
            "parameter": {},
        {
            "parameter": {
                "postSql": [],//导入后的完整语句。
                "datasource": "px_aliyun_hy***",//数据源名。
                "column": [//目标端列名。
                    "id",
                    "name",
                    "sex",
                    "salary",
                    "age",
                    "pt"
                ],
                "writeMode": "insert",//写入模式。
                "batchSize": 256,//一次性批量提交的记录数大小。
                "encoding": "UTF-8",//编码格式。
                "table": "person_copy",//目标表名。
                "preSql": []//导入前的准备语句。
            },
            "name": "Writer",
            "category": "writer"
        }
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
            "concurrent": 7,//并发数。
            "throttle": true,//false代表不限流，下面的限流的速度不生效，true代表限流。
            "mbps": 1,//限流值。
        }
    }
}
```

