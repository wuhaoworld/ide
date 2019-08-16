# Use Data Integration to ship log data collected by LogHub {#concept_uk4_vgb_pfb .concept}

This topic describes how to use Data Integration to ship data collected by LogHub to supported destinations, such as MaxCompute, Object Storage Service \(OSS\), Table Store, Relational Database Management Systems \(RDBMSs\), and DataHub. In this topic, we use MaxCompute as an example.

**Note:** This feature is available inthe following regions: China \(Beijng\), China \(Shanghai\), China \(Shenzhen\), China\(Hong Kong\), US \(Silicon Valley\), Singapore, Germany \(Frankfurt\), Australia \(Sydney\), Malaysia \(Kuala Lumpur\), Japan \(Tokyo\), and India \(Mumbai\).

## Scenarios {#section_ogh_b2g_4fb .section}

-   Synchronize cross-region databetween different data source types, such as LogHub and MaxCompute data sources.
-   Synchronize data using different Alibaba Cloud accounts between different data source types, such as LogHub and MaxCompute data sources.
-   Synchronize data using one Alibaba Cloud account between different data source types, such as LogHub and MaxCompute data sources.
-   Synchronize data with a public cloud account and an Alibaba Finance Cloud account between different data source types, such as LogHub and MaxCompute data sources.

## Note on cross-account data synchronization {#section_pvp_22g_4fb .section}

If you want to create a Data Integration task with Account B to synchronize LogHub data underAccount A to MaxCompute data source under Account B.

1.  Create a LogHub data source with the Access ID and the Access Key of Account A.

    Account B has permissions to access all Log Service projects created by Account A.

2.  Create a LogHub data source with the Access ID and the Access Key of RAM user A1.
    -   Use Alibaba Cloud account A to grant pre-defined Log Service permissions \(`AliyunLogFullAccess` and `AliyunLogReadOnlyAccess`\) to RAM user A1. For more information, see [Grant RAM user accounts permissions to access Log Service](https://www.alibabacloud.com/help/doc-detail/47664.htm).
    -   Use Alibaba Cloud account A to assign custom Log Service permissions to RAM user A1.

        Choose **RAM Console** \> **Policies** and choose **Custom Policy** \> **Create Authorization Policy** \> **Blank Template**.

        For more information about authorization, see [Access control RAM](https://www.alibabacloud.com/help/doc-detail/62663.htm) and [RAM user account access](https://www.alibabacloud.com/help/doc-detail/29049.htm).

        If the following policy is applied to RAM user A1, thenAccount B can only read project\_name1 and project\_name2 data in Log Service through RAM user A1.

        ``` {#codeblock_0ol_2u3_3uw}
        {
        "Version": "1",
        "Statement": [
        {
        "Action": [
        "log:Get*",
        "log:List*",
        "log:CreateConsumerGroup",
        "log:UpdateConsumerGroup",
        "log:DeleteConsumerGroup",
        "log:ListConsumerGroup",
        "log:ConsumerGroupUpdateCheckPoint",
        "log:ConsumerGroupHeartBeat",
        "log:GetConsumerGroupCheckPoint"
        ],
        "Resource": [
        "acs:log:*:*:project/project_name1",
        "acs:log:*:*:project/project_name1/*",
        "acs:log:*:*:project/project_name2",
        "acs:log:*:*:project/project_name2/*"
        ],
        "Effect": "Allow"
        }
        ]
        }
        ```


## Add a data source {#section_zyq_xgg_4fb .section}

1.  Log on to the [DataWorks console](https://partners-intl.aliyun.com) as a developer with Account B or a RAM user of Account B, and find the project, and then click **Data Integration**.
2.  Choose **Sync Resources** \> **Data Source**, and click **Add Data Source** in the upper-right corner.
3.  Select **LogHub** as the data source type, and then configure the data source in the Add Data Source LogHub dialog box.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/24566/156594782633924_en-US.png)

    |Configuration|Description|
    |:------------|:----------|
    |**Data source name**|The name can contain letters, numbers, and underscores \(\_\). It must start with a letter, and cannot exceed 60 characters in length.|
    |**Description**|The data source description cannot exceed 80 characters in length.|
    |**LogHub endpoint**|The endpoint of the LogHub data source in the format of http://example.com.|
    |**Project**| For more information, see [Service endpoints](https://www.alibabacloud.com/help/doc-detail/29008.htm).

 |
    |**Access ID and Access Key**|The logon credential, similar to the account name and the password. You may enter the Access ID and the Access Key of an Alibaba Cloud account or a RAM user account.|

4.  Click **Test Connectivity**.
5.  When the connection test is passed, click **OK**.

## Configure a synchronization task in GuideMode {#section_hph_skg_4fb .section}

1.  Choose **Business Flow** \> **Data Integration** and click **Create Integration Node** in the upper-left corner.
2.  Set up configurations in the Create Node dialog box and click **Submit**. Then, the configuration page of the data synchronization task appears.
3.  Select a source.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/24566/156594782614351_en-US.png)

    |Configuration|Description|
    |:------------|:----------|
    |**Data source**|Select LogHub and enter the LogHub data source name.|
    |**Logstore**|The table name from which incremental data is exported. You must enable the Stream feature on the table when creating the table or using the UpdateTable operation after creation.|
    |**Start time**|The start \(includes\) the selected time range for filtering log entries by log time. The format is yyyyMMddHHmmss, for example: 20180111013000. These parameters correspond to the scheduling time of DataWorks tasks.|
    |**End time**|The end \(excluded\) of the selected time range for filtering log entries by log time. The format is yyyyMMddHHmmss, for example: 20180111013000. These parameters correspond to the scheduling time of DataWorks tasks.|
    |**Number of records read per batch**|Number of data entries read each time. The default value is 256.|

    You can click the Data preview button to preview data.

    **Note:** Data Preview allows you to view a small number of LogHub data entries in a preview box, which may be different from the synchronized data. The data that you synchronize is determined by the Start Time and End Time.

4.  Select a destination.

    Select a MaxCompute destination and select a table. In this example, select the OK table.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/24566/156594782614352_en-US.png)

    |Configuration|Description|
    |:------------|:----------|
    |**Data source**|Select MaxCompute and enter a destination name.|
    |**Table**|Select the table for synchronization.|
    |**Partition information**|The table for synchronization is a non-partitioned table. Therefore, no partition information is displayed.|
    |**Clearance rule**|     -   **Clear Existing Data Before Writing \(Insert Overwrite\)**: All data in the table or partition is cleared before import.
    -   **Retain Existing Data \(Insert Into\)**: No data is cleared before import. New data is always appended with each run.
 |
    |**Compression**|The default value is Disable.|
    |**Consider empty string as null**|The default value is No.|

5.  Set field mappings.

    Map fields in source and destination tables. Fields in the source table \(left\) have a one-to-one correspondence with fields in the destination table. Select the**Enable Same Line Mapping**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/24566/156594782614353_en-US.png)

