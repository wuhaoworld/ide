# Create a custom node type {#concept_ypb_gr3_pgb .concept}

The Configure Custom Node Type page consists of three sections: Basic Information, Interaction, and Wrapper.

1.  On the DataStudio page, choose **Node Config** \> **Custom Node Types**.
2.  Click **Create** in the upper-right corner.
3.  Specify the parameters in the **Basic Information** section.

    |Parameter|Description|
    |:--------|:----------|
    |**Name**|Name the node type. The name cannot be changed after the node type is created. Each node type has a unique name within the workspace. The name is up to 20 characters in length, and can only contain letters, spaces, and underscores \(\_\).|
    |**Tabs**|You can select Ad-Hoc Query, Data Analytics, and Manually Triggered Workflows.|
    |**Folder**|You can select Data Integration or Data Analytics.|

4.  Specify the parameters in the **Interaction** section.

    |Parameter|Description|
    |:--------|:----------|
    |**Shortcut Menu**|     -   The following options are selected by default: Rename, Move, Clone, Steal Lock, View Versions, Locate in Operation Center, Delete, and Submit for Review.
    -   You can also select Send to DataWorks Desktop \(Shortcut\).
 |
    |**Tool Bar**|     -   The following options are selected by default: Save, Commit, Commit and Unlock, Steal Lock, Run, Show/Hide, Run with Arguments, Stop, Reload, Run Smoke Test in Development Environment, View Smoke Test Log in Development Environment, Run Smoke Test, View Smoke Test Log, Go to Operation Center of Development Environment, and Format.
    -   You can also select Precompile.
 |
    |**Editor Type**|You can select **Editor Only** or **Data Source Selection Section and Editor**.|
    |**Right-Side Bar**|     -   The Properties and Versions options are selected by default.
    -   You can also select Lineage and Code Structure.
 |
    |**Auto Parse Option**|If you enable Auto Parse Option, the Auto Parse option is displayed in the Properties tab. Otherwise, it is not displayed. If you set Auto Parse to Yes for a node, the input and output of the node is automatically parsed from the code.|

5.  Specify the parameters in the **Wrapper** section.
    -   The following table describes the parameters you need to specify if you set the editor type to **Editor Only**.

        |Parameter|Description|
        |:--------|:----------|
        |**Wrapper**|Select a wrapper that has been deployed.|
        |**Editor Language**|You can select JSON or ODPS SQL.|
        |**Use MaxCompute as Engine**|Select Yes if your wrapper uses MaxCompute as the compute engine. Select No in other scenarios. This parameter is set to Yes by default.|

    -   The following table describes the parameters you need to specify if you set the editor type to **Data Source Selection Section and Editor**.

        |Parameter|Description|
        |:--------|:----------|
        |**Wrapper**|Select a wrapper that has been deployed.|
        |**Editor Language**|You can select JSON or ODPS SQL.|
        |**Connection Type**|Select the type of connections.|

6.  Click **Save and Exit** to create the custom node type. Then, you can use the custom node type that is created.

