# MaxCompute高级配置 {#concept_gpt_dn4_1fb .concept}

您可以通过工作空间管理中的MaxCompute高级配置操作，对当前工作空间的MaxCompute属性进行管理和配置。

单击数据开发页面右上角的**工作空间管理**，即可进入工作空间配置页面。

![工作空间管理](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/20193/156385608349187_zh-CN.png)

单击左侧导航栏中的**MaxCompute高级配置**，即可进入MaxCompute高级配置页面。该页面包括**基本设置**和**自定义用户角色**两个模块。

## 基本设置 {#section_gsn_ln4_1fb .section}

您可以在基本设置模块，进行MaxCompute安全配置。

![常用权限点](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/20193/156385608311291_zh-CN.png)

**MaxCompute安全设置**：涉及底层MaxCompute相关的权限及安全设置，详情请参见[项目空间的安全配置](../../../../intl.zh-CN/管理/安全功能详解/项目空间的安全配置.md#)。

|配置|说明|
|--|--|
|**使用ACL授权**|激活/冻结该开关，相当于Owner账号在MaxCompute Project中执行`set CheckPermissionUsingACL=true/false`操作，默认激活。|
|**允许对象创建者访问对象**|激活/冻结该开关，相当于Owner账号在MaxCompute Project中执行`set ObjectCreatorHasAccessPermission=true/false`操作，默认激活。|
|**允许对象创建者授权对象**|激活/冻结该开关，相当于Owner账号在MaxCompute Project中执行`set ObjectCreatorHasGrantPermission=true/false`操作，默认激活。|
|**项目空间数据保护**|激活/冻结该开关，相当于Owner账号在MaxCompute Project中执行`set ProjectProtection=true/false`，默认冻结。|
|**子账号服务**|激活/冻结该开关，控制子账号可以访问/禁止访问该MaxCompute Project，默认激活。|
|**使用Policy授权**|激活/冻结Policy授权机制，相当于Owner账号在MaxCompute project中执行`set CheckPermissionUsingPolicy=true/false`操作，默认激活。|
|**启动列级别访问控制**|项目空间中的LabelSecurity安全机制默认关闭，ProjectOwner可以自行开启，相当于Owner账号在MaxCompute Project中执行`Set LabelSecurity=true/false`。|

## 自定义用户角色 {#section_twg_hv4_1fb .section}

![自定义用户角色](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/20193/156385608311293_zh-CN.png)

|配置|说明|
|--|--|
|**角色名称**|MaxCompute项目中的角色名称。|
|**操作**| -   **查看详情**：查看当前角色中包含的成员列表，以及当前角色对表或项目的权限。
-   **成员管理**：添加或删除当前角色中的成员。
-   **权限管理**：设置并管理当前角色对表/项目的权限，详情请参见[授权](../../../../intl.zh-CN/管理/安全功能详解/用户及授权管理/授权.md#)。
-   **删除**：删除当前角色。

 |
|**新增角色**|单击右上角的**新增角色**，在新增角色对话框中填写**角色名称**，在待添加账号处勾选需要添加的成员账号，单击**\>**，将需要添加的账号移动至已添加的账号中，单击**确定**，即可添加成功。![新增角色](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/20193/156385608452552_zh-CN.png)

|

**说明：** 此处自定义角色所设置的权限，将与原有的系统权限取并集。