6.  Configure the channel control policies.

    Configure the maximum transmission rate and dirty data check rules.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/24566/156594782714354_en-US.png)

    |Configuration|Description|
    |:------------|:----------|
    |**DMU**|The Data Integration billing unit. **Note:** The DMU value limits the maximum number of concurrent jobs. Set the DMU value to a valid value.

 |
    |**Number of concurrent jobs**|When you configure Synchronization Concurrency, the data records are split into several tasks based on the specified reader shard key. These tasks run simultaneously to improve transmission rates.|
    |**Transmission rate**|Setting a transmission rate protects the source database from excessive read activity and heavy load. We recommend that you throttle the transmission rate and configure the transmission rate based on the source database configurations.|
    |**If there are more than**|The number of dirty data entries. For example, if varchar type data in the source is written into a destination column of the int type, a data conversion exception occurs, and the data cannot be written into the destination column. You can set an upper limit for the dirty data entries to control the synchronized data quality. Set an upper limit based on your business requirements.|
    |**Taskresource group**|The resource group used for running synchronization tasks. By default, the task runs with the default resource group. When the project has insufficient resources, you can add a custom resource group and run the synchronization task with the custom resource group. For more information about how to add custom resource groups, see [Add scheduling resources](reseller.en-US/User Guide/Data integration/Common configuration/Add task resources.md#). Choose aresource group based on your data source network conditions, project resources, and business importance.

 |

7.  Run the task.

    You can run the task using either of the following methods:

    -   Directly run the task \(one-time running\).

        Click **Run** in the tool bar to run the task. After setting certain parameters, you can run the task on the DataStudio page.

    -   Schedule the task.

        Click **Submit** to submit the synchronization task to the scheduling system. The scheduling system periodically runs the task starting from the next day,based on the task configurations.


## Configure a synchronization task in Script Mode {#section_hcl_h4g_4fb .section}

To configure this task in Script Mode, click **Switch to Script Mode** in the tool bar, and click **OK**.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/24566/156594782733929_en-US.png)

Script Mode allows you to set up configurations as needed. The following isan example script:

``` {#codeblock_yyp_9k0_dj0}
{
"type": "job",
"version": "1.0",
"Configuration ":{
"reader": {
"plugin": "loghub",
"parameter": {
"datasource": "loghub_lzz",//Data source name. Use the name of the data resource that you have added.
"logstore": "logstore-ut2",//Source Logstore name. A Logstore is a log data collection, storage, and query unit in LogHub.
"beginDateTime": "${startTime}",//Start (included) time for filtering log entries by log time.
"endDateTime": "${endTime}",//End (included) time for filtering log entries by log time.
"batchSize": 256,//The number of data entries that are read each time. The default value is 256.
"splitPk": "",
"column": [
"key1",
"key2",
"key3"
]
}
},
"writer": {
"plugin": "odps",
"parameter": {
"datasource": "odps_first",//Data source name. Use the name of the data resource that you have added.
"table": "ok",//Destination table name
"truncate": true,
"partition": "",//Partition information
"column": [//Destination column name
"key1",
"key2",
"key3"
]
}
},
"Setting ":{
"Speed ":{
"mbps": 8,//Maximum transmission rate
"concurrent": 7//Number of concurrent jobs
}
}
}
}
```

