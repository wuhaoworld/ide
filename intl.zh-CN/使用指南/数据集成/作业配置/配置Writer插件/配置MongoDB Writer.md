# 配置MongoDB Writer {#concept_gmn_qwm_q2b .concept}

本文为您介绍MongoDB Writer支持的数据类型、写入方式、字段映射和数据源等参数和配置示例。

MongoDB Writer插件利用MongoDB的Java客户端MongoClient进行MongoDB的写操作。最新版本的Mongo已经将DB锁的粒度从DB级别降低到Document级别，配合MongoDB强大的索引功能，基本可以满足数据源向MongoDB写入数据的需求。针对数据更新的需求，通过配置业务主键的方式也可以实现。

**说明：** 

-   在开始配置MongoDB Writer插件前，请首先配置好数据源，详情请参见[配置MongoDB数据源](intl.zh-CN/使用指南/数据集成/数据源配置/配置MongoDB数据源.md#)。
-   如果您使用的是云数据库MongoDB版，MongoDB默认会有root账号。
-   出于安全策略的考虑，数据集成仅支持使用 MongoDB数据库对应账号进行连接，您添加使用MongoDB数据源时，也请避免使用root作为访问账号。

MongoDB Writer通过数据集成框架获取Reader生成的协议数据，然后将支持的类型通过逐一判断转换成MongoDB支持的类型。数据集成本身不支持数组类型，但MongoDB支持数组类型，并且数组类型的索引很强大。

为了使用MongoDB的数组类型，您可以通过参数的特殊配置，将字符串可以转换成MongoDB中的数组，类型转换之后，便可并行写入MongoDB。

## 类型转换列表 {#section_m2v_hxm_q2b .section}

MongoDB Writer支持大部分MongoDB类型，但也存在部分没有支持的情况，请注意检查您的类型。

MongoDB Writer针对MongoDB类型的转换列表，如下所示。

|类型分类|MongoDB数据类型|
|:---|:----------|
|整数类|INT和LONG|
|浮点类|DOUBLE|
|字符串类|STRING和ARRAY|
|日期时间类|DATE|
|布尔型|BOOL|
|二进制类|BYTES|

**说明：** 此处DATE类型，写入到MongoDB后即为DATETIME类型。

## 参数说明 {#section_jn2_gqh_p2b .section}

|参数|描述|是否必选|默认值|
|:-|:-|:---|:--|
|datasource|数据源名称，脚本模式支持添加数据源，此配置项填写的内容必须要与添加的数据源名称保持一致。|是|无|
|collectionName|MonogoDB的集合名。|是|无|
|column|MongoDB的文档列名，配置为数组形式表示MongoDB的多个列。 -   name：Column的名字。
-   type：Column的类型。
-   splitter：特殊分隔符，当且仅当要处理的字符串要用分隔符分隔为字符数组Array时，才使用此参数。通过此参数指定的分隔符，将字符串分隔存储到MongoDB的数组中。

 |是|无|
|writeMode|指定了传输数据时是否覆盖的信息。 -   isReplace：当设置为true时，表示针对相同的replaceKey做覆盖操作。当设置为false时，表示不覆盖。
-   replaceKey：replaceKey指定了每行记录的业务主键，用来做覆盖时使用（不支持replaceKey为多个键，一般是指Monogo中的主键）。

 |否|无|
|preSql|表示数据同步写出MongoDB前的前置操作，例如清理历史数据等。如果preSql为空，表示没有配置前置操作。配置preSql时，需要确保preSql符合JSON语法要求。preSql的格式要求如下： -   需要配置type字段，表示前置操作类别，支持drop和remove，例如`"preSql":{"type":"remove"}`。
    -   drop：表示删除集合和集合内的数据，collectionName参数配置的集合即是待删除的集合。
    -   remove：表示根据条件删除数据。
    -   json：您可以通过JSON控制待删除的数据条件，例如`"preSql":{"type":"remove", "json":"{'operationTime':{'$gte':ISODate('${last_day}T00:00:00.424+0800')}}"}`。 此处的`${last_day}`为DataWorks调度参数，格式为`$[yyyy-mm-dd]`。您可以根据需要具体使用其他MongoDB支持的条件操作符号（$gt、$lt、$gte和$lte等）、逻辑操作符（and和or等）或函数（max、min、sum、avg和ISODate等），详情请参见MongoDB查询语法。

数据集成通过如下MongoDB标准API执行您的数据，删除query：

        ``` {#codeblock_mlf_52t_d0g}
query=(BasicDBObject) com.mongodb.util.JSON.parse(json);                
col.deleteMany(query);
        ```

**说明：** 如果您需要条件删除数据，建议您优先使用JSON配置形式。

    -   item：您可以在item中配置数据过滤的列名（name）、条件（condition）和列值（value）。例如`"preSql":{"type":"remove","item":[{"name":"pv","value":"100","condition":"$gt"},{"name":"pid","value":"10"}]}`。

数据集成会基于您配置的item条件项，构造查询query条件，进而通过MongoDB标准API执行删除。例如`col.deleteMany(query);`。

-   不识别的preSql，不需进行任何前置删除操作。

 |否|无|

## 向导开发介绍 {#section_bp2_wsh_p2b .section}

暂不支持向导开发模式。

## 脚本开发介绍 {#section_cp2_wsh_p2b .section}

配置写入MongoDB的数据同步作业，详情请参见上述参数说明。

``` {#codeblock_n9j_us5_day .language-json}
{
    "type": "job",
    "version": "2.0",//版本号
    "steps": [//下面是关于Reader的模板，可以查看相应的读插件文档。
        {
            "stepType": "stream",
            "parameter": {},
            "name": "Reader",
            "category": "reader"
        },
        {
            "stepType": "mongodb",//插件名
            "parameter": {
                "datasource": "",//数据源名
                "column": [
                    {
                        "name": "name",//列名
                        "type": "string"//数据类型
                    },
                    {
                        "name": "age",
                        "type": "int"
                    },
                    {
                        "name": "id",
                        "type": "long"
                    },
                    {
                        "name": "wealth",
                        "type": "double"
                    },
                    {
                        "name": "hobby",
                        "type": "array",
                        "splitter": " "
                    },
                    {
                        "name": "valid",
                        "type": "boolean"
                    },
                    {
                        "name": "date_of_join",
                        "format": "yyyy-MM-dd HH:mm:ss",
                        "type": "date"
                    }
                ],
                "writeMode": {//写入模式
                    "isReplace": "true",
                    "replaceKey": "id"
                },
                "collectionName": "datax_test"//连接名称
            },
            "name": "Writer",
            "category": "writer"
        }
    ],
    "setting": {
        "errorLimit": {//错误记录数
            "record": "0"
        },
        "speed": {
            "jvmOption": "-Xms1024m -Xmx1024m",
            "throttle": true,//false代表不限流，下面的限流的速度不生效，true代表限流。
            "concurrent": 1,//作业并发数
            "mbps": "1"//限流的速度
        }
    },
    "order": {
        "hops": [//从reader同步writer
            {
                "from": "Reader",
                "to": "Writer"
            }
        ]
    }
}
```

