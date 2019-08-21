# Add a relational database driver for RDBMS Reader {#concept_ndq_3bl_ngb .concept}

RDBMS Reader uses a JDBC connector to connect to a remote RDBMS database and runs a SELECT statement to extract data from the RDBMS database. Currently, RDBMS Reader supports reading data from databases including DM, DB2, PPAS, and Sybase. RDBMS Reader is a common plugin for reading data from relational databases. You can add or register the driver of a relational database type to enable RDBMS Reader to read data from this type of database.

## Background {#section_ugc_5bl_ngb .section}

[RDBMS Reader](intl.en-US/User Guide/Data integration/Task configuration/Configure reader plug-in/Configure RDBMS Reader.md#) uses a JDBC connector to connect to a remote RDBMS database, generates a SELECT statement based on your configuration, and sends the statement to the remote RDBMS database. Then, RDBMS Reader assembles the running result of the SQL statement into abstract datasets by using the custom data types of DataX, and passes the datasets to the downstream writer.

RDBMS Reader assembles the table, column, and where information that you configured into an SQL statement and sends the statement to the RDBMS database. RDBMS Reader sends the querySql information that you configured to the RDBMS database.

Currently, RDBMS Reader supports most common relational database types such as digits and characters. Check whether your database type is supported.

## Preparation {#section_yvs_xbl_ngb .section}

Before adding a relational database driver, you need to purchase an ECS instance as a [resource in the custom resource group](intl.en-US/User Guide/Data integration/Common configuration/Add task resources.md#). The recommended specifications are as follows:

-   CentOS V6, CentOS V7, or AliOS is recommended.
-   If the added ECS instance needs to run MaxCompute nodes or synchronization nodes, verify that the current Python version of the ECS instance is V2.6 or V2.7. \(The Python version of CentOS V5 is V2.4 while those of other operating systems are later than V2.6.\)
-   Make sure that the ECS instance can access the Internet. \(Ping www.alibabacloud.com on the ECS instance and check whether it can be pinged.\)
-   We recommend that you configure the ECS instance with an 8-core CPU and 16 GB memory.

## Add a custom resource group {#section_j21_vgq_ngb .section}

Add a custom resource group. For more information, see [Add task resources](intl.en-US/User Guide/Data integration/Common configuration/Add task resources.md#).

1.  After creating a workspace, click **Data Integration**.
2.  On the Data Integration page, choose **Resources** \> **Add Resource Group**.
3.  Follow the instructions to install and initialize the agent. When the ECS instance is in the **Available** status, the custom resource group is added.

    **Note:** If the ECS instance is still in the Stop status after you refresh the page, switch to the admin account and run the following command:

    ``` {#codeblock_4d3_57b_5jo}
    /home/admin/alisatasknode/target/alisatasknode/bin/serverct1 restart
    ```


## Add a MySQL driver {#section_gwf_mrq_ngb .section}

The following describes how to add a MySQL driver:

1.  Access the directory of RDBMS Reader. $\{DATAX\_HOME\} indicates the home directory of DataX, and RDBMS Reader is in the /home/admin/datax3/plugin/reader/rdbmsreader directory.

    ``` {#codeblock_4mw_xzl_tha}
    
    [root@izbp1czjkv9fpzmsbv0qcdz rdbmsreader]# pwd
    /home/admin/datax3/plugin/reader/rdbmsreader
    [root@izbp1czjkv9fpzmsbv0qcdz rdbmsreader]# ls
    libs plugin.json rdbmsreader-0.0.1-SNAPSHOT.jar
    ```

2.  Run the following command to register your database driver, for example, "com.mysql.jdbc.Driver", in the plugin.json configuration file in the directory of RDBMS Reader and put the driver in the drivers array. RDBMS Reader dynamically selects the appropriate database driver to connect to the database when nodes are run.

    ``` {#codeblock_du5_05q_fwp}
    [root@izbp1czjkv9fpzmsbv0qcdz rdbmsreader]# vim plugin.json
    {
        "name": "rdbmsreader",
        "class": "com.alibaba.datax.plugin.reader.rdbmsreader.RdbmsReader",
        "description": "useScene: prod. mechanism: Jdbc connection using the database, execute select sql, retrieve data from the ResultSet. warn: The more you know about the database, the less problems you encounter.",
        "developer": "alibaba",
        "drivers":["dm.jdbc.driver.DmDriver", "com.sybase.jdbc3.jdbc.SybDriver", "com.edb.Driver","com.mysql.jdbc.Driver"]
    }
    ```

3.  Upload the JAR package [mysql-connector-java-5.1.47.jar](https://dev.mysql.com/downloads/file/?id=480090) of the MySQL driver that you downloaded to the libs subdirectory of the directory of RDBMS Reader, as shown in the following figure.

## Configure an RDBMS data synchronization node {#section_fwt_nqr_ngb .section}

Currently, you can only use [RDBMS Reader](intl.en-US/User Guide/Data integration/Task configuration/Configure reader plug-in/Configure RDBMS Reader.md#) to configure synchronization nodes in script mode. The following is a configuration example:

``` {#codeblock_m2t_bjz_4i3 .language-json}
{
"job": {
        "setting": {
            "speed": {
                "byte": 1048576
            },
            "errorLimit": {
                "record": 0,
                "percentage": 0.02
            }
        },
        "content": [
            {
                "reader": {
                    "name": "rdbmsreader",
                    "parameter": {
                        "username": "xxxxx",
                        "password": "yyyyyy",
                        "column": [
                            "*",   
                        ],
                        "splitPk": "id",
                        "connection": [
                            {
                                "table": [
                                    "a2"
                                ],
                                "jdbcUrl": [
                                    "jdbc:mysql://xxx.mysql.yy.aliyuncs.com:3306/xxx"  //
Configure your SQL address.                                ]
                            }
                        ],

                        "where": ""
                    }
                },
                "writer": {  //Configure the writer
as needed.                    "name": "streamwriter",
                    "parameter": {
                        "print": true
                    }
                }
            }
        ]
    }
}
```

