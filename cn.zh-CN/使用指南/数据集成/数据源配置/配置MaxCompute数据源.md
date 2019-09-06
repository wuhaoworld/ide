# 配置MaxCompute数据源 {#concept_tms_vp1_p2b .concept}

MaxCompute数据源作为数据中枢，为您提供读取和写入MaxCompute双向通道的功能，支持Reader和Writer插件。

大数据计算服务（MaxCompute，原名ODPS）提供完善的数据导入方案，能够更快速地解决海量数据计算问题。

**说明：** 

-   标准模式的工作空间支持[数据源隔离](intl.zh-CN/使用指南/数据集成/数据源配置/数据源隔离.md#)功能，您可以分别添加开发环境和生产环境的数据源并进行隔离，以保护您的数据安全。
-   每个项目空间系统都将生成一个默认的数据源（odps\_first），对应的MaxCompute项目名称为当前项目空间对应的计算引擎MaxCompute项目名称。您可以单击右上方的用户信息，在修改AccessKey信息页面切换默认数据源的AK，但需要注意以下问题：
    -   只能从主账号AK切换到主账号AK。
    -   切换时当前必须没有任务在运行中（数据集成或数据开发等一切和DataWorks相关的任务），您自行添加的MaxCompute数据源可以使用子账号AK。

## 操作步骤 {#section_jy4_q4v_42b .section}

1.  以项目管理员身份进入[DataWorks控制台](https://workbench.data.aliyun.com/console)，单击相应工作空间后的**进入数据集成**。
2.  选择**同步资源管理** \> **数据源**，单击**新增数据源**。

    ![新增数据源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16213/15677447727595_zh-CN.png)

3.  在新增数据源弹出框中，选择数据源类型为**MaxCompute（ODPS）**。
4.  填写MaxCompute数据源的各配置项。

    ![配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16204/15677447737543_zh-CN.jpg)

    |配置|说明|
    |:-|:-|
    |**数据源名称**|数据源名称必须以字母、数字、下划线组合，且不能以数字和下划线开头。|
    |**数据源描述**|对数据源进行简单描述，不得超过80个字符。|
    |**适用环境**|可以选择**开发**或**生产**环境。 **说明：** 仅标准模式工作空间会显示此配置。

 |
    |**ODPS Endpoint**|默认只读，从系统配置中自动读取。|
    |**Tunnel Endpoint**|MaxCompute Tunnel服务的连接地址，详情请参见[配置Endpoint](../../../../intl.zh-CN/准备工作/配置Endpoint.md#)。|
    |**ODPS项目名称**|MaxCompute（ODPS）项目名称。|
    |**AccessID/AceessKey**|访问密钥（AccessKeyID和AccessKeySecret），相当于登录密码。|

5.  单击**测试连通性**。
6.  测试连通性通过后，单击**完成**。

    提供测试连通性功能，可以判断输入的信息是否正确 。


## 后续步骤 {#section_dqv_5d1_p2b .section}

现在，您已经学习了如何配置MaxCompute数据源，您可以继续学习下一个教程。在该教程中，您将学习如何配置MaxCompute插件。详情请参见[配置MaxCompute Reader](intl.zh-CN/使用指南/数据集成/作业配置/配置Reader插件/配置MaxCompute Reader.md#)和[配置MaxCompute Writer](intl.zh-CN/使用指南/数据集成/作业配置/配置Writer插件/配置MaxCompute Writer.md#)。

