# 配置OpenSearch Writer {#concept_kwq_vnt_q2b .concept}

本文为您介绍OpenSearch Writer支持的数据类型、字段映射和数据源等参数及配置示例。

OpenSearch Writer插件用于向OpenSearch中插入或更新数据。OpenSearch Writer将处理好的数据导入OpenSearch，以搜索的方式输出。数据传输的速率取决于OpenSearch表对应账号的每秒查询率（QPS）。

## 实现原理 {#section_f5g_g1n_q2b .section}

在底层实现上，OpenSearch Writer通过OpenSearch对外提供的开放搜索接口。

**说明：** 

-   V3版本使用二方包，依赖pom为：com.aliyun.opensearch aliyun-sdk-opensearch 2.1.3。
-   如果您需要使用OpenSearchWriter插件，请务必使用JDK 1.6-32及以上版本，使用`java -version`查看Java版本号。
-   目前默认资源组不支持连接VPC环境，如果是VPC环境可能会存在网络问题。

## 插件特点 {#section_jn2_gqh_p2b .section}

关于列顺序的问题

OpenSearch的列是无序的，因此OpenSearch Writer写入时，需严格按照指定的列的顺序写入。如果指定的列比OpenSearch的列少，则其余列使用默认值或null。

例如需要导入的字段列表有b、c两个字段，但OpenSearch表中的字段有a、b、c三列，在列配置中可以写为"column":\["c","b"\]，表示会把Reader的第一列和第二列导入OpenSearch的c字段和b字段，而OpenSearch表中新插入的a字段会被置为默认值或null。

-   列配置错误的处理

    为保证写入数据的可靠性，避免多余列数据丢失造成数据质量故障。对于写入多余的列，OpenSearch Writer将报错。例如OpenSearch表字段为a、b、c，如果OpenSearch Writer写入的字段多于3列，OpenSearch Writer将报错。

-   表配置注意事项

    OpenSearch Writer一次只能写入一个表。

-   任务重跑和Failover

    重跑后会自动根据ID覆盖。所以插入OpenSearch的列中，必须有一个ID，该ID是OpenSearch的一行记录的唯一标识。唯一标识一样的数据，会被覆盖掉。

-   任务重跑和failover

    重跑后会自动根据ID覆盖。


OpenSearch Writer支持大部分OpenSearch类型，请注意检查您的数据类型。

OpenSearch Writer针对OpenSearch类型的转换列表，如下所示。

|类型分类|OpenSearch数据类型|
|:---|:-------------|
|整数类|INT|
|浮点类|DOUBLE和FLOAT|
|字符串类|TEXT、LITERAL和SHORT\_TEXT|
|日期时间类|INT|
|布尔类|LITERAL|

## 参数说明 {#section_amt_td4_q2b .section}

|参数|描述|是否必选|默认值|
|:-|:-|:---|:--|
|accessId|阿里云系统登录ID。|是|无|
|accessKey|阿里云系统登录Key。|是|无|
|host| OpenSearch连接的服务地址，您可以在应用详情页面进行查看。

 |是|无|
|indexName|OpenSearch项目的名称。|是|无|
|table|写入数据的表名，不能填写多张表，因为DataX不支持同时导入多张表。|是|无|
|column|需要导入的字段列表。当导入全部字段时，可以配置为`"column":["*"]`。当需要插入部分OpenSearch列时，填写需要插入的列，例如：`"column":["id","name"]`。 OpenSearch支持列筛选、列换序，例如：表有a、b和c三个字段，只需同步c，b两个字段，则可以配置为`["c","b"]`。导入过程中，字段a自动补空，设置为null。

 |是|无|
|batchSize|单次写入的数据条数。OpenSearch写入为批量写入，通常OpenSearch的优势在于查询，写入的每秒处理事务数（TPS）不高，请根据账号申请的资源进行设置。 通常OpenSearch的单条数据小于1MB，单次写入小于2MB。

 |如果是分区表，该选项必填。如果是非分区表，该选项不可填写。|300|
|writeMode|OpenSearch Writer通过配置"writeMode":"add/update"，保证写入的幂等性。 -   "add"：当出现写入失败再次运行时，OpenSearch Writer将清理该条数据，并导入新数据（原子操作）。
-   "update"：表示该条插入数据以修改的方式插入（原子操作）。

**说明：** OpenSearch的批量插入并非原子操作，有可能会部分成功，部分失败。writeMode参数的选择较为重要，目前V3版本暂不支持update操作。


 |是|无|
|ignoreWriteError|忽略写错误。 配置示例：`"ignoreWriteError":true`。OpenSearch为批量写入，是否忽略当前批次的写失败。如果忽略，则继续执行其它的写操作。如果不忽略，则直接结束当前任务，并返回错误。建议使用默认值。

 |否|false|
|version|OpenSearch的版本信息，例如`"version":"v3"`。由于V2版本对于push操作的限制较多，建议使用V3版本。|否|v2|

## 脚本开发介绍 {#section_hy1_dys_q2b .section}

配置写入OpenSearch的数据同步作业。

``` {#codeblock_5dc_glt_44e .language-json}
{
    "type": "job",
    "version": "1.0",
    "configuration": {
        "reader": {},
        "writer": {
            "plugin": "opensearch",
            "parameter": {
                "accessId": "*********",
                "accessKey": "********",
                "host": "http://yyyy.aliyuncs.com",
                "indexName": "datax_xxx",
                "table": "datax_yyy",
                "column": [
                "appkey",
                "id",
                "title",
                "gmt_create",
                "pic_default"
                ],
                "batchSize": 500,
                "writeMode": add,
                "version":"v2",
                "ignoreWriteError": false
            }
        }
    }
}
```

