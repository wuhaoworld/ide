# Baseline Management {#concept_uwf_rzn_42b .concept}

You can create and define baselines on the Baseline Management page.

## Create a baseline {#section_tzy_vzn_42b .section}

1.  Go to the **Operation Center** page, and then choose **Alarm** \> **Baseline Management** in the left-side navigation pane.
2.  On the Baseline Management page, click **Create Baseline** in the upper-right corner.

    ![Create a baseline](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16370/15669961077441_en-US.png)

    **Note:** Currently, only the project administrator can create baselines.

3.  In the Create Baseline dialog box that appears, set the parameters, and then click **OK**.

    ![Confirm settings](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16370/15669961077442_en-US.png)

    |Parameter|Description|
    |:--------|:----------|
    |**Baseline Name**|The name of the baseline.|
    |**Workspace**|The workspace of the task associated with the baseline.|
    |**Owner**|The name or ID of the owner.|
    |**Recurrence**|Specifies whether the baseline is detected by day or hour.     -   **By the Day Interval**: Select this option for daily scheduled tasks.
    -   **By the Hour Interval**: Select this option for hourly scheduled tasks.
 |
    |**Node**|     -   **Node**: the task node associated with the baseline. Enter the name or ID of a task node, and then click the icon on the right to add the task node. You can add multiple task nodes.
    -   **Workflow**: the business flow associated with the baseline. Enter the name or ID of a business flow, and click the icon on the right to add the business flow. We recommend that you only add the last task node of a business flow instead of all task nodes.
 |
    |**Priority**|The priority of the baseline. A baseline with a higher priority is scheduled first. Currently, the only available priority value is 1.|
    |**Estimated Completion Time**|The completion time of the task estimated based on the average running time of the task during previous scheduling. If no historical data is available, the message **The completion time cannot be estimated due to a lack of historical data.** is displayed.|
    |**Committed Time**|The time point when a task should be completed. An alert is triggered if the task is not completed until the time point obtained by subtracting the alert margin time from the committed completion time.|
    |**Margin Threshold**|The interval before an alert is triggered. For example, set Committed Time to 3:30 and Margin Threshold to 10 minutes. An alert is triggered if the task is not completed at 3:20. Assume that the average running time of the task is 30 minutes. If the task is not started at 2:50, an alert is triggered. **Note:** The average running time of a task can be calculated based on the data of the last 15 days.

 |

4.  After a baseline is created, click **Enable** in the Actions column to enable the baseline.

    ![Enable a baseline](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16370/15669961077443_en-US.png)

    You can click **View Details**, **Change**, **Enable**, Disable, or **Delete** in the Actions column to perform related operations.

    -   **View Details**: Click **View Details** to view the basic information about the corresponding baseline.
    -   **Change**: Click **Change** to modify the corresponding baseline.
    -   **Enable** or Disable: Click Enable or Disable to enable or disable the corresponding baseline. A baseline instance can be generated only when the corresponding baseline is enabled.
    -   **Delete**: Click **Delete** to delete the corresponding baseline.

## Add a task to a baseline {#section_dhy_pbv_hhb .section}

By default, all tasks in the production environment are in the **default project baseline**. When you create a baseline, you actually move tasks from the default project baseline to the baseline you create.

**Note:** A task must belong to a baseline, so you cannot directly remove tasks from the default project baseline. Instead, you can create a new baseline to move tasks from the default project baseline to the new baseline. When you delete a baseline that you create, you actually move the tasks in the baseline to the default project baseline.

To change the baseline of a task, perform either of the following operations:

-   On the Baselines page, click **Create Baseline** in the upper-right corner. Then, create a baseline by following the instructions in the Create a baseline section.

    ![Create a baseline](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16370/156699610743372_en-US.png)

-   On the **Cycle Task** page, find the task, click **More** in the Actions column, and then select **Add to Baseline** from the drop-down list.

    ![Add a task to a baseline](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16370/156699610743373_en-US.png)


