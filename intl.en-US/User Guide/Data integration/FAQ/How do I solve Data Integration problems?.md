# How do I solve Data Integration problems? {#concept_bnt_kkb_r2b .concept}

To troubleshoot any Data Integration operation problems, you must identify relevant information, such as: theserver for running tasks, the data sources information, and the region in which the synchronization tasks are configured.

## View runningresources {#section_bhk_mhb_r2b .section}

-   Running on Alibabaserver:

    Running in Pipeline\[basecommon\_ group\_xxxxxxxxx\]

-   Running on the on-premise server:

    Running in Pipeline\[basecommon\_xxxxxxxxx\]


## Viewthe data sources information {#section_v3x_shb_r2b .section}

When Data Integration fails, youmust view the following data sources information:

-   Check the data sources in which the synchronization tasks are run.
-   Check the data sources environment.

    For example: The Alibaba Cloud database, data sources with or without public IP addresses or VPC network environment \(RDS and other sources\), and Financial Cloud \(VPC and classic nCtwork\).

-   Check if the data source connectivity test is successful.

    Compared tothe Data Source Configuration documents: Check if the entereddata source information is incorrect. Common mistakes include mixing multiple databases, adding spaces, or special characters when entering the information, orconnectivity test is not supported. \(The data source from database without public IP addresses or a VPC environment except RDS.\)


## Check the region in which synchronization tasks are configured {#section_dfl_snb_r2b .section}

You can view regions in the DataWorks console, such as East China 2, North China 1, China\(Hong Kong\)****, Southeast Asia Pacific 1, Central Europe 1, and Southeast Asia Pacific 2. Typically, the default region isEast China 2. You can view the region after purchasing MaxCompute.

## Copy the troubleshooting code when interface pattern errors are reported {#section_n3w_ynb_r2b .section}

When the interface pattern errors are reported, copy the troubleshooting code for the relevant personnel.

## Log report exceptions {#section_i2l_g4b_r2b .section}

**The log reports an error while running the SQL statement \(the column contains the keyword\)**

``` {#codeblock_z5z_wk3_pj9}
2017-05-31 14:15:20.282 [33881049-0-0-reader] ERROR ReaderRunner - Reader runner Received Exceptions:com.alibaba.datax.common.exception.DataXException: Code:[DBUtilErrorCode-07]
```

Error details:

Failed to read database data. Check your column, table, WHERE, querySQL configuration, or ask the DBA for help.

The executed SQL statement is as follows:

``` {#codeblock_de8_vcf_tic}
select **index**,plaid,plarm,fget,fot,havm,coer,ines,oumes from xxx
```

The error details are shown as follows:

``` {#codeblock_xwx_dkn_ce4}
You have an error in your SQL syntax; check the manual that corresponds to your MySQL Server version for the right syntax to use near Index, plaid, plarm, fget, fot, havm, coer, Ines, oums from XXX
```

Troubleshooting:

-   Then, run another SQL statement:

    ``` {#codeblock_xvb_0up_oiy}
    select **index**,plaid,plarm,fget,fot,havm,coer,ines,oumes from
              xxx
    ```

    If you view the results, there will also be corresponding errors.

-   If the field contains the keyword index, you can add single quotes or modify the field to solve the problem.

**The log reports an error occurred, while running the SQL statement. \(The table name is in single quotes within double quotes.\)** 

``` {#codeblock_gsb_xxd_e21}
 
com.alibaba.datax.common.exception.DataXException: Code:[DBUtilErrorCode-07]
```

Error details:

Failed to read database data. Check your column,table, WHERE, querySQL configuration or ask DBA for help.

The executed SQL statement is as follows:

``` {#codeblock_r18_n9a_z9y}
select /_+read_consistency(weak) query_timeout(100000000)_/ _ from** 'ql_ddddd_[0-31]’ **where 1=2
```

The error details are shown as follows:

``` {#codeblock_tcv_m0z_qox}
You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ‘‘ql_live_speaks[0-31]’ where 1=2’ at line 1 - com.mysql.jdbc.exceptions.jdbc4. Mysqlsyntaxerrorexception: You have an error in your SQL syntax; check the manual that corresponds to your MySQL Server version for the right syntax to use near **' 'ql _ ddddd _ [0-31] 'where 1 = 2 '**
```

