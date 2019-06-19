# My Permissions {#concept_j44_rvq_pgb .concept}

On the My Permissions page, you can view your table and field permissions in a workspace, and request or revoke table and field permissions.

## View table and field permissions {#section_frr_2wq_pgb .section}

1.  Log on to Data Guard. In the left-side navigation pane, click **My Permissions**. The **Table** tab appears.
2.  On this tab, you can select a workspace and specify the environment \(for a workspace in standard mode\) to view all the tables of the workspace in the specified environment. You can also enter a table name in the search box to search for required tables in fuzzy match mode.

    You can view the names and owners of tables in a workspace, view your permissions on the tables, and request or revoke table and field permissions.


## Request table and field permissions {#section_ymn_txq_pgb .section}

1.  Select the tables and fields on which you want to request permissions.
    -   Request permissions on a single table or some fields in the table

        Select the required fields on which you have no permissions in a table and choose **More** \> **Request Approval** in the Actions column.

        Alternatively, choose **More** \> **Request Approval** in the Actions column for a table without selecting any fields to request permissions on all the fields in the table.

        **Note:** You can request permissions on fields only in a workspace with LabelSecurity enabled. If LabelSecurity is disabled for a workspace, you can request permissions only on tables in this workspace.

    -   Request permissions on multiple tables and fields

        Select all the required tables and fields and click **Request Approval**.

        **Note:** You can also click **Request Approval** without selecting any tables or fields and then select the required tables and fields in the Table Permission Request dialog box.

2.  Set the parameters in the Table Permission Request dialog box.

    |Parameter|Description|
    |:--------|:----------|
    |**Workspace**|The workspace, which is automatically set based on the information you specified on the My Permissions page. You can change the workspace as required.|
    |**Environment**|The environment of the workspace.|
    |**MaxCompute Project**|The MaxCompute project name.|
    |**Grant To**|The account for which you request the permissions. You can request permissions for the current account or a production account of another workspace you joined.|
    |**Valid Until**|Validity period of the permissions. The options include **1 Month**, **3 Months**, **6 Months**, **12 Months**, **Permanent**, and **Others**.|
    |**Reason for Request**|The reason why you request the permissions.|
    |**Objects Requested**|The tables on which you request permissions. The tables that you select on the previous page are displayed. You can add tables or delete existing tables as required.|

3.  Click **Submit** to submit the request. If you do not want to request the permissions, click **Cancel**.

## Revoke permissions {#section_ekl_2dr_pgb .section}

You can revoke table and field permissions.

-   Revoke field permissions

    **Note:** 

    -   You can revoke permissions on fields only in a workspace with LabelSecurity enabled.
    -   To revoke permissions on all the fields in a table, revoke the permissions on the table directly.
    1.  Choose **More** \> **Revoke Field Permission** in the **Actions** column for the table on which you want to revoke permissions.
    2.  In the Revoke Field Permission dialog box, select the fields on which you want to revoke permissions.
    3.  Click **OK**.
-   Revoke table permissions
    1.  Choose **More** \> **Revoke Permission** in the **Actions** column for the table on which you want to revoke permissions.
    2.  In the Revoke Permission dialog box, select the permissions you want to revoke.
    3.  Click **OK**.

