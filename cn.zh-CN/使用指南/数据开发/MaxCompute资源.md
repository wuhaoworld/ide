# MaxCompute资源 {#concept_tfj_nsm_2gb .concept}

您可以通过MaxCompute资源面板，查看在MaxCompute计算引擎中存在的资源、资源的变更历史，并可以一键添加资源文件至数据开发面板的业务流程中。

## 查看资源 {#section_fjk_3bs_2gb .section}

1.  进入**数据开发**页面，单击左侧菜单栏中的**MaxCompute资源**，即可查看在MaxCompute计算引擎对应项目中存在的资源。

    ![MaxCompute资源面板](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81298/156750782334792_zh-CN.png)

    |序号|图标|说明|
    |--|--|--|
    |1|![切换](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81298/156750782334797_zh-CN.png)|单击后，可以在弹出的面板中切换不同环境下的资源。 **说明：** 简单模式的工作空间只有生产环境。

 |
    |2|![筛选](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81298/156750782334798_zh-CN.png)|单击后，可以筛选不同的资源类型。|
    |3|![排序](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81298/156750782334799_zh-CN.png)|单击后，可以切换条目排序，默认按更新时间倒序排列。|

    **说明：** 目前支持Jar、Archive、File和Python四种资源类型。

2.  单击相应的资源，即可查看**资源名称**、**资源类型**和**资源大小**等详细信息。

    ![查看资源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81298/156750782358758_zh-CN.png)


**说明：** 

-   **MaxCompute资源**面板中所列的资源，并非一定与**数据开发**面板中的资源一致。
    -   **数据开发**面板中的资源只有**同时上传到MaxCompute**，并**提交**/**发布**后，才会出现在**MaxCompute资源**面板的开发/生产环境中。
    -   通过**odpscmd**、**MaxCompute Studio**等非DataWorks渠道上传的资源文件，不会在**数据开发**面板显示，但会出现在**MaxCompute资源**面板中。
-   使用**MaxCompute资源**面板中所列的资源时，需注意与**数据开发**面板中资源的区别。

    |使用场景|数据开发|MaxCompute资源|
    |----|----|------------|
    |在ODPS SQL节点中使用|是（需同时上传至MaxCompute）|是|
    |在ODPS MR节点中使用|是（需同时上传至MaxCompute）|否|
    |在Shell节点中使用|是|否|
    |在临时查询中使用|是（需同时上传至MaxCompute）|是|
    |在业务流程中创建函数|是（需同时上传至MaxCompute）|否|


## 添加资源到数据开发面板 {#section_z3h_gbs_2gb .section}

添加资源到数据开发面板的流程，如下图所示。

![天津资源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81298/156750782334812_zh-CN.png)

1.  找到需要的资源后，单击**添加到数据开发**。

    您可以通过此操作，快速将**MaxCompute资源**面板中的资源文件同步至**数据开发**的业务流程中。

    ![数据开发](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81298/156750782334807_zh-CN.png)

2.  填写新建资源对话框中的配置。

    ![新建资源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81298/156750782334811_zh-CN.png)

    上传过程中，您可以进行如下操作：

    -   重命名资源名称。
    -   选择目标文件夹，即修改资源所处的业务流程。
    上传过程中，您不可以进行如下操作：

    -   更改资源类型。
    -   选择是否上传为ODPS资源。
    -   重新上传文件。
3.  配置完成后，单击**确定**，即可完成资源的创建。

**说明：** 

-   创建完成后，您需要手动完成保存、提交、发布等操作，与业务流程中对资源进行的操作一致。详情请参见[资源](cn.zh-CN/使用指南/数据开发/业务流程/资源.md#)。
-   资源提交、发布过程中，会同样上传至开发环境、生产环境的MaxCompute，同时更新在**MaxCompute资源**面板的资源文件中。
-   由于资源在MaxCompute项目中的唯一性，如果在同一项目中有同名资源，添加过程将会覆盖原有函数。如果原有函数处于不同业务流程，将会在新业务流程下完成覆盖。

## 查看资源的变更历史 {#section_dph_vgs_2gb .section}

1.  单击相应资源下的**查看变更历史**。

    ![查看变更历史](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81298/156750782334813_zh-CN.png)

2.  查看资源文件的创建、修改记录。

    ![查看历史](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81298/156750782334815_zh-CN.png)


