# Approval Center {#concept_vqb_gfl_qgb .concept}

On the Approval Center page, you can view your requests and their status, view and handle the requests pending your approval, and view the requests that you have handled.

## My Requests {#section_rqc_2gl_qgb .section}

1.  Log on to Data Guard. In the left-side navigation pane, click **Approval Center**. The **My Requests** tab appears.

    On this tab, you can view the following information about each of your requests: object type, workspace, MaxCompute project, tables, request time, and status.

    **Note:** If a request contains permissions on tables that belong to different owners, Data Guard automatically splits the request into multiple requests by table owner.

2.  Click **Details** in the Actions column to view details about a request.

## Pending Approval {#section_cbq_2jl_qgb .section}

1.  Log on to Data Guard. In the left-side navigation pane, click **Approval Center**. Click the **Pending Approval** tab.

    On this tab, you can view the requests pending your approval. If a request is pending your approval, a red dot appears next to **Approval Center** and **Pending Approval** to remind you.

    You can view the following information about each request pending your approval: object type, grant-to account, workspace, MaxCompute project, tables, and request time.

2.  Click **Handle** in the Actions column to view details about a request and handle it on the Request Details page. The request details include the progress and objects requested.
3.  Enter your comment and click **Approve** or **Reject** as required.

## Handled by Me {#section_opq_hkl_qgb .section}

1.  Log on to Data Guard. In the left-side navigation pane, click **Approval Center**. Click the **Handled by Me** tab.**** 

    On this tab, you can view the following information about each request that you have handled: object type, grant-to account, workspace, MaxCompute project, tables, and request time.

2.  Click **Details** in the Actions column to view details about a request. The request details include the progress and objects requested.

