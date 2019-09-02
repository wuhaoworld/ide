# SQL Console {#concept_1893530 .concept}

在HoloStudio中，SQL Console是基于SQL命令语句的编辑器，支持您在HoloStudio中单纯的通过SQL命令语句即可进行交互式分析（Interactive Analytics）开发，为您提供秒级交互式查询体验。本小节将会为您介绍HoloStudio中SQL Console基本功能和用法。

## 文件夹 {#section_3oq_4rs_oae .section}

文件夹模块可以存放新建的临时查询，方便您管理临时查询。

单击左侧菜单栏**SQL Console** \> **新建** \> **文件夹**，即可创建一个属于自己的文件夹。您可以在该文件夹里新建临时查询，使用标准的SQL语句完成对表的命令操作。同时您也可以选中文件夹中的某张表，右键单击，即可移动、重命名、删除该表。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1501232/156739232358667_zh-CN.png)

## SQL Console {#section_hxz_urn_daw .section}

SQL Console模块可以生成SQL编辑器，方便您使用标准SQL语句操作。

1.  单击左侧菜单栏**SQL Console**，并填写查询的基本信息。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1501232/156739232358668_zh-CN.png)

    |属性|说明|
    |节点名称|临时查询的名称|
    |目标文件夹|临时查询存放的文件夹位置|
    |数据库|临时查询的目标数据库|

2.  填写临时查询SQL语句，并单击上方**运行**，执行查询，即可查看结果。示例新建一张表并导入数据，查询表的全过程。

    ``` {#codeblock_8yr_vzl_wnb}
    CREATE TABLE holo_test2 (
     id int ,
     name text
    );
    
    INSERT INTO  holo_test2 (id,name) VALUES 
        (1,'张三'),
        (2,'李四'),
        (3,'王五'),
        (4,'狗六');
    
    SELECT * from holo_test2;
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1501232/156739232358669_zh-CN.png)

    |属性|说明|
    |SQL编辑框|可填写SQL命令语句。|
    |保存|单击可保存SQL编辑器中的全部内容，方便下次查看。|
    |运行|单击可运行SQL编辑器内的全部内容，结果展现在底部。也可以只选中某条SQL语句，单击运行，系统默认只执行该条语句。|
    |重新加载|单击可刷新SQL编辑框内容，只保留已保存部分。|
    |停止|单击可停止正在运行的SQL语句。|
    |运行日志|可查看运行结果以及报错提示。|
    |结果|可查看运行成功后表的内容。|

    **说明：** ：对于无结果返回语句，如create table语句，只有运行日志，无查询结果。


