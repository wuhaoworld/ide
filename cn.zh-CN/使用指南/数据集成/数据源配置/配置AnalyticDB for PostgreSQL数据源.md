# 配置AnalyticDB for PostgreSQL数据源 {#concept_z3q_wyb_5fb .concept}

AnalyticDB for PostgreSQL数据源提供读取和写入AnalyticDB for PostgreSQL的双向功能，您可以通过向导模式和脚本模式配置同步任务。

**说明：** 

标准模式的工作空间支持[数据源隔离](intl.zh-CN/使用指南/数据集成/数据源配置/数据源隔离.md#)功能，您可以分别添加开发环境和生产环境的数据源并进行隔离，以保护您的数据安全。

如果是在VPC环境下的AnalyticDB for PostgreSQL，需要注意以下问题：

-   自建的PostgreSQL数据源
    -   不支持测试连通性，但仍支持配置同步任务，创建数据源时单击**完成**即可。
    -   必须使用自定义调度资源组运行对应的同步任务，请确保自定义资源组可以连通您的自建数据库，详情请参见[（一端不通）数据源网络不通的情况下的数据同步](intl.zh-CN/使用指南/数据集成/最佳实践/（一端不通）数据源网络不通的情况下的数据同步.md#)和[（两端不通）数据源网络不通的情况下的数据同步](intl.zh-CN/使用指南/数据集成/最佳实践/（两端不通）数据源网络不通的情况下的数据同步.md#)。
-   通过实例ID创建的AnalyticDB for PostgreSQL数据源

    您无需选择网络环境，系统自动根据您填写的RDS实例信息进行判断。


## 操作步骤 {#section_uvj_mzr_5fb .section}

1.  以项目管理员身份登录[DataWorks控制台](https://workbench.data.aliyun.com/console)，单击对应工作空间后的**进入数据集成**。
2.  选择**同步资源管理** \> **数据源**，单击**新增数据源**。

    ![新增数据源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16213/15677406307595_zh-CN.png)

3.  在新增数据源弹出框中，选择数据源类型为**AnalyticDB for PostgreSQL**。
4.  填写AnalyticDB for PostgreSQL数据源的各配置项。

    AnalyticDB for PostgreSQL数据源类型包括**阿里云数据库（AnalyticDB）**和**连接串模式（数据集成网络可直接连通）**。

    -   以新增**AnalyticDB for PostgreSQL** \> **阿里云数据库（AnalyticDB）**类型的数据源为例。

        ![配置](images/32075_zh-CN.jpeg)

        |配置|说明|
        |:-|:-|
        |**数据源类型**|当前选择的数据源类型为**AnalyticDB for PostgreSQL** \> **阿里云数据库（AnalyticDB）**。|
        |**数据源名称**|数据源名称必须以字母、数字、下划线组合，且不能以数字和下划线开头。|
        |**数据源描述**|对数据源进行简单描述，不得超过80个字符。|
        |**适用环境**|可以选择**开发**或**生产**环境。 **说明：** 仅标准模式工作空间会显示此配置。

 |
        |**RDS实例ID**|您可以进入AnalyticDB for PostgreSQL的控制台，查看相应的实例ID。|
        |**主账号ID**|您可以进入AnalyticDB for PostgreSQL控制台的安全设置页面，查看相应的信息。![安全设置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/62183/156774063032076_zh-CN.png)

|

    -   以新增**AnalyticDB for PostgreSQL** \> **连接串模式（数据集成网络可直接连通）**类型的数据源为例。

        ![新增数据源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/62183/156774063057838_zh-CN.png)

        |配置|说明|
        |:-|:-|
        |**数据源类型**|当前选择的数据源类型为**AnalyticDB for PostgreSQL** \> **连接串模式（数据集成网络可直接连通）**。|
        |**数据源名称**|数据源名称必须以字母、数字、下划线组合，且不能以数字和下划线开头。|
        |**数据源描述**|对数据源进行简单描述，不得超过80个字符。|
        |**适用环境**|可以选择**开发**或**生产**环境。 **说明：** 仅标准模式工作空间会显示此配置。

 |
        |**JDBC URL**|JDBC连接信息，格式为`jdbc:postgresql://ServerIP:Port/Database`。|
        |**用户名/密码**|数据库对应的用户名和密码。|

5.  单击**测试连通性**。
6.  测试连通性通过后，单击**完成**。

**说明：** 您需要先添加白名单才能连接成功，详情请参见[添加白名单](intl.zh-CN/使用指南/数据集成/常见配置/添加白名单.md#)。

## 测试连通性说明 {#section_w31_g1s_5fb .section}

-   经典网络下，能够提供测试连通性功能，可以判断输入的信息是否正确。
-   专有网络下，如果您使用实例模式配置数据源，可以判断输入的信息是否正确。
-   专有网络下，如果您将VPC内部地址作为JDBC URL添加数据源，测试连通性会报告失败。
-   经典网络/专有网络下，如果您将数据源的公网地址作为JDBC URL添加数据源，可以判断输入的信息是否正确。

## 后续步骤 {#section_xsp_r1s_5fb .section}

现在，您已经学习了如何配置AnalyticDB for PostgreSQL数据源，您可以继续学习下一个教程。在该教程中，您将学习如何配置AnalyticDB for PostgreSQL插件，详情请参见[配置AnalyticDB for PostgreSQL Reader](intl.zh-CN/使用指南/数据集成/作业配置/配置Reader插件/配置AnalyticDB for PostgreSQL Reader.md#)和[配置AnalyticDB for PostgreSQL Writer](intl.zh-CN/使用指南/数据集成/作业配置/配置Writer插件/配置AnalyticDB for PostgreSQL Writer.md#)。

