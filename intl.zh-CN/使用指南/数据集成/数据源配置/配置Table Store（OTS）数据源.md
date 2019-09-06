# 配置Table Store（OTS）数据源 {#concept_ccz_rqb_p2b .concept}

表格存储（Table Store）是构建在阿里云飞天分布式系统之上的NoSQL数据存储服务，提供海量结构化数据的存储和实时访问。

**说明：** 

-   标准模式的工作空间支持[数据源隔离](intl.zh-CN/使用指南/数据集成/数据源配置/数据源隔离.md#)功能，您可以分别添加开发环境和生产环境的数据源并进行隔离，以保护您的数据安全。
-   如果您想对表格存储有更深入的了解，请参见[什么是表格存储](../../../../intl.zh-CN/产品简介/什么是表格存储.md#)。

## 操作步骤 {#section_jy4_q4v_42b .section}

1.  以项目管理员身份进入[DataWorks控制台](https://workbench.data.aliyun.com/console)，单击相应工作空间后的**进入数据集成**。
2.  选择**同步资源管理** \> **数据源**，单击**新增数据源**。

    ![新增数据源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16213/15677414337595_zh-CN.png)

3.  在新增数据源弹出框中，选择数据源类型为**Table Store（OTS）**。
4.  填写Table Store（OTS）数据源的各配置项。

    ![配置项](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16210/15677414337571_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**数据源名称**|数据源名称必须以字母、数字、下划线组合，且不能以数字和下划线开头。|
    |**数据源描述**|对数据源进行简单描述，不得超过80个字符。|
    |**适用环境**|可以选择**开发**或**生产**环境。 **说明：** 仅标准模式工作空间会显示此配置。

 |
    |**Endpoint**|Table Store服务对应的Endpoint。|
    |**Table Store实例ID**|Table Store服务对应的实例ID。|
    |**AccessID/AceessKey**|访问密钥（AccessKeyID和AccessKeySecret），相当于登录密码。|

5.  单击**测试连通性**。
6.  测试连通性通过后，单击**完成**。

## 测试连通性说明 {#section_eq3_lnb_p2b .section}

-   经典网络下，能够提供测试连通性功能，可以判断输入的信息是否正确。
-   专有网络目前不支持数据源连通性测试，直接单击**完成**。

## 后续步骤 {#section_x2g_1kp_y2b .section}

现在，您已经学习了如何配置OTS数据源，您可以继续学习下一个教程。在该教程中，您将学习如何配置Table Store（OTS） Reader插件。详情请参见[配置Table Store（OTS） Reader](intl.zh-CN/使用指南/数据集成/作业配置/配置Reader插件/配置Table Store（OTS） Reader.md#)。

