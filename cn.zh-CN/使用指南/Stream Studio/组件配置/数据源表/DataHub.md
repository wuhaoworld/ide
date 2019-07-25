# DataHub {#concept_a2s_bds_wgb .concept}

DataHub作为一个流式数据总线，为阿里云数加平台提供了大数据的入口服务。

实时计算通常使用DataHub作为流式数据存储头和输出目的端。同时，上游众多流式数据，包括DTS、IOT等均选择DataHub作为大数据平台的数据入口。DataHub本身是流数据存储，实时计算只能将其作为流式数据输入。更多信息请参见[创建数据总线DataHub源表](../../../../cn.zh-CN/Flink SQL开发指南/Flink SQL/DDL语句/创建数据源表/创建数据总线 DataHub源表.md#)。

## 配置面板说明 {#section_p5b_dms_wgb .section}

|参数|注释说明|备注|
|--|----|--|
|血缘表名（任务唯一）|任务中表的唯一标志，不能与任务中其他血缘表重名。|无|
|定义列|要读取的DataHub内容字段列表，以及属性字段列表。|无|
|消费端点信息|消费端点信息。|无|
|读取的AccessID|读取的AccessID。|无|
|读取的秘匙|读取的秘匙。|无|
|读取的项目|读取的项目。|无|
|topic|项目下的具体的topic。|无|
|日志开始时间|日志开始时间。|格式为`yyyy-MM-dd hh:mm:ss`|
|读取最大尝试次数|可以尝试读取的最大次数。|无|
|重试间隔|重试间隔。|无|
|单次读取条数|单次读取条数。|无|
|单行字段条数检查策略|单行字段条数检查策略。|默认为SKIP，其它可选值为EXCEPTION和PAD -   SKIP：字段数目不符合时跳过
-   EXCEPTION：字段数目不符合时抛出异常
-   PAD：按顺序填充，不存在的置为null

 |
|调试开关|如果打开调试开关，会打印出解析异常的日志。|无|
|DataHub是否为BLOB类型|DataHub是否为BLOB类型。|无|
|数据质量|跳转至数据质量页面，查看相关监控任务。|无|

## 类型映射 {#section_hgc_mnf_xgb .section}

DataHub和实时计算字段类型对应关系，建议您使用该对应关系进行DDL声明。

|DataHub字段类型|实时计算字段类型|
|-----------|--------|
|BIGINT|BIGINT|
|DOUBLE|DOUBLE|
|TIMESTAMP|BIGINT|
|BOOLEAN|BOOLEAN|
|DECIMAL|DECIMAL|

## 属性字段 {#section_ajn_rnf_xgb .section}

列定义支持获取DataHub的属性字段，可以记录每条信息写入DataHub的系统时间。

![属性字段](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130387/156405916639580_zh-CN.png)

|字段名|注释说明|
|---|----|
|**System Time**|每条记录入DataHub的System Time。|

