# Data Guard overview {#concept_s3p_xtq_pgb .concept}

Data Guard provides flexible permission management features and allows users to request permissions and handle requests visually. Data Guard not only improves data security but also facilitates data permission management.

**Note:** Data Guard is open for beta testing.

You can click the DataWorks icon in the upper-left corner and then click Data Guard to go to the Data Guard page.

Data Guard consists of the following modules: My Permissions, Authorizations, and Approval Center. Currently, Data Guard provides the following features:

-   Self-service permission request: Users can select the required tables to quickly initiate a permission request online. This request mode features high efficiency, compared with the original mode in which users need to contact administrators offline.
-   Permission revocation: Administrators can view the users who have permissions on database tables and revoke unnecessary permissions as required. Users can also revoke permissions themselves.
-   Request approval: Administrators approve permission requests of users instead of directly granting permissions to users. This provides a visual and process-based permission management mechanism, and supports post-event backtracking on the approval process.

By using Data Guard, you can view permissions on all the tables in an organization, request and revoke table permissions, and approve or reject permission requests.

Each operation in Data Guard applies to all the workspaces of a tenant in standard mode \(including the development and production environments\) and basic mode.

