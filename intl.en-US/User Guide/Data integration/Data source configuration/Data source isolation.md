# Data source isolation {#concept_e3s_bxq_kgb .concept}

Data source isolation can be used to isolate data of the development environment from data of the production environment for workspaces in standard mode.

If a data source is configured in both the development and production environments, you can use data source isolation to isolate the data source in the development environment from that in the production environment.

**Note:** Currently, only workspaces in standard mode support data source isolation.

When you configure a data synchronization task, the data source in the development environment is used. When you submit the data synchronization task to the production environment for running, the data source in the production environment is used. To submit a task to the production environment for scheduling, you must configure a data source in both the development and production environments. A data source must have the same name in the development and production environments.

Data source isolation has the following impacts on workspaces:

-   Workspaces in basic mode: The functions and configuration pages of data sources are the same as those before the data source isolation feature is added. For more information, see [Data source configuration](reseller.en-US/User Guide/Data integration/Data source configuration/Supported data sources.md#).
-   Workspaces in standard mode: The Applicable Environment parameter is added on the configuration pages of data sources.
-   Workspaces upgraded from the basic mode to the standard mode: During the upgrade, you will be prompted to upgrade data sources. After the upgrade, the data sources in the development environment are isolated from those in the production environment.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/100089/155650097041225_en-US.png)

|Page element|Description|
|:-----------|:----------|
|**Migrate Tables from Data Stores**|Click **Migrate Tables from Data Stores** to go to the Batch Sync page.**Note:** You can select a data source on the Batch Sync page only after the data source is configured in both the development and production environments and has passed the connectivity test.

|
|**Add Connections**|Currently, you can add only multiple MySQL, SQL Server, or Oracle data sources at a time. The template contains the data source type, data source name, data source description, environment type \(0 for development and 1 for production\), and URL. You can download the template, configure multiple data sources in the template, and upload the template to add the data sources at a time. On the page for adding multiple data sources at a time, details about the data sources will be displayed.|
|**Add Data Source**| -   If the environment is set to development for a data source, you can select the data source when creating a data synchronization node. The node task can be executed in the development environment. However, you cannot submit the node task to the production environment for running.
-   If the environment is set to production for a data source, you can use the data source only in the production environment. You cannot select the data source when creating a data synchronization node.

 **Note:** A data source must have the same name in the development and production environments.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/100089/155650097041235_en-US.png)

 |
|**Applicable Environment**|For a workspace in basic mode, this column is not displayed. For a workspace in standard mode, this column is displayed to show the environment of each data source.|
|**Actions**| -   **Migrate Tables Configuration**: This button is displayed for a data source in the development environment and can be clicked when the data source is configured in both the development and production environments.
-   **Add Data Source**: This button is displayed if a data source is not configured in an environment.
-   **Edit** and **Delete**: The two buttons are displayed for a data source that has been configured in an environment.
    -   Before deleting a data source from both the development and production environments, check whether the data source is used by any synchronization task in the production environment. The delete operation cannot be rolled back. After the data source is deleted, you cannot select it when configuring a synchronization task in the development environment.

If a synchronization task in the production environment uses the data source, the synchronization task cannot be executed after the data source is deleted. Delete the synchronization task before deleting the data source.

    -   Before deleting a data source from the development environment, check whether the data source is used by any synchronization task in the production environment. The delete operation cannot be rolled back. After the data source is deleted, you cannot select it when configuring a synchronization task in the development environment.

If a synchronization task in the production environment uses the data source, you cannot obtain metadata when editing the synchronization task after the data source is deleted. However, the synchronization task can be executed.

    -   Before deleting a data source from the production environment, check whether the data source is used by any synchronization task in the production environment. If you select the data source when configuring a synchronization task in the development environment, you cannot submit the task for publishing in the production environment after the data source is deleted.

If a synchronization task in the production environment uses the data source, the synchronization task cannot be executed after the data source is deleted.


 |
|**Select**|Select multiple data sources in this column to test the connectivity of the data sources or delete them at a time.|

