# 配置LogHub数据源 {#concept_hrr_q41_p2b .concept}

LogHub数据源作为数据中枢，为您提供读取和写入LogHub双向通道的功能，支持Reader和Writer插件。

**说明：** 标准模式的工作空间支持[数据源隔离](intl.zh-CN/使用指南/数据集成/数据源配置/数据源隔离.md#)功能，您可以分别添加开发环境和生产环境的数据源并进行隔离，以保护您的数据安全。

## 操作步骤 {#section_jy4_q4v_42b .section}

1.  以项目管理员身份登录[DataWorks控制台](https://workbench.data.aliyun.com/console)，单击对应工作空间操作栏中的**进入数据集成**。
2.  选择**同步资源管理** \> **数据源**，单击**新增数据源**。

    ![新增数据源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16213/15660098027595_zh-CN.png)

3.  在新增数据源弹出框中，选择数据源类型为**LogHub**。
4.  填写LogHub数据源的各配置项。

    ![数据源配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16203/15660098027541_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**数据源名称**|数据源名称必须以字母、数字、下划线组合，且不能以数字和下划线开头。|
    |**数据源描述**|对数据源进行简单描述，不得超过80个字符。|
    |**适用环境**|可以选择**开发**或**生产**环境。 **说明：** 仅标准模式工作空间会显示此配置。

 |
    |**LogHub Endpoint**| 通常格式为`http://cn-shanghai.log.aliyun.com`。详情请参见[服务入口](https://www.alibabacloud.com/help/doc-detail/29008.htm)。

 |
    |**Project**|输入对应的Project。|
    |**AccessID/AceessKey**|访问密钥（AccessKeyID和AccessKeySecret），相当于登录密码。|

5.  单击**测试连通性**。
6.  测试连通性通过后，单击**确定**。

    提供测试连通性功能，可以判断输入的信息是否正确 。


## 后续步骤 {#section_dqv_5d1_p2b .section}

现在，您已经学习了如何配置LogHub数据源，您可以继续学习下一个教程。在该教程中您将学习如何配置LogHub插件，详情请参见[配置LogHub Reader](intl.zh-CN/使用指南/数据集成/作业配置/配置Reader插件/配置LogHub Reader.md#)和[配置LogHub Writer](intl.zh-CN/使用指南/数据集成/作业配置/配置Writer插件/配置LogHub Writer.md#)。

