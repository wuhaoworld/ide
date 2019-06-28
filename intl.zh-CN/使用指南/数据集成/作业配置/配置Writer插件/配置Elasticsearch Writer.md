# 配置Elasticsearch Writer {#concept_okj_c24_q2b .concept}

本文为您介绍Elasticsearch Writer支持的数据类型、写入方式、字段映射和数据源等参数及配置示例。

Elasticsearch是遵从Apache开源条款的一款开源产品，是当前主流的企业级搜索引擎。Elasticsearch是一个基于Lucene的搜索和数据分析工具，它提供分布式服务。Elasticsearch核心概念同数据库核心概念的对应关系如下所示。

``` {#codeblock_6xw_fw6_szf}
Relational DB(实例) -> Databases(数据库) -> Tables(表) -> Rows(一行数据) -> Columns(一行数据的一列)
Elasticsearch -> Index  -> Types -> Documents -> Fields
```

Elasticsearch中可以有多个索引/数据库，每个索引可以包括多个类型/表，每个类型可以包括多个文档/行，每个文档可以包括多个字段/列。Elasticsearch Writer插件使用Elasticsearch的Rest API接口，批量把从Reader读入的数据写入Elasticsearch中。

## 参数说明 {#section_a3m_424_q2b .section}

|参数|描述|是否必选|默认值|
|:-|:-|:---|:--|
|endpoint|Elasticsearch的连接地址，通常格式为`http://xxxx.com:9999`。|否|无|
|accessId|Elasticsearch的username，用于与Elasticsearch建立连接时的鉴权。 **说明：** AccessID和AccessKey为必填项，如果不填写会产生报错。如果您使用的是自建Elasticsearch，不设置basic验证，不需要账号密码，此处AccessId和AccessKey填写随机值即可。

 |否|无|
|accessKey|Elasticsearch的password。|否|无|
|index|Elasticsearch中的index名。|否|无|
|indexType|Elasticsearch中index的type名。|否|Elasticsearch|
|cleanup|是否删除所配索引中已有数据，清理数据的方法为删除并重建对应索引，默认值为false，表示保留已有索引中的数据。|否|false|
|batchSize|每次批量数据的条数。|否|1,000|
|trySize|失败后重试的次数。|否|30|
|timeout|客户端超时时间。|否|600,000|
|discovery|启用节点发现将轮询并定期更新客户机中的服务器列表。|否|false|
|compression|HTTP请求，开启压缩。|否|true|
|multiThread|HTTP请求，是否有多线程。|否|true|
|ignoreWriteError|忽略写入错误，不重试，继续写入。|否|false|
|ignoreParseError|忽略解析数据格式错误，继续写入。|否|true|
|alias|Elasticsearch的别名类似于数据库的视图机制，为索引my\_index创建一个别名my\_index\_alias，对my\_index\_alias的操作与my\_index的操作一致。 配置alias表示在数据导入完成后，为指定的索引创建别名。

 |否|无|
|aliasMode|数据导入完成后增加别名的模式，包括append（增加模式）和exclusive（只留这一个）。|否|append|
|settings|如果待插入目标端数据列类型是array数组类型，则使用指定分隔符（-,-），将源头数据进行拆分写出。示例如下： 源头列是字符串类型数据`a-,-b-,-c-,-d`，使用分隔符（-,-）拆分后是数组`["a", "b", "c", "d"]`，最终写出至Elasticsearch对应Filed列中。

 |否|-,-|
|column|column用来配置文档的多个字段Filed信息，具体每个字段项可以配置name（名称）、type（类型）等基础配置，以及Analyzer、Format和Array等扩展配置。 Elasticsearch所支持的字段类型如下所示。

``` {#codeblock_5io_1d2_04s}
- id
- string
- text
- keyword
- long
- integer
- short
- byte
- double
- float
- date
- boolean
- binary
- integer_range
- float_range
- long_range
- double_range
- date_range
- geo_point
- geo_shape
- ip
- token_count
- array
- object
- nested
```

 -   列类型为text类型时，可以配置analyzer（分词器）、norms和index\_options等参数，示例如下。

    ``` {#codeblock_0it_vfz_olc}
{
    "name": "col_text",
    "type": "text",
    "analyzer": "ik_max_word"
    }
    ```

-   列类型为日期Date类型时，可以配置Format和Timezone参数，分别表示日期序列化格式和时区，示例如下。

    ``` {#codeblock_iiw_e3m_2hb}
{
    "name": "col_date",
    "type": "date",
    "format": "yyyy-MM-dd HH:mm:ss",
    "timezone": "UTC"
    }
    ```

