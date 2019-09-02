# 配置Lightning数据源 {#concept_nvl_451_p2b .concept}

MaxCompute Lightning是MaxCompute产品的交互式查询服务，支持以PostgreSQL协议及语法连接访问Maxcompute项目，让您使用熟悉的工具以标准SQL查询分析MaxCompute项目中的数据，快速获取查询结果。

## 操作步骤 {#section_jy4_q4v_42b .section}

1.  以项目管理员身份登录[DataWorks控制台](https://workbench.data.aliyun.com/console)，单击相应工作空间后的**进入数据集成**。
2.  选择**同步资源管理** \> **数据源**，单击**新增数据源**。

    ![新增数据源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16213/15674232007595_zh-CN.png)

3.  在新增数据源弹出框中，选择数据源类型为**Lightning**。
4.  填写Lightning数据源的各配置项。

    ![Lightning数据源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1000681/156742320052196_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**数据源名称**|数据源名称必须以字母、数字、下划线组合，且不能以数字和下划线开头。|
    |**数据源描述**|对数据源进行简单描述，不得超过80个字符。|
    |**适用环境**|可以选择**开发**或**生产**环境。 **说明：** 仅标准模式工作空间会显示此配置。

 |
    |**Lightning Endpoint**|Lightning的连接信息，详情请参见[访问域名Endpoint](../../../../cn.zh-CN/开发/交互式分析 (Lightning)/访问域名Endpoint.md#)。|
    |**Port**|默认值为443。|
    |**MaxCompute项目名称**|填写MaxCompute的项目名称。|
    |**AccessKey ID/AccessKey Secret**|访问密钥（AccessKey ID和AccessKey Secret），相当于登录密码。|
    |**JDBC扩展参数**|JDBC扩展参数中的`sslmode=require&prepareThreshold=0`默认且不可删除，否则会无法连接。详情请参见[配置JDBC连接](../../../../cn.zh-CN/开发/交互式分析 (Lightning)/通过JDBC连接MaxCompute服务/配置JDBC连接.md#)。|

5.  单击**测试连通性**。
6.  测试连通性通过后，单击**完成**。

## 测试连通性说明 {#section_je4_f1j_5qu .section}

-   经典网络下，能够提供测试连通性能力，可以判断输入的信息是否正确。
-   专有网络目前不支持数据源连通性测试，直接单击**完成**。

