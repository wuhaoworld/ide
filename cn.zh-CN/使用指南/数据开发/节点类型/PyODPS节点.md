# PyODPS节点 {#concept_d5y_vhl_p2b .concept}

DataWorks也提供PyODPS任务类型，集成了Maxcompute的Python SDK。您可以在DataWorks的PyODPS节点上直接编辑Python代码，用于操作Maxcompute。

Maxcompute提供了[Python SDK](../../../../intl.zh-CN/SDK参考/Python SDK.md#)，您可以使用Python的SDK来操作Maxcompute。

**说明：** PyODPS节点底层的Python版本为2.7。

PyODPS节点获取到本地处理的数据**不能超过50MB**，节点运行时占用内存**不能超过1G**，否则节点任务会被系统Kill，请避免在PyODPS任务中写入过多的数据处理代码。

## 新建PyODPS节点 {#section_eyd_w3l_p2b .section}

1.  右键单击**数据开发**下的**业务流程**，选择**新建业务流程**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16292/15616274417651_zh-CN.png)

2.  右键单击**数据开发**，选择**新建数据开发节点** \> **PyODPS**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16295/15616274417741_zh-CN.png)

3.  编辑PyODPS节点。
    1.  ODPS入口

        DataWorks的PyODPS节点中，将会包含一个全局的变量odps或o，即ODPS入口，您不需要手动定义ODPS入口。

        ``` {#codeblock_e4u_il8_w2n}
        print(odps.exist_table('PyODPS_iris'))
        ```

    2.  执行SQL

        PyODPS支持ODPS SQL的查询，并可以读取执行的结果。execute\_sql或run\_sql方法的返回值是运行实例。

        **说明：** 并非所有在MaxCompute客户端中可以执行的命令都是PyODPS可以接受的SQL语句。在调用非DDL/DML语句时，请使用其他方法：例如，GRANT/REVOKE等语句，请使用run\_security\_query方法，PAI命令请使用run\_xflow或execute\_xflow方法。

        ``` {#codeblock_xxd_js5_6xo}
        o.execute_sql('select * from dual')  #  同步的方式执行，会阻塞直到SQL执行完成。
        instance = o.run_sql('select * from dual')  # 异步的方式执行。
        print(instance.get_logview_address())  # 获取logview地址。
        instance.wait_for_success()  # 阻塞直到完成。
        ```

    3.  设置运行参数

        您可通过设置hints参数来设置运行时的参数，参数类型是dict。

        ``` {#codeblock_ykf_czl_ota}
        o.execute_sql('select * from PyODPS_iris', hints={'odps.sql.mapper.split.size': 16})
        ```

        对全局配置设置sql.settings后，每次运行时都需要添加相关的运行时参数。

        ``` {#codeblock_2os_24m_xw2}
        from odps import options
        options.sql.settings = {'odps.sql.mapper.split.size': 16}
        o.execute_sql('select * from PyODPS_iris')  # 会根据全局配置添加hints
        ```

    4.  读取SQL执行结果

        运行SQL的instance能够直接执行open\_reader的操作，一种情况是SQL返回了结构化的数据。

        ``` {#codeblock_br3_aec_jc1}
        with o.execute_sql('select * from dual').open_reader() as reader:
        for record in reader:  # 处理每一个record
        ```

        另一种情况是SQL可能执行的desc等，通过reader.raw属性取到原始的SQL执行结果。

        ``` {#codeblock_0z1_sfw_ww3}
        with o.execute_sql('desc dual').open_reader() as reader:
        print(reader.raw)
        ```

        **说明：** 在数据开发使用了自定义调度参数，页面上直接触发运行PyODPS节点时，需要写死时间，PyODPS节点无法像SQL一样直接替换。


## PyODPS节点参数与调度配置 {#section_okd_4mt_cgb .section}

单击节点任务编辑在区域右侧的**调度配置**，即可进入节点调度配置页面。

PYODPS节点使用调度参数需时，**系统定义的调度参数**，可以直接通过在页面赋值获取。

**说明：** 由于默认资源组无法直接访问外网环境，建议当您有公网访问需求时使用自定义资源组。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16295/156162744134264_zh-CN.png)

在赋值完成后，提交节点并在运维中心进行**测试运行**，可查看赋值结果。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16295/156162744234265_zh-CN.png)

对于**自定义参数**，您可以在调度配置页面的**基础属性**一栏配置。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16295/156162744234268_zh-CN.png)

**说明：** 自定义参数需要使用args\['参数名'\]形式调用，例如`print (args['ds'])`。

完成配置后提交节点并在运维中心进行**测试运行**，可查看赋值结果。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16295/156162744234289_zh-CN.png)

## 后续操作 {#section_lkd_4mt_cgb .section}

1.  提交节点任务。

    完成调度配置后，单击左上角的**保存**，**提交（提交并解锁）**到开发环境。

2.  发布节点任务。

    具体操作请参见[发布管理](intl.zh-CN/使用指南/数据开发/发布管理/任务发布.md#)。

3.  在生产环境测试。

    具体操作请参见[周期任务](intl.zh-CN/使用指南/运维中心/任务列表/周期任务.md#)。


