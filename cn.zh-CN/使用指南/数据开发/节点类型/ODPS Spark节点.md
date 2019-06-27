# ODPS Spark节点 {#concept_xpk_tvm_jhb .concept}

DataWorks提供ODPS Spark节点类型，本文将为您介绍如何新建和配置ODPS Spark节点。

## WordCount {#section_mfm_k1n_jhb .section}

1.  右键单击数据开发下的**业务流程**，选择**新建业务流程**。
2.  右键单击**资源**，选择**新建资源** \> **JAR**，上传编译的Jar包。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/156167/156161326744146_zh-CN.png)

    WordCount的示例代码请参见[WordCount示例](../../../../intl.zh-CN/开发/MapReduce/示例程序/WordCount示例.md#)。

3.  右键单击业务流程下的**数据开发**，选择**新建数据开发节点** \> **ODPS Spark**，新建ODPS Spark节点。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/156167/156161326745963_zh-CN.png)

4.  填写**ODPS Spark**对话框中的配置。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/156167/156161326744155_zh-CN.png)

5.  配置完成后，发布和执行该节点。

## Python读写表 {#section_kmw_bmn_jhb .section}

1.  准备好Python代码，并上传Python资源。
2.  新建并配置ODPS Spark节点。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/156167/156161326744161_zh-CN.png)

3.  配置完成后，发布和运行该节点。

## Lenet（BigDL） {#section_fx4_ymn_jhb .section}

1.  上传Jar包和数据（以archive资源类型上传mnist.zip）。
2.  新建并配置ODPS Spark节点。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/156167/156161326844165_zh-CN.png)

3.  配置完成后，发布和运行该节点。

