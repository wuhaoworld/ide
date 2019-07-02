# 准备RAM子账号 {#concept_j4w_qnp_r2b .concept}

本文将为您介绍如何创建RAM子账号。

**说明：** 

-   如果只是本人使用数加产品，请根据[准备阿里云账号](intl.zh-CN/准备工作/管理员使用云账号/准备阿里云账号.md#)的操作准备好您的账号，并跳过此章节进行后续操作。
-   如果您计划邀请其他用户协作使用数加产品，请您根据本文的操作准备RAM子账号。

## 创建子账号 {#section_v3r_xxp_r2b .section}

1.  使用主账号登录DataWorks控制台，单击右上角的用户名下的**访问控制**，进入RAM访问控制页面。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16176/15620556398944_zh-CN.png)

2.  导航至**人员管理** \> **用户**页面，单击**新建用户**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16176/15620556398945_zh-CN.png)

3.  填写新建用户页面的配置。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16176/15620556398946_zh-CN.png)

    |配置|说明|
    |--|--|
    |**用户账号信息**|设置子账号的**登录名称**和**显示名称**。|
    |**访问方式**|支持以下两种访问访问方式：     -   **控制台密码登录**：勾选后，您可以使用账号密码访问阿里云控制台。
        -   **控制台密码**：您可以选择**自动生成默认密码**或**自定义登录密码**。
        -   **要求重置密码**：您可以选择**用户在下次登录时必须重置密码**或**无需重置**。
        -   **多因素认证**：您可以选择**要求开启MFA认证**或**不要求**。
    -   **编程访问**：勾选后，启用AccessKey ID和AccessKey Secret，支持通过API或其他开发工具访问。
 |

4.  设置完成后，单击**确认**，即可创建子账号。

## 允许子账号登录 {#section_cyg_nyp_r2b .section}

1.  成功创建子账号后，主账号进入**RAM访问控制** \> **人员管理** \> **用户**页面。
2.  单击对应子账号，进入用户详情页面。
3.  如果您在创建子账号时未设置**控制台密码登录**，单击**修改登录设置**并设置密码，填写该子账号用于登录的密码。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16176/15620556408947_zh-CN.png)


## 创建子账号的运行密钥 {#section_z4g_vyp_r2b .section}

运行密钥对您在DataWorks中创建的任务顺利运行非常重要，因此主账号需要为子账号创建AccessKey，或者允许子账号用户自行创建和管理自己的AccessKey信息。

-   为子账号创建AccessKey。
    1.  主账号进入**访问控制** \> **用户管理**页面。
    2.  单击对应子账号后，进入用户详情页面。
    3.  单击**创建Accesskey**，填写手机收到的验证码，即可为子账号创建新的AccessKey。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16176/15620556408948_zh-CN.png)

        **说明：** 子账号的AccessKeySecret只会出现一次，请在创建时妥善保管。如果遗失AccessKey信息，只能重新创建。

-   允许子账号自行创建AccessKey并进行管理。
    1.  主账号进入**RAM访问控制** \> **人员管理** \> **设置**页面，单击**修改RAM用户安全设置**。
    2.  勾选RAM用户安全设置页面中**自主管理AccessKey**的**允许**。
    3.  单击**确定**即可生效。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16176/15620556408949_zh-CN.png)

        该选项默认不勾选，所以使用子账号的用户，默认无法为自己创建AccessKey并进行管理。启用允许自主管理AcessKey后，子账号登录阿里云官网后，即可在管理控制台自行创建AccessKey。

        **说明：** 运行密钥AccessKey非常重要，无论是主账号的AccessKey还是子账号的AccessKey，一旦创建成功，请您务必保证它的安全和使用范围。一旦有泄漏的风险，请及时禁用和更新。


## 给子账号授权 {#section_yxy_5rz_jfb .section}

如果您需要让子账号能够创建DataWorks工作空间，需要给子账号授予**AliyunDataWorksFullAccess**权限。

1.  进入**RAM访问控制** \> **人员管理** \> **用户**页面。
2.  单击需要授权的子账号后的**添加权限**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16176/156205564050626_zh-CN.png)

3.  在添加权限对话框中，搜索出AliyunDataWorksFullAccess并单击，确保其显示在**已选择**框中。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16176/156205564050628_zh-CN.png)

4.  单击**确定**。

**说明：** 

-   完成授权后，子账号即可创建工作空间，且自动成为该工作空间的管理员，子账号对应的主账号为工作空间所有者。
-   不是子账号自己创建的工作空间，仍需主账号为该子账号进行工作空间授权。

## 将子账号交付其他用户使用 {#section_sng_tzp_r2b .section}

**说明：** 

-   子账号归属于主账号，本身不拥有资源，也没有独立的计量计费。
-   子账号在阿里云各产品中操作产生的费用，将由创建这些子账号的主账号统一付费。
-   主账号需要查看RAM用户登录链接和自己的企业别名（默认域名），并告知子账号。

主账号进入**RAM访问控制** \> **概览**页面，即可看到登录链接及默认域名。

单击**域别名**，即可更新域名。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16176/15620556418950_zh-CN.png)

交付子账号给其他用户使用时，需要提供如下信息：

-   RAM用户登录链接。
-   所属主账号的企业别名或默认域名。
-   该子账号的用户名和密码。
-   该子账号的Access Key ID和Access Key Secret。
-   确认已经允许子账号启用控制台登录。
-   确认已经允许子账号自主管理AccessKeys。

