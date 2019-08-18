# Get started {#concept_swz_1x3_bhb .concept}

To build a data portal, engineers need to develop data, build backend services, and develop frontend pages. This topic describes the basic features of App Studio and how to use App Studio.

Originally, DataWorks is mainly used by data engineers to implement offline or streaming data development. As DataWorks becomes increasingly easy to use, many roles such as algorithm engineers, BI analysts, operators, and product managers who are familiar with SQL can use DataWorks to develop data.

App Studio helps different types of users quickly build webpages for data viewing and apps for data query.

## Understand App Studio {#section_vgs_5x3_bhb .section}

-   Top navigation bar

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136608/156610591041851_en-US.png)

    -   **Project** 

        From the Project menu, you can select **Create Project**, **Import Project from Git**, **Open Project**, **Character Set**, and **Project Information**. By selecting Project Information, you can view information about a project, including the project ID, project type, Git repo URL, and creation time.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136608/156610591141852_en-US.png)

    -   **File** 

        From the File menu, you can select **Create File** and **Re-Open Most Recent Files**.

    -   **Edit** 

        From the Edit menu, you can perform common editing operations. To search all the code in the project and open the related file, select Find in Path. For more information, see [Find in Path](intl.en-US/User Guide/App Studio/Features/Code editing/Find in Path.md#).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136608/156610591141854_en-US.png)

    -   **Version** 

        From the Version menu, you can select **Check Out Branch**, **Pull**, **Push**, **View Edits**, **Submit**, **View Log**, and **Connect to Remote Repo**.

        -   **Check Out Branch** 

            In the Check Out Branch dialog box, you can click **+Create Branch** to create a local branch and push it to the remote repo. You can click a local branch and select **checkout** from the shortcut menu on the right to switch to the branch. You can also select **merge** to merge the selected branch to the current branch.

            You can click a remote branch and select **check out as a new local branch** from the shortcut menu on the right to check out the remote branch locally. Then rename the branch. You can also select **merge** to merge the selected branch to the current branch.

        -   **Pull** 

            Select Pull to pull the code of a remote branch to a local branch.

        -   **Push** 

            Select Push to stage edits on a local branch and push the staged code to a remote branch.

        -   **View Edits** 

            Select **View Edits** to view the list of edited files on a local branch in the right pane.

        -   **Submit** 

            Select Submit to submit and stage edits on a local branch. You must enter the commit information.

        -   **View Log** 

            On the View Log tab, you can view all submission records of branches and filter them.

        -   **Connect to Remote Repo** 

            You can associate a new project with a remote repo for version control.

    -   **View** 

        You can select **Toggle Full Screen** and press **Esc** on the keyboard to enter and exit the full screen mode of App Studio, respectively. You can select **Show/Hide Side Bar** and **Show/Hide Status Bar** to show or hide the sidebars and status bar, respectively.

    -   **Debug** 
        -   For a frontend project, you can configure running parameters and add custom images.
        -   For a backend project, App Studio supports Java-based debugging. In addition to configuring running parameters and adding custom images, you can perform many other operations for debugging backend projects. You can also perform full or incremental builds and compile the Main.java file.
    -   **Settings** 

        Before using App Studio, you must specify the SSH key and Git configuration. You can also select Preference to set properties as you like. Currently, you can only set the font size. App Studio will support setting the color, style, theme, and keyboard shortcuts in the future.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136608/156610591141879_en-US.png)

    -   **Help** 

        From the Help menu, you can select Documentation, Keyboard Shortcuts, Version History, and Clear Local Cache.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136608/156610591141880_en-US.png)

    -   **Feedback** 

        From the Feedback menu, you can select Raise Question and Submit Request.

-   Left sidebar
    -   Entry

        To go to the project area, click the icon framed in red in the following figure.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136608/156610591141956_en-US.png)

        To go to the API definition area, click the icon framed in red in the following figure.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136608/156610591241957_en-US.png)

    -   API definition area

        You can click Add API to add an API. In the API list, you can click Generate Code in the Actions column of an API to generate the API class code. In the Generate Code dialog box, you can click the arrow to synchronize the new code on the left to the local code on the right.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136608/156610591241958_en-US.png)

    -   Project area
        -   Folder-related operations

            For a backend project, after you create a file based on the template, some framework code is automatically generated.

        -   File-related operations

            For a frontend project, after you right-click a folder and select Create, the shortcut menu only contains the File option.

            You can rename, copy, or delete a file, view its historical versions submitted in Git, and compare these versions.

