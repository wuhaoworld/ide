# Add a prefix to target table names when migrating multiple tables to the cloud {#concept_ncw_ynf_qfb .concept}

This topic describes how to add a prefix to target table names when migrating multiple tables to the cloud.

1.  Add a data source. For more information, see [Bulk Sync](intl.en-US/User Guide/Data integration/Bulk sync/Bulk Sync.md#).
2.  Click **Create Batch Sync Task** and select the data source you created.
3.  Click **Add Rule**, select **Rules for Transforming Table Names**, and enter the regular expression for transforming table names. In this example, `(. +)` is used to match all table headers, and `(ods_$1)` indicates that the `ods_` prefix is added to the table headers.
4.  After the configuration is completed, click **Implementation Rules**. You can see that the table names have been transformed in the **Tables to Synchronize** area.
5.  Select a table to be synchronized and click **Submit Task**.