-   列类型为地理形状geo\_shape时，可以配置tree（geohash或quadtree）、precision（精度）属性，示例如下。

    ``` {#codeblock_bpd_rjc_1wo}
{
    "name": "col_geo_shape",
    "type": "geo_shape",
    "tree": "quadtree",
    "precision": "10m"
    }
    ```


 如果您在列Filed中配置了array属性，且值为true时，则表示数组列。Elasticsearch Writer会使用splitter配置的分隔符（一个任务仅支持配置一种切分分隔符），将对应源端数据进行拆分，转换为字符串数组形式最终写出至目的端，示例如下。

``` {#codeblock_0n9_jvw_7ua}
{
    "name": "col_integer_array",
    "type": "integer",
    "array": true
    }
```

 |是|无|
|dynamic|如果为true，则使用Elasticsearch的自动mappings，而非使用datax的mappings。|否|false|
|actionType|表示Elasticsearch在数据写出时的action类型，目前数据集成支持index和update两种actionType，默认值为index。 -   index：底层使用了Elasticsearch SDK的Index.Builder构造批量请求。Elasticsearch index插入的逻辑为：首先判断插入的文档数据中是否指定ID。
    -   如果没有指定ID，Elasticsearch会默认生成一个唯一ID。该情况下会直接添加文档至Elasticsearch中。
    -   如果已指定ID，会进行更新（替换整个文档），且不支持针对特定Field进行修改。

**说明：** 此处的更新并非Elasticsearch中的更新（替换部分指定列替换）。

-   update：底层使用了Elasticsearch SDK的Update.Builder构造批量请求。Elasticsearch update更新的逻辑为：每次update都会调用InternalEngine中的get方法，来获取整个文档信息，从而实现针对特定字段进行修改。该逻辑导致每次更新都需获取一遍原始文档，对性能有较大影响，但可以更新用户指定的列。如果匹配的文档不存在，则执行文档插入操作。

 |否|index|

## 脚本开发介绍 {#section_pcz_fh4_q2b .section}

脚本配置示例如下，具体参数请参见上文的参数说明。

``` {#codeblock_lkw_w3m_8fa}
{
    "order": {
        "hops": [
            {
                "from": "Reader",
                "to": "Writer"
            }
        ]
    },
    "setting": {
        "errorLimit": {
            "record": "0"
        },
        "speed": {
            "concurrent": 1,
            "throttle": false
        }
    },
    "steps": [
        {
            "category": "reader",
            "name": "Reader",
            "parameter": {
                 //下面是关于Reader的模板，您可以查找相应的读插件文档。
            },
            "stepType": "stream"
        },
        {
            "category": "writer",
            "name": "Writer",
            "parameter": {
                "endpoint": "http://xxxx.com:9999",
                "accessId": "xxxx",
                "accessKey": "yyyy",
                "index": "test-1",
                "type": "default",
                "cleanup": true,
                "settings": {
                    "index": {
                        "number_of_shards": 1,
                        "number_of_replicas": 0
                    }
                },
                "discovery": false,
                "batchSize": 1000,
                "splitter": ",",
                "column": [
                    {
                        "name": "pk",
                        "type": "id"
                    },
                    {
                        "name": "col_ip",
                        "type": "ip"
                    },
                    {
                        "name": "col_double",
                        "type": "double"
                    },
                    {
                        "name": "col_long",
                        "type": "long"
                    },
                    {
                        "name": "col_integer",
                        "type": "integer"
                    },
                    {
                        "name": "col_keyword",
                        "type": "keyword"
                    },
                    {
                        "name": "col_text",
                        "type": "text",
                        "analyzer": "ik_max_word"
                    },
                    {
                        "name": "col_geo_point",
                        "type": "geo_point"
                    },
                    {
                        "name": "col_date",
                        "type": "date",
                        "format": "yyyy-MM-dd HH:mm:ss"
                    },
                    {
                        "name": "col_nested1",
                        "type": "nested"
                    },
                    {
                        "name": "col_nested2",
                        "type": "nested"
                    },
                    {
                        "name": "col_object1",
                        "type": "object"
                    },
                    {
                        "name": "col_object2",
                        "type": "object"
                    },
                    {
                        "name": "col_integer_array",
                        "type": "integer",
                        "array": true
                    },
                    {
                        "name": "col_geo_shape",
                        "type": "geo_shape",
                        "tree": "quadtree",
                        "precision": "10m"
                    }
                ]
            },
            "stepType": "elasticsearch"
        }
    ],
    "type": "job",
    "version": "2.0"
}
```

**说明：** 目前VPC环境的Elasticsearch仅能使用自定义调度资源，运行在默认资源组会存在网络不通的情况。添加自定义资源组的具体操作请参见[新增任务资源](intl.zh-CN/使用指南/数据集成/常见配置/新增任务资源.md#)。