Troubleshooting

If the table name is in single quotes within double quotes, you can delete the single quotes directly in the configuration constant "table":\["'ql*ddddd*\[0-31\]'"\].

**The data source connectivity test fails \(the exception message "Access denied for..." is reported\)**

An error occurred while connecting to the database. The database connection string: jdbc:mysql://xx.xx.xx.x:3306/t\_demo. User name: fn\_test. Exception message: Access denied for user 'fn\_test’@’%’ to database 't\_demo'. Make sure you have added a whitelist in RDS.

Troubleshooting:

-   When the exception message Access denied for... is reported, it generally indicates exceptions of the entered information. Check the information.
-   Check whether the whitelist or your account has permission to access the database. You can add the required whitelist and permissions in the RDS console.

**When the routing policy encounters problems, and the running pool are OXS and ECS clusters.** 

``` {#codeblock_jdn_0eg_4uu}
 
2017-08-08 15:58:55 : Start Job[xxxxxxx], traceId **running in Pipeline[basecommon_group_xxx_cdp_oxs]**ErrorMessage:Code:[DBUtilErrorCode-10]
```

Error details:

An error occurred while connecting to the database. Check your account, password, database name, IP address and port or ask DBA for help \(note the network environment\). An error occurred while connecting to the database because not connecting JDBC URL can be found from jdbc:oracle:thin:@xxx.xxxxx.x.xx:xxxx:prod. Check and modify your configurationsto make changes.

The error message "java.lang.Exception: DataX" indicates that the corresponding database cannot be connected for the following reasons:

-   The IP address, port, database, and JDBC you configured is incorrect and cannot be connected.
-   The user name or password you configured is incorrect, and the authentication is unsuccessful. Confirm whether the DBA database connection information is correct.

Troubleshooting:

Scenario 1:

-   To synchronize RDS-PostgreSQL data sources from Oracle, and you can click **Run**. The tasks cannot be performed by the scheduler because different pools are required.
-   You can add data sources in the form of JDBC to RDS then the RDS-PostgreSQL data sources can be synchronized from Oracle.

Scenario 2:

-   RDS-PostgreSQL data sources in the VPC environment cannot run on a Custom Resource Group. The RDS in the VPC environment provides reverse proxy capability, leading to network problems for the Custom Resource Group. Therefore, RDS in VPC environment can directly run on Alibaba Cloud server. If our server cannot meet your requirements, and you want to run tasks on the server. You must add data source in the form of JDBC to RDS in the VPC environment, and purchase the ECS in the same network segment.

-   - The "jdbc:mysql://100.100.70.1:4309/xxx,100" mapped out by the RDS in the VPC environment often starts with an IP address mapped out by the background. If it starts with adomain, the RDS is not in a VPC environment.

HBase Writer does not support the Date type

Hbase synchronization to hbase: 2017-08-15 11: 19: 29: State: 4 \(fail\) | Total: 0r 0b | speed: 0r/s 0b/S | error: 0r 0b | stage: 0.0% errormessage: Code: \[fig\]

Error details:

The parameter value you entered is invalid.

**Hbase writer does not support the type: Date**. The data types currently supported are: \[string, boolean, short, int, long, float, double\].

Troubleshooting:

-   HBase Writer does not support the Date type, and you cannot configure any data in the Date type of the Writer.

-   You can configure the data in string type because HBase has no limit in terms of data type. The bottom layer of the HBase is generally the byte array.


**JSON format configuration error**

Column configuration error

Based on DataX analysis, the most likely error cause is as follows:

`com.alibaba.datax.common.exception.DataXException: Code:[Framework-02]`

Error details:

The DataX engine encountered an error while running. For more information about the errors, see the error diagnostic information after DataX stops running

java.lang.ClassCastException: com.alibaba.fastjson. Jsonobject cannot be cast to java.lang.String

Troubleshooting:

When JSON is configured incorrectly.

