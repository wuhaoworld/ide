# 配置Redis Writer {#concept_fdm_sxn_q2b .concept}

Redis Writer是基于数据集成框架实现的Redis写入插件，可以通过Redis Writer从数仓或者其它数据源导入数据至Redis。

Redis（REmote DIctionary Server）是一个可以基于内存也可以持久化的日志型、高性能、支持网络的key-value存储系统，可以用作数据库、高速缓存和消息队列代理。Redis支持较丰富的存储value类型，包括String（字符串）、List（链表）、Set（集合）、ZSet（sorted set有序集合）和Hash（哈希类型）。Redis详情请参见[redis.io](http://redis.io/)。

Redis Writer与Redis Server之间的交互基于Jedis实现，Jedis是Redis官方首选的Java客户端开发包。

**说明：** 

-   开始配置Redis Writer插件前，请首先配置好数据源，详情请参见[配置Redis数据源](intl.zh-CN/使用指南/数据集成/数据源配置/配置Redis数据源.md#)。
-   使用Redis Writer向Redis写入数据时，如果value类型是list，重跑同步任务同步结果不是幂等的。因此，如果value类型是list ，重跑同步任务时，需要您手动清空Redis上相应的数据。

## 参数说明 {#section_jn2_gqh_p2b .section}

|参数|描述|是否必选|默认值|
|:-|:-|:---|:--|
|datasource|数据源名称，脚本模式支持添加数据源，此配置项填写的内容必须与添加的数据源名称保持一致。|是|无|
|keyIndexes|keyIndexes表示源端需要作为key（第1列是从0开始）的列。如果是第1列和第2列需要组合作为key，则keyIndexes的值为\[0,1\]。 **说明：** 配置keyIndexes后，Redis Writer会将其余的列作为value。如果您只想同步源表的某几列作为key，某几列作为value，则不需要同步所有字段，在Reader插件端指定好column进行列筛选即可。

 |是|无|
|keyFieldDelimiter|写入Redis的key分隔符。例如key=key1\\u0001id，如果有多个key需要拼接时，该值为必填项，如果只有1个key，则可以忽略该配置项。|否|\\u0001|
|batchSize|一次性批量提交的记录数大小，该值可以极大减少数据同步系统与Redis的网络交互次数，并提升整体吞吐量。如果该值设置过大，会导致数据同步运行进程OOM异常。|否|1,000|
|expireTime|Redis value值缓存失效时间（如果需要永久有效，则可以不填该配置项），单位为秒。 -   seconds：相对当前时间的秒数，该时间指定了从现在开始多长时间后数据失效。
-   unixtime：Unix时间（自1970.1.1开始到现在的秒数），该时间指定了到未来某个时刻数据失效。

**说明：** 如果过期时间的秒数大于60\*60\*24\*30（即30天），则服务端认为是Unix时间。


 |否|0（0表示永久有效）|
|timeout|写入Redis的超时时间，单位为毫秒。|否|30,000|
|dateFormat|写入Redis时，Date的时间格式为yyyy-MM-dd HH:mm:ss。|否|无|
|writeMode|Redis支持丰富的value类型，包括字符串（string）、字符串列表（list）、字符串集合（set）、有序字符串集合（zset）和哈希（hash）。Redis Writer支持上述5种类型的写入，根据不同的value类型，writeMode配置会略有差异，writeMode的配置说明如下表所示。 **说明：** 您在配置Redis Writer时，只能配置以下5种类型中的1种。您需要配置其中一种写入数据类型，如果您不填，默认数据类型是string。

 |否|string|

您在配置Redis Writer时，只能配置以下5种类型中的1种。

|类型|配置|描述|是否必选|
|--|--|--|----|
|字符串（string） ``` {#codeblock_cs4_fco_zje}
"writeMode":{
        "type": "string",
        "mode": "set",
        "valueFieldDelimiter": "\u0001"
        }
```

 |type|value为string类型。|是|
|mode|value为string类型时，写入的模式。|是，可选值为set（如果需存储的数据已经存在，则覆盖原有的数据）。|
|valueFieldDelimiter|该配置项主要考虑的是源数据每行超过两列的情况。如果您的源数据只有两列，即key和value时，则可以忽略该配置项，无需填写。 value类型为string时，value之间的分隔符。例如value1\\u0001value2\\u0001value3。

 |否，默认值为\\u0001。|
|字符串列表（list） ``` {#codeblock_nwo_6cb_8uq}
"writeMode":{
    "type": "list",
    "mode": "lpush|rpush",
    "valueFieldDelimiter": "\u0001"
}
```

 |type|value为list类型。|是|
|mode|value为list类型时，写入的模式。|是，可选值为lpush（在list最左边存储数据）和rpush（在list最右边存储数据）。|
|valueFieldDelimiter|value为string类型时，value之间的分隔符。例如value1\\u0001value2\\u0001value3。|否，默认值为\\u0001。|
|字符串集合（set） ``` {#codeblock_ttm_6f2_nde}
"writeMode":{
        "type": "set",
        "mode": "sadd",
        "valueFieldDelimiter": "\u0001"
        }
```

 |type|value为set类型。|是|
|mode|value为set类型时，写入的模式。|是，可选值：sadd（向set集合中存储数据，如果已经存在则覆盖）。|
|valueFieldDelimiter|value类型是string时，value之间的分隔符，例如value1\\u0001value2\\u0001value3。|否，默认值为\\u0001。|
|有序字符串集合（zset） ``` {#codeblock_flk_d6f_p2i}
"writeMode":{
        "type": "zset",
        "mode": "zadd"
        }
```

 |type|value为zset类型。 **说明：** 当value类型为zset时，数据源的每行记录均需遵循相应的规范。即每行记录除key外，只能有1对score和value，并且score必须在value前面，rediswriter方可解析出column对应的是score或value。

 |是|
|mode|value为zset类型时，写入的模式。|是，可选值为zadd（向zset有序集合中存储数据，如果已经存在则覆盖）。|
|哈希（hash） ``` {#codeblock_itv_2em_kh8}
"writeMode":{
        "type": "hash",
        "mode": "hset"
        }
```

 |type|value为hash类型。 **说明：** 当value类型为hash时，数据源的每行记录都需遵循相应的规范。即每行记录除key外，只能有1对attribute和value，并且attribute必须在value前面，Rediswriter方可解析出column对应的是attribute或value。

 |是|
|mode|value为hash类型时，写入的模式。|是，可选值为hmset（向hash有序集合中存储数据，如果已经存在则覆盖）。 您需要配置其中一种写入数据类型，如果您不填，默认数据类型是string。

 |

## 向导开发介绍 {#section_bp2_wsh_p2b .section}

暂不支持向导开发模式。

## 脚本开发介绍 {#section_cp2_wsh_p2b .section}

配置写入Redis的数据同步作业，具体参数填写请参见参数说明。

``` {#codeblock_o7d_vwr_llr}
{
    "type":"job",
    "version":"2.0",//版本号
    "steps":[
        { 
            "stepType":"stream",
            "parameter":{},
            "name":"Reader",
            "category":"reader"
        },
        {
            "stepType":"redis",//插件名。
            "parameter":{
                "expireTime":{//Redis value值缓存失效时间。
                    "seconds":"1000"
                },
                "keyFieldDelimiter":"u0001",//写入Redis的key的分隔符。
                "dateFormat":"yyyy-MM-dd HH:mm:ss",//写入Redis时，Date的时间格式。
                "datasource":"",//数据源。
                "writeMode":{//写入模式。
                    "mode":"",//value是某类型时，写入的模式。
                    "valueFieldDelimiter":"",//value之间的分隔符。
                    "type":""//value类型。
                },
                "keyIndexes":[//主键索引。
                    0,
                    1
                ],
                "batchSize":"1000"//一次性批量提交的记录数大小。
            },
            "name":"Writer",
            "category":"writer"
        }
    ],
    "setting":{
        "errorLimit":{
            "record":"0"//错误记录数。
        },
        "speed":{
            "throttle":false,////false代表不限流，下面的限流的速度不生效，true代表限流。
            "concurrent":1,//作业并发数。
        }
    },
    "order":{
        "hops":[
            {
                "from":"Reader",
                "to":"Writer"
            }
        ]
    }
}Writer"
            }
        ]
    }
}
```

