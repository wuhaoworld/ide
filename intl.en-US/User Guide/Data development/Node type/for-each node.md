# for-each node {#concept_183549 .concept}

This topic describes how to use a for-each node to repeat a loop twice and display the loop count.

## Create a workflow {#section_sj5_17z_kmo .section}

1.  On the DataStudio page, click **Data Analytics** in the left-side navigation pane. Move the pointer over the Create icon and choose **Control** \> **for-each**.
2.  In the Create Node dialog box that appears, set the parameters and click **Commit**.
3.  In the created workflow, create an assignment node as the parent node of the for-each node.

    The assignment node is a SHELL node. The sample code for the node is as follows:

    ``` {#codeblock_9ye_wvg_5xb}
    echo 'this is name,ok';
    ```

    The outputs parameter is the default output parameter of the assignment node.


**Note:** 

-   The start and end nodes of the for-each node have fixed logic and cannot be edited.
-   After modifying the code for the SHELL node of the for-each node, save the modification. You are not prompted to save the modification when submitting the node. If you do not save the modification, the latest code cannot be updated in time.

The code for the SHELL node is as follows:

``` {#codeblock_q7w_51t_ksy}
echo ${dag.loopTimes} ----Displays the loop count.
```

A for-each node supports the following environment variables:

-   $\{dag.foreach.current\}: the current data row.
-   $\{dag.loopDataArray\}: the input dataset.
-   $\{dag.offset\}: the offset of the loop count to 1.
-   $\{dag.loopTimes\}: the loop count, whose value equals to the value of $\{dag.offset\} plus 1.

``` {#codeblock_e20_ayj_czj}
// Compare the code of the SHELL node with that of a common for loop.
data=[]  // It is equivalent to ${dag.loopDataArray}.
// i is equivalent to ${dag.offset}.
for(int i=0;i<data.length;i++) {
  print(data[i]);  // data[i] is equivalent to ${dag.foreach.current}.
}
```

The $\{dag.loopDataArray\} parameter is the default input parameter of the for-each node. Set this parameter to the value of the outputs parameter of the parent node. If you do not set this parameter, an error occurs when you submit the node.

Click the Submit icon. On the O&M page that appears, check the running result.

