# ODPS SQL节点 {#concept_cc4_1x3_p2b .concept}

ODPS SQL采用类似SQL的语法，适用于海量数据（TB级）但实时性要求不高的分布式处理场景。

因为每个作业从前期准备到提交等阶段都需要花费较长时间，因此如果要求处理几千至数万笔事务的业务，可以使用ODPS SQL顺利完成。它是主要面向吞吐量的OLAP应用。

## 新建ODPS SQL节点 {#section_zfn_smw_vej .section}

1.  进入DataStudio（数据开发）页面，选择**新建** \> **数据开发** \> **ODPS SQL**。

    ![ODPS SQL](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16293/156654883051559_zh-CN.png)

    **说明：** 您也可以找到相应的业务流程，右键单击**数据开发**，选择**新建数据开发节点** \> **ODPS SQL**。

    ![ODPS SQL](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16293/156654883051560_zh-CN.png)

2.  填写新建节点对话框中的配置，单击**提交**。

    ![提交](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16293/156654883051563_zh-CN.png)

3.  编辑节点代码。

    编写符合语法的ODPS SQL代码，SQL语法请参见[SQL概述](../../../../intl.zh-CN/开发/SQL及函数/SQL概述.md#)。

    ![编写代码](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16293/15665488307680_zh-CN.png)

    **说明：** 由于国际标准化组织发布的中国时区信息调整，通过DataWorks执行相关SQL时，日期显示某些时间段会存在时间差异：1900-1928年的日期时间差异5分52秒，1900年之前的日期时间差异9秒。

    目前DataWorks不允许节点代码中只包含[set语句](../../../../intl.zh-CN/开发/常用命令/SET操作.md#)。如果您需要运行set语句，可以和其他SQL语句一起执行，如下所示：

    ``` {#codeblock_fc2_yrd_kep .lanuage-shell}
    setproject odps.sql.allow.fullscan=true;
    select 1;
    ```

    示例：创建一张表并向表中插入数据，查询结果。

    1.  创建一张表test1。

        ``` {#codeblock_utt_hmi_rph .lanuage-shell}
        CREATE TABLE IF NOT EXISTS test1 
        ( id BIGINT COMMENT '' ,
          name STRING COMMENT '' ,
          age BIGINT COMMENT '' ,
          sex STRING COMMENT '');
        ```

    2.  插入准备好的数据。

        ``` {#codeblock_7f4_e4q_e6j .lanuage-shell}
        INSERT INTO test1 VALUES (1,'张三',43,'男') ;
        INSERT INTO test1 VALUES (1,'李四',32,'男') ;
        INSERT INTO test1 VALUES (1,'陈霞',27,'女') ;
        INSERT INTO test1 VALUES (1,'王五',24,'男') ;
        INSERT INTO test1 VALUES (1,'马静',35,'女') ;
        INSERT INTO test1 VALUES (1,'赵倩',22,'女') ;
        INSERT INTO test1 VALUES (1,'周庄',55,'男') ;
        ```

    3.  查询表数据。

        ``` {#codeblock_qhu_zck_t46 .lanuage-shell}
        select * from test1;
        ```

    4.  SQL语句编辑完成后，单击顶部的**运行**，系统会按照从上往下的顺序执行SQL语句，并打印日志。

        ![运行日志](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16293/156654883111262_zh-CN.jpg)

        **说明：** 在SQL中使用insert into语句有可能造成不可预料的数据重复。虽然已经对`insert into`语句取消SQL级别的重试，但仍然存在进行任务级别重试的可能性，请尽量避免使用`insert into`语句。

        如果继续使用`insert into`语句，表明您已经明确`insert into`语句存在的风险，且愿意承担由于使用`insert into`语句造成的潜在的数据重复后果。

    5.  执行无误后，单击左上角的**保存**，即可保存当前SQL代码。
4.  展示查询结果。

    DataWorks的查询结果接入了电子表格功能，方便您对数据结果进行操作。

    查询出的结果，会直接以电子表格的形式展示。您可以在DataWorks中执行操作，或者在电子表格中打开，也可以自由复制内容粘贴在本地Excel中。

    ![查询结果](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16335/15665488318260_zh-CN.png)

    |操作|说明|
    |--|--|
    |**隐藏列**|选中需要隐藏的一列或多列后，单击**隐藏列**。|
    |**复制该行**|左侧选中需要复制的一行或多行后，单击**复制该行**。|
    |**复制该列**|顶部选中需要复制的一列或多列后，单击**复制该列**。|
    |**复制选中**|选中需要复制的内容后，单击**复制选中**。|
    |**数据分析**|单击**数据分析**，即可跳转至**数据分析**页面。|
    |**搜索**|单击**搜索**后，在查询结果的右上角会出现搜索框，方便对表中的数据进行搜素。|
    |**下载**|支持下载GBK和UTF-8两种格式。|

5.  估计运行成本。

    您可以单击**成本估计**按钮，估算本次SQL任务可能产生的费用。

    ![成本估计](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16293/156654883132188_zh-CN.png)

    单击**成本估计**后，会显示估算出的任务执行费用。如果预估费用一栏报错，您可以将鼠标悬停在**X**按钮上查看报错原因。

    ![查看报错原因](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16293/156654883132189_zh-CN.png)

6.  节点调度配置。

    单击节点编辑区域右侧的**调度配置**，即可进入节点调度配置页面，详情请参见[调度配置](intl.zh-CN/使用指南/数据开发/调度配置/基础属性.md#)模块。

7.  提交节点任务。

    完成调度配置后，单击左上角的**保存**，提交（提交并解锁）到开发环境。

8.  发布节点任务。

    具体操作请参见[发布管理](intl.zh-CN/使用指南/数据开发/发布管理/任务发布.md#)。

9.  在生产环境测试。

    具体操作请参见[周期任务](intl.zh-CN/使用指南/运维中心/周期任务运维/周期任务.md#)。


## 注意事项 {#section_o5v_zan_pet .section}

-   ODPS SQL不支持单独使用set、use和alias语句，必须和具体的SQL语句一起执行。示例如下：

    ``` {#codeblock_6g8_in4_8hr}
    set a=b;
    create table name(id string);
    ```

-   ODPS SQL不支持关键字（set、use和alias）语句后单独加注释。示例如下：

    ``` {#codeblock_tp2_gxt_pjf}
    create table name(id string);
    set a=b; --注释 //不支持该注释
    create table name1(id string)；
    ```

-   数据开发与调度运行的区别

    -   数据开发：合并当前任务代码内所有的关键字（set、use和alias）语句，作为所有SQL的前置语句。
    -   调度运行：按照顺序执行。
    示例如下：

    ``` {#codeblock_wf5_68y_kwg}
    set a=b;
    create table name1(id string);
    set c=d;
    create table name2(id string);
    ```

    运行结果如下表所示。

    |执行SQL|数据开发|调度运行|
    |-----|----|----|
    |第1条SQL语句|     ``` {#codeblock_eg7_j6z_pee}
set a=b;
set c=d;
create table name1(id string);
    ```

 |     ``` {#codeblock_ngx_tmz_dyo}
set a=b;
create table name1(id string);
    ```

 |
    |第2条SQL语句|     ``` {#codeblock_l9q_i4s_yt4}
set a=b;
set c=d;
create table name2(id string);
    ```

 |     ``` {#codeblock_amh_owv_yd6}
set c=d;
create table name2(id string);
    ```

 |

-   调度参数配置必须是key=value的格式，且（=）前后不支持空格。示例如下：

    ``` {#codeblock_ppw_mds_bkq}
    time={yyyymmdd hh:mm:ss} //错误
    a =b //错误  
    ```

-   如果设置bizdate、date等关键字作为调度参数变量，格式必须是yyyymmdd。如果需要其它格式，请使用其它变量名称，避免冲突。示例如下：

    ``` {#codeblock_9sg_3ob_tn6}
    bizdate=201908 //错误，不支持
    ```

-   数据开发需要查询结果，仅支持select、read和with起始的SQL语句，否则无结果输出。
-   执行多条SQL语句时，请用（;）分隔，且需要换行。
    -   错误示例：

        ``` {#codeblock_0ky_ybp_9uc}
        create table1;create table2
        ```

    -   正确示例：

        ``` {#codeblock_5j4_6an_wd9}
        create table1;
        create table2;
        ```


