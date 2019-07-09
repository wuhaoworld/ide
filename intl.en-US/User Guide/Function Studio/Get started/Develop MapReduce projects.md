# Develop MapReduce projects {#concept_td3_c1j_5gb .concept}

After a project is created, the framework code is automatically generated for the project, based on which you can create MapReduce tasks. This topic takes the WordCount sample code as an example to describe how to perform the test and publish the project from the very beginning.

## Create projects {#section_qs2_wfk_5gb .section}

1.  In the top navigation bar, choose **Project** \> **Create Project**.
2.  In the Create Project dialog box, set parameters.

    In the specified MaxCompute workspace cdo\_datax, create a project named wordcountDemo, and select **UDFJava Project** as the project template.

3.  Click **OK**.

## Develop projects {#section_tc2_2kk_5gb .section}

The mapred package comes with the MapReduce sample code of WordCount. The sample code is used to count words in an input table and write the statistical result to an output table. The input table and output table are different tables. For more information, see [MapReduce](../../../../intl.en-US/User Guide/MapReduce/Summary/MapReduce.md#).

## Debug projects {#section_asw_clk_5gb .section}

Currently, you cannot debug MapReduce projects in Function Studio. To debug a MapReduce project, you must publish the code to the DataWorks development environment, and then verify the logic in DataWorks.

**Note:** Currently, Function Studio only allows you to write, compile, and package code.

## Publish projects {#section_d4g_qlk_5gb .section}

1.  Function Studio allows you to compile and package the code and publish it to the DataWorks development environment.
    1.  Click the **Publish** icon and then select **Submit Resource to Development Environment**.
    2.  In the **Submit Resource to Development Environment** dialog box, set parameters.

        |Parameter|Description|
        |:--------|:----------|
        |**Target Workspace**|The target workspace in which you publish the JAR package. The target workspace must be the same as the workspace where you create the DataWorks compute node of the ODPS MR type in step 2. In this example, the target workspace is cdo\_datax.|
        |**Target Workflow**|The target workflow.|
        |**Resource**|You can specify the resource name, which is referenced in the subsequent compute node scripts.|
        |**Force Overwrite**|The project name can be the same as the name used in the previous publish. If you select **Force Overwrite**, the new name is used.|

    3.  Click **OK**. The code is published to the DataWorks development environment.

        A message appears, indicating whether the code is published successfully.

2.  Create a compute node of the ODPS MR type in DataWorks for testing.
    1.  Open the DataWorks workspace named cdo\_datax, and create a compute node of the ODPS MR type.
    2.  The information in the red box of the following figure must be added to the script of the compute node. Currently, you must manually replace some variables in the script with those in the JAR package.

        **Note:** Replace the following variables in the script with those in the JAR package that you published in Function Studio and generate the final code:

        -   jar -resources: Replace it with the name of the JAR package that you published in Function Studio.
        -   -classpath: Replace it with the path of the JAR package in DataWorks.
        -   Separate the parameters of the main method of a class by space.
    3.  Click the target workflow, and select **Resource** to view the information of the JAR package that you published in Function Studio and replace relevant information in the script with that in the JAR package.

        -   The name of the JAR package is WordCountDemo\_1.0.0.jar, corresponding to -resource in the script.
        -   Right-click the JAR package and choose **View Change History**. The path of the JAR package is `http://schedule@{env}inside.cheetah.alibaba-inc.com/scheduler/res?id=106342493`, corresponding to -classpath in the script.
        The final script:

        ``` {#codeblock_rz6_3lt_a6r}
        # Manually replace relevant information in the script with that in the JAR package. The final script is generated.
        jar -resources WordCountDemo_1.0.0.jar
        -classpath http://schedule@{env}inside.cheetah.alibaba-inc.com/scheduler/res?id=106342493
        com.alibaba.dataworks.mapred.WordCount wordcount_demo_input wordcount_demo_output
        ```

    4.  Create a test table and prepare test data.

        After the data is prepared, run the script in the development environment.

        Now, the test of WordCount in the development environment has been completed. The compute node, JAR package, and input and output tables of WordCount are all in the development environment. Therefore, you need to publish them to the production environment.

3.  Publish the resource package, data tables, and nodes to the production environment of DataWorks.
    1.  Commit the code of the compute node.
    2.  Configure the publish items.
    3.  On Publish Task page, select the JAR package and node that you want to publish and click Publish in the Actions column.
    4.  Publish the tables.
    5.  On the Operation Center tab page, perform testing for the MapReduce project online.

        The log indicates that the project has run successfully.


Function Studio allows you to write, compile, and publish the code to a DataWorks compute node. You must manually generate a compute node in DataWorks, and run the compute node in the development environment and production environment separately.

