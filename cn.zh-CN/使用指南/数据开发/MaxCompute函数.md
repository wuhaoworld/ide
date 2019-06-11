# MaxCompute函数 {#concept_d1n_hsm_2gb .concept}

MaxCompute函数面板可以用来查看在MaxCompute计算引擎中存在的函数（UDF）、回溯函数的变更历史，以及将函数一键添加到数据开发面板的业务流程中。

## 查看函数 {#section_gq1_w3s_2gb .section}

1.  您可通过**MaxCompute函数**面板，查看在MaxCompute计算引擎对应项目中存在的自定义函数（UDF）。

    -   单击![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81296/156023534049034_zh-CN.png)按钮，可在弹出的面板中切换工作空间下的项目（简单模式的工作空间只有生产环境项目）。
    -   单击![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81296/156023534049035_zh-CN.png)按钮，可以切换条目排序，默认按照创建时间倒序排列。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81296/156023534034822_zh-CN.png)

2.  选中某项函数，即可查看其详细信息。

## 删除函数 {#section_89z_shc_bd6 .section}

如果您需要删除函数，可切换至数据开发面板，右键单击相应业务流程下的函数名称，选择**删除**。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81296/156023534149043_zh-CN.png)

## 添加函数到数据开发面板 {#section_op4_vks_2gb .section}

添加函数到数据开发面板的流程，如下图所示。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81296/156023534134829_zh-CN.png)

**操作步骤**

1.  进入MaxCompute函数面板，单击**添加到数据开发**。可以快速将**MaxCompute函数**面板的函数同步到**数据开发**面板的业务流程中。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81296/156023534134827_zh-CN.png)

2.  在新建函数对话框中填写函数名称，并选择目标文件夹。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81296/156023534134828_zh-CN.png)

    在上传过程中，您可以重命名函数名称、选择目标目标文件夹（即修改函数所处的业务流程）。 但不可以修改函数定义。

3.  单击**提交**。

**说明：** 

-   创建完成后，您还需要手动完成保存、提交、发布等过程，与在业务流程中的[注册函数](cn.zh-CN/使用指南/数据开发/业务流程/注册函数.md#)相同。
-   函数提交、发布过程中，会同样上传到开发、生产环境的MaxCompute，也会同时更新您在**MaxCompute函数**面板中的自定义函数。
-   由于资源在MaxCompute项目中的唯一性，如果在同一项目中有同名资源，添加过程将会覆盖原有函数。若原有函数处于不同业务流程，将会在新业务流程下完成覆盖。

## 查看函数的变更历史 {#section_nb5_xks_2gb .section}

1.  单击**查看变更历史**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81296/156023534134831_zh-CN.png)

2.  查看函数的创建、修改记录。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81296/156023534234830_zh-CN.png)

    **说明：** 在MaxCompute中，函数无法被修改，因此对于函数的历史操作类型统一为创建。