``` {#codeblock_ou6_fm7_m6w}



Writer: 
"column":[ 
{ 
"name":"busino", 
"type"": "string" 
} 
] 
Write the statement as follows: 
"column":[ 
{ 
"Busino" 
} 
]
```

-   The JSON list is written less \[\]

    Common errors found using DataX smart analysis include:

    `com.alibaba.datax.common.exception.DataXException: Code:[Framework-02]`

    Error details:

    The DataX engine encountered an error while running. For more information about an error diagnostic information after DataX stops running.

    ``` {#codeblock_7go_wem_6nk}
    java.lang.String cannot be cast to java.util.List - java.lang.String cannot be cast to java.util.List  
    at com.alibaba.datax.common.exception.DataXException.asDataXException(DataXException.java:41)
    ```

    Troubleshooting:

    When the brackets\(\[\]\) is missing, the list type changes into other formats. You can resolve this by enteringthe brackets \(\[\]\) in the missing location.


**Permission issues**

-   Permission issues \(no "delete"permission\)

    For MaxCompute to RDS-MySQL synchronization, the error message is: Code:DBUtilErrorCode-07

    Error details:

    An error occurred while reading the database data. Check your column,table,WHERE, and querySQL configuration or ask DBA for help.

    The executed SQL statement is as follows:

    `delete from fact_xxx_d where sy_date=20170903`

    The error details are shown as follows:

    ``` {#codeblock_su4_nlv_amq}
    **DELETE command denied** to user ‘xxx_odps’@‘[xx.xxx.xxx.xxx](http://xx.xxx.xxx.xxx)’ for table ‘fact_xxx_d’ - com.mysql.jdbc.exceptions.jdbc4. MySQLSyntaxErrorException: DELETE command denied to user ‘xxx_odps’@‘[xx.xxx.xxx.xxx](http://xx.xxx.xxx.xxx)’ for table 'fact_xxx_d’
    ```

    Troubleshooting:

    The error message "DELETE command denied to" indicates that you have no permission to delete the table, and you must grant permissions required in the corresponding database.

-   Permission issues \(no "drop" permission\)

    Code:DBUtilErrorCode-07

    Error details:

    An error occurred while reading the database data. Check your column,table,WHERE, querySQL configuration or ask DBA for help.

    The executed SQL: truncate table be\_xx\_ch

    The error details are shown as follows:

    ``` {#codeblock_tx9_prh_k7q}
    **DROP command denied to user** ‘xxx’@‘[xxx.xx.xxx.xxx](http://xxx.xx.xxx.xxx)’ for table ‘be_xx_ch’ - com.mysql.jdbc.exceptions.jdbc4. MySQLSyntaxErrorException: DROP command denied to user ‘xxx’@‘[xxx.xx.xxx.xxx](http://xxx.xx.xxx.xxx)’ for table 'be_xx_ch’
    ```


Troubleshooting:

The preceding error is reported when the prepared statement "Truncate" is performed before the MySQLWriter configuration execution is performed to delete the table data because you have no "drop" permission.

**ADS permission issues**

``` {#codeblock_12h_y2s_w6q}
2016-11-04 19:49:11.504 [job-12485292] INFO OriginalConfPretreatmentUtil - Available jdbcUrl:jdbc:mysql://100.98.249.103:3306/ads_rdb? yearIsDateType=false&zeroDateTimeBehavior=convertToNull&tinyInt1isBit=false&rewriteBatchedStatements=true.  
2016-11-04 19:49:11. 505 [job-12485292] warn maid
```

There are column configuration risksin your configuration file. Because you have not configured columns to read database tables, when there are changes in the number and table field types, may affect task correctness or even run errors. Check your configurations and make changes.

`2016-11-04 19:49:11.528 [job-12485292] INFO Writer$Job`

You must complete the following authorizations for MaxCompute \> ADS data synchronization:

-   The ADS official account must have "describe" and "select" permissions for the tablessynchronization because the ADS system requires the table structure and data information to be synchronized from MaxCompute.

-   The account AccessKey you configured to access the ADS data source must have permission to initiate a request to load data to the specified ADS database. You can add authorization in the ADS system.


`2016-11-04 19:49:11.528 [job-12485292] INFO Writer$Job`

