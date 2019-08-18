# DataOS API {#concept_264222 .concept}

App Studio provides the DataOS API and DataService Studio API. This topic describes the functions, request parameters, and response parameters of the DataOS API operations, and provides guidance on configuring and using the DataOS API.

## CheckMetaTable {#section_inf_zom_lgc .section}

-   Function: checks whether a table exists.
-   Request: The tableGuid parameter is required.
-   Syntax: `odps.<project>.<table>`.
-   Response: true or false.
-   Example:
    -   Request: `request.setTableGuid("odps.autotest.daily_test");`
    -   Response: `{"requestId":"0b85c9d915548770462378104e","errMsg":"success","errCode":0,"data":true}`

## GetMetaDB {#section_h65_hge_7zt .section}

-   Function: gets the information of a MaxCompute project.
-   Request: The project GUID is required.
-   Syntax: `odps.<project>`.
-   Response: The details of the project are returned, including the parameters listed in the following table.

    |Parameter|Description|
    |---------|-----------|
    |appGuid|The GUID of the project.|
    |project|The name of the project in English.|
    |projectNameCn|The name of the project in Chinese.|
    |comment|The comments on the project.|
    |ownerId|The ID of the project owner.|
    |createTime|The time when the project was created.|
    |modifyTime|The time when the project was modified.|

-   Example:
    -   Request: `request.setDbGuid("odps.autotest");`
    -   Response:

        ``` {#codeblock_u04_r1k_ual}
        {
            "requestId": "0bfaefec****61500671805e",
            "errMsg": "success",
            "errCode": 0,
            "data": {
                "appGuid": "odps.meta",
                "projectName": "meta",
                "projectNameCn": "ODPS metadata",
                "comment": "",
                "ownerId": "13101879118",
                "createTime": "2014-02-18",
                "modifyTime": "2018-04-16"
          }
        }
        ```


## GetMetaTable {#section_yep_nnv_i3p .section}

-   Function: gets the information of a MaxCompute table.
-   Request: The tableGuid parameter is required.
-   Syntax: `odps.<project>.<table>`.
-   Response: The details of the table are returned, including the parameters listed in the following table.

    |Parameter|Description|
    |---------|-----------|
    |appGuid|The GUID of the project.|
    |tableGuid|The GUID of the table.|
    |tableName|The name of the table.|
    |id|The ID of the database.|
    |ownerId|The ID of the project owner.|
    |hasPart|Indicates whether the table is partitioned. The value 1 indicates that the table is partitioned. The value 0 indicates that the table is not partitioned.|
    |dataSize|The size of data in the table.|
    |createTime|The time when the table was created.|
    |lastDdlTime|The last time when a Data Definition Language \(DDL\) statement was executed for the table.|
    |lastModifyTime|The last time when the table was modified.|

-   Example:
    -   Request: `request.setTableGuid(tableGuid);`
    -   Response:

        ``` {#codeblock_o7w_uto_r2w}
        {
            "requestId": "0b8906da****8175861e",
            "errMsg": "success",
            "errCode": 0,
            "data": {
                "appGuid": "odps.meta",
                "tableGuid": "odps.meta.m_table",
                "tableName": "m_table",
                "id": 64809,
                "OwnerId": "dp-base-odps@aliyun-test.com",
                "hasPart": 1,
                "dataSize": 49397610904693,
                "createTime": "2014-12-10 21:20:23",
                "lastDdlTime": "2017-04-18 10:10:06",
                "lastModifyTime": "2019-04-09 20:24:08"
          }
        }
        ```


## ListMetaTableColumn {#section_ynk_yud_nbf .section}

-   Function: gets the column information of a MaxCompute table.
-   Request: The tableGuid parameter is required.
-   Syntax: `odps.<project>.<table>`.
-   Response: The details of columns in the table are returned, including the parameters listed in the following table.

    |Parameter|Description|
    |---------|-----------|
    |appGuid|The GUID of the project.|
    |tableGuid|The GUID of the table.|
    |tableName|The name of the table.|
    |columnGuid|The GUID of a column. Syntax: `odps.<project>.<table>.<col>`.|
    |columnName|The name of the column.|
    |columnType|The type of the column.|
    |seqNumber|The sequence number of the column, which starts from 1.|
    |isPartitionCol|Indicates whether the column is partitioned. The value 0 indicates that the column is not partitioned. The value 1 indicates that the column is partitioned.|
    |comment|The comments on the project.|
    |safeLevel|The safety level of the project.|

-   Example:
    -   Request: `request.setTableGuid(tableGuid);`
    -   Response:

        ``` {#codeblock_xmb_x6p_8kl}
        {
            "requestId": "0b8906d*****9796824e",
            "errCode": 0,
            "errMsg": "success",
            "columnList": [{
                "appGuid": "odps.meta",
                "tableGuid": "odps.meta.m_table",
                "tableName": "m_table",
                "columnGuid": "odps.meta.m_table.project_name",
                "columnName": "project_name",
                "columnType": "string",
                "seqNumber": 1,
                "isPartitionCol": 0,
                "comment": "project name",
                "safeLevel": "C2"
          }, 
        {
            "appGuid": "odps.meta",
            "tableGuid": "odps.meta.m_table",
            "tableName": "m_table",
            "columnGuid": "odps.meta.m_table.name",
            "columnName": "name",
            "columnType": "string",
            "seqNumber": 2,
            "isPartitionCol": 0,
            "isPrimaryKey": 0,
            "isNullable": 0,
            "comment": "table name",
            "safeLevel": "C2"
          } ... ]
        }
        ```


