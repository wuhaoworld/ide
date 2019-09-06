# DataWorks数据服务对接DataV最佳实践 {#concept_sv4_hjn_4gb .concept}

DataV通过与DataWorks数据服务的对接，可以使用DataWorks数据服务开发数据API，快速在DataV中调用API并展现MaxCompute的数据分析结果。

## 数据服务对接DataV产生背景 {#section_g5b_ljn_4gb .section}

MaxCompute是阿里巴巴集团自主研究的快速、完全托管的TB/PB/EB级数据仓库解决方案。当今社会数据收集的方式不断丰富，行业数据大量积累，导致数据规模已增长到传统软件行业无法承载的海量级别。MaxCompute服务于批量结构化数据的存储和计算，已经连续多年稳定支撑阿里巴巴全部的离线分析业务。

过去，如果您想要通过DataV展示海量数据的分析结果，需要自建一套离线数据计算自动导入MySQL的任务流程，这个过程非常繁琐，且成本很高。而现在通过DataWorks为您提供的**数据集成** \> **数据开发** \> **数据服务**的全链路数据研发平台，并结合MaxCompute可快速搭建企业数仓。

DataWorks数据服务提供了快速将数据表生成API的能力，通过可视化的向导模式操作，无需代码便可快速生成API，然后通过DataV调用API并在大屏中展示数据分析结果，高效实现数仓的开发和数据的展示。

## 前提条件 {#section_hf5_w4n_4gb .section}

