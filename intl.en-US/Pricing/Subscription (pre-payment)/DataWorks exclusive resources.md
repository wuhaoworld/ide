# DataWorks exclusive resources {#concept_265438 .concept}

This topic describes the billing standards, scale-out, renewal, and expiration of DataWorks exclusive resources. It also provides the scenarios and limits of DataWorks exclusive resources.

DataWorks provides three types of exclusive resources: **exclusive resources for scheduling**, **exclusive resources for Data Integration instances**, and **App Studio operating space \(production environments\)**. These resources deliver optimal performance assurance.

## Exclusive resource groups for scheduling {#section_55p_1bv_1ut .section}

When nodes run in high concurrency while load shifting is not an option, enterprises need exclusive computing resources to ensure that nodes are scheduled and run on as planned. To address this problem, DataWorks provides exclusive resource groups.

**Note:** Exclusive resources for scheduling in a single order can only be used in one exclusive resource group. They cannot be split among multiple exclusive resource groups. After paying for the order, you can scale out the resources \(increase the number of resources\) based on the resources purchased in the order.

-   Billing standard

    Exclusive resource groups for scheduling are billed in subscription mode. You can select an appropriate specification for billing as needed. For more information, see [Billing standards of exclusive resources for scheduling](intl.en-US/Pricing/Appendix/Billing standards of exclusive resources for scheduling.md#).

-   Scale-out

    You can scale out the resources in each exclusive resource group order based on your business needs. You only need to pay for the difference between the numbers of the new and original resources from the time when you add the resources to the time when the original order expires.

    **Note:** 

    -   Scale-out increases the number of resources but does not upgrade their CPU and memory configurations.
    -   Scale-out only allows you to add resources of the same capacity as the purchased resources in the current order.
    -   After scale-out, the new configuration takes effect within 20 minutes of payment.
-   Renewal

    You can choose to renew all resources within the 30 days before or after the exclusive resource group order expires. If you do not renew the subscription within 15 days after expiration, the resources in the order are suspended immediately.

-   Expiration
    -   Service suspension

        By default, the billing system sends expiration warnings to the mobile number and email address that were bound to your primary Alibaba Cloud account 8 days, 12 days, and 14 days before your exclusive resources expire. If you do not renew the subscription within 15 days after expiration, the resources in the order are suspended immediately.

    -   Resource release

        After the exclusive resource groups expire, you are given a 15-day grace period. If you do not renew the subscription within 15 days, the instances are released.

        A release notification is sent to the mobile number and email address that were bound to your Alibaba Cloud primary account one day before the exclusive resource groups are released.


## Exclusive resource groups for Data Integration instances {#section_hcx_l05_vcg .section}

When Data Integration nodes run in high concurrency while load shifting is not an option, enterprises need exclusive computing resources to ensure that data is transmitted quickly and reliably. To address this challenge, DataWorks provides exclusive resource groups for Data Integration instances.

**Note:** The exclusive resources for Data Integration instances in a single order can only be used in one exclusive resource group for Data Integration instances. They cannot be split among exclusive resource groups for Data Integration instances. After paying for the order, you can scale out the resources \(increase the number of resources\) based on the resources purchased in the order.

-   Billing standard

    Exclusive resource groups for Data Integration instances are billed in subscription mode. You can select an appropriate specification for billing as needed. For more information, see [Billing standards of exclusive resources for Data Integration instances](intl.en-US/Pricing/Appendix/Billing standards of exclusive resources for Data Integration instances.md#).

    **Note:** Running a Data Integration node not only consumes concurrent processes in the exclusive resource group for Data Integration instances, but also consumes concurrent instances in the exclusive resource groups \(one Data Integration instance consumes one concurrent instance\).

    Assume that you purchase four 8c16g exclusive resource groups for Data Integration instances for a workspace in China \(Hangzhou\) and the purchase period is one year. For sync node instances running on these exclusive resources, the fee is `4 × 152.45 USD/month × 12 months = 7,317.60 USD`.

    Within the one-year validity period, DataWorks charges no additional fees for the number of concurrent instances scheduled by sync nodes running on the exclusive resources. The generated public network traffic is billed separately.

-   Scale-out

    You can scale out the resources in each exclusive resource group for Data Integration instances order based on your business needs. You only need to pay for the difference between the numbers of the new and original resources from the time when you add the resources to the time when the original order expires.

    **Note:** 

    -   Scale-out increases the number of resources but does not upgrade their CPU and memory configurations.
    -   Scale-out only allows you to add resources of the same capacity as the purchased resources in the current order.
    -   After scale-out, the new configuration takes effect within 20 minutes of payment.
-   Renewal

    You can renew all resources within the 30 days before or after the exclusive resource group for Data Integration instances order expires. If you do not renew the subscription within 15 days after expiration, the resources in the order are suspended immediately.

-   Expiration
    -   Service suspension

        By default, the billing system sends expiration warnings to the mobile number and email address that were bound to your primary Alibaba Cloud account 8 days, 12 days, and 14 days before your purchased exclusive resource groups for Data Integration instances expire. If you do not renew the subscription within 15 days after expiration, the resources in the order are suspended immediately.

    -   Resource release

        After the exclusive resource groups for Data Integration instances expire, they are retained for 15 days. If you do not renew the subscription within 15 days, the instances are released.

        A release notification is sent to the mobile number and email address that were bound to your Alibaba Cloud primary account one day before the resources are released.


## App Studio production environments {#section_vl2_oor_zzk .section}

**Note:** 

-   If you use App Studio to publish code to the production environment and run it, you must purchase App Studio production environments.
-   You must purchase or upgrade your DataWorks edition to the Enterprise or Ultimate edition before you can purchase this product. For more information, see [DataWorks advanced editions](intl.en-US/Pricing/Subscription (pre-payment)/DataWorks advanced editions.md#).

-   Billing standard

    After developing and debugging code in the App Studio development environment, you may need to publish the code to the public network for running and provide an application O&M environment. In this case, you can purchase an App Studio production environment by subscription. This is the production environment where the code is run after it is published. The billing standard is listed in the following table.

    |App Studio production environment|Price \(USD/month\)|Region|
    |---------------------------------|-------------------|------|
    |2c4g|37.40|China \(Shanghai\) China \(Hangzhou\)

 China \(Shenzhen\)

 China \(Beijing\)

 |
    |4c8g|74.80|
    |8c16g|149.61|

-   Renewal

    You can renew your subscription within 30 days before or after the App Studio production environment order expires. If you do not renew the subscription within 15 days after expiration, the resources in the order are suspended immediately.

-   Expiration
    -   Service suspension

        By default, the billing system sends expiration warnings to the mobile number and email address that were bound to your primary Alibaba Cloud account 8 days, 12 days, and 14 day before your purchased App Studio production environment expires. If you do not renew the subscription within 15 days after expiration, the resources in the order are suspended immediately.

    -   Resource release

        After the App Studio production environment expires, the code in the production environment is retained for 15 days. If you do not renew the subscription within 15 days, the instances are released.

        A release notification is sent to the mobile number and email address that were bound to your primary Alibaba Cloud account one day before the App Studio production environment is released.


## Application scenarios of exclusive resources {#section_gfh_41s_ss8 .section}

-   Exclusive resources are used in exclusive mode, which can isolate resources between tenants and between different tasks of the same tenant.

    If your tasks use default resources, the tasks may be delayed upon high concurrency because they need to wait for resources. In this case, we recommended that you use exclusive resources for scheduling and exclusive resources for Data Integration instances.

-   Exclusive resources can be accessed on the public network.
    -   If you need to access public network services or user-created services through PyODPS, we recommend that you use exclusive resources for scheduling.
    -   If you need to access public network services or user-created services through Shell, we recommend that you use exclusive resources for scheduling.
-   You can decide the specifications of the exclusive resources. If you need to run resource-consuming tasks, we recommend that you use exclusive resources for scheduling.

## Limits of exclusive resources {#section_5lq_obp_v4i .section}

-   Exclusive resources for Data Integration instances cannot access the Alibaba Cloud classic network. If your data source is on the classic network, we recommend that you use the default resource group to run sync tasks.
-   When you create exclusive resources for Data Integration instances, confirm the region and zone of the exclusive resource group. Exclusive resources for Data Integration instances can only access the data sources of the VPC in the same region and zone.

    **Note:** To ensure that the exclusive resource group has the permission to access the data source, you need to add a network access whitelist.

-   Currently, the software environment, such as Python, for exclusive resources for scheduling cannot be customized.