## ListMetaTablePartition {#section_xoi_ivr_73a .section}

-   Function: gets the partition information of a MaxCompute table.
-   Request:

    |Parameter|Description|
    |---------|-----------|
    |tableGuid|The GUID of the table. Syntax: `odps.<project>.<table>`.|
    |pageNum|The number of the page to return.|
    |pageSize|The number of entries to return on each page.|

-   Response: The partition details of the table are returned, including the parameters listed in the following table.

    |Parameter|Description|
    |---------|-----------|
    |appGuid|The GUID of the project.|
    |tableGuid|The GUID of the table.|
    |tableName|The name of the table.|
    |partitionGuid|The GUID of a partition. Syntax: `odps.<project>.<table>.<partition>`.|
    |partitionName|The name of the partition.|
    |createTime|The time when the partition was created.|
    |modifyTime|The time when the partition was modified.|
    |dataSize|The size of data in the partition.|
    |records|The number of entries in the partition.|
    |pageNum|The number of the page that is returned.|
    |pageSize|The number of entries on the page that is returned.|
    |totalNum|The total number of entries.|

-   Response example:

    ``` {#codeblock_je3_rax_dxv}
    {
        "requestId": "0baf3e0*****5025570e",
        "errCode": 0,
        "errMsg": "success",
        "pageNum": 1,
        "pageSize": 10,
        "totalNum": 1101,
        "partitionList": [{
            "appGuid": "odps.meta",
            "tableGuid": "odps.meta.m_table",
            "tableName": "m_table",
            "id": 168504514,
            "partitionGuid": "odps.meta.m_table.ds\u003d20190408",
            "partitionName": "ds\u003d20190408",
            "createTime": "2019-04-08 13:59:52",
            "modifyTime": "2019-04-08 19:54:51",
            "dataSize": 273248012568,
            "records": 720503170
      } ... ]
    }
    ```


## SearchMetaTables {#section_dpm_dcp_k4y .section}

-   Function: performs fuzzy search in a table.
-   Request:

    |Parameter|Description|
    |---------|-----------|
    |keyword|The keyword of the table name.|
    |pageNum|The number of the page to return.|
    |pageSize|The number of entries to return on each page.|

-   Response:

    |Parameter|Description|
    |---------|-----------|
    |appGuid|The GUID of the project.|
    |tableGuid|The GUID of the table.|
    |tableName|The name of the table.|
    |ownerId|The ID of the project owner.|
    |createTime|The time when the table was created.|
    |lastDdlTime|The last time when a DDL statement was executed for the table.|
    |lastModifyTime|The last time when the table was modified.|

-   Example:
    -   Request: `request.setKeyword("test");`
    -   Response:

        ``` {#codeblock_udq_ia2_3k7}
        {
            "message": null,
            "code": 200,
            "success": true,
            "data": {
                "requestId": "0be41b***22277597924e",
                "errCode": 0,
                "errMsg": "success",
                "pageNum": 1,
                "pageSize": 2,
                "totalNum": 5000,
            "data": [{
                "appGuid": null,
                "tableGuid": "odps.ant_p13n.finance_newsrec_tab_dataset_ds",
                "tableName": "finance_newsrec_tab_dataset_ds",
                "createTime": "2018-07-06 16:24:41",
                "lastModifyTime": "2019-04-26 10:49:23",
                "lastDdlTime": null,
                "lastAccessTime": null,
                "ownerId": "163585"
            }, 
            {
                "appGuid": null,
                "tableGuid": "odps.tbcdm.dws_tm_itm_cate_food_ftr_test_cm",
                "tableName": "dws_tm_itm_cate_food_ftr_test_cm",
                "createTime": "2017-11-23 17:06:18",
                "lastModifyTime": "2019-04-26 20:34:12",
                "lastDdlTime": null,
                "lastAccessTime": null,
                "ownerId": "108292"
            }]
          },
            "timestamp": 1556452227875,
            "sessionId": null
        }
        ```


## Call the DataOS API {#section_9u5_cmo_ub8 .section}

Configure the pom file as follows:

``` {#codeblock_aq5_ceb_36y}
<! --DataOS Start-->
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-java-sdk-dataworks-enterprise-ultimate</artifactId>
    <version>0.0.3</version>
</dependency>

<! -- JSON 2.8.5 or later -->
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-java-sdk-core</artifactId>
    <version>4.4.0</version>
</dependency>
<! --DataOS End-->
```

Configure the hosts file as follows:

