# Delete a node {#concept_t4m_wnp_pgb .concept}

In some scenarios, you need to delete a node from the development or production environment.

## Delete a node from the development environment {#section_alt_c4p_pgb .section}

1.  Log on to the DataWorks console and go to the Data Analytics page.
2.  Search by node type and keyword for the node to be deleted.
3.  Right-click the node and select **Delete**. The node is deleted from the development environment.

## Delete a node from the production environment {#section_fvq_zpp_pgb .section}

To delete a node from the production environment, you need to delete the node from the development environment and deploy the deletion of the node.

**Note:** Before deleting a node from the production environment, you need to remove its dependencies with child nodes. Otherwise, a message appears, indicating that the node to be deleted has child nodes and cannot be deleted.

To remove dependencies between a node and its child nodes, follow these steps:

1.  Find each child node of the target node. You can view the dependencies of the target node in the workflow kanban.
2.  On the configuration tab of a child node, click Properties on the right-side bar, and change the parent node. Alternatively, delete the child node.

If a message appears indicating that the child node has next-level child nodes, repeat these steps to remove the dependencies.

1.  Delete a node from the development environment.

    For more information, see the section provided above.

2.  Create a deploy task for the deleted node.

    **Note:** Only administrators and administration experts can deploy nodes. If you are using an account with another role, contact an administrator or administration expert to deploy the nodes.

    1.  After deleting the node, click **Deploy** in the upper-right corner.
    2.  On the Create Deploy Task page, select the node.
    3.  Click **Deploy Selected**.
3.  Start the deploy task.

    On the Deploy Tasks page, click the Deploy button in the upper-right corner. In the Start Task dialog box that appears, click **Deploy** to deploy the node deletion.


