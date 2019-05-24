# FAQ {#concept_pml_qmz_xgb .concept}

This topic describes the frequently asked questions \(FAQs\) about Data Guard of DataWorks.

-   Q: What permissions can I request by using Data Guard?

    A: You can request permissions on tables in DataWorks workspaces in the development and production environments by using Data Guard.

-   Q: Why cannot I select fields sometimes when requesting permissions?

    A: If LabelSecurity is enabled for a workspace, you can request permissions on individual fields in this workspace. If LabelSecurity is disabled for a workspace, you can request permissions only on tables in this workspace.

-   Q: Who will approve my request?

    A: Your request is approved by a project administrator or a table owner. After either a project administrator or a table owner approves or rejects your request, the request is closed.

-   Q: Why do I find two requests on the **My Requests** page after I submit only one request?

    A: The tables in your request belong to two owners. In this case, Data Guard automatically splits your request into two by table owner.

-   Q: I request permissions on a field for one month only. Why is the validity period of the permissions becomes permanent after my request is approved?

    A: The security level of this field is 0 or not higher than the security level of your account.

-   Q: Why do I find permissions on some tables and fields on which I have not requested any permissions?

    A: The possible causes are as follows:

    -   An administrator has granted the permissions to you by running commands in the DataWorks console.
    -   After your request is approved in Data Guard, Data Guard also grants you the permissions on fields whose security level is 0 or not higher than the security level of your account, even though you have not requested the permissions.
-   Q: Why does a request disappear from the **Pending Approval** page before I handle it?

    A: Another project administrator or table owner has approved or rejected the request. The request is closed and no longer needs to be handled.

-   Q: What can I do if the message "You cannot perform this operation because there is a problem with the MaxCompute project" appears when I specify the workspace and environment?

    A: Send the error message and error code to a project administrator for troubleshooting.

-   Q: Why do I fail to revoke permissions on a field?

    A: You can revoke permissions only on the fields whose security level is higher than the security level of your account.


