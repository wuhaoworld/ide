# 在PyODPS任务中调用第三方包 {#concept_xrr_sfx_mfb .concept}

本文将为您介绍如何使用DataWorks PyODPS类型任务节点调用单文件第三方包。

1.  右键单击相应业务流程下的**资源**，选择**新建资源** \> **Python**。

    ![Python](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23998/156378311613917_zh-CN.png)

2.  在**新建资源**对话框中，填写**资源名称**，并勾选**上传为ODPS资源**。

    ![新建资源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23998/156378311613918_zh-CN.png)

3.  单击**确定**。
4.  在新建的Python资源内，粘贴需要引用的第三方包的代码，示例如下。

    ``` {#codeblock_zcd_2yr_p9d}
    # import os
    # print os.getcwd()
    # print os.path.abspath('.')
    # print os.path.abspath('..')
    # print os.path.abspath(os.curdir)
    
    def printname():
        print 'test2'
    print 123
    ```

    粘贴代码完成后，单击**提交**。

    ![提交](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23998/156378311613919_zh-CN.png)

5.  在您的业务流程内新建一个PyODPS类型节点。

    ![新建节点](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23998/156378311613921_zh-CN.png)

6.  在节点内输入引用第三方包的代码并测试，示例如下。

    ``` {#codeblock_6ir_dg2_nur}
    ##@resource_reference{"test2.py"}
    
    import sys 
    import os
    sys.path.append(os.path.dirname(os.path.abspath('test2.py'))) #将资源引入工作空间
    import test2 #引用资源
    test2.printname() #调用方法
    ```

    请注意下图中框内的代码，用于引用业务流程中您之前新建的test2.py资源，请不要遗漏。

    ![引用资源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23998/156378311613923_zh-CN.png)

7.  完成上述操作后，单击**运行**测试您的代码。您可以在下方的日志中查看运行结果。

    ![运行](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23998/156378311713924_zh-CN.png)


