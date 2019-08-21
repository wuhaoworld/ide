# OSS object inspection {#concept_189375 .concept}

You can use the Object Storage Service \(OSS\) object inspection feature to monitor OSS objects if child tasks depend on that OSS objects are stored to OSS. For example, you can start a task for synchronizing OSS data files to DataWorks only after the OSS data files are generated. In this case, you can use the OSS object inspection feature to monitor the OSS data files.

Inspection objects: OSS objects of all tenants.

1.  In Data Analytics, click the **Create** icon and choose **Control** \> **OSS Object Inspection**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/163479/156637789045563_en-US.png)

2.  In the Create Node dialog box that appears, set the parameters and click **Commit**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/163479/156637789145564_en-US.png)

3.  On the **OSS Object Inspection** page that appears, set the parameters.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/163479/156637789245565_en-US.png)

    |No.|Parameter|Description|
    |---|---------|-----------|
    |1|**OSS Object**|The storage path of the OSS object. You can add a scheduling parameter to the storage path. For more information, see [Parameter configuration](intl.en-US/User Guide/Data development/Scheduling configuration/Parameter configuration.md#).|
    |2|**Timeout**|The timeout period. During the timeout period, DataWorks checks whether the OSS object exists in OSS every five seconds. If the OSS object is not detected before the timeout period ends, the OSS object inspection task fails.|
    |3|**Storage Address**|The storage space of the OSS object. Valid values:     -   **Myself**: detects the OSS object in the storage space of the current tenant.
    -   **Other**: detects the OSS object in the storage space of another tenant.
 ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/163479/156637789345573_en-US.png)

|

    **Note:** 

    -   When the OSS object inspection task is running, it monitors the OSS object through MaxCompute. Make sure that MaxCompute has the required permissions on the OSS bucket. For more information, see [OSS STS mode authorization](../../../../intl.en-US/User Guide/External table/OSS STS mode authorization.md#).
    -   In the development or production environment, the task monitors the OSS object through the access identity of the development or production environment. Make sure that the access identity has the required permissions on the OSS bucket.
4.  Grant MaxCompute the permission to access OSS in the Resource Access Management \(RAM\) console.

    MaxCompute uses RAM and Security Token Service \(STS\) of Alibaba Cloud to resolve security issues of accounts.

    -   If the owners of MaxCompute and OSS are using the same Alibaba Cloud account, you can authorize MaxCompute to access OSS with one click in the RAM console.
    -   If the owners of MaxCompute and OSS are using different Alibaba Cloud accounts, you can authorize MaxCompute to access OSS as follows:
        1.  Create a role in the RAM console.

            Create a role, such as AliyunODPSDefaultRole or AliyunODPSRoleForOtherUser, and set the following policy:

            ``` {#codeblock_bz8_u0p_k8q}
            --The owners of MaxCompute and OSS are using different Alibaba Cloud accounts.
            {
            "Statement": [
            {
            "Action": "sts:AssumeRole",
            "Effect": "Allow",
            "Principal": {
            "Service": [
            "The ID of the Alibaba Cloud account used by the owner of MaxCompute@odps.aliyuncs.com"
            ]
            }
            }
            ],
            "Version": "1"
            }
            ```

        2.  Create the AliyunODPSRolePolicy permission policy that contains the permissions required for accessing OSS.

            ``` {#codeblock_esn_j5h_7n1}
            {
            "Version": "1",
            "Statement": [
            {
            "Action": [
             "oss:ListBuckets",
             "oss:GetObject",
             "oss:ListObjects",
             "oss:PutObject",
             "oss:DeleteObject",
             "oss:AbortMultipartUpload",
             "oss:ListParts"
            ],
            "Resource": "*",
            "Effect": "Allow"
            }
            ]
            }
            --You can also add other permissions as required.
            ```

        3.  Grant the AliyunODPSRolePolicy permission policy to the role.
5.  Go to Operation Center and view the run logs.

    If the following log information is found, the OSS object is not detected:

    ``` {#codeblock_1oc_uh6_chf}
    <Error>
     <Code>NoSuchKey</Code>
     <Message>The specified key does not exist. </Message>
     <RequestId></RequestId>
     <HostId>OSS object</HostId>
     <Key>xc/111.txt</Key>
    </Error>
    ```


