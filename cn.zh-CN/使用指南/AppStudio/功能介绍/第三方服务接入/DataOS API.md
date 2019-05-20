# DataOS API {#concept_264222 .concept}

本文将为您介绍DataOS API的功能、输入、输出等详情，以及如何进行配置使用。

## CheckMetaTable {#section_inf_zom_lgc .section}

-   功能：判断table是否存在。
-   输入：tableGuid（必选）。
-   格式：`odps.<project>.<table>`。
-   输出：true/false。
-   示例如下：
    -   输入：`request.setTableGuid("odps.autotest.daily_test");`
    -   输出：`{"requestId":"0b85c9d915548770462378104e","errMsg":"success","errCode":0,"data":true}`

## GetMetaDB {#section_h65_hge_7zt .section}

-   功能：获取MaxCompute项目的信息。
-   输入：项目GUID（必选）。
-   格式：`odps.<project>`。
-   输出：项目详情。

    |字段|描述|
    |--|--|
    |appGuid|项目唯一标识。|
    |project|项目英文名称。|
    |projectNameCn|项目名称。|
    |comment|备注。|
    |ownerId|owner的id。|
    |createTime|创建时间。|
    |modifyTime|修改时间。|

-   示例如下：
    -   输入：`request.setDbGuid("odps.autotest");`
    -   输出：

        ``` {#codeblock_u04_r1k_ual}
        {
          "requestId": "0bfaefec****61500671805e",
          "errMsg": "success",
          "errCode": 0,
          "data": {
            "appGuid": "odps.meta",
            "projectName": "meta",
            "projectNameCn": "ODPS元仓",
            "comment": "",
            "ownerId": "13101879118",
            "createTime": "2014-02-18",
            "modifyTime": "2018-04-16"
          }
        }
        ```


## GetMetaTable {#section_yep_nnv_i3p .section}

-   功能：获取MaxCompute表的信息。
-   输入：tableGuid（必选）。
-   格式：`odps.<project>.<table>`。
-   输出：表的详情。

    |字段|描述|
    |--|--|
    |appGuid|项目唯一标识。|
    |tableGuid|表唯一标识。|
    |tableName|表名称。|
    |id|数据库ID 。|
    |ownerId|owner的ID 。|
    |hasPart|是否为分区表，1为分区表，0为非分区表。|
    |dataSize|表数据的大小。|
    |createTime|表的创建时间。|
    |lastDdlTime|表DDL最后的更新时间。|
    |lastModifyTime|表最后的修改时间。|

-   示例如下：
    -   输入：`request.setTableGuid(tableGuid);`
    -   输出：

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

-   功能：获取MaxCompute的列信息。
-   输入：tableGuid（必选）。
-   格式：`odps.<project>.<table>`。
-   输出：列详情。

    |字段|描述|
    |--|--|
    |appGuid|项目唯一标识。|
    |tableGuid|表唯一标识。|
    |tableName|表名称。|
    |columnGuid|列唯一标识，格式为`odps.<project>.<table>.<col>`。|
    |columnName|列名。|
    |columnType|列类型。|
    |seqNumber|列编号（从1开始）。|
    |isPartitionCol|是否为分区列： 0为非分区列，1为分区列。|
    |comment|备注。|
    |safeLevel|安全等级。|

-   示例如下：
    -   输入：`request.setTableGuid(tableGuid);`
    -   输出：

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
            "comment": "Project名称",
            "safeLevel": "C2"
          }, {
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
            "comment": "表名",
            "safeLevel": "C2"
          } ... ]
        }
        ```


## ListMetaTablePartition {#section_xoi_ivr_73a .section}

-   功能：获取MaxCompute的分区信息。
-   输入：

    |参数|说明|
    |--|--|
    |tableGuid|格式为`odps.<project>.<table>`。|
    |pageNum|页码。|
    |pageSize|每页最多显示记录数。|

-   输出：表分区的详情。

    |字段|描述|
    |--|--|
    |appGuid|项目唯一标识。|
    |tableGuid|表唯一标识。|
    |tableName|表名称。|
    |partitionGuid|分区唯一标识，格式为`odps.<project>.<table>.<partition>`。|
    |partitionName|分区名称。|
    |createTime|分区的创建时间。|
    |modifyTime|分区的修改时间。|
    |dataSize|分区的数据大小。|
    |records|分区的记录数。|
    |pageNum|当前分页页码。|
    |pageSize|当前分页大小。|
    |totalNum|总记录数。|

-   返回示例如下：

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

-   功能：模糊查找表。
-   输入：

    |参数|说明|
    |--|--|
    |keyword|表名称的关键字。|
    |pageNum|页码。|
    |pageSize|每页最多显示的记录数。|

-   输出：

    |字段|描述|
    |--|--|
    |appGuid|项目唯一标识。|
    |tableGuid|表唯一标识。|
    |tableName|表名称。|
    |ownerId|owner的ID。|
    |createTime|表的创建时间。|
    |lastDdlTime|表DDL最后的更新时间。|
    |lastModifyTime|表最后的修改时间。|

-   示例如下：
    -   输入：`request.setKeyword("test");`
    -   输出：

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
            }, {
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


## 使用DataOS API {#section_9u5_cmo_ub8 .section}

pom配置如下所示：

``` {#codeblock_aq5_ceb_36y}
<dependency>
      <groupId>com.aliyun</groupId>
      <artifactId>aliyun-java-sdk-dataworks</artifactId>
      <version>0.11.10</version>
    </dependency>

    <dependency>
      <groupId>com.aliyun</groupId>
      <artifactId>aliyun-java-sdk-core</artifactId>
      <version>4.4.0</version>
    </dependency>

    <dependency>
        <groupId>com.google.code.gson</groupId>
        <artifactId>gson</artifactId>
        <version>2.8.5</version>
    </dependency>
```

host配置如下所示：

``` {#codeblock_646_ejd_3v7}
#预发（办公网可以直接访问）
100.67.30.222 dataworks-share.aliyuncs.com
```

Java代码如下所示，其中创建IClientProfile时，需要指定云账号的AccessKeyID和AccessKeySecret，详情请参见下文的常见问题。

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
    IClientProfile profile = DefaultProfile.getProfile("cn-hangzhou", "<!!!!id>",
        "<!!!key>");
    DefaultProfile.addEndpoint("cn-hangzhou", "cn-hangzhou", "dataworks", "dataworks-share.aliyuncs.com");
    client = new DefaultAcsClient(profile);
  }

}
```

## 常见问题 {#section_3le_fib_x5t .section}

-   无法访问API，错误提示如下所示：

    ``` {#codeblock_ivd_ilv_wa7}
    Exception in thread "main" com.aliyuncs.exceptions.ClientException: InvalidApi.NotFound : Specified api is not found, please check your url and method.
    RequestId : B081CCF1-9F19-473E-9B99-68F202E7572B
    ```

    错误原因：没有获取API权限。

-   如何查询AccessKeyID和AccessKeySecret？

    单击页面右上角账号下的**accesskeys**，即可进行查询。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/217865/155832319447429_zh-CN.png)


