# 配置FTP Writer {#concept_mrn_q4l_q2b .concept}

本文为您介绍FTP Writer支持的数据类型、字段映射和数据源等参数及配置示例。

FTP Writer实现了向远程FTP文件写入CSV格式的一个或多个文件。在底层实现上，FTP Writer将数据集成传输协议下的数据转换为CSV格式，并使用FTP相关的网络协议写出至远程FTP服务器。

**说明：** 开始配置FTP Writer插件前，请首先配置好数据源，详情请参见[配置FTP数据源](intl.zh-CN/使用指南/数据集成/数据源配置/配置FTP数据源.md#)。

写入FTP文件内容存放的是一张逻辑意义上的二维表，例如CSV格式的文本信息。

FTP Writer实现了从数据集成协议转为FTP文件功能，FTP文件本身是无结构化数据存储。目前FTP Writer支持的功能如下：

-   支持且仅支持写入文本类型（不支持BLOB，如视频数据）的文件，且要求文本中schema为一张二维表。
-   支持类CSV和TEXT格式的文件，自定义分隔符。
-   写出时不支持文本压缩。
-   支持多线程写入，每个线程写入不同子文件。

暂时不支持以下两种功能：

-   单个文件不能支持并发写入。
-   FTP本身不提供数据类型，FTP Writer均将数据以STRING类型写入FTP文件。

## 参数说明 {#section_jn2_gqh_p2b .section}

|参数|描述|必选|默认值|
|:-|:-|:-|:--|
|datasource|数据源名称，脚本模式支持添加数据源，此配置项填写的内容必须要与添加的数据源名称保持一致。|是|无|
|timeout|连接FTP服务器连接超时时间，单位毫秒。|否|60,000（1分钟）|
|path|FTP文件系统的路径信息，FTP Writer会写入Path目录下多个文件。|是|无|
|fileName|FTP Writer写入的文件名，该文件名会添加随机的后缀作为每个线程写入实际文件名。|是|无|
|writeMode|FTP Writer写入前数据清理处理模式。 -   truncate：写入前清理目录下，fileName前缀的所有文件。
-   append：写入前不做任何处理，数据集成FTP Writer直接使用filename写入，并保证文件名不冲突。
-   nonConflict：如果目录下有fileName前缀的文件，直接报错。

 |是|无|
|fieldDelimiter|写入的字段分隔符。|是，单字符|无|
|skipHeader|类CSV格式文件可能存在表头为标题情况，需要跳过。默认不跳过，压缩文件模式下不支持skipHeader。|否|false|
|compress|支持gzip和bzip2两种压缩形式。|否|无压缩|
|encoding|读取文件的编码配置。|否|utf-8|
|nullFormat|文本文件中无法使用标准字符串定义null（空指针），数据集成提供nullFormat定义哪些字符串可以表示为null。 例如您配置`nullFormat="null"`，如果源头数据是null，数据集成视作null字段。

 |否|无|
|dateFormat|日期类型的数据序列化到文件中时的格式，例如"dateFormat":"yyyy-MM-dd"。|否|无|
|fileFormat|文件写出的格式，包括CSV和TEXT两种，CSV是严格的CSV格式，如果待写数据包括列分隔符，则会按照CSV的转义语法转义，转义符号为双引号。TEXT格式是用列分隔符简单分割待写数据，对于待写数据包括列分隔符情况下不做转义。|否|TEXT|
|header|txt写出时的表头，例如\['id', 'name', 'age'\]。|否|无|
|markDoneFileName|标档文件名，同步任务结束后生成标档文件，根据此标档文件可以判断同步任务是否成功。此处应配置为绝对路径。|否|无|

## 向导开发介绍 {#section_bp2_wsh_p2b .section}

1.  选择数据源。

    配置同步任务的**数据来源**和**数据去向**。

    ![选择数据源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16222/15637951007697_zh-CN.png)

    |配置|说明|
    |--|--|
    |**数据源**|即上述参数说明中的datasource，通常填写您配置的数据源名称。|
    |**文件路径**|即上述参数说明中的path。|
    |**文本类型**|读取的文件类型，默认情况下文件作为csv格式文件进行读取。|
    |**列分隔符**|即上述参数说明中的fieldDelimiter，默认值为（,）。|
    |**编码格式**|即上述参数说明中的encoding，默认值为utf-8。|
    |**null值**|即上述参数说明中的nullFormat，定义表示null值的字符串。|
    |**时间格式**|即上述参数说明中的dateFormat。|
    |**前缀冲突**|即上述参数说明中的writeMode，定义表示null值的字符串。|

2.  字段映射，即上述参数说明中的column。

    左侧的源头表字段和右侧的目标表字段为一一对应的关系。单击**添加一行**可以增加单个字段，将鼠标放至需要删除的字段上，即可单击**删除**按钮进行删除。

    ![字段映射](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16222/15637951007701_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**同名映射**|单击**同名映射**，可以根据名称建立相应的映射关系，请注意匹配数据类型。|
    |**同行映射**|单击**同行映射**，可以在同行建立相应的映射关系，请注意匹配数据类型。|
    |**取消映射**|单击**取消映射**，可以取消建立的映射关系。|

3.  通道控制。

    ![通道控制](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16221/15637951007675_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**任务期望最大并发数**|数据同步任务内，可以从源并行读取或并行写入数据存储端的最大线程数。向导模式通过界面化配置并发数，指定任务所使用的并行度。|
    |**同步速率**|设置同步速率可以保护读取端数据库，以避免抽取速度过大，给源库造成太大的压力。同步速率建议限流，结合源库的配置，请合理配置抽取速率。|
    |**错误记录数**|错误记录数，表示脏数据的最大容忍条数。|
    |**任务资源组**|任务运行的机器，如果任务数比较多，使用默认资源组出现等待资源的情况，建议购买独享数据集成资源或添加自定义资源组，详情请参见[DataWorks独享资源](../../../../intl.zh-CN/产品定价/预付费（包年包月）/DataWorks独享资源.md#)和[新增任务资源](intl.zh-CN/使用指南/数据集成/常见配置/新增任务资源.md#)。|


## 脚本开发介绍 {#section_cp2_wsh_p2b .section}

配置一个写入FTP数据库的同步作业。

``` {#codeblock_be6_kgd_cth}
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
            "stepType":"ftp",//插件名。
            "parameter":{
                "path":"",//文件路径。
                "fileName":"",//文件名称。
                "nullFormat":"null",//null值。
                "dateFormat":"yyyy-MM-dd HH:mm:ss",//时间格式。
                "datasource":"",//数据源。
                "writeMode":"",//写入模式。
                "fieldDelimiter":",",//列分隔符。
                "encoding":"",//编码格式。
                "fileFormat":""//文本类型。
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

