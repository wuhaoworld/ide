# Data Lake Analytics节点 {#concept_978557 .concept}

您可以在Dataworks中新建Data Lake Analytics节点，构建在线ETL数据处理流程。

1.  进入DataStudio（数据开发）页面，选择**新建** \> **数据开发** \> **Data Lake Analytics**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/790667/156222344950757_zh-CN.png)

    **说明：** 您也可以找到相应的业务流程，右键单击**数据开发**，选择**新建数据开发节点** \> **Data Lake Analytics**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/790667/156222345050759_zh-CN.png)

2.  在新建节点对话框中，填写**节点名称**，选择**目标文件夹**（用于节点代码分类管理，可以不选），单击**目标文件夹**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/790663/156222345050744_zh-CN.png)

3.  编辑Data Lake Analytics节点。

    代码编辑页面分为选择数据源和编辑SQL代码两部分。

    1.  选择数据源。

        选择任务要执行的目标数据源。如果下拉选项中没有需要的数据源，单击右侧的**新建数据源**，前往**新建数据源**页面进行新建，详情请参见[数据源配置](cn.zh-CN/使用指南/数据集成/数据源配置/支持的数据源.md#)。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/790663/156222345050753_zh-CN.png)

    2.  编辑SQL语句。

        选择相应的数据源后，即可根据Data Lake Analytics支持的语法，编写SQL语句。通常支持DML语句，您也可以执行DDL语句。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/790667/156222345050760_zh-CN.png)

    3.  保存并执行SQL语句。

        代码编辑完成后，单击**保存**按钮，将其保存至服务器。然后单击**运行**按钮，即可立即执行编辑的SQL语句。

4.  节点调度配置。

    单击节点任务编辑在区域右侧的**调度配置**，即可进入节点调度配置页面，详情请参见[调度配置](cn.zh-CN/使用指南/数据开发/调度配置/基本属性.md#)模块。

5.  提交节点任务。

    完成调度配置后，单击左上角的**保存**，提交（提交并解锁）到开发环境。

6.  发布节点任务。

    具体操作请参见[发布管理](cn.zh-CN/使用指南/数据开发/发布管理/任务发布.md#)。

7.  在生产环境测试。

    具体操作请参见[周期任务](cn.zh-CN/使用指南/运维中心/任务列表/周期任务.md#)。


