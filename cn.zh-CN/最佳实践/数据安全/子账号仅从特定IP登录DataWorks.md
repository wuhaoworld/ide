# 子账号仅从特定IP登录DataWorks {#task_1580347 .task}

在数据开发过程中，部分对权限控制较为严格的用户要求RAM子账号仅能通过公司内某个特定IP进行登录。本文将为您介绍如何实现RAM子账号仅从特定本地IP登录DataWorks。

您需要首先参见[准备RAM子账号](../intl.zh-CN/准备工作/管理员使用云账号/准备RAM子账号.md#)，创建RAM子账号，并且给子账号授权。权限**AliyunDataWorksFullAccess**为系统默认权限，无法修改，您需要额外创建一个自定义授权策略。

## 创建自定义策略 {#section_okb_r5o_dte .section}

1.  云账号登录[RAM控制台](https://ram.console.aliyun.com/)。
2.  在左侧导航栏的**权限管理**菜单下，单击**权限策略管理**。
3.  单击**新建权限策略**。
4.  在**新建自定义权限策略**对话框中，填写**策略名称**为**dataworksIPlimit1**，勾选**配置模式**为**脚本配置**，配置您的自定义权限。 

    ![脚本配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/125807/156523050938925_zh-CN.png)

    自定义权限的完整内容如下所示，"acs:SourceIP"后填写的IP，即为您允许访问DataWorks的IP，本示例设置为100.1.1.1/32。

    ``` {#codeblock_qvr_kt4_m8w .language-json}
    {
          "Version": "1",
          "Statement":
            [{
              "Effect": "Deny",
                "Action": ["dataworks:*"],
                "Resource": ["acs:dataworks:*:*:*"],
                "Condition":
                 {
                    "NotIpAddress":
                     {
                        "acs:SourceIp": "100.1.1.1/32"
                      }
                  }
             }]
    }
    ```

    **说明：** 

    -   acs:SourceIP只能为一个IP或一个网段，不允许填写多个IP或网段。
    -   自定义权限配置项说明请参见[Policy基本元素](../../intl.zh-CN/用户指南/权限策略/权限策略语言/权限策略基本元素.md#)。
5.  单击**确认**。

## 授权自定义策略给RAM用户 {#section_n8j_tx3_5lb .section}

1.  在左侧导航栏的**人员管理**菜单下，单击**用户**。
2.  在**用户登录名称/显示名称**列表下，找到目标RAM用户。
3.  单击**添加权限**，被授权主体会自动填入。
4.  在左侧**权限策略名称**列表下，单击需要授予RAM用户的权限策略。 

    **说明：** 在右侧区域框，选择某条策略并单击**×**，可撤销该策略。

5.  单击**确定**。
6.  单击**完成**。

## 验证结果 {#section_lne_8qf_425 .section}

使用不同于100.1.1.1/32的地址登录DataWorks控制台，发现登录失败。

![登录失败](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/125807/156523050938934_zh-CN.png)

