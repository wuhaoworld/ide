# 通过Function Studio开发UDF最佳实践 {#task_405448 .task}

本文将为您介绍如何通过Function Studio开发UDF，并将其提交至DataStudio开发环境。

使用Function Studio前，您需要填写当前用户的用户名、Email、对应Git服务商的SSH等基本信息。

**说明：** 目前仅华东2支持Function Studio功能。

1.  登录DataWorks控制台，进入DataStudio（数据开发）页面。
2.  单击左上角的![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440848083_zh-CN.png)图标，鼠标悬停至**全部产品**，选择**数据开发** \> **Function Studio**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440848084_zh-CN.png)

3.  第一次进入Function Studio，会出现欢迎页面。关闭后，单击左上角的**设置**，进行**SSH KEY**、**Git Config**和**偏好设置**的配置。
    -   选择**SSH KEY**中的**service**为`code.aliyun.com`，单击**生成sshKey**，即可生成**Public key**，单击**保存**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440848104_zh-CN.png)

    -   填写**Git Config**中的**User Name**和**Email**，单击**保存**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440848108_zh-CN.png)

    -   根据自身需求选择**偏好设置**中的**编辑器字号**，单击**保存**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440848110_zh-CN.png)

4.  设置完成后，访问[Code](https://code.aliyun.com/profile)页面，单击左侧导航栏中的**设置**。
5.  进入设置页面，选择**SSH公钥** \> **增加SSH密钥**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440848117_zh-CN.png)

6.  在增加SSH密匙对话框中填写前文生成的**Public key**，单击**增加密匙**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440848119_zh-CN.png)


1.  从Git仓库导入工程。 

    1.  进入**Function Studio**页面，鼠标悬停至**工程**，单击**从Git仓库导入工程**。 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440848122_zh-CN.png)

    2.  选择**UDFJava Project**，填写从Git仓库导入工程对话框中的配置。 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440848125_zh-CN.png)

        |配置|说明|
        |--|--|
        |**工程类型**|默认为**FunctionStudio/MaxCompute/UDFJava Project**，不可更改。|
        |**工程介绍**|默认为**MaxCompute UDF（Java）**，不可更改。|
        |**Git地址**|填写Git地址为git@code.aliyun.com:alicode-template/ip2region-udf-showcase.git。|
        |**工程名**|自定义工程名称。|
        |**工程描述**|对导入的工程进行描述。|

    3.  配置完成后，单击**确认**。
    导入完成后，Function Studio会自动拉取该工程。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440948201_zh-CN.png)

2.  测试需要运行的类。 
    1.  打开需要运行的类，单击右上角的![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440948202_zh-CN.png)按钮进行测试。 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440948203_zh-CN.png)

    2.  在Run/Debug Configurations对话框中，手动添加测试类的信息。 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440948204_zh-CN.png)

    3.  添加完成后，单击**Run**，便可看到输出的测试信息。 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440948205_zh-CN.png)

        **说明：** 

        -   第一次启动时速度较慢，之后的启动速度会逐渐接近本地编辑器的体验。
        -   如果需要运行的类已经存在，直接在右上角进行选择，单击![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440948202_zh-CN.png)按钮即可。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440948206_zh-CN.png)

3.  提交函数和资源至DataStudio开发环境。 

    确认代码无误后，可提交函数和资源至DataStudio开发环境。

    -   提交资源至DataStudio开发环境。
        1.  鼠标悬停至![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440948207_zh-CN.png)，单击**提交资源至DataStudio开发环境**。
        2.  选择提交资源至DataStudio开发环境对话框中的**目标业务空间**和**目标业务流程**，并填写**资源**。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440948208_zh-CN.png)

        3.  单击**确认**。
    -   提交函数至DataStudio开发环境。
        1.  鼠标悬停至![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440948207_zh-CN.png)，单击**提交函数至DataStudio开发环境**。
        2.  选择提交函数至DataStudio开发环境对话框中的**目标业务空间**、**目标业务流程**和**类名**，并填写**资源**和**函数名**。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440948209_zh-CN.png)

        3.  单击**确认**。
    当资源和函数都提交至DataStudio开发环境后 ，便可直接在SQL节点中使用。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156013440948210_zh-CN.png)


