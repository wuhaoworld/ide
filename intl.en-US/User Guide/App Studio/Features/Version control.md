# Version control {#concept_as5_pl2_v2b .concept}

App Studio integrates general Git services. This topic describes how to use VCS-Git in App Studio.

## Create a project and associate it with Git {#section_bmh_flf_v2b .section}

1.  Create a project.
2.  Enter basic user information.

    Before associating the project with Git, you must enter basic user information. Click **Settings** in the top navigation bar and select SSH Key. Generate an SSH key and add it to the public key list of the account that owns the Git repo as prompted.

    **Note:** The new project is not associated with Git by default. To use Git, associate the current project with your Git repo.

3.  Create a Git repo.
4.  Obtain the HTTPS URL of the current repo.
    1.  Click **HTTPS**. The HTTPS URL of the current repo appears.
    2.  Click the Copy icon next to the HTTPS URL to copy it to the clipboard.
5.  Associate the project with the Git repo.
    1.  In the top navigation bar, choose **Version** \> **Connect to Remote Repo**.
    2.  In the Connect to Remote Repo dialog box, enter the HTTPS URL of the Git repo and click **Submit**.
    3.  After the association is completed, the version control icon appears in the left sidebar of App Studio.
    4.  In the top navigation bar, choose **Version** \> **Push** to push the local code to the remote repo.

## Entry to Git-related operations {#section_s3f_pql_v2b .section}

You can click the version control icon in the left sidebar or click Version in the top navigation bar and select options to perform Git-related operations.

## Git control panel {#section_i5r_zql_v2b .section}

The file editing status is dynamically updated on the Git control panel.

You can perform basic Git-related operations, such as `git add, git rm, git commit, and git revert`, on the Git control panel.

## Basic Git operations {#section_zvd_ndm_v2b .section}

Edited files are listed on the Git panel, including the file names and paths. The basic operations that are supported are displayed on the right.

As shown in the preceding figure, the supported operations and file icons are marked by the red boxes.

-   **Source Code: Git** 

    You can perform the commit, refresh, pull, and push operations.

    -   Commit: Click ![commit](images/9680_zh-US.png) and select Commit & Push.
    -   Refresh: Click ![refresh](images/9681_zh-US.png) to refresh the current control panel. This operation is equivalent to running the git status command and refreshing the page.
    -   Pull and push: Click ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17729/15661065569682_en-US.png) and select **Pull** or **Push** as required.
-   **Save Edits** 
    -   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17729/15661065569683_en-US.png): discards all edits. This operation is equivalent to running the git reset command.
    -   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17729/15661065569684_en-US.png): indicates the number of files.
    -   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17729/15661065569685_en-US.png): indicates that the file is edited.
-   **Modify** 
    -   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17729/15661065569686_en-US.png): discards all edits.
    -   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17729/15661065569687_en-US.png): adds all files to the cache. This operation is equivalent to running the git add command.
    -   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17729/15661065569684_en-US.png): indicates the number of files.
    -   The following operations can be performed for the listed files:
        -   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17729/15661065569686_en-US.png): discards all edits.
        -   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17729/15661065569687_en-US.png): stages all edits.
        -   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17729/15661065579688_en-US.png): indicates that the file is edited.

**Note:** 

-   The logic of the Git client is the same. You must perform the push operation so that the local code is pushed to the remote repo.
-   Similarly, you must perform the pull operation so that the remote code is pulled to the local repo.

## Manage branches {#section_l4q_tfm_v2b .section}

Open the branch management window. Click the branch name in the status bar at the bottom of the page. The branch management window appears.

## Create a local branch {#section_i3g_cgm_v2b .section}

After a branch is created, the page of the new branch appears.

## Create, switch, and merge branches {#section_um2_ggm_v2b .section}

After a local branch is created, it can be directly pushed to the remote repo. The name of the local branch is the same as that of the remote one.

## Show Git history {#section_kcv_5p4_fhb .section}

You can right-click a file and choose **Git** \> **Show History** to view its Git history. You can compare the differences between the specific commit version and the current version.

## View Git logs {#section_pfx_qgm_v2b .section}

In the top navigation bar, choose **Version** \> **View Log**. On the Log tab, you can view the message, time, and committer of the submitted logs. You can also filter the submitted logs by message, branch, committer, and time.

