# SearchManualDagNodeInstance {#concept_yfd_3sv_kfb .concept}

SearchManualDagNodeInstance：查询手动业务流程实例。

## 描述 {#section_c2z_1xn_fgb .section}

SearchManualDagNodeInstance用于查询已触发的手动业务流程示例状态和名称等信息，包括运行中和运行完成的实例。

## 请求参数 {#section_llt_r5v_kfb .section}

|参数名|参数位置|类型|是否必选|顺序|示例值|描述|
|:--|:---|:-|:---|:-|:--|:-|
|**ProjectName**|Query|String|否|200|test\_odps\_project|项目英文名称|
|**DagId**|Query|Long|否|200|123434234|手动业务流程运行实例ID，[createManualDag](cn.zh-CN/API参考/手动业务流程/CreateManualDag.md#)接口返回的值|

## 请求示例 {#section_rch_t5v_kfb .section}

```language-java
/?DagId=123434234
&ProjectName=test_odps_project
&<公共请求参数>
```

## 返回参数 {#section_zq5_v14_fgb .section}

|参数名|结构类型|数据类型|顺序|示例值|描述|
|:--|:---|:---|:-|:--|:-|
|**Data**|Array|N/A|200|N/A|返回的手动业务流程内部运行任务的列表|
|└InstanceId|Normal|Long|200|12322434112|任务实例ID|
|└DagId|Normal|Long|200|12434232423|业务流程运行实例ID|
|└DagType|Normal|Integer|200|5|业务流程类型,5标识手动业务流程|
|└Status|Normal|Integer|200|6|任务状态```
/** * 未运行：上游实例未全部成功 */ NOT_RUN(1, "未运行"), /** * 等待定时时间（dueTime/cycleTime）到来 */ WAIT_TIME(2, "等待时间"), /** * 已经下发到执行引擎，在等待排队调度执行 */ WAIT_RESOURCE(3, "等待资源"), /** * 执行中 */ RUNNING(4, "运行中"), /** * 执行完毕，已经下发做数据校验 */ CHECKING(7, "校验中"), /** * 执行完毕，正在做分支条件校验 */ CHECKING_CONDITION(8, "条件检测中"), /** * 执行失败 */ FAILURE(5, "运行失败"), /** * 执行成功 */ SUCCESS(6, "运行成功");
```

|
|└Bizdate|Normal|String|200|2018-12-12 00:00:00|业务日期|
|└ParaValue|Normal|String|200|param\_k1=param\_v1|任务参数信息|
|└FinishTime|Normal|String|200|2018-12-12 00:00:00|任务结束时间|
|└BeginWaitTimeTime|Normal|String|200|2018-12-12 00:00:00|开始等待时间的时间点|
|└BeginWaitResTime|Normal|String|200|2018-12-12 00:00:00|开始等待资源的时间点|
|└BeginRunningTime|Normal|String|200|2018-12-12 00:00:00|开始运行时间|
|└CreateTime|Normal|String|200|2018-12-12 00:00:00|创建时间|
|└ModifyTime|Normal|String|200|2018-12-12 00:00:00|修改时间|
|└NodeName|Normal|String|200|test\_node|任务节点名称|
|**RequestId**|Normal|String|200|2d9ced66-38ef-4923-baf6-391dd3a7e656|请求ID|
|**ErrCode**|Normal|String|200|0|错误码|
|**ErrMsg**|Normal|String|200|test|错误信息|
|**Success**|Normal|Boolean|200|true|是否成功|

