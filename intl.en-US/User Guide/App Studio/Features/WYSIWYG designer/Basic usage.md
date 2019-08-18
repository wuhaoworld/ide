# Basic usage {#concept_ov4_dsm_v2b .concept}

This topic describes basic operations in the WYSIWYG designer, including creating a project and building a visual page.

## Create a project {#section_yvz_xsm_v2b .section}

1.  Log on to App Studio. On the Projects page, click **Create Project from Code**.
2.  On the Create Project page, specify **Project Name** and **Project Description**, and set **Runtime Environment** to **appstudio sample template**.
3.  After the configuration is completed, click **Submit**.
4.  Go to the santa/pages directory.
5.  Click any .santa file to go to the WYSIWYG designer.

    You can also right-click **pages** and choose **Create** \> **Template** to develop the page based on a template.


## Build a visual page {#section_zjx_gvm_v2b .section}

The WYSIWYG designer consists of the component menu and operation panel.

-   Component menu

    The component menu lists all components that the WYSIWYG designer presets, including layout components, basic components, form components, chart components, and advanced components.

-   Operation panel

    You can click the corresponding icon on the operation panel to switch to the code mode, configure the navigation, configure a global data flow, revoke or redo an operation, preview the rendering result, or save edits.

-   Visual operation area

    Select a component from the component menu and drag and drop it to the visual operation area.

-   Component property configuration panel

    The component property configuration panel consists of the Properties, Style, and Advanced Settings tabs.


Click the Navigation Settings icon in the upper-right corner of the operation panel to go to the page for configuring the navigation of an app.

On the navigation configuration page, you can configure the public header, sidebars, and menu of the app.

The WYSIWYG designer adds the public header and sidebars to an app by default. You can click the Navigation Settings icon to customize the navigation configuration, for example, hiding the sidebars. The system supports the following configuration:

-   You can set the following parameters for the header:
    -   Logo Image
    -   Title
    -   Menu Items
    -   Enabled
    -   Fix to Page Top
    -   Theme: Valid values: Dark and Light.
-   You can set the following parameters for the sidebars:
    -   Menu Items
    -   Enabled
    -   Enable Folding
    -   Theme: Valid values: Dark and Light.

## Configure a global data flow {#section_lfp_kvm_v2b .section}

For more information, see [Global configuration](intl.en-US/User Guide/App Studio/Features/WYSIWYG designer/Save as template.md#).

-   Configure component properties

    On the Properties tab, you can visually configure component properties.

    Based on the rules for configuring component properties, a visual form is generated on the Properties tab. After you configure component properties in this form, the WYSIWYG designer re-renders the component in the visual operation area based on the new properties. You can view the rendering results of the component with different properties in real time.

-   Configure component styles

    On the Style tab, you can configure the styles of a component.

    A visual panel for configuring common styles is provided on the Style tab. On this panel, you can customize the basic styles of a component, including the layout, text, background, border, and effect.

    After you add or modify the component styles on this tab, the WYSIWYG designer collects all the style settings and re-renders the component in the visual operation area based on the new component style. You can view the component configuration effect in real time.

-   Configure association between components

    On the Advanced Settings tab, you can configure association between components.

    Select a component in the visual operation area and click the Advanced Settings tab. The properties of the selected component are listed on the left of the tab. Click the icon on the right and select the component to be associated to your selected component.

    The properties of the associated component appear on the right of the tab.

-   Select a property, for example, searchParams, in the left property list and connect it to a property, for example, requestParams, in the right property list.

    In this way, any change of the searchParams parameter of the left component is transferred to the requestParams parameter of the right component in real time. This achieves property-based association between the two components.


## Configure the code mode {#section_wfw_1wm_v2b .section}

By using the code mode, you can implement complex interactions in a more advanced way. For more information, see [Code mode](intl.en-US/User Guide/App Studio/Features/WYSIWYG designer/Code mode.md#).

## Save, preview, run, and hot code replacement {#section_ox3_dsp_fhb .section}

For more information, see [Save, preview, run, and hot code replacement](intl.en-US/User Guide/App Studio/Features/WYSIWYG designer/Save, preview, run, and hot code replacement.md#).

