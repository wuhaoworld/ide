# Data Lake Analytics node {#concept_978557 .concept}

You can create a Data Lake Analytics node in DataWorks to build an online ETL process.

1.  Go to the DataStudio page, and choose **Create** \> **Data Analytics** \> **Data Lake Analytics**.

    ![Data Lake Analytics](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/790667/156353387750757_en-US.png)

    **Note:** You can also select a workflow, right-click **Data Analytics**, and then choose **Create Data Analytics Node** \> **Data Lake Analytics**.

    ![Data Lake Analytics](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/790667/156353387750759_en-US.png)

2.  In the Create Node dialog box, enter the **Node name**, select the **Destination folder**, and then click **Commit**. The Location field is optional. You can specify this field to classify and manage nodes.

    ![Create Node](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/790663/156353387750744_en-US.png)

3.  Edit the Data Lake Analytics node.

    You can select a connection and edit SQL code on the node editing tab.

    1.  Select a connection.

        Select a target connection for the node. If you cannot find the required connection in the drop-down list, click **Add Connection** to open the **Add Connection** page. You can add the connection on the Data Integration page. For more information, see [Configure a connection](intl.en-US/User Guide/Data integration/Data source configuration/Supported data sources.md#).

        ![Select a connection](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/790663/156353387750753_en-US.png)

    2.  Edit SQL statements.

        After selecting a connection, you can write SQL statements based on the syntax supported by Data Lake Analytics. You can write DML and DDL statements in the code editor.

        ![Edit SQL](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/790667/156353387850760_en-US.png)

    3.  Save and run the SQL statements.

        After you finish editing the SQL statements, click the **Save** button to save the settings of the node to the server. Then, click the **Run** button to run the SQL statements you have saved.

4.  Set properties of the node.

    Click **Properties** on the right of the node editing tab to open the Properties tab. For more information, see [Properties](intl.en-US/User Guide/Data development/Scheduling configuration/Basic attributes.md#).

5.  Commit the node.

    After you set the properties, click **Save** in the tool bar to commit the node to the development environment. After you commit the node to the development environment, the node is unlocked.

6.  Deploy the node.

    For more information, see [Deploy a node](intl.en-US/User Guide/Data development/Publish management/Publish a task.md#).

7.  Test the node in the production environment.

    For more information, see [Cyclic task](intl.en-US/User Guide/O&M Center/Task list/Cyclic task.md#).