``` {#codeblock_646_ejd_3v7}
# from src/main/resources/application.properties
# dataos api configuration
dataworks.dataos.auth.accessId= <indicate user accessid, refer to aliyun>
dataworks.dataos.auth.accessKey= <indicate user accessid, refer to aliyun>
dataworks.dataos.region=cn-shanghai
dataworks.dataos.endpoint=dataworks-ee-ue-share.cn-shanghai.aliyuncs.com
dataworks.dataos.product=dataworks-enterprise-ultimate
```

The Java code is as follows. When creating IClientProfile, you must specify the AccessKey ID and AccessKey Secret of your Alibaba Cloud account. For more information, see the following FAQ.

``` {#codeblock_ndx_miw_uxk}
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.dataworks.model.v20171212.CheckMetaTableRequest;
import com.aliyuncs.dataworks.model.v20171212.CheckMetaTableResponse;
import com.aliyuncs.dataworks.model.v20171212.GetMetaDBRequest;
import com.aliyuncs.dataworks.model.v20171212.GetMetaDBResponse;
import com.aliyuncs.dataworks.model.v20171212.GetMetaTableRequest;
import com.aliyuncs.dataworks.model.v20171212.GetMetaTableResponse;
import com.aliyuncs.dataworks.model.v20171212.ListMetaTableColumnRequest;
import com.aliyuncs.dataworks.model.v20171212.ListMetaTableColumnResponse;
import com.aliyuncs.dataworks.model.v20171212.ListMetaTablePartitionRequest;
import com.aliyuncs.dataworks.model.v20171212.ListMetaTablePartitionResponse;
import com.aliyuncs.dataworks.model.v20171212.SearchMetaTablesRequest;
import com.aliyuncs.dataworks.model.v20171212.SearchMetaTablesResponse;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.profile.DefaultProfile;
import com.aliyuncs.profile.IClientProfile;
import com.google.gson.Gson;

public class Simple {
  IAcsClient client = null;

  @org.junit.Test
  public void testCheckMetaTable() throws ServerException, ClientException {
    String tableGuid = "odps.meta.m_table";

    CheckMetaTableRequest request = new CheckMetaTableRequest();
    request.setTableGuid(tableGuid);
    CheckMetaTableResponse response = client.getAcsResponse(request);
    System.out.println(new Gson().toJson(response));
  }

  @org.junit.Test
  public void testGetProject() throws ServerException, ClientException {
    String appGuid = "odps.meta";

    GetMetaDBRequest request = new GetMetaDBRequest();
    request.setDbGuid(appGuid);
    GetMetaDBResponse getMetaDBResponse = client.getAcsResponse(request);
    System.out.println(new Gson().toJson(getMetaDBResponse));
  }

  @org.junit.Test
  public void testGetPartitions() throws ServerException, ClientException {
    String tableGuid = "odps.meta.m_table";

    ListMetaTablePartitionRequest request = new ListMetaTablePartitionRequest();
    request.setTableGuid(tableGuid);
    request.setPageNum(1);
    request.setPageSize(10);
    ListMetaTablePartitionResponse response = client.getAcsResponse(request);
    System.out.println(new Gson().toJson(response));
  }

  @org.junit.Test
  public void testSearchTables() throws ServerException, ClientException {
    SearchMetaTablesRequest request = new SearchMetaTablesRequest();
    request.setKeyword("test");
    request.setPageNum(1);
    request.setPageSize(10);
    SearchMetaTablesResponse response = client.getAcsResponse(request);
    System.out.println(new Gson().toJson(response));
  }

    @org.junit.Test
    public void testGetColumns() throws ServerException, ClientException {
        String tableGuid = "odps.meta.m_table";

        ListMetaTableColumnRequest request = new ListMetaTableColumnRequest();
        request.setTableGuid(tableGuid);
        ListMetaTableColumnResponse response = client.getAcsResponse(request);
        System.out.println(new Gson().toJson(response));
    }

  @org.junit.Test
  public void testGetTable() throws ServerException, ClientException {
    String tableGuid = "odps.meta.m_table";

    GetMetaTableRequest request = new GetMetaTableRequest();
    request.setTableGuid(tableGuid);
    GetMetaTableResponse response = client.getAcsResponse(request);
    System.out.println(new Gson().toJson(response));
  }

  public Simple() throws ClientException {
    IClientProfile profile = DefaultProfile.getProfile("cn-hangzhou", "<!!!! id>",
        "<!!! key>");
    DefaultProfile.addEndpoint("cn-hangzhou", "cn-hangzhou", "dataworks", "dataworks-share.aliyuncs.com");
    client = new DefaultAcsClient(profile);
  }

}
```

## FAQ {#section_3le_fib_x5t .section}

-   Why does the API operation calling fail, with the following information returned?

    ``` {#codeblock_ivd_ilv_wa7}
    Exception in thread "main" com.aliyuncs.exceptions.ClientException: InvalidApi.NotFound : Specified api is not found, please check your url and method.
    RequestId : B081CCF1-9F19-473E-9B99-68F202E7572B
    ```

    You do not have the permission to call the API operation.

-   How do I query the AccessKey ID and AccessKey Secret?

    In the Alibaba Cloud console, click your account in the upper-right corner and select **accesskeys** from the drop-down list. Then, the AccessKey ID and AccessKey Secret appear.


