# OTSStream配置同步任务 {#concept_llg_dpx_pfb .concept}

OTSStream插件主要用于导出Table Store增量数据。增量数据可以看作操作日志，除数据本身外还附有操作信息。

OTSStream插件与全量导出插件不同，增量导出插件仅支持多版本模式，且不支持指定列，详情请参见[配置OTSStream Reader](intl.zh-CN/使用指南/数据集成/作业配置/配置Reader插件/配置OTSStream Reader.md#)。

**说明：** OTSStream配置同步任务时，请注意以下问题：

-   当前时间的前5分钟之前和24小时之内是可读数据。
-   设置的结束时间不能超过系统显示的时间，即您设置的结束时间要比运行时间早5分钟。
-   配置日调度会出现数据丢失的情况。
-   不可以配置周期调度和月调度。

示例如下：

开始时间和结束时间要包含操作Table Store表的时间，例如20171019162000您向Table Store插入2条数据，则开始时间设置为20171019161000，结束时间设置为20171019162600。

## 新增数据源 {#section_zvh_wrx_pfb .section}

1.  以项目管理员身份登录[DataWorks控制台](https://workbench.data.aliyun.com/console)，单击对应工作空间后的**进入数据集成**。
2.  进入**同步资源管理** \> **数据源**页面，单击右上角的**新增数据源**。

    ![新增数据源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40324/156713498158554_zh-CN.png)

3.  在新增数据源弹出框中，选择数据源类型为**Table Store（OTS）**。
4.  填写Table Store（OTS）数据源的各配置项。

    ![配置项](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40324/156713498121071_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**数据源名称**|数据源名称必须以字母、数字、下划线组合，且不能以数字和下划线开头。|
    |**数据源描述**|对数据源进行简单描述，不得超过80个字符。|
    |**适用环境**|可以选择**开发**或**生产**环境。 **说明：** 仅标准模式工作空间会显示此配置。

 |
    |**Endpoint**| Table Store服务对应的Endpoint。

 |
    |**Table Store实例ID**|Table Store服务对应的实例ID。|
    |**AccessID/AceessKey**|访问密钥（AccessKeyID和AccessKeySecret），相当于登录密码。|

5.  单击**测试连通性**。
6.  测试连通性通过后，单击**完成**。

## 通过向导模式配置同步任务 {#section_xxh_45x_pfb .section}

1.  进入**任务列表** \> **离线同步任务**页面，单击右上角的**新建任务**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40324/156713498258555_zh-CN.png)

2.  在新建节点对话框中，填写**节点名称**并选择**目标文件夹**，单击**提交**。
3.  进入数据同步节点配置页面，选择数据来源。

    ![数据来源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40324/156713498221076_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**数据源**|填写数据源的名称。|
    |**表**|导出增量数据的表的名称。该表需要开启Stream，您可以在建表时开启，或使用UpdateTable接口开启。|
    |**开始时间**|增量数据的时间范围（左闭右开）的左边界，格式为yyyymmddhh24miss，单位毫秒。|
    |**结束时间**|增量数据的时间范围（左闭右开）的右边界，格式为yyyymmddhh24miss，单位毫秒。|
    |**状态表**|用于记录状态的表的名称。|
    |**最大重试次数**|从TableStore中读增量数据时，每次请求的最大重试次数，默认是30。|
    |**导出时序信息**|是否导出时序信息，时序信息包含了数据的写入时间等。|

4.  选择数据去向。

    ![数据去向](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40324/156713498221078_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**数据源**|填写配置的数据源名称。|
    |**表**|选择需要同步的表。|
    |**分区信息**|此处需同步的表是非分区表，所以无分区信息。|
    |**清理规则**|     -   **写入前清理已有数据**：导数据之前，清空表或者分区的所有数据，相当于`insert overwrite`。
    -   **写入前保留已有数据**：导数据之前，不清理任何数据，每次运行数据都是追加进去的，相当于`insert into`。
 |
    |**空字符串作为null**|默认值为**否**。|

5.  字段映射。

    左侧的源头表字段和右侧的目标表字段为一一对应的关系。单击**添加一行**可以增加单个字段，鼠标放至需要删除的字段上，即可单击**删除**图标进行删除。

    ![字段映射](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40324/156713498221080_zh-CN.png)

6.  通道控制。

    ![通道控制](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/24566/156713498214354_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**任务期望最大并发数**|数据同步任务内，可以从源并行读取或并行写入数据存储端的最大线程数。向导模式通过界面化配置并发数，指定任务所使用的并行度。|
    |**同步速率**|设置同步速率可以保护读取端数据库，以避免抽取速度过大，给源库造成太大的压力。同步速率建议限流，结合源库的配置，请合理配置抽取速率。|
    |**错误记录数**|错误记录数，表示脏数据的最大容忍条数。|
    |**任务资源组**|任务运行的机器，如果任务数比较多，使用默认资源组出现等待资源的情况，建议购买独享数据集成资源或添加自定义资源组，详情请参见[DataWorks独享资源](../../../../intl.zh-CN/产品定价/包年包月/DataWorks独享资源.md#)和[新增任务资源](intl.zh-CN/使用指南/数据集成/常见配置/新增任务资源.md#)。|

7.  **保存**并**运行**任务。

    单击任务上方的**运行**按钮，将直接在数据集成页面运行任务，运行之前需要配置自定义参数的具体数值。

    ![运行](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40324/156713498221083_zh-CN.png)


## 通过脚本模式配置同步任务 {#section_cbl_n3y_pfb .section}

如果您需要通过脚本模式配置此任务，单击工具栏中的**转换脚本**，选择**确认**即可进入脚本模式。

![脚本模式](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/24565/156713498214347_zh-CN.png)

您可以根据自身进行配置，示例脚本如下。

``` {#codeblock_nid_kw6_o0m}
{
  "type": "job",
  "version": "1.0",
  "configuration": {
    "reader": {
      "plugin": "otsstream",
      "parameter": {
        "datasource": "otsstream",//数据源名，需要与您添加的数据源名称保持一致。
        "dataTable": "person",//导出增量数据的表的名称。该表需要开启Stream，可以在建表时开启，或者使用UpdateTable接口开启。
        "startTimeString": "${startTime}",//增量数据的时间范围（左闭右开）的左边界，格式为yyyymmddhh24miss，单位毫秒。
        "endTimeString": "${endTime}",//运行时间。
        "statusTable": "TableStoreStreamReaderStatusTable",//用于记录状态的表的名称。
        "maxRetries": 30,//请求的最大重试次数。
        "isExportSequenceInfo": false,
      }
    },
    "writer": {
      "plugin": "odps",
      "parameter": {
        "datasource": "odps_first",//数据源名。
        "table": "person",//目标表名。
        "truncate": true,
        "partition": "pt=${bdp.system.bizdate}",//分区信息。
        "column": [//目标列名。
          "id",
          "colname",
          "version",
          "colvalue",
          "optype",
          "sequenceinfo"
        ]
      }
    },
    "setting": {
      "speed": {
        "mbps": 7,//作业速率上限。
        "concurrent": 7//并发数。
      }
    }
  }
}
```

**说明：** 

-   关于运行时间参数和结束时间参数，有两种表现形式（配置任务选择其中一种）。
    -   `"startTimeString": "${startTime}"` 

        增量数据的时间范围（左闭右开）的左边界，格式为yyyymmddhh24miss，单位毫秒。

         `"endTimeString": "${endTime}"` 

        增量数据的时间范围（左闭右开）的右边界，格式为yyyymmddhh24miss，单位毫秒。

    -   `"startTimestampMillis":""` 

        增量数据的时间范围（左闭右开）的左边界，单位毫秒。

        Reader插件会从statusTable中找对应startTimestampMillis的位点，从该点开始读取开始导出数据。

        如果statusTable中找不到对应的位点，则从系统保留的增量数据的第1条开始读取，并跳过写入时间小于startTimestampMillis的数据。

    -   `"endTimestampMillis":" "` 

        增量数据的时间范围（左闭右开）的右边界，单位毫秒。

        Reade插件startTimestampMilli位置开始导出数据后，当遇到第1条时间戳大于等于endTimestampMilli的数据时，结束导出数据，导出完成。

        当读取完当前全部的增量数据时，结束读取，即使未达endTimestampMillis。

-   如果配置isExportSequenceInfo项为true，如`“isExportSequenceInfo”: true`，则会导出时序信息，目标会多出1行，目标字段列则多1列。时序信息包含了数据的写入时间等，默认该值为false，即不导出。