If the data synchronization is between RDSor other non-MaxCompute data sources and ADS, the implementation logic is to first load data to the MaxCompute temporary table, and then synchronize data from the MaxCompute temporary table to ADS \(set the temporary MaxCompute project as cdp\_ads\_project, and set the temporary project account to cloud- data-pipeline@aliyun-inner.com\).

Permissions:

-   The ADS official account must have at least "describe" and "select" permissions for the tables \(MaxCompute temporary table\) to be synchronized because the ADS system requires the table structure and data information to be synchronized from MaxCompute \(the authorization was completed at deployment\).

-   The account cloud-data-pipeline@aliyun-inner.com of the temporary MaxCompute must have permission to initiate a request to load data to the specified ADS database.You can add the authorization in the ADS.


Troubleshooting:

This problem is caused because of the lack of load data permission.

The temporary project account is cloud-data-pipeline@aliyun-inner.com. The ADS official account must have at least "describe" and "select" permissions for the tables \(MaxCompute temporary table\) forsynchronization because the ADS system requires the table structure and data informationto be synchronized from MaxCompute.The authorization has been completed at deployment. Log on to the ADS console and grant the "load data" permission to ADS.

**Whitelist issues**

-   The whitelist has not been added, and the data source connectivity test failed.

    The test connection failed and thedata source connectivity test failed:

    ``` {#codeblock_l6p_vyb_rsr}
    error message: Timed out after 5000 ms while waiting for a server that matches ReadPreferenceServerSelector{readPreference=primary}. Client view of cluster state is {type=UNKNOWN, servers=[{[address:3717=dds-bp1afbf47fc7e8e41.mongodb.rds.aliyuncs.com](http://address:3717=dds-bp1afbf47fc7e8e41.mongodb.rds.aliyuncs.com), type=UNKNOWN, state=CONNECTING, exception={com.mongodb.MongoSocketReadException: Prematurely reached end of stream}}, {[address:3717=dds-bp1afbf47fc7e8e42.mongodb.rds.aliyuncs.com](http://address:3717=dds-bp1afbf47fc7e8e42.mongodb.rds.aliyuncs.com), type=UNKNOWN, state=CONNECTING,** exception={com.mongodb.MongoSocketReadException: Prematurely reached end of stream**}}]
    ```

    Troubleshooting

    When adding the data source to MongoDB in a non-VPC environment, if the error message Timed Out after 5000 is reported, it means that the whitelist has a problem.

    **Note:** If you are using ApsaraDB for MongoDB, a root account is provided by default. To ensure security, Data Integration only supports using the relevant MongoDB account for connection. Avoid using the root account as the access account when adding and using the MongoDB data source.

-   Whitelist is incomplete

    for Code:\[DBUtilErrorCode-10\]

    Error details:

    An error occurred while connecting to the database. Check your account, password, database name, IP address and port or ask DBA for help \(note the network environment\).

    The error details are shown as follows:

    ``` {#codeblock_k89_ey3_lv5}
    java.sql.SQLException: Invalid authorization specification, message from server: "#**28000ip not in whitelist, client ip is xx.xx.xx.xx". **  
    2017-10-18 11:03:00. 673 [job-Newfoundland] Error retryutil-exception when calling callable
    ```

    Troubleshooting:

    The whitelist you added is incomplete. You have not added the server to the whitelist.


**The data source information is invalid**

-   When configuring the Script Mode, the corresponding data source information \(cannot be left blank\) and is missing.

    ``` {#codeblock_2w8_0at_edr}
    2017-09-06 12:47:05 INFO Success to fetch meta data for table with projectId 43501 project ID and instance ID mongodbdata source name. **  
     2017-09-06 12:47:05 [INFO] Data transport tunnel is CDP.  
    2017-09-06 12:47:05 [INFO] Begin to fetch alisa account info for 3DES encrypt with parameter account: [zz_683cdbcefba143b7b709067b362d4385].  
     
    2017-09-06 12:47:05 [INFO] Begin to fetch alisa account info for 3DES encrypt with parameter account: [zz_683cdbcefba143b7b709067b362d4385].  
    [Error] exception when running task, message: ** configuration property [adord] is generally the information to be filled in by ODPS data source could not be blank! **
    ```

    Troubleshooting:

    The error message shows that the corresponding AccessId information is blank. This is generally because ofScript Mode issues. Check the configured JSON code to see whether the corresponding data source name is missing.

