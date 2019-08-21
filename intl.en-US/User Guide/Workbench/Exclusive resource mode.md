# Exclusive resource mode {#concept_592761 .concept}

DataWorks provides you with an exclusive resource mode, which allows you to purchase exclusive resources and assign them to workspaces to run tasks.

In exclusive resource mode, the physical resources \(such as the network, disk, CPU, and memory\) on hosts are completely exclusive to users. This helps isolate resources of different users or different workspaces. In addition, exclusive resources can be flexibly scaled in or out. This meets the requirements of resource exclusiveness and flexible configuration.

## Purchase exclusive resources {#section_5dk_xbo_yo2 .section}

DataWorks exclusive resources are purchased in subscription mode. You can go to the purchase page of exclusive resources from the DataWorks product page or by clicking Add Exclusive Resource in the DataWorks console.

-   From the DataWorks product page
-   By clicking Add Exclusive Resource
    1.  Log on to the DataWorks console and click the **Resources** tab at the top of the page. The **Exclusive Resources** page appears.
    2.  If you have not purchased any exclusive resources in the current region, click **Add Exclusive Resource** in the upper-right corner of the page.
    3.  In the Add Exclusive Resource dialog box that appears, click **Purchase** next to Order Number to go to the purchase page.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/474487/156637747948915_en-US.png)


On the purchase page, set the region, exclusive resource type, exclusive resource specification, resource count, and billing cycle as required, and click **Buy Now**.

**Note:** Exclusive resources cannot be used across regions. For example, the exclusive resources in China \(Shanghai\) can only be used by the workspaces in China \(Shanghai\).

## Add exclusive resources {#section_6gv_z6w_qmx .section}

1.  Log on to the DataWorks console and click the **Resources** tab at the top of the page. The **Exclusive Resources** page appears. Click **Add Exclusive Resource** in the upper-right corner of the page.
2.  In the Add Exclusive Resource dialog box that appears, set the parameters.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/474487/156637747948927_en-US.png)

    |Parameter|Description|
    |---------|-----------|
    |**Resource Type**|The type of the exclusive resource. Exclusive resources are classified into **Exclusive Resources** and **Exclusive Resources for Data Integration**. They are applicable to general tasks and data synchronization tasks respectively.|
    |**Resource Name**|The name of the exclusive resource. The value must be unique within all resources of a tenant.|
    |**Resource Description**|The description of the exclusive resource.|
    |**Order Number**|The order number of the exclusive resource. If you have not purchased any exclusive resources, click **Purchase** next to Order Number to go to the purchase page.|
    |**Zone**|The zone of hosts available in the region. Select a zone based on your requirements.|

3.  After you complete the configuration, click **Create** to add the exclusive resource.

    **Note:** The exclusive resource is initialized within 20 minutes. Wait until its status changes to **Running**.


## View exclusive resources {#section_l0d_24e_6r6 .section}

After adding exclusive resources, you can view basic information of the exclusive resources on the Exclusive Resources page, including **Valid Until**, **Resource Count**, and **Resource Usage**.

-   **Valid Until**: the expiration date of the exclusive resource. It depends on the billing cycle that you set when purchasing the exclusive resource.
    -   You can renew the exclusive resource before it expires. When the exclusive resource expires, it cannot be used by new tasks.
    -   You can activate the exclusive resource within seven days after its expiration. If the exclusive resource is not activated within seven days after its expiration, it is released.
-   **Resource Count**: the quantity of the exclusive resource.
-   **Resource Usage**: the usage of the exclusive resource in percentage.

## Manage exclusive resources {#section_maj_9t9_pfl .section}

After adding exclusive resources, you can scale and renew the exclusive resources, bind them to your Virtual Private Cloud \(VPC\), or change the workspaces that can use the exclusive resources.

-   **Scale out exclusive resources** 

    If the usage of an exclusive resource remains high or the current quantity cannot meet your requirements, you can click **Scale Out** to scale out the exclusive resource.

-   **Scale in exclusive resources** 

    If an exclusive resource is sometimes idle, you can click **Scale In** to scale in the exclusive resource.

-   **Renew exclusive resources** 

    Click **Renew** to extend the validity period of an exclusive resource.

-   **Bind exclusive resources to your VPC** 

    Exclusive resources are deployed in a VPC hosted by DataWorks. To use exclusive resources in your own VPC, you need to bind the exclusive resources to your VPC.

    Click **Add VPC Binding** to go to the binding page.

    **Note:** Before binding exclusive resources to your VPC, you must authorize DataWorks to access your cloud resources in the RAM console.

    After the authorization is complete, click **Add Binding**. In the Add VPC Binding dialog box that appears, set the parameters.

    If the information of the exclusive resource or your VPC changes after the binding, you can rebind the exclusive resource to your VPC. Currently, you cannot unbind an exclusive resource from a VPC.

-   **Change the workspaces that can use an exclusive resource** 

    An exclusive resource must be bound to a workspace so that the exclusive resource can be used by tasks. An exclusive resource can be bound to multiple workspaces.


## Use exclusive resources {#section_442_xzp_r7r .section}

After an exclusive resource is bound to a workspace, you can allocate the exclusive resource to tasks in the workspace.

-   Exclusive resources

    In Operation Center, select a task to change its resource group.

-   Exclusive resources for data integration

    You can select an exclusive resource for data integration when configuring a data integration task.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/474487/156637748148969_en-US.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/474487/156637748248972_en-US.png)


