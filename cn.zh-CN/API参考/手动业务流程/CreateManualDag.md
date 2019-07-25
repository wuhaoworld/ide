# CreateManualDag {#doc_api_dataworks-public_CreateManualDag .reference}

触发手动业务流程执行。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=dataworks-public&api=CreateManualDag&type=RPC&version=2018-06-01)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateManualDag|系统规定参数，取值为**CreateManualDag**。

 |
|Bizdate|String|是|2018-12-12 00:00:00|业务日期。

 |
|FlowName|String|是|test\_flow|手动业务流程名称。

 |
|ProjectName|String|是|test\_project|项目名称。

 |
|DagPara|String|否|param\_k1=param\_v1 param\_k2=param\_v2|业务流程参数。

 |
|NodePara|String|否|\{"103180025": "test=$\[yyyy-mm-dd\]"\}|节点参数，节点ID到节点参数的map。如果节点有多个参数，在节点参数值中用空格分隔。

 |
|RegionId|String|否|cn-shanghai|地域ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|2d9ce-38ef-4923-baf6-391a7e656|请求ID。

 |
|ReturnCode|String|0|响应代码编号，0标识成功。

 |
|ReturnErrorSolution|String|test|如果异常，会显示异常的解决方案信息。

 |
|ReturnMessage|String|test|异常信息。

 |
|ReturnValue|Long|1244311235|返回值，此处返回手动业务流程的运行实例ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

/?Bizdate=2018-12-12 00:00:00
&FlowName=test_flow
&ProjectName=test_project
&DagPara=param_k1=param_v1 param_k2=param_v2
&NodePara={"103180025": "test=$[yyyy-mm-dd]"}
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateManualDagMetaResponse>
  <requestId>D394A-96-4C7-96E-FCDEB0AB3</requestId>
	  <returnCode>0</returnCode>
	  <returnErrorSolution></returnErrorSolution>
	  <returnMessage></returnMessage>
	  <returnValue>13245685</returnValue>
</CreateManualDagMetaResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"returnCode":"0",
	"requestId":"D394A-96-4C7-96E-FCDEB0AB3",
	"returnValue":13245685,
	"returnErrorSolution":"",
	"returnMessage":""
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/dataworks-public)查看更多错误码。

