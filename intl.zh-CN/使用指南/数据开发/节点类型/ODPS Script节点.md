# ODPS Script节点 {#concept_lxj_tcb_ygb .concept}

ODPS Script节点是MaxCompute基于2.0的SQL引擎提供的脚本模式。编译脚本时，将一个多语句的SQL脚本文件作为一个整体进行编译，不需逐条语句进行编译。将其作为一个整体提交运行，生成一个执行计划，保证一次排队、一次执行，充分利用MaxCompute的资源。

1.  进入DataStudio（数据开发）页面，选择**新建** \> **数据开发** \> **ODPS Script**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/133906/156092963648439_zh-CN.png)

    **说明：** 您也可以找到相应的业务流程，右键单击**数据开发**，选择**新建数据开发节点** \> **ODPS Script**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/133906/156092963748438_zh-CN.png)

2.  填写新建节点对话框中的配置，单击**提交**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/133906/156092963748435_zh-CN.png)

3.  编辑ODPS SCRIPT节点。

    您可在此节点中进行脚本模式的脚本编辑，详情请参见[编写SQL脚本](../../../../intl.zh-CN/工具及下载/MaxCompute Studio/开发SQL程序/编写SQL脚本.md#)。

4.  节点调度配置。

    单击节点任务编辑在区域右侧的**调度配置**，即可进入节点调度配置页面，详情请参见[调度配置](intl.zh-CN/使用指南/数据开发/调度配置/基本属性.md#)模块。

5.  提交节点任务。

    完成调度配置后，单击左上角的**保存**，提交（提交并解锁）到开发环境。

6.  发布节点任务。

    具体操作请参见[发布管理](intl.zh-CN/使用指南/数据开发/发布管理/任务发布.md#)。

7.  在生产环境测试。

    具体操作请参见[周期任务](intl.zh-CN/使用指南/运维中心/任务列表/周期任务.md#)。


## Script Mode语法结构 {#section_eyn_sa8_o53 .section}

Script Mode的SQL编译较为简单，只需按照业务逻辑，用类似于普通编程语言的方式进行编译，不需考虑如何组织语句。

``` {#codeblock_vqt_3oj_0pt}
--SET语句
set odps.sql.type.system.odps2=true;
[set odps.stage.reducer.num=***;]
[...]
--DDL语句
create table table1 xxx;
[create table table2 xxx;]
[...]
--DML语句
@var1 := SELECT [ALL | DISTINCT] select_expr, select_expr, ...
    FROM table3
    [WHERE where_condition];
@var2 := SELECT [ALL | DISTINCT] select_expr, select_expr, ...
    FROM table4
    [WHERE where_condition];
@var3 := SELECT [ALL | DISTINCT] var1.select_expr, var2.select_expr, ...
    FROM @var1 join @var2 on ...;
INSERT OVERWRITE|INTO TABLE [PARTITION (partcol1=val1, partcol2=val2 ...)]
    SELECT [ALL | DISTINCT] select_expr, select_expr, ...
    FROM @var3;
[@var4 := SELECT [ALL | DISTINCT] var1.select_expr, var.select_expr, ... FROM @var1
    UNION ALL | UNION
    SELECT [ALL | DISTINCT] var1.select_expr, var.select_expr, ... FROM @var2;
CREATE [EXTERNAL] TABLE [IF NOT EXISTS] table_name
    AS
    SELECT [ALL | DISTINCT] select_expr, select_expr, ...
    FROM var4;]
```

-   脚本模式支持SET语句、部分DDL语句（结果是屏显类型的语句除外，例如desc、show）和DML语句。
-   一个脚本的完整形式是SET语句\>DDL语句\>DML语句。每种类型语句都可以有0到多个语句，但不同类型的语句不能交错。
-   多个语句以@开始，表示变量连接。
-   一个脚本，目前最多支持一个屏幕显示结果的语句（例如单独的Select语句），否则会报错。不建议您在脚本中执行屏幕显示的Select语句。
-   一个脚本，目前最多支持一个`Create table as`语句，并且必须是最后一句。建议将建表语句和Insert语句分开写。
-   脚本模式下，如果有一个语句失败，整个脚本的语句都不会执行成功。
-   脚本模式下，只有所有输入的数据都准备完成，才会生成一个作业进行数据处理。
-   脚本模式下，如果一个表被写入后，又被读取，会报错。如下所示：

    ``` {#codeblock_r0r_qfk_wxg}
    insert overwrite table src2 select * from src where key > 0;
    @a := select * from src2;
    select * from @a;
    ```

    为避免先写后读，可以进行如下修改。

    ``` {#codeblock_wmj_418_ho3}
    @a := select * from src where key > 0;
    insert overwrite table src2 select * from @a;
    select * from @a;
    ```


示例如下：

``` {#codeblock_drc_7g4_n6w}
create table if not exists dest(key string , value bigint) partitioned by (d string);
create table if not exists dest2(key string,value bigint ) partitioned by (d string);
@a := select * from src where value >0;
@b := select * from src2 where key is not null;
@c := select * from src3 where value is not null;
@d := select a.key,b.value from @a left outer join @b on a.key=b.key and b.value>0;
@e := select a.key,c.value from @a inner join @c on a.key=c.key;
@f := select * from @d union select * from @e union select * from @a;
insert overwrite table dest partition (d='20171111') select * from @f;
@g := select e.key,c.value  from @e join @c on e.key=c.key;
insert overwrite table dest2 partition (d='20171111') SELECT * from @g;
```

## Script Mode适用场景 {#section_xhd_tls_y4i .section}

-   脚本模式更适合用来改写需要层层嵌套子查询的单个语句，或因为脚本复杂性而不得不拆成多个语句的脚本。
-   多个输入的数据源数据准备完成的时间相差很大（例如一个凌晨1点可以准备好，另一个上午7点可以准备好），不适合通过table variable衔接，可以拼接为一个大的脚本模式SQL。