-   Data source is not configured

    ``` {#codeblock_mtu_8wo_ux1}
    
     
    2017-10-10 10:30:08 INFO =================================================== 
     
    File “/home/admin/synccenter/src/Validate.py”, line 16, in notNone 
    raise Exception(“Configuration property [%s] could not be blank!” % (Context )) 
    ** Exception: configuration property [username] could not be blank! **
    ```

    Troubleshooting:

    -   Check with the normal logs:

        ``` {#codeblock_86u_awd_gqb}
        
        [56810] and instanceId(instanceName) [spfee_test_mysql]… 
        2017-10-09 21:09:44 [INFO] Success to fetch meta data for table with projectId [56810] and instanceId [spfee_test_mysql].
        ```

    -   Typically, this information shows that an error occurred while calling the data source. If the empty user name is reported, it shows that the data source has not been configured or the data source location has not been configured correctly. In this case, the user has configured an incorrect data source position.
-   DRDS data connection time-out

    When synchronizing data from MaxCompute to DRDS, the frequent common errors as follows:

    ``` {#codeblock_tgb_hht_jub}
    [2017-09-11 16:17:01. 729 [49892464-0-0-writer] warn maid $ task
    ```

    Roll back the data written this time and write a single data row each time and submit again. The reasons are as follows:

    ``` {#codeblock_q94_jtm_2xr}
    
    
     
    com.mysql.jdbc.exceptions.jdbc4.  CommunicationsException: **Communications link failure **   
    The last packet successfully received from the server was 529 milliseconds ago.   
    The last packet sent successfully to the server was** 528 milliseconds ago**.
    ```

    Troubleshooting:

    DataX client timeouts can be added while adding DRDS data sources `? useUnicode=true&characterEncoding=utf-8&socketTimeout=3600000` timeout Parameter.

    Example:

    ``` {#codeblock_kvt_gpv_bg4}
    jdbc:mysql://10.183.80.46:3307/ae_coupon? useUnicode=true&characterEncoding=utf-8&socketTimeout=3600000
    ```

-   System internal problems

    Troubleshooting:

    Typically, the system internal problems are reported when the data source in JSON format is mistakenly modified and saved in the development environment.When the page is blank, you can submit the project name and the node name to Alibaba Cloud development team for background processing.


**Dirty data**

-   Dirty data \(the string \[""\] cannot be converted to long\)

    ``` {#codeblock_n3v_0hl_zxm}
    2017-09-21 16:25:46.125 [51659198-0-26-writer] ERROR WriterRunner - Writer Runner Received Exceptions:  
    com.alibaba.datax.common.exception.DataXException: Code:[Common-01]
    ```

    Error details:

    The business dirty data generated during data synchronization that is caused by incorrect data type conversion. The string \[""\] cannot be converted to long.

    Troubleshooting:

    The String \[""\] cannot be converted to long: The statements for table creation in the two tables are the same. The preceding error is reported because the field type empty cannot be converted to long. You can directly configure it as a String.

-   Dirty data \(out of range value\)

    ``` {#codeblock_3p6_cij_wlc}
    2017-11-07 13:58:33.897 [503-0-0-writer] ERROR StdoutPluginCollector 
    Dirty data: 
    {"exception":"Data truncation:Out of range value for column 'id' at row 1","record":{"byteSize":2,"index":0,"rawData":-3,"type":"LONG"},{"byteSize":2,"index":1,"rawData":-2,"type":"LONG"},{"byteSize":2,"index":2,"rawData":"other","type":"STRING"},{"byteSize":2,"index":3,"rawData":"other","type":"STRING"},"type":"writer"}
    ```

    Troubleshooting:

    When the source data type of mysql2mysql is set as smallint\(5\), and the target data type is int\(11\) unsigned, dirty data is generated because the smallint\(5\) data contains negative numbers, and the data in the type of unsigned cannot be negative.

