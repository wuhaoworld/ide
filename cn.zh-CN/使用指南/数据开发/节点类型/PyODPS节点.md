# PyODPS节点 {#concept_d5y_vhl_p2b .concept}

DataWorks提供PyODPS节点类型，集成了MaxCompute的Python SDK。您可以在DataWorks的PyODPS节点上，直接编辑Python代码，用于操作MaxCompute。

MaxCompute提供了[Python SDK](../../../../intl.zh-CN/SDK参考/Python SDK.md#)，您可以使用Python的SDK来操作MaxCompute。

**说明：** PyODPS节点底层的Python版本为2.7。

PyODPS节点主要针对MaxCompute的Python SDK应用。对于纯Python代码的执行，您可以使用Shell节点执行上传至DataWorks的py脚本。

PyODPS节点获取到本地处理的数据不能超过50MB，节点运行时占用的内存不能超过1G，否则节点任务会被系统Kill。请避免在PyODPS节点中写入过多的数据处理代码。

## 新建PyODPS节点 {#section_eyd_w3l_p2b .section}

1.  进入数据开发，选择**新建** \> **数据开发** \> **PyODPS**。

    ![PyODPS](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16292/15646434537651_zh-CN.png)

    **说明：** 您也可以找到相应的业务流程，右键单击**数据开发**，选择**新建数据开发节点** \> **PyODPS**。

    ![PyODPS](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16295/156464345351147_zh-CN.png)

2.  填写新建节点对话框中的配置，单击**提交**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16295/156464345351148_zh-CN.png)

3.  编辑PyODPS节点。
    1.  ODPS入口。

        DataWorks的PyODPS节点中，将会包含一个全局的变量odps或o，即ODPS入口，您不需要手动定义ODPS入口。

        ``` {#codeblock_e4u_il8_w2n}
        print(odps.exist_table('PyODPS_iris'))
        ```

    2.  执行SQL。

        PyODPS支持ODPS SQL的查询，并可以读取执行的结果。execute\_sql或run\_sql方法的返回值是运行实例。

        **说明：** 并非所有在MaxCompute客户端中可以执行的命令，都是PyODPS支持的SQL语句。调用非DDL/DML语句时，请使用其他方法。

        例如，执行GRANT/REVOKE等语句时，请使用run\_security\_query方法。PAI命令请使用run\_xflow或execute\_xflow方法。

        ``` {#codeblock_qh6_bph_1gx}
        o.execute_sql('select * from dual')  #  同步的方式执行，会阻塞直到SQL执行完成。
        instance = o.run_sql('select * from dual')  # 异步的方式执行。
        print(instance.get_logview_address())  # 获取logview地址。
        instance.wait_for_success()  # 阻塞直到完成。
        ```

    3.  设置运行参数。

        您可以通过设置hints参数，来设置运行时的参数，参数类型是dict。

        ``` {#codeblock_ykf_czl_ota}
        o.execute_sql('select * from PyODPS_iris', hints={'odps.sql.mapper.split.size': 16})
        ```

        对全局配置设置sql.settings后，每次运行时，都需要添加相关的运行时的参数。

        ``` {#codeblock_2os_24m_xw2}
        from odps import options
        options.sql.settings = {'odps.sql.mapper.split.size': 16}
        o.execute_sql('select * from PyODPS_iris')  # 根据全局配置添加hints。
        ```

    4.  读取SQL执行结果。

        运行SQL的instance能够直接执行open\_reader的操作，有以下两种情况：

        -   SQL返回了结构化的数据。

            ``` {#codeblock_ylu_k8m_uog}
            with o.execute_sql('select * from dual').open_reader() as reader:
            for record in reader:  # 处理每一个record。
            ```

        -   可能执行的是desc等SQL语句，通过reader.raw属性，获取到原始的SQL执行结果。

            ``` {#codeblock_8gk_qn5_p75}
            with o.execute_sql('desc dual').open_reader() as reader:
            print(reader.raw)
            ```

            **说明：** 如果使用了自定义调度参数，页面上直接触发运行PyODPS节点时，需要写死时间，PyODPS节点无法直接替换。

4.  PyODPS节点参数与调度配置。
    1.  单击右侧导航栏中的**调度配置**，即可弹出调度配置对话框。

        PyODPS节点使用调度参数时，如果使用系统定义的调度参数，可以直接在页面赋值获取。

        **说明：** 由于默认资源组无法直接访问外网环境，建议您有公网访问需求时，使用自定义资源组或独享调度资源。仅专业版DataWorks提供自定义资源组，任意版本均可购买独享调度资源，详情请参见[DataWorks独享资源](../../../../intl.zh-CN/产品定价/预付费（包年包月）/DataWorks独享资源.md#)。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16295/156464345334264_zh-CN.png)

    2.  赋值完成后，提交节点并进入运维中心页面，进行**测试运行**，即可查看赋值结果。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16295/156464345434265_zh-CN.png)

    3.  您可以在**调度配置** \> **基础属性**中，配置自定义参数。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16295/156464345434268_zh-CN.png)

        **说明：** 自定义参数需要使用args\['参数名'\]的形式调用，例如`print (args['ds'])`。

    4.  完成配置后，提交节点并进入运维中心页面，进行**测试运行**，即可查看赋值结果。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16295/156464345434289_zh-CN.png)

5.  提交节点任务。

    完成调度配置后，单击左上角的**保存**，**提交（提交并解锁）**至开发环境。

6.  发布节点任务。

    具体操作请参见[发布管理](intl.zh-CN/使用指南/数据开发/发布管理/任务发布.md#)。

7.  在生产环境测试。

    具体操作请参见[周期任务](intl.zh-CN/使用指南/运维中心/周期任务运维/周期任务.md#)。


## PyODPS节点预装模块列表 {#section_e7s_rm3_cyl .section}

PyODPS节点包括以下预装模块：

-   setuptools
-   cython
-   psutil
-   pytz
-   dateutil
-   requests
-   pyDes
-   numpy
-   pandas
-   scipy
-   scikit\_learn
-   greenlet
-   six
-   其他Python 2.7内置已安装的模块，如smtplib等。

