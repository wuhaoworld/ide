# DataHub通过数据集成批量导入数据 {#concept_mpp_nmw_pfb .concept}

本文将为您介绍如何通过数据集成对离线DataHub进行数据的导入操作。

数据集成是阿里巴巴集团提供的数据同步平台。该平台具备可跨异构数据存储系统、可靠、安全、低成本、可弹性扩展等特点，可以为20多种数据源提供不同网络环境下的离线（全量/增量）数据进出通道。数据源类型的详情请参见[支持的数据源](intl.zh-CN/使用指南/数据集成/数据源配置/支持的数据源.md#)。

## 准备工作 {#section_ght_gnw_pfb .section}

1.  准备阿里云账号，并创建账号的访问密钥，即AccessID和AccessKey。详情请参见[准备阿里云账号](../../../../intl.zh-CN/准备工作/管理员使用云账号/准备阿里云账号.md#)。
2.  开通MaxCompute，自动产生一个默认的MaxCompute数据源，并使用主账号登录DataWorks。
3.  创建工作空间，您可以在工作空间中协作完成业务流程，共同维护数据和任务等，因此使用DataWorks之前需要先创建一个工作空间。详情请参见[创建工作空间](../../../../intl.zh-CN/准备工作/管理员使用云账号/创建工作空间.md#)。

    **说明：** 如果您想通过子账号创建数据集成任务，可以赋予其相应的权限。详情请参见[准备RAM用户](../../../../intl.zh-CN/准备工作/管理员使用云账号/准备RAM用户.md#)和[成员管理](intl.zh-CN/使用指南/工作空间管理/成员管理.md#)。


## 操作步骤 {#section_myv_r4w_pfb .section}

以Stream同步数据至DataHub的脚本模式为例，操作如下。

1.  以开发者身份登录[DataWorks控制台](https://workbench.data.aliyun.com/console)，单击对应工作空间后的**进入数据集成**。
2.  进入**任务列表** \> **离线同步任务**页面，单击右上角的**新建任务**。

    ![新建任务](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40315/156713492358543_zh-CN.png)

3.  在新建节点对话框中，填写**节点名称**并选择**目标文件夹**，单击**提交**。

    ![新建节点](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40315/156713492358547_zh-CN.png)

4.  成功创建数据同步节点后，单击工具栏中的**转换脚本**。

    ![转换脚本](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/24565/156713492314347_zh-CN.png)

5.  单击提示对话框中的**确认**，即可进入脚本模式进行开发。

    ![确认](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40315/156713492358550_zh-CN.png)

6.  单击工具栏中的**导入模板**。

    ![导入模板](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40315/156713492358551_zh-CN.png)

7.  在**导入模板**对话框中，选择**来源类型**、**数据源**、**目标类型**及**数据源**。

    ![对话框](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40315/156713492321027_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**来源类型**|此处选择**Stream**类型。|
    |**目标类型**|此处选择**DataHub**类型。|
    |**数据源**|选择配置好的数据源。 **说明：** 如果没有提前配置数据源，可以单击**新增数据源**进行新增操作。

 |

8.  单击**确认**生成初始脚本，您可以根据自身需求进行配置。

    ``` {#codeblock_rvl_k0w_63n}
    {
    "type": "job",
    "version": "1.0",
    "configuration": {
     "setting": {
       "errorLimit": {
         "record": "0"
       },
       "speed": {
         "mbps": "1",
         "concurrent": 1,//作业并发数。
         "throttle": false
       }
     },
     "reader": {
       "plugin": "stream",
       "parameter": {
         "column": [//源端列名。
           {
             "value": "field",//列属性。
             "type": "string"
           },
           {
             "value": true,
             "type": "bool"
           },
           {
             "value": "byte string",
             "type": "bytes"
           }
         ],
         "sliceRecordCount": "100000"
       }
     },
     "writer": {
       "plugin": "datahub",
       "parameter": {
         "datasource": "datahub",//数据源名。
         "topic": "xxxx",//Topic是DataHub订阅和发布的最小单位，您可以用Topic来表示一类或者一种流数据。
         "mode": "random",//随机写入。
         "shardId": "0",//Shard 表示对一个Topic进行数据传输的并发通道，每个Shard会有对应的ID。
         "maxCommitSize": 524288,//为了提高写出效率，待攒数据大小达到maxCommitSize大小（单位MB）时，批量提交到目的端。默认是1,048,576，即1MB数据。
         "maxRetryCount": 500
       }
     }
    }
    }
    ```

9.  单击**保存**并**运行**。

    **说明：** 

    -   DataHub仅支持以脚本模式导入数据。
    -   如果需要选择新模板，可以单击工具栏中的**导入模板**，导入新模板后，会覆盖原有模板的所有内容。
    -   保存同步任务后，直接单击**运行**，任务会立刻运行。

        您也可以单击**提交**，将同步任务提交到调度系统中。调度系统会按照配置属性，从第2天开始自动定时执行。


## 参考文档 {#section_cvw_n2b_pfb .section}

其它数据源的配置同步任务详情，请参见下述文档：

-   [配置Reader插件](https://www.alibabacloud.com/help/faq-list/74300.htm)。
-   [配置Writer插件](https://www.alibabacloud.com/help/faq-list/74301.htm)。

