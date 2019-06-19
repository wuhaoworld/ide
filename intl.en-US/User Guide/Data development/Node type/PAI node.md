# PAI node {#concept_qfy_kc4_yfb .concept}

Machine Learning Platform for Artificial Intelligence \(PAI\) nodes are used to call tasks created on PAI and schedule production activities based on the node configuration. PAI nodes can be added to DataWorks only after PAI experiments are created on PAI.

## Create a PAI experiment {#section_flr_4c4_yfb .section}

Only experiments that can be found on PAI can be loaded into PAI nodes.

## Create a PAI node {#section_qlb_xc4_yfb .section}

Follow the instructions in the preceding section to create a PAI experiment. In this example, the experiment name is **Heart Disease Prediction\_4294**. Then, create a PAI node in DataWorks. The procedure is as follows:

1.  Select a [Business flow](intl.en-US/User Guide/Data development/Business flow/Business flow.md#) you created, right-click **Algorithm** and choose **Create Algorithm Node** \> **PAI**.
2.  Enter the node name.
3.  Select a PAI experiment you created on PAI and load it.

    After the experiment is loaded, click **Edit in PAI Console** or directly submit the experiment.


