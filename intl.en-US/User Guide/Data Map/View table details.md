# View table details {#concept_268248 .concept}

This topic describes how to view the details about a table.

On the **Data Map** page, click a table in any list to go to the details page of the table, as shown in the following figure.

On the details page, you can view the basic information, business information, permission information, technical information, detailed information \(including the fields, partitions, and change history\), output information, lineage information, reference record, and description of the table. You can also preview the table.

## Apply for table permissions {#section_yow_vuc_pib .section}

For more information about how to apply for table permissions, see [Apply for data permissions](reseller.en-US/User Guide/Data Map/Apply for data permissions.md#).

## Add a table to favorites {#section_5h5_efv_jf6 .section}

To add a table to favorites, click **Add to Favorites** under the table name. After a table is added to favorites, you can choose **Data Map** \> **My Tables** \> **My Favorites** to view the table.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16350/15622118218458_en-US.png)

## Access DataService Studio {#section_g9u_jco_kq0 .section}

Click **Create API in DataService Studio** under the table name to go to **DataService**. For more information, see [DataService studio overview](reseller.en-US/User Guide/DataService studio/DataService studio overview.md#).

## Basic information {#section_u0f_zsp_l53 .section}

In the Basic Information section, you can view the number of reads, favorites, and views. You can also check the output task, MaxCompute project name, owner name, creation time, time to live \(TTL\), storage capacity, description, and tags of the table.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16350/15622118228460_en-US.png)

-   You can click the name of the **MaxCompute project** to go to the project details page.
-   You can click ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16350/156221182247422_en-US.png) next to **Tags** to add tags for the table.

## Business information {#section_2fy_4ry_wtr .section}

In the Business Information section, you can view the DataWorks workspace name, environment type, and category.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16350/15622118228461_en-US.png)

## Permission information {#section_4xb_nlr_sif .section}

In the Permissions section, you can view your permissions next to **My Permissions** and click **More** to go to [Search for data](reseller.en-US/User Guide/Data Map/Search for data.md#).

## Technical information {#section_sy3_h18_s4v .section}

In the Technical Information section, you can view the technical type, last DDL change time, last data change time, last data view time, and compute engine information.

-   The default time format is yyyy-mm-dd hh:ss:mm.
-   Click **View** next to **Compute Engine**. A dialog box appears, displaying information about the compute engine.

## Detailed information {#section_gf0_ayl_8n8 .section}

On the Content tab, you can view the metadata of the table, including the definition, popularity, and security level. You can also check the table structure changes and whether a field is a primary key or foreign key.

-   **Field information** 

    On the Fields tab, you can view the name, type, description, and popularity of fields. You can also check whether a field is a primary key or foreign key.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16350/15622118228462_en-US.png)

    -   Edit Field Security Level: You can click this button to go to the corresponding node. If you do not have the corresponding permission, you are prompted to apply for it.
    -   Download Field Information: You can click this button to download the field information.
    -   View DDL Statement: If you click this button, a dialog box appears, displaying the related table creation statements.
    -   Generate SELECT Statement: If you click this button, a dialog box appears, displaying the related SELECT statements.
-   **Partition information** 

    On the Partitions tab, you can view the name, number of records, storage volume, creation time, and last update time of each partition of the table.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16350/15622118228463_en-US.png)

-   **Change history** 

    On the Change History tab, you can view the change description, change type, granularity, time, and operator involved in each change. You can also select a change type from the drop-down list to filter change records.


## Output information {#section_svf_o1i_o0c .section}

If the table data changes periodically with the corresponding task, you can view the change status and data that is continuously updated.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16350/15622118238465_en-US.png)

## Lineage information {#section_dlp_oj6_rng .section}

On the Lineage tab, you can view data lineage and interaction between tables.

-   **Table lineage** 

    On the Table Lineage tab, you can search for the ancestor and descendant tables of a table based on the GUID, as shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16350/15622118238548_en-US.png)

-   **Field lineage** 

    On the Field Lineage tab, you can specify the field name to search for the ancestor and descendant tables of a table, as shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16350/15622118238549_en-US.png)


## References {#section_yee_rjp_izp .section}

-   **Foreign key references** 

    On the Foreign Key References tab, you can check the number of users who reference the table.

-   **References in clauses** 

    The References in Clause tab displays the table reference record by using a line chart, as shown in the following figure.


## Data preview {#section_twf_65f_7qb .section}

-   On the Data Preview tab, you can preview the data information of the current table.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16350/15622118238550_en-US.png)

-   To preview a table in the production environment, you must have the required permission. If you do not have the permission, you are prompted to apply for it.

## Usage notes {#section_2sf_uxt_eff .section}

On the Usage Notes tab, you can edit the description for the table and view the related history versions and Markdown syntax. You can also learn related information based on the data business description.