-   Editing area
    -   Right-click operations

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136608/156610591241963_en-US.png)

        |Operation|Description|
        |:--------|:----------|
        |**Go to Definition**|Jumps to the definition.|
        |**Peek Definition**|Previews the definition.|
        |**Find All References**|Searches for all references.|
        |**Workspace Symbol**|Searches for a symbol in the project.|
        |**Go to Symbol...**|Jumps to the symbol.|
        |**Generate...**|Generates the code.|
        |**Rename Symbol**|Renames the symbol.|
        |**Change All Occurrences**|Changes the name of all occurrences of a symbol throughout the file.|
        |**Format Document**|Formats the file.|
        |**Cut**|Cuts the file.|
        |**Copy**|Copies the file.|
        |**Command Palette**|Goes to the command palette.|

    -   Code hinting

        ![](images/41964_en-US.gif)

    -   Code completion

        ![](images/41965_en-US.gif)

    -   Smart diagnosis

        ![](images/41966_en-US.gif)

    -   Definition search

        ![](images/41967_en-US.gif)

    -   Reference search

        ![](images/41968_en-US.gif)

    -   Auto import

        ![](images/41969_en-US.gif)

    -   Symbol search

        ![](images/41970_en-US.gif)

    -   Multiple selections

        ![](images/41971_en-US.gif)

    -   Search and replacement
    -   Code formatting

        ![](images/41973_en-US.gif)

    -   Bracket matching
-   Icons in the upper-right corner
    -   Alibaba Coding Guidelines

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136608/156610591241975_en-US.png)

    -   Build

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136608/156610591241976_en-US.png)

        **Note:** You can perform this operation only when you are running or debugging a project.

    -   Run/Debug Configurations

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136608/156610591241978_en-US.png)

    -   Debugging entry

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136608/156610591341981_en-US.png)

        The icons from left to right are respectively used to run, debug, and stop a project.

-   Bottom bar
    -   RUN or DEBUG tab

        If you click the Run or Debug icon for a project, this tab appears, showing the progress and information of the project.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136608/156610591342013_en-US.png)

    -   PROBLEM tab

        If you click the Run or Debug icon for a project that has a problem, this tab appears.

    -   Terminal tab

        When running or debugging a project, you can click the Terminal tab and run bash or vim commands on the ECS instance.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136608/156610591342016_en-US.png)

    -   Version Control tab

        This tab displays the Git history and Git logs.

