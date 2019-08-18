# Code mode {#concept_l3p_3sm_v2b .concept}

By using the code mode, you can implement complex interactions in a more advanced way.

Click the Code Mode icon in the upper-right corner of the operation panel to enable the code mode.

The code area appears on the right of the page.

The WYSIWYG designer uses DSL at the intermediate layer to switch between the visualization mode and code mode. DSL can be considered as a simplified version of React. The DSL syntax is basically the same as the React syntax.

As shown in the code area in the preceding figure, DSL uses a tag to describe a component. The tag properties are the component properties. The property value can be of a simple data type such as a string or a number. The property value can also be an expression. You can enter `state.xxx` to obtain data from the global data flow.

The code mode has the following features:

-   If you drag and drop a component or configure the component properties in the visualization area, the edits are updated in the code in real time.
-   If you edit the code in the code area, the edits are updated in the visualization area in real time.
-   The drag-and-drop operation and component property configuration in the visualization area and code edits in the code area can be converted between each other.