要想实现DataWorks数据服务与DataV的对接，您需提前准备好数据源，并开通[DataV服务](../../../../../cn.zh-CN/产品简介/什么是DataV数据可视化.md#)。

## 新建数据源 {#section_vt3_gsn_4gb .section}

数据服务支持丰富的数据源类型，如下所示。

-   关系型数据库：RDS/DRDS/MySQL/PostgreSQL/Oracle/SQL Server
-   分析型数据库：AnalyticDB（ADS）
-   NoSQL数据库：TableStore（OTS）/MongoDB
-   大数据存储：Lightning（MaxCompute）

1.  登录DataWorks控制台，单击对应工作空间后的**进入数据服务**。
2.  鼠标悬停至**新建**图标，选择**新建数据源**。

    ![新建数据源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/120377/156774732038177_zh-CN.png)

3.  单击左上角的DataWorks图标，选择**全部产品** \> **数据集成**，进入**数据集成**页面。
4.  选择**同步资源管理** \> **数据源**，单击**新增数据源**。

    ![新增数据源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16213/15677473207595_zh-CN.png)

    本文将以Lightning数据源为例，通过Lighning数据源可以直接实时查询MaxCompute中的数据。

    **说明：** Lightning目前是内测阶段，需要单独申请才能开通，您也可以加入数据服务用户群（钉钉群号21993540）咨询Lightning服务的开通事项。

5.  在新增数据源弹出框中，选择数据源类型为**Lightning**。
6.  填写Lightning数据源的各配置项。

    ![填写配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/120377/156774732138185_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**数据源名称**|数据源名称必须以字母、数字、下划线组合，且不能以数字和下划线开头。|
    |**数据源描述**|对数据源进行简单描述，不得超过80个字符。|
    |**适用环境**|可以选择**开发**或**生产**环境。 **说明：** 仅标准模式工作空间会显示此配置。

 |
    |**Lightning Endpoint**|Lightning的连接信息，详情请参见[访问域名Endpoint](../../../../../cn.zh-CN/开发/交互式分析 (Lightning)/访问域名Endpoint.md#)。|
    |**Port**|默认值为443。|
    |**MaxCompute项目名称**|填写MaxCompute的项目名称。|
    |**AccessKey ID/AccessKey Secret**|访问密钥（AccessKey ID和AccessKey Secret），相当于登录密码。|
    |**JDBC扩展参数**|JDBC扩展参数中的`sslmode=require&prepareThreshold=0`默认且不可删除，否则会无法连接。详情请参见[配置JDBC连接](../../../../../cn.zh-CN/开发/交互式分析 (Lightning)/通过JDBC连接MaxCompute服务/配置JDBC连接.md#)。|

7.  单击**测试连通性**。
8.  测试连通性通过后，单击**完成**。

## 新建API {#section_jz5_ywn_4gb .section}

数据源创建完成后，进入数据服务页面。本文以向导模式生成API为例，为您介绍如何新建API。

1.  单击左上角的DataWorks图标，选择**全部产品** \> **数据服务**，进入**数据服务**页面。
2.  鼠标悬停至**新建**图标，选择**生成API** \> **向导模式**。

    ![向导模式](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16407/156774732154268_zh-CN.png)

3.  填写**生成API**对话框中的配置。

    ![生成API](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16407/15677473218791_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**API名称**|支持中文、英文、数字、下划线，且只能以英文或中文开头，4~50个字符。|
    |**API分组**|API分组是指针对某一个功能或场景的API集合，也是API网关对API的最小管理单元。在阿里云API市场中，一个API分组对应于一个API商品。 您可以将鼠标悬停至**新建**图标，单击**新建分组**进行新建。

 |
    |**API Path**|API存放的路径，如/user。|
    |**协议**|目前支持HTTP和HTTPS协议。|
    |**请求方式**|目前支持GET和POST请求方式。|
    |**返回类型**|目前仅支持JSON返回类型。|
    |**描述**|对API进行简要描述。|

4.  完成API基础信息的填写后，单击**确认**，即可进入API参数配置页面。

## 配置API参数 {#section_rdq_1wp_jp7 .section}

1.  选择**数据源类型**、**数据源名称**和**数据表名称**。

    ![选择表](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16407/156774732158631_zh-CN.png)

    **说明：** 

    -   您需提前在数据集成中配置好数据源，数据表下拉框支持表名搜索。
    -   创建好API后，会自动跳转至数据表配置页面，您可以直接进行配置。
2.  设置**内存**和**超时时间**。

    ![环境配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16408/156774732158590_zh-CN.png)

3.  选择好数据表后，下方的**选择参数**模块会自动列出该表的所有字段。勾选需要**设为请求参数**和**设为返回参数**的字段，分别添加至请求参数和返回参数列表中。

    ![选择参数](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16407/156774732158632_zh-CN.png)

4.  编辑请求参数信息。

    单击右侧的**请求参数**，设置**参数名称**、**参数类型**、**操作符**、**是否必填**、**示例值**、**默认值**和**描述**。

    ![请求参数](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16407/15677473218794_zh-CN.png)

5.  编辑返回参数信息。

    单击右侧的**返回参数**，设置**参数名称**、**参数类型**、**示例值**和**描述**，并可以进行**返回结果分页**和**使用过滤器**等高级配置。

    ![返回参数](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16407/156774732143272_zh-CN.png)

    配置过程中需要注意返回结果分页的设置：

    -   如果不开启**返回结果分页**，则API默认最多返回500条记录。
    -   如果返回结果可能超过500条，请开启**返回结果分页**功能。

## 测试API {#section_2fe_sl9_ot2 .section}

完成API参数的配置并保存后，单击右上角的**测试**，即可进入API测试环节。

![测试](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16407/15677473218797_zh-CN.png)

填写参数值，单击**开始测试**，即可在线发送API请求，在右侧可以看到API请求详情及返回内容。如果测试失败，请仔细查看错误提示并做相应的修改重新测试。

您可以在测试页面看到API延迟，会发现通过Lightning查询MaxCompute表仅花费了1秒多，比直接通过MaxCompute SQL查询更高效。

## 发布API {#section_plf_pf3_pgb .section}

1.  完成API测试后，返回**服务开发**页面。
2.  单击**发布**，即可成功生成一个数据API。
3.  发布完成后，您可以单击顶部导航栏中的**服务管理**查看API详情。

如果您要调用API，可进入**服务管理****API调用**页面，数据服务为您提供简单身份认证（AppCode）和加密签名身份认证（AppKey&AppSecret）两种认证方式，您可以自由选择。下文将为您介绍如何在DataV中进行数据服务API的调用。

## 添加数据服务为数据源 {#section_ink_zg3_pgb .section}

1.  登录DataV控制台。
2.  进入我的数据页面，单击**添加数据**。
3.  填写添加数据对话框中的配置。

    ![添加数据](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/120377/156774732138233_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**类型**|添加的数据源类型。|
    |**自定义数据源名称**|数据源的显示名称，可以自由命名。|
    |**项目**|DataWorks项目（工作空间）。|
    |**AppKey/AppSecret**|拥有DataWorks数据服务中某一项目访问权限的账号的AppKeyID和AppSecret。 **说明：** 您可以登录DataWorks数据服务控制台，进入**服务管理** \> **API调用**页面进行查看。

![API调用](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/120377/156774732138235_zh-CN.png)

 |


## 在大屏中调用数据服务API {#section_jxk_tm3_pgb .section}

1.  进入DataV控制台中的我的可视化页面，单击**新建可视化**。
2.  选择一个模板，单击**创建**，本文以**智能工厂**模板为例。

    ![智能工厂](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/120377/156774732138239_zh-CN.png)

    **说明：** 模板中的组件自带了静态数据，下文将以把模板中间的基本折线图改为调用上文创建好的查询成交金额增长趋势的API为例，为您介绍如何在组件中使用数据服务API。

3.  选中基本折线图组件，切换到数据面板，在**数据源类型**中选择**DataWorks数据服务**。
4.  选择刚刚创建的数据源和API，并设置查询参数，本示例将**pageSize**设置为31，以查询一个月的数据。

    ![查询](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/120377/156774732238242_zh-CN.png)

5.  单击**查看数据响应结果**，即可查看API的查询结果。
6.  填写字段映射关系，在x中填写**date**，将日期作为横轴，在y中填写**amount**，将成交金额作为纵轴。

    ![字段映射](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/120377/156774732238246_zh-CN.png)

    **说明：** 由上图可见，当前x和y无法匹配到字段。这是因为DataV对数据格式有一定要求，不能识别结构较深的字段，因此需要添加一个数据过滤器，过滤掉不必要的字段，在本例中直接返回rows数组即可。

7.  勾选**使用过滤器**，单击**新建**图标。此处支持编写JS代码对数据结果进行二次过滤和处理，过滤器的data参数为API返回结果JSON对象。

    **说明：** 本示例只需返回API结果中的rows数组，因此您只需输入`return data.data.rows;`，便可在下方预览过滤后的结果，并单击**完成**。

    ![使用过滤器](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/120377/156774732238247_zh-CN.png)

    添加过滤器后，字段便会匹配成功。

    ![匹配成功](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/120377/156774732238248_zh-CN.png)

    **说明：** 但此时的折线图并没有正确展示，由于API返回的日期格式与组件默认的格式不一样，因此还需要设置一下折线横轴的日期格式。

8.  切换至配置面板，在**x轴** \> **轴标签**中选择数据种类为**时间型**，数据格式选择本API所返回的格式2016/01/01，即可看见折线图的正常展示。

    ![展示](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/120377/156774732338249_zh-CN.png)


至此，便完成了通过数据服务将MaxCompute表生成API，然后在DataV数据大屏中进行展示的所有操作，效果如下图所示。

![效果](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/120377/156774732338250_zh-CN.png)

## 注意事项 {#section_l2c_qvj_pgb .section}

DataWorks数据服务与DataV进行无缝对接后，则不需要使用DataV中的API数据源去填写一个URL调用API，直接新建一个DataWorks数据服务作为数据源，便可直接选用数据服务中的API，无需每个API都设置AppKey和AppSecret认证信息，且支持通过表单填写API参数，操作快捷方便并安全可靠。

通过数据服务，您可以将MaxCompute中加工好的数据结果，直接在DataV中进行呈现，实现数据开发-数据服务-数据分析展现的全链路开发。在开发过程中，请注意以下事项。

-   DataWorks数据服务向导模式生成API只支持单表简单条件查询，脚本模式支持用户编写查询SQL语句，支持多表关联查询、函数以及复杂条件。您可以根据自己的需求灵活选择。
-   [Lightning](../../../../../cn.zh-CN/开发/交互式分析 (Lightning)/概述.md#)采用的是PostgreSQL语法，在编写SQL时，需要注意使用PostgreSQL函数，而不是MaxCompute的UDF。目前Lightning仅支持MaxCompute的UDF max\_pt，可用于获取当前最新分区。连接字符串时使用||。
-   Lightning目前只支持秒级查询，并且查询的MaxCompute不宜过大（控制在GB级），尽量将分区作为请求参数，尽量避免扫描过多分区，否则会比较慢。
-   如果您要求毫秒级API查询，则建议采用关系型数据库、NoSQL数据库或AnalyticDB作为数据源。
-   DataV组件要求的数据格式是个数组，数据服务生成的API返回结果是带有错误码的完整JSON，因此要使用过滤器对API结果进行处理。您可以选择在DataV中添加过滤器，也可以选择直接在数据服务配置API时添加过滤器。

    通常对于未分页查询的API，直接返回data数组即可，对于分页查询的API直接返回data.rows数组。

-   若您要在DataV的折线图或柱状图中添加多个系列，通常DataV要求每个系列的数据是一个对象，并通过字段s来区分系列，此时要注意使用过滤器进行格式转换。