-   Dirty data \(store emoj\)

    The data table is configured to store emoj and dirty data is reported during data synchronization.

    Troubleshooting:

    By default, data integration is supported by utf 8. When you add a data source in JDBC format, you need to modify the settings, such jdbc:mysql://xxx.x.x.x:3306/database? characterEncoding=utf8&com.mysql.jdbc.faultInjection.serverCharsetIndex=45, so that you can set the emojis in the data source for synchronization.

-   Dirty data caused by empty fields

    ``` {#codeblock_qqr_ovo_89w}
     {“exception”:“Column ‘xxx_id’ cannot be null”,“record”:[{“byteSize”:0,“index”:0,“type”:“LONG”},{“byteSize”:8,“index”:1,“rawData”:-1,“type”:“LONG”},{“byteSize”:8,“index”:2,“rawData”:641,“type”:“LONG”}
    ```

    Based on DataX analysis, the most likely cause of error is as follows:

    com.alibaba.datax.common.exception.DataXException: Code:\[Framework-14\]

    Error details:

    The dirty data transmitted by DataX exceeds the user expectations. This error often occurs when a lot of dirty business data exists within the data source. Please check carefully the dirty data log information reported by DataX, or adjust the dirty data threshold accordingly.

    The check on the number of dirty data entries failed. The number of dirty data entries is limited to 1, but seven are captured.

    Troubleshooting:

    The dirty data is generated because the field "Column 'xxx\_id' cannot be null" must be specified, and empty data is used during data synchronization. You can modify those empty data or modify the field.

-   The field "data too long for column 'flash'" is too short and dirty data is generated.

    ``` {#codeblock_e2d_82g_hh6}
     2017-01-02 17:01:19.308 [16963484-0-0-writer] ERROR StdoutPluginCollector 
    Dirty data:  
    {"exception": "Data updatation: data Too long for column 'Flash 'at Row 1, "record ": [{"bytesize": 8, "Index": 0, "rawdata": 1, "type": "long"}, {"bytesize": 8, "Index ": 3, "rawdata": 2, "type": "long "}, {"bytesize": 8, "Index": 4, "rawdata": 1, "type": "long"}, {"bytesize": 8, "Index ": 5, "rawdata": 1, "type": "long "}, {"bytesize": 8, "Index": 6, "rawdata": 1, type: "Long "}
    ```

    Troubleshooting:

    When the field "data too long for column 'flash'" is too short, but the synchronized data is too long. Therefore, dirty data is generated. You can modify the data or the field.

-   Read-only permission to database settings

    ``` {#codeblock_neg_94t_qes}
    2017-11-07 13:58:33.897 503-0-0-writer ERROR StdoutPluginCollector 
    Dirty data:  
    {"exception": "the MySQL server is running with the -- read-only option so it cannot execute this statement", "record": [{"bytesize": 3, "Index": 0, rawdata: 201, type: Long}, {bytesize ": 8, "Index": 1, "rawdata": 1474603200000, "type ": "date"}, {"bytesize": 8, "Index": 2, rawdata: September 23, "12", "type": "string "}, {"bytesize": 5, "Index": 3, "rawdata ": "12", "type": "string"}
    ```

    Troubleshooting:

    When the read-only mode is set, you can change the "read-only" mode of the database to "writable" mode, if all data synchronized is dirty data.

-   Logs generated when partition error occurs

    An error message is reported when the parameter is configured as $yyyymm. The log is generated as follows:

    `[2016-09-13 17:00:43] 2016-09-13 16:21:35. 689 [job-10055875] Error Engine`

    Based on the analysis by DataX, the most likely cause of this error is as follows:

    `com.alibaba.datax.common.exception.DataXException: Code:[OdpsWriter-13]`

    Error details:

    You can try again if an exception occurs while running MaxCompute SQL. If the MaxCompute target table throws an exception when executing MaxCompute SQL, contact the MaxCompute administrator. The SQL content is as follows:

    ``` {#codeblock_nnm_w09_ekq}
    alter table db_rich_gift_record add IF NOT EXISTS
          partition(pt=’${thismonth}’);
    ```

    Troubleshooting:

    The single quotes added causes invalid scheduling parameter replacing. Solution: Remove the single quotes of '$\{thismonth\}'.

