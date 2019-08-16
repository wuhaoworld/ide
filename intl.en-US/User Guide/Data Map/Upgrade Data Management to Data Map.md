# Upgrade Data Management to Data Map {#concept_268401 .concept}

This topic describes the latest progress and plan of upgrading Data Management to Data Map.

## First release plan of the Data Map module of DataWorks {#section_l8k_esb_lxp .section}

-   Version: DataWorks Data Map
-   Date: May 21, 2019
-   Region: China \(Shanghai\), China \(Hangzhou\), China \(Shenzhen\), China\(Hong Kong\), and Singapore
-   Description: Developed based on Data Management, Data Map provides features by role and controls permissions such as the data preview permission and table creation permission. It helps you build an enterprise-level knowledge base.
-   Plan:
    -   May 21, 2019: first batch of users in China \(Shanghai\)
    -   May 22, 2019: second batch of users in China \(Shanghai\), and users in China \(Hangzhou\) and China \(Shenzhen\)
    -   May 23, 2019: third batch of users in China \(Shanghai\), and users in China\(Hong Kong\) and Singapore

## Feature comparison between Data Map and Data Management {#section_1ip_4rb_rpr .section}

Compared with Data Management, Data Map improves user experience in terms of the overall visual interaction and role distinguishing. The following table compares Data Management and Data Map.

|Item|Data Management|Data Map|Improvement|
|----|---------------|--------|-----------|
|Associate page features with roles|Based on the feature types, the Data Management module provides the following pages: -   Overview page
-   Page for searching for data
-   Page for managing tables
-   Page for managing permissions
-   Page for managing settings

 | -   Based on the relationship between roles and features, the Data Map module provides the following pages:
    -   **Overview**
    -   Homepage of **Data Map** and **All Categories**: allows you to search for data.
    -   **My Tables**: allows you to manage your tables, add tables to favorites, apply for permissions, and approve applications.
    -   **Settings**: allows you to manage workspaces or categories.
-   Data Map enhances the search capabilities for data operators and supports category-based search.

 | -   Data operators who account for the largest proportion of users can easily and quickly find required data.
-   Dedicated pages are provided for data administrators, including table owners, workspace administrators, and category administrators, by role. In this way, data administrators can easily understand their responsibilities and use required features.

 |
|Centralize personal operations|Different pages are provided for you to manage tables, manage favorites, manage permissions, and apply for resource and function permissions.| -   On the My Tables page, you can apply for resource and function permissions and approve applications for table, resource, and function permissions.
-   On the My Tables page, you can also operate tables and add tables to favorites.

 |Data-related operations are centralized on one page for easy search and implementation.|
|Control the table preview permission|Any user can preview tables. The table owner or workspace administrator cannot control the preview permission.| -   Only the owner of a table can preview the table. Other users must apply for the corresponding permission to view the table.
-   The workspace administrator can turn on or off the corresponding switches to determine whether to allow other users to preview tables in the production or development environment.
    -   By default, users can preview tables in the development environment.
    -   By default, users cannot preview tables in the production environment.

 | -   Table owners can manage permissions of their tables in detail.
-   Workspace administrators can easily control the data preview permission of tables in their workspaces.

 |
|Control the table creation permission|You can directly create a table in Data Management without any permission restriction.| -   No entry is provided for table creation.
-   We recommend that you create or modify a table on the **Tables** or **Ad-Hoc Business Flows** page of **DataStudio**. You can reuse the permission configurations of the development or O&M role in DataStudio.
-   You can choose **Data Map** \> **My Tables** to add a table to a category.

 | -   Tables must be created and modified in **DataStudio**. Permissions are controlled by role.
-   Only table owners can change the table structure. This avoids unauthorized users from creating tables or adding tables to categories.

 |

## Data Map problem feedback {#section_1ov_g5c_5p2 .section}

If you have any questions when using Data Map, search for the DingTalk group number 23182329 to join the DataWorks DingTalk group. We are happy to answer your questions.

