# 配置OSS Reader {#concept_d33_12q_p2b .concept}

本文将为您介绍OSS Reader支持的数据类型、字段映射和数据源等参数及配置示例。

OSS Reader插件提供了读取OSS数据存储的能力。在底层实现上，OSS Reader使用OSS官方Java SDK获取OSS数据，并转换为数据同步传输协议传递给Writer。

-   如果您想对OSS产品有更深了解，请参见[OSS产品概述](../../../../intl.zh-CN/产品简介/什么是对象存储 OSS.md#)。
-   OSS Java SDK的详细介绍，请参见[阿里云OSS Java SDK](http://oss.aliyuncs.com/aliyun_portal_storage/help/oss/OSS_Java_SDK_Dev_Guide_20141113.pdf)。
-   处理OSS等非结构化数据的详细介绍，请参见[处理非结构化数据](../../../../intl.zh-CN/开发/外部表/访问OSS非结构化数据.md#)。

OSS Reader实现了从OSS读取数据并转为数据集成/DataX协议的功能，OSS本身是无结构化数据存储。对于数据集成/DataX而言，目前OSS Reader支持的功能如下所示。

-   支持且仅支持读取TXT格式的文件，且要求TXT中schema为一张二维表。
-   支持类CSV格式文件，自定义分隔符。
-   支持多种类型数据读取（使用String表示），支持列裁剪、列常量。
-   支持递归读取、支持文件名过滤。
-   支持文本压缩，现有压缩格式为gzip、bzip2和zip。

    **说明：** 一个压缩包不允许多文件打包压缩。

-   多个Object可以支持并发读取。

OSS Reader暂时不能实现以下功能。

-   单个Object（File）支持多线程并发读取。
-   单个Object在压缩情况下，从技术上无法支持多线程并发读取。

OSS Reader支持OSS中的BIGINT、DOUBLE、STRING、DATATIME和BOOLEAN数据类型。

## 支持的数据类型 {#section_vjw_ldp_f6v .section}

|类型分类|数据集成column配置类型|数据库数据类型|
|:---|--------------|:------|
|整数类|long|long|
|字符串类|string|string|
|浮点类|double|double|
|布尔类|boolean|bool|
|日期时间类|date|date|

## 参数说明 {#section_jn2_gqh_p2b .section}

|参数|描述|必选|默认值|
|:-|:-|:-|:--|
|datasource|数据源名称，脚本模式支持添加数据源，此配置项填写的内容必须要与添加的数据源名称保持一致。|是|无|
|Object|OSS的Object信息，此处可以支持填写多个Object。例如xxx的bucket中有yunshi文件夹，文件夹中有ll.txt文件，则Object直接填yunshi/ll.txt。 -   当指定单个OSS Object时，OSS Reader暂时只能使用单线程进行数据抽取。后期将考虑在非压缩文件情况下针对单个Object可以进行多线程并发读取。
-   当指定多个OSS Object时，OSS Reader支持使用多线程进行数据抽取。线程并发数通过通道数指定。
-   当指定通配符时，OSS Reader尝试遍历出多个Object信息。例如配置 abc\[0-9\]表示abc0、abc1、abc2、abc3等。配置通配符会导致内存溢出，通常不建议您进行配置。详情请参见[OSS产品概述](../../../../intl.zh-CN/产品简介/什么是对象存储 OSS.md#)。

 **说明：** 

-   数据同步系统会将一个作业下同步的所有Object视作同一张数据表。您必须保证所有的Object能够适配同一套schema信息。
-   请注意控制单个目录下的文件个数，否则可能会触发系统OutOfMemoryError报错。若遇到此情况，请将文件拆分到不同目录后再尝试进行同步。

 |是|无|
|column|读取字段列表，type指定源数据的类型，index指定当前列来自于文本第几列（以0开始），value指定当前类型为常量，不是从源头文件读取数据，而是根据value值自动生成对应的列。 默认情况下，您可以全部按照String类型读取数据，配置如下：

``` {#codeblock_409_48c_5qz}
json
"column": ["*"]
```

 您可以指定column字段信息，配置如下：

``` {#codeblock_3sx_6x9_mkp}
json
"column":
    {
       "type": "long",
       "index": 0    //从OSS文本第一列获取int字段。
    },
    {
       "type": "string",
       "value": "alibaba"  //从OSSReader内部生成alibaba的字符串字段作为当前字段。
    }
```

 **说明：** 对于您指定的column信息，type必须填写，index/value必须选择其一。

 |是|全部按照STRING类型读取。|
|fieldDelimiter|读取的字段分隔符。 **说明：** OSS Reader在读取数据时，需要指定字段分割符，如果不指定默认为（,），界面配置中也会默认填写为（,）。

 |是|,|
|compress|文本压缩类型，默认不填写（即不压缩）。支持压缩类型为gzip、bzip2和zip。|否|不压缩|
|encoding|读取文件的编码配置。|否|utf-8|
|nullFormat|文本文件中无法使用标准字符串定义null（空指针），数据同步系统提供nullFormat定义哪些字符串可以表示为null。例如您配置`nullFormat="null"`，那么如果源头数据是"null"，数据同步系统会视作null字段。针对空字符串，需要加一层转义：\\N=\\\\N。|否|无|
|skipHeader|类CSV格式文件可能存在表头为标题情况，需要跳过。默认不跳过，压缩文件模式下不支持skipHeader。|否|false|
|csvReaderConfig|读取CSV类型文件参数配置，Map类型。读取CSV类型文件使用的CsvReader进行读取，会有很多配置，不配置则使用默认值。|否|无|

## 向导开发介绍 {#section_bp2_wsh_p2b .section}

1.  选择数据源。

    配置同步任务的**数据来源**和**数据去向**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16229/15656702357815_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**数据源**|即上述参数说明中的datasource，通常填写您配置的数据源名称。|
    |**Object前缀**|即上述参数说明中的Object。 **说明：** 假如您的OSS文件名有根据每天的时间命名的部分，例如aaa/20171024abc.txt，关于Object系统参数就可以设置aaa/$\{bdp.system.bizdate\}abc.txt。

 |
    |**列分隔符**|即上述参数说明中的fieldDelimiter，默认值为（,）。|
    |**编码格式**|即上述参数说明中的encoding，默认值为utf-8。|
    |**null值**|即上述参数说明中的nullFormat，将要表示为空的字段填入文本框，如果源端存在则将对应的部分转换为空。|
    |**压缩格式**|即上述参数说明中的compress，默认值为不压缩。|
    |**是否包含表头**|即上述参数说明中的skipHeader，默认值为No。|

2.  字段映射，即上述参数说明中的column。

    左侧的源头表字段和右侧的目标表字段为一一对应的关系。单击**添加一行**可以增加单个字段，鼠标放至需要删除的字段上，即可单击**删除**图标进行删除。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16229/15656702357818_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**同名映射**|单击**同名映射**，可以根据名称建立相应的映射关系，请注意匹配数据类型。|
    |**同行映射**|单击**同行映射**，可以在同行建立相应的映射关系，请注意匹配数据类型。|
    |**取消映射**|单击**取消映射**，可以取消建立的映射关系。|

3.  通道控制。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16221/15656702357675_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**任务期望最大并发数**|数据同步任务内，可以从源并行读取或并行写入数据存储端的最大线程数。向导模式通过界面化配置并发数，指定任务所使用的并行度。|
    |**同步速率**|设置同步速率可以保护读取端数据库，以避免抽取速度过大，给源库造成太大的压力。同步速率建议限流，结合源库的配置，请合理配置抽取速率。|
    |**错误记录数**|错误记录数，表示脏数据的最大容忍条数。|
    |**任务资源组**|任务运行的机器，如果任务数比较多，使用默认资源组出现等待资源的情况，建议购买独享数据集成资源或添加自定义资源组，详情请参见[DataWorks独享资源](../../../../intl.zh-CN/产品定价/预付费（包年包月）/DataWorks独享资源.md#)和[新增任务资源](intl.zh-CN/使用指南/数据集成/常见配置/新增任务资源.md#)。|


## 脚本开发介绍 {#section_cp2_wsh_p2b .section}

脚本配置样例如下所示，具体参数填写请参见参数说明。

``` {#codeblock_098_9rq_dqv}
{
    "type":"job",
    "version":"2.0",//版本号。
    "steps":[
        {
            "stepType":"oss",//插件名。
            "parameter":{
                "nullFormat":"",//定义可以表示为null的字符串。
                "compress":"",//文本压缩类型。
                "datasource":"",//数据源。
                "column":[//字段。
                    {
                        "index":0,//列序号。
                        "type":"string"//数据类型。
                    },
                    {
                        "index":1,
                        "type":"long"
                    },
                    {
                        "index":2,
                        "type":"double"
                    },
                    {
                        "index":3,
                        "type":"boolean"
                    },
                    {
                        "format":"yyyy-MM-dd HH:mm:ss", //时间格式。
                        "index":4,
                        "type":"date"
                    }
                ],
                "skipHeader":"",//类CSV格式文件可能存在表头为标题情况，需要跳过。
                "encoding":"",//编码格式。
                "fieldDelimiter":",",//字段分隔符。
                "fileFormat": "",//文本类型。
                "object":[]//object前缀。
            },
            "name":"Reader",
            "category":"reader"
        },
        {//下面是关于Writer的模板，可以查看相应的写插件文档。
            "stepType":"stream",
            "parameter":{},
            "name":"Writer",
            "category":"writer"
        }
    ],
    "setting":{
        "errorLimit":{
            "record":""//错误记录数。
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

## ORC/Parquet文件读取OSS {#section_u07_y9c_p9r .section}

目前通过复用HDFS Reader的方式完成OSS读取ORC/Parquet格式的文件，在OSS Reader已有参数的基础上，增加了Path、FileFormat等扩展配置参数，参数含义请参见[配置HDFS Reader](intl.zh-CN/使用指南/数据集成/作业配置/配置Reader插件/配置HDFS Reader.md#)。

-   以ORC文件格式读取OSS，示例如下：

    ``` {#codeblock_t0k_4qt_aeb}
    
    {
          "stepType": "oss",
          "parameter": {
            "datasource": "",
            "fileFormat": "orc",
            "path": "/tests/case61/orc__691b6815_9260_4037_9899_aa8e61dc7e4b",
            "column": [
              {
                "index": 0,
                "type": "long"
              },
              {
                "index": "1",
                "type": "string"
              },
              {
                "index": "2",
                "type": "string"
              }
            ]
          }
        }
    ```

-   以Parquet文件格式读取OSS，示例如下：

    ``` {#codeblock_yju_tdr_nfg}
    
    {
          "stepType": "oss",
          "parameter": {
            "datasource": "",
            "fileFormat": "parquet",
            "path": "/tests/case61/parquet",
            "parquetSchema": "message test { required int64 int64_col;\n required binary str_col (UTF8);\nrequired group params (MAP) {\nrepeated group key_value {\nrequired binary key (UTF8);\nrequired binary value (UTF8);\n}\n}\nrequired group params_arr (LIST) {\n  repeated group list {\n    required binary element (UTF8);\n  }\n}\nrequired group params_struct {\n  required int64 id;\n required binary name (UTF8);\n }\nrequired group params_arr_complex (LIST) {\n  repeated group list {\n    required group element {\n required int64 id;\n required binary name (UTF8);\n}\n  }\n}\nrequired group params_complex (MAP) {\nrepeated group key_value {\nrequired binary key (UTF8);\nrequired group value {\n  required int64 id;\n required binary name (UTF8);\n  }\n}\n}\nrequired group params_struct_complex {\n  required int64 id;\n required group detail {\n  required int64 id;\n required binary name (UTF8);\n  }\n  }\n}",
            "column": [
              {
                "index": 0,
                "type": "long"
              },
              {
                "index": "1",
                "type": "string"
              },
              {
                "index": "2",
                "type": "string"
              },
              {
                "index": "3",
                "type": "string"
              },
              {
                "index": "4",
                "type": "string"
              },
              {
                "index": "5",
                "type": "string"
              },
              {
                "index": "6",
                "type": "string"
              },
              {
                "index": "7",
                "type": "string"
              }
            ]
          }
        }
    ```