-   When the column is not configured in the array format.

    ``` {#codeblock_gmh_cni_xwj}
    Run Command failed.  
    com.alibaba.cdp.sdk.exception.CDPException: com.alibaba.fastjson.JSONException: syntax error, **expect {,** actual error, pos 0  
    at com.alibaba.cdp.sdk.exception.CDPException.asCDPException(CDPException.java:23)
    ```

    Troubleshooting:

    JSON has the following problem:

    ``` {#codeblock_o9n_axc_rxl}
    
    
    
    "plugin": “mysql”,** 
    "parameter":{ 
    "Datasource": "XXXXX", 
    ** “column”: “uid”,** 
     “where”: “”, 
    “splitPk”: “”, 
     “table”: “xxx” 
    } 
    “column”: “uid”,-----has not been configured as the array form
    ```

-   JDBC formatting error

    Troubleshooting:

    The JDBC format is invalid. The valid format is: jdbc:mysql://ServerIP:Port/Database.

-   Test connectivity failed

    Troubleshooting:

    -   Check whether the firewall limits the IP address and port used by your account.

    -   Check the port development of the security group.

-   uid\[xxxxxxxx\] is reported in the logs

    ``` {#codeblock_4e8_v4z_rhu}
    Run Command failed.  
    com.alibaba.cdp.sdk.exception.CDPException: RequestId[F9FD049B-xxxx-xxxx-xxx-xxxx] Error: there was an exception in the network information for the obtained instance, please check the RDS buyer ID and the RDS Instance name, UID [Newfoundland], instance [rm-bp1cwz5886rmzio92] serviceunavailable: the request has failed due to a maid failure of the server.  
    RequestIdF9FD049B-xxxx-xxxx-xxx-xxxx Error:
    ```

    Troubleshooting:

    Typically, when you synchronize data from RDS to MaxCompute.If the preceding error is reported, you can directly copy the RequestId:F9FD049B-xxxx-xxxx-xxx-xxxx to the RDS personnel.

-   The query parameter in MongoDB is incorrect

    When the following error is reported as synchronizing data from MongoDB to MySQL, if you find that it is caused by incorrect JSON, it means that the JSON query parameter is incorrectly configured.

    ``` {#codeblock_7un_fke_fst}
    Exception in thread “taskGroup-0” com.alibaba.datax.common.exception.DataXException: Code:[Framework-13]
    ```

    Error details:

    The DataX plug-in encountered an error while running. For more information about how to identify the specific causes,see the error diagnostic information after DataX stops running.

    ``` {#codeblock_dcc_zik_329}
    org.bson.json.JsonParseException: Invalid JSON input. Position: 34. Character :'.'.
    ```

    Troubleshooting:

    -   Negative example: "query":"\{‘update\_date’:\{’$gte’:new Date\(\).valueOf\(\)/1000\}\}". The parameter in the form of "new Date\(\) " is not supported.

    -   Correct example: "query":"\{‘operationTime’\{’$gte’:ISODate\(’$\{last\_day\}T00:00:00.424+0800’\)\}\}"

-   Cannot allocate memory

    ``` {#codeblock_h0m_jan_uln}
    
    
     
    2017-10-11 20:45:46.544 [taskGroup-0] INFO TaskGroupContainer - taskGroup[0] taskId[358] attemptCount[1] is started   
    Java HotSpot™ 64-Bit Server VM warning: INFO: os::commit_memory(0x00007f15ceaeb000, 12288, 0) failed; error=‘**Cannot allocate memory’** (errno=12)
    ```

    Troubleshooting:

    The memory is insufficient. If it occurs on your server, you must add extra memory.If it occurs on Alibaba's server, directly contact the technical support personnel.

