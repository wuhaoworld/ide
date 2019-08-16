# 配置Data Lake Analytics（DLA）数据源 {#concept_z3q_wyb_5fb .concept}

本文将为您介绍如何配置Data Lake Analytics（DLA）数据源。

**说明：** 标准模式的工作空间支持[数据源隔离](cn.zh-CN/使用指南/数据集成/数据源配置/数据源隔离.md#)功能，您可以分别添加开发环境和生产环境的数据源并进行隔离，以保护您的数据安全。

## 操作步骤 {#section_uvj_mzr_5fb .section}

1.  以项目管理员身份进入[DataWorks控制台](https://workbench.data.aliyun.com/console)，单击对应工作空间操作栏中的**进入数据集成**。
2.  选择**同步资源管理** \> **数据源**，单击**新增数据源**。

    ![新增数据源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16213/15659474607595_zh-CN.png)

3.  在新增数据源弹出框中，选择数据源类型为**Data Lake Analytics（DLA）**。
4.  填写Data Lake Analytics（DLA）数据源的各配置项。

    ![Data Lake Analytics](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1280075/156594746054881_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**数据源名称**|数据源名称必须以字母、数字、下划线组合，且不能以数字和下划线开头。|
    |**数据源描述**|对数据源进行简单描述，不得超过80个字符。|
    |**适用环境**|可以选择**开发**或**生产**环境。 **说明：** 仅标准模式工作空间会显示此配置。

 |
    |**连接Url**|格式为`Address:Port`。|
    |**数据库**|填写对应的数据库名称。|
    |**用户名/密码**|数据库对应的用户名和密码。|

5.  单击**测试连通性**。
6.  测试连通性通过后，单击**完成**。

## 测试连通性说明 {#section_w2w_05i_c3z .section}

-   经典网络下，能够提供测试连通性能力，可以判断输入的信息是否正确。
-   专有网络VPC目前不支持数据源连通性测试，直接单击**完成**。

    如果是专有网络VPC，需要使用独享资源，详情请参见[独享资源模式](cn.zh-CN/使用指南/管理控制台/独享资源模式.md#)和[Data Lake Analytics节点](cn.zh-CN/使用指南/数据开发/节点类型/Data Lake Analytics节点.md#)。


