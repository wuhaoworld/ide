# MaxCompute advanced settings {#concept_gpt_dn4_1fb .concept}

With the Workspace Manage module of DataWorks, you can manage the advanced settings of MaxCompute for the current workspace.

After logging on to the DataWorks console, click the **Workspace Manage** icon in the upper-right corner to go to the DataOS Panel page.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/20193/156151721949187_en-US.png)

In the left-side navigation pane, click **MaxCompute Advanced Settings**. The MaxCompute Advanced Settings page includes two tabs: **Basic Settings** and **Custom User Roles**.

## Basic Settings {#section_gsn_ln4_1fb .section}

On the Basic Settings tab, you can configure security settings for the MaxCompute project.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/20193/156151721911291_en-US.png)

MaxCompute Security Settings: you can configure security settings for the MaxCompute project in this section. For more information, see [../../../../dita-oss-bucket/SP\_76/DNODPS19101710/EN-US\_TP\_12099.md\#](../../../../intl.en-US/Management/Configure security features/Security configurations.md#).

|Option|Description|
|------|-----------|
| **Enable ACL-based authorization** |Enabling or disabling this option is equivalent to running the `set CheckPermissionUsingACL=true/false` command in the MaxCompute project by using the owner account. This option is enabled by default.|
| **Allow object creators to access objects** |Enabling or disabling this option is equivalent to running the `set ObjectCreatorHasAccessPermission=true/false` command in the MaxCompute project by using the owner account. This option is enabled by default.|
| **Allow object creators to grant object permissions** |Enabling or disabling this option is equivalent to running the `set ObjectCreatorHasGrantPermission=true/false` command in the MaxCompute project by using the owner account. This option is enabled by default.|
| **Protect workspace data** |Enabling or disabling this option is equivalent to running the `set ProjectProtection=true/false` command in the MaxCompute project by using the owner account. This option is disabled by default.|
| **Enable RAM service** |RAM users are only allowed to access the MaxCompute project if this option is enabled. This option is enabled by default.|
| **Enable policy-based authorization** |This option indicates whether to use policies to check access permissions. Enabling and disabling this option is equivalent to running the `set CheckPermissionUsingPolicy=true/false` command in the MaxCompute project by using the owner account. This option is enabled by default.|
| **Enable column-level access control** |The label-based access control mechanism is disabled by default in the MaxCompute project. The project owner can enable or disable it as required. Enabling or disabling this option is equivalent to running the `Set LabelSecurity=true/false` command in the MaxCompute project by using the owner account.|

## Custom User Roles {#section_twg_hv4_1fb .section}

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/20193/156151722011293_en-US.png)

-    **Role Name**: a role name in the MaxCompute project.
-    **Actions**:
    -    **View Details**: you can click this button to view the list of members that are assigned a specific role and the permissions of the role on tables and projects.
    -    **Members**: you can click this button to assign and unassign a role from specified members.
    -    **Authorization**: you can click this button to manage the permissions of a role on tables and projects.
    -    **Delete**: you can click this button to delete a role.
-    **Create Role**: you can click the **Create Role** button in the upper-right corner and specify the configurations in the dialog box that appears to create a role.

    **Note:** The union of the permissions specified for the custom role and the default permissions applies.


