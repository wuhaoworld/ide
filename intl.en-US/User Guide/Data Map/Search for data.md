# Search for data {#concept_265995 .concept}

This topic describes how to search for data on the homepage of Data Map.

In the past, you can only search for tables in DataWorks. However, you may need to search for other objects besides tables. **Data Map** allows you to search for workspaces, functions, APIs, SQL script templates, node types, and TT topics. It provides full support for data development. The following figure shows the search objects that Data Map supports.

## Search for tables and MaxCompute fields {#section_dvu_h0l_1h6 .section}

If a keyword matches multiple results or you search for objects in categories, a filter list appears on the left. You can set the filter conditions in the list to further filter the search results.

-   **Left-side filter pane** 
    -   **Table Type**: Select All Tables or Highlighted Tables as required.
    -   **Environment**: Select Production or Development.
    -   **Filter conditions** 
        -   **Business Unit**: You can select multiple BUs. If you select a BU, a check mark \(√\) appears in the lower-right corner of the selected BU. You can click **More** to view all the BUs.
        -   **Table Type**: Select Upload Table, Temporary Table, or Result Table.
        -   **Category**: If you do not select any category, all the related categories appear. You can filter the categories as required.
    -   **Owner**: You can select multiple owners. If you select an owner, a check mark \(√\) appears in the lower-right corner of the selected owner. You can click **More** to view all the owners.
    -   **Project**: You can select multiple projects. If you select a project, a check mark \(√\) appears in the lower-right corner of the selected project. You can click **More** to view all the projects.
    -   **TTL \(Days\)**: You can select multiple periods. If you select a period, a check mark \(√\) appears in the lower-right corner of the selected period. You can click **More** to view all the periods.

        **Note:** You can specify **TTL \(Days\)** only for MaxCompute fields.

-   **Right-side display pane** 

    You can click all the items in blue to go to the corresponding page. In the **Actions** column, you can click **Add to Favorites**, **Request Permission**, **View Lineage**, or **View DDL Statement**.

    -   **Add to Favorites**: After you click **Add to Favorites** for a table, **Remove from Favorites** appears.
    -   **Request Permission**: After you click Request Permission, the permission application page appears.
    -   **View Lineage**: After you click View Lineage, the lineage details page appears.
    -   **View DDL Statement**: After you click View DDL Statement, a dialog box appears, displaying the related table creation statements. You can copy the DDL statements.

## Search for TT topics {#section_611_kth_vd7 .section}

In the left-side filter pane, you can specify the data sources, including the log source and database source. In the right-side display pane, you can click a topic name to go to the corresponding page. You can also subscribe to a topic.

## Search for workspaces {#section_cg4_gi6_7ee .section}

In the left-side filter pane, you can specify the owner. In the right-side display pane, you can click a workspace name to go to the corresponding page. You can also apply for joining a workspace. In addition, you can click **Functions**, **API**, Node Types, or Script Templates to go to the corresponding data market.

