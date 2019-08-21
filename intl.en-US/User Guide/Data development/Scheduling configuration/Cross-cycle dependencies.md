# Cross-cycle dependencies {#concept_188763 .concept}

Cross-cycle dependencies allow nodes to depend on instances of nodes in the last cycle.

DataWorks supports the following types of cross-cycle dependencies:

-   Dependency on instances of child nodes
    -   Node dependency: depends on instances of child nodes in the last cycle. For example, node A has three child nodes, namely, nodes B, C, and D, and node A depends on instances of nodes B, C, and D in the last cycle.
    -   Business scenario: The current node depends on instances of child nodes in the last cycle to cleanse the output tables of the current node and check whether the final result is generated properly.
-   Dependency on the instance of the current node
    -   Node dependency: depends on the instance of the current node in the last cycle.
    -   Business scenario: The current node depends on the data output result of the instance of the current node in the last cycle.
-   Dependency on instances of custom nodes: You need to manually enter the IDs of the nodes on which the current node depends. Separate the IDs with commas \(,\), for example, 12345,23456.
    -   Node dependency: depends on instances of custom nodes in the last cycle.
    -   Business scenario: In the business logic, the current node depends on the proper output of other service data that is not processed by the current node.

**Note:** The difference between cross-cycle dependencies and dependencies in the current cycle lies in that cross-cycle dependencies are displayed as dotted lines in Operation Center.

Before bringing a node offline, you must delete all dependencies of the node so that other nodes can run properly.

Take the xc\_create and xc\_select nodes in a workflow as an example. The following figure shows the dependency between the two nodes.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/162682/156637829345437_en-US.png)

The following figure shows how the dependency is displayed in Operation Center.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/162682/156637829345439_en-US.png)

## Cross-cycle dependencies: instances of child nodes {#section_vmh_yq4_oqm .section}

Node dependency: depends on instances of child nodes in the last cycle. For example, node A has three child nodes, namely, nodes B, C, and D, and node A depends on instances of nodes B, C, and D in the last cycle.

Business scenario: The current node depends on instances of child nodes in the last cycle to cleanse the output tables of the current node. The current node starts to run in the current cycle only when the child nodes were run successfully in the last cycle.

Select Cross-Cycle Dependencies and set Depend On to Instances of Child Nodes for the xc\_create node. The following figure shows how the dependency is displayed in Operation Center.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/162682/156637829456912_en-US.png)

## Cross-cycle dependencies: instances of current node {#section_fq0_wt6_khb .section}

Node dependency: The current node depends on the running status of the instance of the current node in the last cycle. If the current node is not finished in the last cycle, the current node will not run in the current cycle.

Business scenario: The current node depends on the data cleansing result in the last cycle. In this example, Instance Recurrence is set to Hour.

The following figure shows how the dependency is displayed in **Operation Center**.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/162682/156637829556914_en-US.png)

## Cross-cycle dependencies: instances of custom nodes {#section_1hk_qkf_i11 .section}

Node dependency: The output tables of the xc\_information node are not used in the code of the xc\_create node. However, the xc\_create node depends on the data output result of the xc\_information node in the last cycle according to the business logic. That is, the xc\_create node depends on the instance of the xc\_information node in the last cycle.

Business scenario: In the business logic, the xc\_create node depends on proper data output the xc\_information node in the last cycle, but the xc\_create node does not process the output data of the xc\_information node.

For example, the ID of the xc\_information node is 1000374815. Set Depend On to Instances of Custom Nodes and enter the node ID 1000374815 for the xc\_create node.

The following figure shows how the dependency is displayed in **Operation Center**.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/162682/156637829656915_en-US.png)

