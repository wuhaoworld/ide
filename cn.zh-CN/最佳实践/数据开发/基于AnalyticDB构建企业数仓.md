# 基于AnalyticDB构建企业数仓 {#concept_1305343 .concept}

本文将为您介绍如何基于AnalyticDB构建企业数仓，并进行运维和元数据管理等操作。

## 创建工作空间 {#section_qq1_6hx_z11 .section}

1.  使用主账号登录[DataWorks控制台](https://workbench.data.aliyun.com/console)。
2.  使用主账号登录[DataWorks控制台](https://partners-intl.aliyun.com)。
3.  单击控制台**概览** \> **常用功能**下的**创建工作空间**。

    ![创建工作空间](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1039843/156376672452395_zh-CN.jpg)

    您也可以进入工作空间列表页面，单击**创建工作空间**。

    ![创建工作空间](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1039843/156376672552396_zh-CN.jpg)

4.  填写创建工作空间对话框中的配置项，选择地域、计费方式和服务。

    如果选择的地域没有购买相关的服务，会直接显示该地域下暂无可用服务，默认选中数据集成、数据开发、运维中心和数据质量。

    ![配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16175/15637667258939_zh-CN.png)

    |选项|配置|说明|
    |:-|:-|:-|
    |**选择计算引擎服务**|**MaxCompute**|MaxCompute是一种快速、完全托管的TB/PB级数据仓库解决方案，能够更快速为您解决海量数据计算问题，有效降低企业成本，并保障数据安全。 **说明：** 完成创建Dataworks工作空间后，需要关联MaxCompute项目，否则现执行命令会报project not found的错误。

 |
    |**机器学习PAI**|机器学习是指机器通过统计学算法，对大量的历史数据进行学习从而生成经验模型，利用经验模型指导业务。|
    |**实时计算**|开通后，您可以在DataWorks使用Stream Studio，进行流式计算任务开发。|
    |**选择DataWorks服务**|**数据集成**|数据集成是稳定高效、弹性伸缩的数据同步平台。致力于提供复杂网络环境下、丰富的异构数据源之间数据高速稳定的数据移动及同步能力。详情请参见[数据集成](../cn.zh-CN/使用指南/数据集成/数据集成简介/数据集成概述.md#)模块的文档。|
    |**数据开发**|该页面是您根据业务需求，设计数据计算流程，并实现为多个相互依赖的任务，供调度系统自动执行的主要操作页面。详情请参见[数据开发](../cn.zh-CN/使用指南/数据开发/解决方案.md#)模块的文档。|
    |**运维中心**|该页面可对任务和实例进行展示和操作，您可以在此查看所有任务的实例。详情请参见[运维中心](../cn.zh-CN/使用指南/运维中心/运维中心概述.md#)模块的文档。|
    |**数据质量**|DataWorks数据质量依托DataWorks平台，为您提供全链路的数据质量方案，包括数据探查、数据对比、数据质量监控、SQLScan和智能报警等功能。详情请参见[数据质量](../cn.zh-CN/使用指南/数据质量/数据质量概述.md#)模块的文档。|

5.  单击**下一步**，配置新建工作空间的基本信息和高级设置。

    ![配置工作空间信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16175/15637667258940_zh-CN.png)

    |分类|配置|说明|
    |:-|:-|:-|
    |**基本信息**|**工作空间名称**|工作空间名称的长度需要在3到27个字符，以字母开头，且只能包含字母下划线和数字。|
    |**显示名**|显示名不能超过27个字符，只能字母、中文开头，仅包含中文、字母、下划线和数字。|
    |**模式**|工作空间模式是DataWorks新版推出的新功能，分为简单模式和标准模式，双项目开发模式的区别请参见[简单模式和标准模式的区别](../cn.zh-CN/产品简介/简单模式和标准模式的区别.md#)。     -   简单模式：指一个Dataworks工作空间对应一个MaxCompute项目，无法设置开发和生产环境，只能进行简单的数据开发，无法对数据开发流程以及表权限进行强控制。
    -   标准模式：指一个Dataworks工作空间对应两个MaxCompute项目，可以设置开发和生产双环境，提升代码开发规范，并能够对表权限进行严格控制，禁止随意操作生产环境的表，保证生产表的数据安全。
 |
    |**描述**|对创建的工作空间进行简单描述。|
    |**高级设置**|**启用调度周期**|控制当前工作空间是否启用调度系统，如果关闭则无法周期性调度任务。|
    |**能下载select结果**|控制数据开发中查询的数据结果是否能够下载，如果关闭无法下载select的数据查询结果。|
    |**MaxCompute项目名称**|默认与DataWorks工作空间名称一致。|
    |**MaxCompute访问身份**|推荐使用工作空间所有者。|
    |**Quota组切换**|Quota用来实现计算资源和磁盘配额。|

6.  配置完成后，单击**创建工作空间**。

    工作空间创建成功后，即可在工作空间列表页面查看相应内容。


## 配置AnalyticDB数据源 {#section_w3h_hgz_cke .section}

1.  单击相应工作空间操作栏中的**进入数据集成**。
2.  选择**同步资源管理** \> **数据源**，单击**新增数据源**。

    ![新增数据源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1039843/156376672552397_zh-CN.png)

3.  在新建数据源弹出框中，选择数据源类型为**AnalyticDB（ADS）**。
4.  填写AnalyticDB数据源的各配置项。

    ![新增ADS数据源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16197/15637667257525_zh-CN.png)

    **说明：** 

    -   请配置外网IP。
    -   如果使用的是AnalyticDB2.0版本，通过用户AK信息进行身份验证。
    -   如果使用的是AnalyticDB3.0版本，通过数据库的用户名和密码进行身份验证（开通ADB3.0数据库后，首先在控制台创建用户和密码）。
5.  单击**测试连通性**。
6.  测试连通性通过后，单击**完成**。

    提供测试连通性能力，可以判断输入的信息是否正确 。


## 设置白名单 {#section_f50_oc2_77m .section}

-   设置DataWorks白名单

    您需要在DataWorks中，将AnalyticDB的连接URL和端口设置为白名单，调度引擎方可连接上AnalyticDB数据库。

    1.  单击右上角的**工作空间管理**按钮，进入工作空间配置页面。

        ![工作空间配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1039843/156376672652399_zh-CN.png)

    2.  在**沙箱白名单（配置shell任务可以访问的IP地址或域名）**下，单击**添加**。

        ![添加](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1039843/156376672652400_zh-CN.png)

    3.  在**添加沙箱白名单**对话框中，填写**地址**和**port**。

        ![添加沙箱白名单](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1039843/156376672652401_zh-CN.png)

    4.  单击**确定**。
-   设置AnalyticDB白名单

    由于AnalyticDB3.0版本基于用户名密码访问，因此需要设置客户端白名单，才允许连接数据库。

    1.  获取DataWorks白名单

        为了能让DataWorks gateway请求AnalyticDB3.0，需要将DataWorks的机器IP设置为AnalyticDB3.0的白名单（AnalyticDB2.0不需要设置）。DataWorks文档为您提供了各地域对应的白名单，您根据自身地域进行复制即可，详情请参见[添加白名单](../cn.zh-CN/使用指南/数据集成/常见配置/添加白名单.md#)。

    2.  设置AnalyticDB白名单
        1.  登录AnalyticDB3.0控制台，进入**集群列表** \> **数据安全**页面。

            ![数据安全](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1039843/156376672652404_zh-CN.png)

        2.  单击**添加白名单分组**，将复制的DataWorks白名单粘贴至AnalyticDB中。

            ![AnalyticDB白名单](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1039843/156376672652405_zh-CN.png)


## 新建业务流程 {#section_shf_mmy_a3h .section}

1.  单击左上角的图标，选择**全部产品** \> **DataStudio（数据开发）**。
2.  右键单击**业务流程**，选择**新建业务流程**。

    ![新建业务流程](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16421/15637667269122_zh-CN.png)

3.  在新建业务流程对话框中，填写**业务流程名称**和**描述**。
4.  单击**新建**。

## 创建数据同步任务 {#section_0o2_0ic_35m .section}

1.  右键单击新建业务流程下的**数据集成**，选择**新建数据集成节点** \> **数据同步**。

    ![数据同步](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1039843/156376672752408_zh-CN.png)

2.  在新建节点对话框中，填写**节点名称**，单击**提交**。

    ![新建节点](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1039843/156376672752409_zh-CN.png)

3.  选择数据来源和数据去向，单击**下一步**。

    ![选择数据来源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1039843/156376672752412_zh-CN.png)

4.  字段映射。

    选择字段的映射关系。左侧的源头表字段和右侧的目标表字段为一一对应关系。单击**添加一行**可以增加单个字段，鼠标放至需要删除的字段上，即可单击**删除**图标进行删除 。

    ![字段映射](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1039843/156376672752414_zh-CN.png)

5.  通道控制。

    单击**下一步**，配置作业速率上限和脏数据检查规则。

    ![通道控制](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16182/15637667278997_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**任务期望最大并发数**|数据同步任务内，可以从源并行读取或并行写入数据存储端的最大线程数。向导模式通过界面化配置并发数，指定任务所使用的并行度。|
    |**同步速率**|设置同步速率可以保护读取端数据库，以避免抽取速度过大，给源库造成太大的压力。同步速率建议限流，结合源库的配置，请合理配置抽取速率。|
    |**错误记录数**|错误记录数，表示脏数据的最大容忍条数。|
    |**任务资源组**|任务运行的机器，如果任务数比较多，使用默认资源组出现等待资源的情况，建议购买独享数据集成资源或添加自定义资源组，详情请参见[DataWorks独享资源](../cn.zh-CN/产品定价/预付费（包年包月）/DataWorks独享资源.md#)和[新增任务资源](../cn.zh-CN/使用指南/数据集成/常见配置/新增任务资源.md#)。|

6.  单击右侧的**调度配置**，为节点配置调度属性。

    ![调度配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1039843/156376672852416_zh-CN.png)

7.  配置完成后，单击**保存**并**提交**。

## 新建数据开发任务 {#section_ju7_qtf_vzu .section}

1.  右键单击新建业务流程下的**数据开发**，选择**新建数据开发节点** \> **AnalyticDB for MySQL**。

    ![新建节点](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/133906/156376672848438_zh-CN.png)

2.  在新建节点对话框中，填写**节点名称**，单击**提交**。

    ![新建节点](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/790663/156376672850833_zh-CN.png)

3.  选择相应的数据源后，根据AnalyticDB for MySQL支持的语法，编写SQL语句。通常支持DML语句，您也可以执行DDL语句。

    ![编辑SQL语句](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1039843/156376672852422_zh-CN.png)

4.  单击右侧的**调度配置**，为节点配置调度属性。

    ![调度配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1039843/156376672852424_zh-CN.png)

5.  配置完成后，单击**保存**按钮，将其保存至服务器。然后单击**运行**按钮，即可立即执行编辑的SQL语句。

## 数据运维 {#section_m2h_iq1_pia .section}

提交并发布新建的节点任务后，单击左上角的图标，选择**全部产品** \> **运维中心**，即可进行数据运维操作。详情请参见[运维中心](../cn.zh-CN/使用指南/运维中心/运维中心概述.md#)模块的文档。

![运维大屏](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1039843/156376672952425_zh-CN.png)

![周期任务](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1039843/156376672952426_zh-CN.png)

![规则报警](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1039843/156376672952428_zh-CN.png)

## 元数据管理 {#section_6zw_3g6_vbx .section}

您可以单击左上角的图标，选择**全部产品** \> **数据地图**，进行元数据管理操作。详情请参见[数据地图](../cn.zh-CN/使用指南/数据地图/数据地图概述.md#)模块的文档。

