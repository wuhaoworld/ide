# View the overall information {#concept_268246 .concept}

This topic describes how to view the overall information about a workspace on the Overview page.

Choose **Data Map** \> **Overview**. Data Map collects data of the previous day for the entire organization and generates data information on the **Overview** page offline.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16348/15622116548452_en-US.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16348/15622116548453_en-US.png)

|Item|Description|
|:---|:----------|
|**Projects, Tables, Table Storage, and CPU Usage**|The total number of projects, total number of data tables, storage occupied by data tables, and CPU usage per minute or second for task execution within the organization.|
|**Project Lineage**|A chart that shows the relationships between projects within the organization. An arc represents a project. Two projects are connected if they have the lineage relationship.|
|**Details**|The lineage relationship between projects within the organization. The first column indicates a project in which the ancestor table is located, the second column indicates a project in which the descendant table is located, and the third column indicates the number of lineage relationships between the two projects.|
|**Top Projects by Table Storage**|The top 10 projects that occupy the most storage space within the organization.|
|**Top Tables by Occupied Storage**|The top 10 data tables that occupy the most storage space within the organization. You can click a table name to go to the details page of the table. **Note:** The logical storage space occupied by projects and tables is collected in a **T+1** manner. The numbers next to the project and table names indicate the sizes of the occupied logical storage space. Besides the table storage volume, the project storage volume includes the storage volumes of resources, data in the recycle bin, and other system files. Therefore, the project storage volume is larger than the table storage volume. The table storage volume is charged based on the logical storage rather than the physical storage.

 |
|**Most Frequently Used Tables**|The top 10 data tables that are most frequently referenced within the organization. You can click a table name to go to the details page of the table.|

