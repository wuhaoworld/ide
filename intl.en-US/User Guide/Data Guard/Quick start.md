# Quick start {#concept_xqn_bt5_xgb .concept}

This topic uses a simple example to describe how to use Data Guard.

## Prerequisites {#section_ngt_cz1_ygb .section}

Before using Data Guard, note the following:

-   You can request permissions on fields only in a workspace with LabelSecurity enabled. If LabelSecurity is disabled for a workspace, you can request permissions only on tables in this workspace.
-   To ensure that field permissions are valid in the specified validity period, ensure that the security level of each field is higher than the security level of your account.

    After permissions on a table are granted to you, you automatically obtain permissions on the fields whose security level is 0 or not higher than the security level of your account. The permissions on these fields are permanently valid and cannot be separately revoked.

-   For more information about LabelSecurity, see [../../../../dita-oss-bucket/SP\_76/DNODPS19101710/EN-US\_TP\_12109.md\#](../../../../intl.en-US/Management/Configure security features/Column-level access control.md#).

## Example {#section_icd_355_xgb .section}

This example includes the following operations:

1.  Request permissions on tables A and B by using a RAM account.
2.  Approve the request by using an Alibaba Cloud account.
3.  Revoke the permissions on some fields in table A by using the RAM account.
4.  Revoke the permissions on table A by using the RAM account.
5.  Revoke the permissions of the RAM account on table B by using the Alibaba Cloud account.

## Request permissions on tables A and B by using a RAM account {#section_hsq_x55_xgb .section}

1.  Log on to Data Guard by using the RAM account. In the left-side navigation pane, click **My Permissions**. The **Table** tab appears.****
2.  Select the fields in tables A and B on which you want to request permissions and click **Request Approval**.
3.  Set the parameters in the Table Permission Request dialog box.
4.  Click **Submit**.

## Approve the request by using an Alibaba Cloud account {#section_s4x_xv5_xgb .section}

1.  Log on to Data Guard by using the Alibaba cloud. In the left-side navigation pane, click **Approval Center**. Click **Pending Approval** tab.
2.  Click **Handle** in the Actions column for the request submitted by the RAM account. On the Request Details page that appears, view the progress and objects requested.
3.  Enter your comment and click **Approve** to approve the request.

## Revoke the permissions on some fields in table A by using the RAM account {#section_s24_nx5_xgb .section}

1.  Log on to Data Guard by using the RAM account. In the left-side navigation pane, click **My Permissions**. The **Table** tab appears.****
2.  Choose **More** \> **Revoke Field Permission** in the Actions column for table A.
3.  In the Revoke Field Permission dialog box, select the fields on which you want to revoke permissions and click **OK**.

## Revoke the permissions on table A by using the RAM account {#section_tgz_gy5_xgb .section}

1.  Log on to Data Guard by using the RAM account. In the left-side navigation pane, click **My Permissions**. The **Table** tab appears.
2.  Choose **More** \> **Revoke Permission** in the Actions column for table A.
3.  In the Revoke Permission dialog box, select the permissions you want to revoke and click **OK**.

## Revoke the permissions of the RAM account on table B by using the Alibaba Cloud account {#section_zkb_sy5_xgb .section}

1.  Log on to Data Guard by using the Alibaba Cloud account and click **Authorizations** in the left-side navigation pane. The **Table** tab appears.
2.  Click the plus sign \(+\) in front of table B to view all the accounts that have permissions on the table.
3.  Click **Revoke Permission** in the Actions column for the RAM account.
4.  In the Revoke Permission dialog box, select the permissions you want to revoke and click **OK**. The selected permissions of the RAM account on the table are revoked.