-   max\_allowed\_packet parameter

    The error details are shown as follows:

    ``` {#codeblock_94p_hmx_dyb}
    Packet for query is too large (70>-1 ). You can change this value on the server by setting the max_allowed_packet’ variable. **com.mysql.jdbc.PacketTooBigException: Packet for query is too large (70 > -1). You can change this value on the server by setting the max_allowed_packet’ variable. **
    ```

    Troubleshooting:

    The max\_allowed\_packet parameter is used to define the maximum length of the communication buffer. MySQL may limit the receiveddata packet size by the server based on the configuration file. Occasionally, large size insertions and updates may fail because of the limitation of the max\_allowed\_packet parameter.

-   If the value Max\_allowed\_packet parameter is too large, you can change it into a smaller one. 10 MB = 10\_1024\_1024.
-   "HTTP Status 500" is reported and an error occurred while reading the logs.

    ``` {#codeblock_a2j_lov_s0h}
    Unexpected Error:  
    Response is com.alibaba.cdp.sdk.util.http.Response@382db087[proxy=HTTP/1.1 500 Internal Server Error [Server: Tengine, Date: Fri, 27 Oct 2017 16:43:34 GMT, Content-Type: text/html;charset=utf-8, Transfer-Encoding: chunked, Connection: close,  
    **HTTP Status 500** - Read timed out**type** Exception report**message**++Read timed out++**description**++The server encountered an internal error that prevented it from fulfilling this request.++**exception**  
    java.net.SocketTimeoutException: Read timed out
    ```

    Troubleshooting:

    When "HTTP Status 500" is reported while your tasks are running, if an error occurred during log reading of the tasks running on Alibaba's server, contact technical support personnel. If you are running tasks on your own server restart Alisa.

    **Note:** If the service status remains Stopped after refreshing, restart the following Alisa command to switch to the admin account: /home/admin/alisatatasknode/target/alisatatasknode/bin/serverct1 restart.

-   hbasewriter parameter: hbase.zookeeper.quorum configuration error

    ``` {#codeblock_355_18j_cxf}
    2017-11-08 09:29:28.173 [61401062-0-0-writer] INFO ZooKeeper - Initiating client connection, connectString=xxx-2:2181,xxx-4:2181,xxx-5:2181,xxxx-3:2181,xxx-6:2181 sessionTimeout=90000 watcher=hconnection-0x528825f50x0, quorum=node-2:2181,node-4:2181,node-5:2181,node-3:2181,node-6:2181, baseZNode=/hbase  
    Nov 08, 2017 9:29:28 AM org.apache.hadoop.hbase.zookeeper.RecoverableZooKeeper checkZk  
    WARNING: **Unable to create ZooKeeper Connection**
    ```

    Troubleshooting:

    -   Error example: "hbase. zoolokeeper. quorum: "xxx-2, xxx-4, xxx-5, xxxx-3, xxx-6"

    -   "Hbase.zookeeper.quorum":"your zookeeper IP address"

-   No relevant files are found

    Based on the analysis by DataX, the most common cause of errors as follows:

    com.alibaba.datax.common.exception.DataXException: Code:\[HdfsReader-08\]

    Error details:

    The file directory you are trying to read is empty. Failed to locate the read file, check your configuration items.

    ``` {#codeblock_gi0_x76_9gu}
    Path:/user/hive/warehouse/maid /*  
    at com.alibaba.datax.common.exception.DataXException.asDataXException(DataXException.java:41)
    ```

    Troubleshooting:

    Find the corresponding location using the path to check the file. If the file is not found, perform the necessary operations on the file.

-   The table does not exist

    Based on the DataX analysis, the most likely cause of error is as follows:

    com.alibaba.datax.common.exception.DataXException: Code:\[MYSQLErrCode-04\]

    Error details:

    The table does not exist. Check the table name or contact DBA to confirm whether the table exists.

    Table name: xxxx.

    The SQL executed is: `Select * from Newfoundland where 1 = 2;`

    The error details are shown as follows:

    ``` {#codeblock_nql_z95_uod}
    Table ‘darkseer-test.xxxx’ doesn’t exist - com.mysql.jdbc.exceptions.jdbc4. MySQLSyntaxErrorException: Table ‘darkseer-test.xxxx’ doesn’t exist
    ```

    Troubleshooting:

    Select \* from xxxx where 1=2 and check if the table xxxx has a problem. Take actions if any problem exists.


