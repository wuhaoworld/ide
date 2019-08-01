# Shell节点 {#concept_m5l_3z4_p2b .concept}

Shell节点支持标准Shell语法，不支持交互性语法。

Shell节点任务可以在默认资源组上运行，如果想要访问IP/域名，需要将IP/域名添加到白名单中。

## 新建Shell节点 {#section_r4m_kz4_p2b .section}

1.  进入DataStudio（数据开发）页面，选择**新建** \> **数据开发** \> **Shell**。

    ![Shell](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16296/156464338154084_zh-CN.png)

    **说明：** 您也可以找到相应的业务流程，右键单击**数据开发**，选择**新建数据开发节点** \> **Shell**。

    ![Shell](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16296/156464338254085_zh-CN.png)

2.  填写新建节点对话框中的配置，单击**提交**。

    ![新建节点](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16296/156464338254086_zh-CN.png)

3.  编辑节点代码。

    进入Shell节点代码编辑页面编辑代码。

    ![编辑代码](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16296/15646433827753_zh-CN.png)

    如果需要在Shell中调用系统调度参数，Shell语句如下所示：

    ``` {#codeblock_6qk_ntg_e7s}
    echo "$1 $2 $3"
    ```

    **说明：** 参数1 参数2…多个参数之间用空格分隔。更多系统调度参数的使用，请参见[参数配置](intl.zh-CN/使用指南/数据开发/调度配置/参数配置.md#)。

4.  节点调度配置。

    单击节点编辑区域右侧的**调度配置**，即可进入节点调度配置页面，详情请参见[调度配置](intl.zh-CN/使用指南/数据开发/调度配置/基础属性.md#)模块。

5.  提交节点任务。

    完成调度配置后，单击左上角的**保存**，提交（提交并解锁）到开发环境。

6.  发布节点任务。

    具体操作请参见[发布管理](intl.zh-CN/使用指南/数据开发/发布管理/任务发布.md#)。

7.  在生产环境测试。

    具体操作请参见[周期任务](intl.zh-CN/使用指南/运维中心/周期任务运维/周期任务.md#)。


