# DataHub {#concept_a2s_bds_wgb .concept}

DataHub作为一个流式数据总线，为阿里云数加平台提供了大数据的入口服务。

实时计算通常使用DataHub作为流式数据存储头和输出目的端。同时，上游众多流式数据，包括DTS、IOT等均选择DataHub作为大数据平台的数据入口。DataHub本身是流数据存储，实时计算只能将其作为流式数据输入。更多详情请参见[创建数据总线DataHub源表](../../../../cn.zh-CN/Flink SQL开发指南/Flink SQL/DDL语句/创建数据源表/创建数据总线 DataHub源表.md#)。

## 配置面板说明 {#section_p5b_dms_wgb .section}

|参数|注释说明|备注|
|--|----|--|
|血缘表名（任务唯一）|任务中表的唯一标志，不能与任务中其他血缘表重名。|无|
|定义列|要读取的DataHub内容字段列表，以及属性字段列表。|无|
|连接地址|对应SQL中的参数endPoint。|无|
|accessId|对应SQL中的参数accessId。|无|
|accessKey|对应SQL中的参数accessKey。|无|
|项目名|读取的项目名称，对应SQL中的参数project。|无|
|主题|对应SQL中的参数topic。|无|
|开始时间|对应SQL中的参数startTime。流计算任务将从指定的开始时间消费DataHub中的数据，此处指定的开始时间优先于启动任务时指定的启动位点。|格式为`yyyy-MM-dd hh:mm:ss`|
|读取最大重试次数|读取时最多可以重试的次数，对应SQL中的参数maxRetryTimes。|无|
|读取重试间隔|对应SQL中的参数retryIntervalMs，单位为毫秒。|无|
|单次读取条数|对应SQL中的参数batchReadSize。|无|
|单行字段条数检查策略|对应SQL中的参数lengthCheck。|默认为NONE，其它可选值为SKIP、EXCEPTION和PAD -   NONE：解析出的字段数大于定义字段数时，按照从左到右的顺序取定义字段数量的数据，解析出的字段数小于定义字段数时跳过该行数据。
-   SKIP：字段数目不符合时跳过。
-   EXCEPTION：字段数目不符合时抛出异常。
-   PAD：解析出的字段数大于定义字段数时，按照从左到右的顺序取定义字段数量的数据，解析出的字段数小于定义字段数时，在行尾用null填充缺少的字段。

 |
|调试开关|对应SQL中的参数columnErrorDebug，是否打开调试开关。|如果打开调试开关，会打印解析异常的日志，您可以进入运维中心，查看任务的日志详情。|

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

![属性字段](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130387/156681334339580_zh-CN.png)

|字段名|注释说明|
|---|----|
|**System Time**|每条记录写入DataHub的系统时间。|