-   Right sidebar
    -   Runtime

        When running of a project is completed, this tab appears, showing the ECS instance information and access links.

        -   For a backend project, only the backend access link appears.
        -   For a frontend project, only the frontend access link appears.
        -   For a project built by using the WYSIWYG designer, both the frontend and backend access links appear.
    -   Share

        You can invite other users for collaborative coding. Currently, App Studio allows a maximum of eight users to edit the same file of a project online at the same time.

    -   Data

        DataService Studio is an important foundation for running DataStudio and App Studio.

        You can use DataService Studio in App Studio in the following two ways. For more information, see [DataService Studio](intl.en-US/User Guide/App Studio/Features/Access third-party services/DataService Studio.md#).

        -   Use DataService Studio APIs through code or reprocess API results.
        -   Configure DataService Studio as the data source of components in the WYSIWYG designer.
    -   Preview

        For a frontend project, the Preview tab appears on the right sidebar, allowing you to preview the frontend page in real time when running the project.

-   WYSIWYG designer page

    This page appears only for a project built by using the WYSIWYG designer. Go to the santa/pages directory in your project and double-click a .santa file.

    In the component area in the upper-left corner, you can select components as required or enter a component name to search for the component. The icons from left to right in the upper-right corner are respectively used to: switch to the code mode, configure the navigation, configure a global data flow, revoke or redo an operation, preview the rendering result, save the project as a template, or save edits.

    After you drag a table component to the canvas and click the component, the component configuration area appears on the right. You can configure the properties and style of the component or associate it with another component.


## Create a backend project {#section_v2c_gh2_ghb .section}

1.  Create a project based on the sample project.
    1.  Log on to App Studio. On the Projects page, click **Create Project from Code**.
    2.  On the Create Project page, specify **Project Name** and **Project Description**, and set **Runtime Environment** to **springboot sample template**.
    3.  After the configuration is completed, click **Submit**.
2.  Configure running parameters.

    Enter a configuration name, select a main function to be run, select an ECS instance type, and then click **OK**.

    You can click **Add** on the left of the Run/Debug Configurations dialog box to add multiple configurations for running.

3.  Run the project.

    Click the icon framed in red in the following figure to run the project.

    The initial running process takes a longer time because App Studio needs to allocate the ECS instance and initialize the language service. After the running is completed, the Runtime tab appears, showing the access link.

4.  Access the project.

    Click **Open Link** to access the project.

    Append /testapi to the link and refresh the page.


## Create a frontend project {#section_sm5_gn2_ghb .section}

App Studio provides complete frontend development capabilities that allow you to develop frontend projects in the same way as in a local IDE. Without the need to master or understand any new concepts, you can create frontend projects in App Studio and develop HTML, CSS, JavaScript, and React files in a way that you are familiar with.

1.  Create a project based on the sample project.
    1.  Log on to App Studio. On the Projects page, click **Create Project from Code**.
    2.  On the Create Project page, specify **Project Name** and **Project Description**, and set **Runtime Environment** to **springboot sample template**.
    3.  Enter the project name and description and click **OK**.
2.  Configure running parameters.

    Select an ECS instance type and specify the port number as required. You can use the default configuration unless otherwise required. Then, click **OK**.

3.  Run the project.

    Click the Run icon in the upper-right corner to run the project. Currently, you can run the `tnpm start` command to start frontend projects. You can seamlessly run projects with the webpack-dev-server set up.

    During project running, you can view the dependency installation and app startup logs. After the project running is completed, the Preview tab appears on the right sidebar. You can edit and save the code in real time. The edited code takes effect immediately.

4.  Access the project.

    Click the arrow next to the access link to open the project. In App Studio, you can edit and develop frontend projects in the same way as in a local IDE. App Studio supports code completion, function signature, refactoring, and redirection for HTML, CSS, LESS, SCSS, JavaScript, TypeScript, JSX, and TSX files. In addition, you can develop frontend projects based on templates without the need to build any environment or download any dependency.


## Create a frontend project by using the WYSIWYG designer {#section_agk_qh1_hhb .section}

1.  Create a project based on the sample project.
    1.  Log on to App Studio. On the Projects page, click **Create Project from Code**.
    2.  On the Create Project page, specify **Project Name** and **Project Description**, and set **Runtime Environment** to **appstudio sample template**.
    3.  After the configuration is completed, click **Submit**.
2.  Open the home.santa file.

    Go to the santa/pages directory. The home.santa and list.santa files are stored in this directory.

    1.  Double-click the home.santa file to open it. A simple report page appears.
    2.  Select a component. The component configuration pane appears on the right.
    3.  Click the Data Source field. The API list appears.

        App Studio provides some DataService Studio APIs for your quick start. You can click **+Add DataService Studio API** to add APIs in DataService Studio or view the APIs of the current component in the API Route column.

        **Note:** You can remove the existing APIs and customize APIs to experience the data source configuration of the component. You can also change the style of the component.

3.  Add a component and configure APIs.

    1.  Choose Charts \> Bar and drag a bar chart to the canvas.
    2.  Select the component. In the component configuration pane, click the Data Source field.
    3.  In the API list, click **Select** next to the seventh API. The API is configured.
    4.  No result is returned for the component because you have not specified the request parameters and columns to be returned.

        Click Details next to the seventh API to view the request and response parameters.

        **Note:** You are not allowed to access this page because the project is a sample project. We recommend that you use your own account to create DataService Studio APIs when building a project by using the WYSIWYG designer.

    5.  Configure the component.
    After the configuration is completed, the data appears in the component.

4.  Open the list.santa file.

    You can use the WYSIWYG designer of App Studio to create both reports and apps.

    Double-click the list.santa file to open it. The file includes a simple data app consisting of components such as icons, links, videos, lists, and search box. For more information, see [Overview of the WYSIWYG designer](intl.en-US/User Guide/App Studio/Features/WYSIWYG designer/Overview of the WYSIWYG designer.md#).

5.  Configure the navigation.

    More than one page may exist in your created app. Therefore, you need to configure the navigation to navigate between pages.

    Click the Navigation Settings icon in the upper-right corner. The navigation configuration page appears.

6.  Configure running parameters. For more information, see the procedure for creating a backend project.
7.  Run the project.

    Click the Run icon in the upper-right corner. After the project running is completed, the Runtime tab appears. You can click the frontend link to access the project.


