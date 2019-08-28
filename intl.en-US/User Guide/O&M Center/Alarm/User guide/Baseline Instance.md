# Baseline Instance {#concept_uwf_rzn_42b .concept}

You can view the baseline information on the Baseline Instance page.

## Baseline instance {#section_my5_bb4_42b .section}

After creating a baseline, you need to enable the baseline so that a baseline instance can be generated. On the Baseline Instances page, you can search for the corresponding instances by business date, owner, event ID, workspace, and baseline name. You can also click **View Details**, **Handle**, and **View Gantt Chart** in the Actions column to perform related operations.

![Operations](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16370/15669962437445_en-US.png)

A baseline can be in either of the following four states:

-   **Normal**: indicates that all tasks in the baseline are completed before the alerting time.
-   **Alerting**: indicates that one or more tasks in the baseline are not completed until the alerting time expires but the committed completion time is not reached.
-   **Overtime**: indicates that one or more tasks in the baseline are not completed until the committed completion time expires.
-   **Others**: indicates that all tasks in the baseline are paused or the baseline is not associated with any task.

You can click **View Details**, **Handle**, and **View Gantt Chart** in the Actions column to perform related operations.

-   **View Details**: Click **View Details** to go to the **Baseline Instance Details** page.

    ![View details](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16370/156699624339826_en-US.png)

    On the Baseline Instance Details page, you can view the **General**, **Critical Path**, **Baseline Instance**, **History**, and **Events**.

    **Note:** The business date is one day prior to the system date. The Cycle parameter appears only for hourly baselines.

-   **Handle**: The baseline that generates an alert stops alerting while the alert is being handled.
-   **View Gantt Chart**: Click **View Gantt Chart** to view the critical path of tasks.

