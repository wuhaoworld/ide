# 通过Function Studio开发UDF {#task_1830097 .task}

本文将为您介绍如何通过Function Studio开发UDF，并将其提交至DataStudio的开发环境。

## 新建工程 {#section_xj6_quf_6j7 .section}

如果您已经有Git代码，可以直接导入Git代码创建工程。此处仅支持[Code](https://code.aliyun.com/?spm=a2c4g.11186623.2.14.68936f8d20UN9z)中的代码导入。

1.  登录DataWorks控制台，进入DataStudio（数据开发）页面。
2.  单击左上角的图标，鼠标悬停至**全部产品**，选择**数据开发** \> **Function Studio**。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156645718548084_zh-CN.png)


3.  单击**工作空间**页面的**导入Git工程**。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1449101/156645718557038_zh-CN.png)


4.  填写新建项目对话框中的**Git地址**、**工程名**和**工程描述**，并**选择运行环境**。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1449101/156645718657040_zh-CN.png)

    新创建的工程默认未关联Git服务，会弹出**设置**对话框，请首先进行**SSH KEY**、**Git Config**和**偏好设置**的配置，单击**保存**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1449101/156645718657042_zh-CN.png)

    -   选择**SSH Key**中的**service**为`code.aliyun.com`，单击**生成sshKey**，即可生成**Public key**，单击**保存**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156645718648104_zh-CN.png)

    -   填写**Git Config**中的**User Name**和**Email**，单击**保存**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156645718648108_zh-CN.png)

    -   根据自身需求选择**偏好设置**中的**编辑器字号**，单击**保存**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156645718648110_zh-CN.png)

    **说明：** 如果工程创建完成后，需要修改相关信息，可以鼠标悬停至顶部菜单栏中的**设置**进行修改。

5.  单击**提交**。 工程创建完成后，Function Studio会自动拉取该工程。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156645718748201_zh-CN.png)


## 新建SSH密钥 {#section_xmz_m4c_uv3 .section}

设置好**SSH KEY**、**Git Config**和**偏好设置**后，可以新增SSH密钥。

1.  访问[Code](https://code.aliyun.com/profile)页面，单击左侧导航栏中的**设置**。
2.  进入设置页面，选择**SSH公钥** \> **增加SSH密钥**。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156645718748117_zh-CN.png)


3.  在增加SSH密钥对话框中填写前文生成的**Public key**，单击**增加密钥**。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156645718748119_zh-CN.png)



## 测试需要运行的类 {#section_c28_bbk_ngl .section}

1.  打开需要运行的类，单击右上角的运行按钮进行测试。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156645718748203_zh-CN.png)


2.  在Run/Debug Configurations对话框中，手动添加测试类的信息。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156645718848204_zh-CN.png)


3.  添加完成后，单击**Run**，即可看到输出的测试信息。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156645718848205_zh-CN.png)

    **说明：** 

    -   第一次启动时速度较慢，之后的启动速度会逐渐接近本地编辑器的体验。
    -   如果需要运行的类已经存在，直接在右上角进行选择，单击运行按钮即可。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156645718848206_zh-CN.png)


## 提交函数和资源至DataStudio开发环境 {#section_4ll_bwc_9lg .section}

确认代码无误后，可以提交函数和资源至DataStudio开发环境。

-   提交资源至DataStudio开发环境。
    1.  鼠标悬停至**提交**按钮，单击**提交资源至DataStudio开发环境**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156645718848207_zh-CN.png)

    2.  选择提交资源至DataStudio开发环境对话框中的**目标业务空间**和**目标业务流程**，并填写**资源**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156645718848208_zh-CN.png)

    3.  单击**确认**。
-   提交函数至DataStudio开发环境。
    1.  鼠标悬停至**提交**按钮，单击**提交函数至DataStudio开发环境**。
    2.  选择提交函数至DataStudio开发环境对话框中的**目标业务空间**、**目标业务流程**和**类名**，并填写**资源**和**函数名**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156645718948209_zh-CN.png)

    3.  单击**确认**。

当资源和函数都提交至DataStudio开发环境后，即可直接在SQL节点中使用。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/223331/156645718948210_zh-CN.png)

