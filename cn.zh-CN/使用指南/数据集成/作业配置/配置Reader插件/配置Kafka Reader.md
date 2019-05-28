# 配置Kafka Reader {#concept_263538 .concept}

Kafka Reader通过Kafka服务的Java SDK从Kafka读取数据。

Apache Kafka是一个快速、可扩展、高吞吐和可容错的分布式发布订阅消息系统。Kafka具有高吞吐量、内置分区、支持数据副本和容错的特性，适合在大规模消息处理的场景中使用。

消费消息的详情参见[订阅者最佳实践](https://help.aliyun.com/document_detail/68166.html)。

## 实现原理 {#section_q3l_b2d_faw .section}

Kafka Reader通过Kafka Java SDK读取Kafka中的数据，使用的日志服务Java SDK版本如下所示。

``` {#codeblock_6yw_y6z_paj}
<dependency>
   <groupId>org.apache.kafka</groupId>
   <artifactId>kafka-clients</artifactId>
   <version>2.0.0</version>
</dependency>
```

主要涉及的Kafka SDK调用方法如下，您可以参见Kafka官方了解接口的功能和限制。

-   使用KafkaConsumer作为消息消费的客户端。

    ``` {#codeblock_g6m_rpf_rsd}
    org.apache.kafka.clients.consumer.KafkaConsumer<K,V>
    ```

-   根据unix时间戳查询Kafka点位offSet。

    ``` {#codeblock_hba_ae1_ffn}
    Map<TopicPartition,OffsetAndTimestamp> offsetsForTimes(Map<TopicPartition,Long> timestampsToSearch)
    ```

-   定位到开始点位offSet。

    ``` {#codeblock_r94_wtz_f2u}
    public void seekToBeginning(Collection<TopicPartition> partitions)
    ```

-   定位到结束点位offSet。

    ``` {#codeblock_ktc_yk7_d4p}
    public void seekToEnd(Collection<TopicPartition> partitions)
    ```

-   定位到指定点位offSet。

    ``` {#codeblock_f5x_wkx_h7q}
    public void seek(TopicPartition partition,long offset)
    ```

-   客户端从服务端拉取poll数据。

    ``` {#codeblock_bty_l1b_dlr}
    public ConsumerRecords<K,V> poll(final Duration timeout)
    ```


**说明：** Kafka Reader消费数据使用了自动点位提交机制。

## 参数说明 {#section_s0h_ngm_hef .section}

|参数|说明|是否必填|
|--|--|----|
|server|Kafka的broker server地址，格式为ip:port。|是|
|topic|Kafka的topic，是Kafka处理资源的消息源（feeds of messages）的聚合。|是|
|column|需要读取的Kafka数据，支持常量列、数据列和属性列。 -   常量列：使用单引号包裹的列为常量列，例如\["'abc'", "'123'"\]。
-   数据列
    -   如果您的数据是一个JSON，支持获取JSON的属性，例如\["event\_id"\]。
    -   如果您的数据是一个JSON，支持获取JSON的嵌套子属性，例如\["tag.desc"\]。
-   属性列

    -   \_\_key\_\_ 表示消息的key。
    -   \_\_value\_\_ 表示消息的完整内容 。
    -   \_\_partition\_\_ 表示当前消息所在分区。
    -   \_\_headers\_\_ 表示当前消息headers信息。
    -   \_\_offset\_\_ 表示当前消息的偏移量。
    -   \_\_timestamp\_\_ 表示当前消息的时间戳。
完整示例如下：

    ``` {#codeblock_jvs_137_5s1}
"column": [
    "__key__",
    "__value__",
    "__partition__",
    "__offset__",
    "__timestamp__",
    "'123'",
    "event_id",
    "tag.desc"
    ]
    ```


 |是|
|keyType|Kafka的key的类型，包括BYTEARRAY、DOUBLE、FLOAT、INTEGER、LONG和SHORT。|是|
|valueType|Kafka的value的类型，包括BYTEARRAY、DOUBLE、FLOAT、INTEGER、LONG和SHORT。|是|
|beginDateTime|数据消费的开始时间位点，为时间范围（左闭右开）的左边界。yyyymmddhhmmss格式的时间字符串，可以和[时间属性](cn.zh-CN/使用指南/数据开发/调度配置/时间属性.md#)配合使用。Kafka 0.10.2以上的版本支持此功能。|需要和beginOffset二选一。 **说明：** beginDateTime和endDateTime配合使用。

 |
|endDateTime|数据消费的结束时间位点，为时间范围（左开右闭）的右边界。yyyymmddhhmmss格式的时间字符串，可以和[时间属性](cn.zh-CN/使用指南/数据开发/调度配置/时间属性.md#)配合使用。Kafka 0.10.2以上的版本支持此功能。|需要和endOffset二选一。 **说明：** endDateTime和beginDateTime配合使用。

 |
|beginOffset|数据消费的开始时间位点，您可以配置以下形式。 -   例如15553274的数字形式，表示开始消费的点位。
-   seekToBeginning：表示从开始点位消费数据。
-   seekToLast：表示从上次的偏移位置读取数据。
-   seekToEnd：表示从最后点位消费数据，会读取到空数据。

 |需要和beginDateTime二选一。|
|endOffset|数据消费的结束位点，用来控制什么时候应该结束数据消费任务退出。|需要和endDateTime二选一。|
|skipExceedRecord|Kafka使用`public ConsumerRecords<K, V> poll(final Duration timeout)`消费数据，一次poll调用获取的数据可能在endOffset或者endDateTime之外。skipExceedRecord用来控制这些多余的数据是否写出到目的端。由于消费数据使用了自动点位提交，建议： -   Kafka 0.10.2之前版本：建议skipExceedRecord配置为false。
-   Kafka 0.10.2及以上版本：建议skipExceedRecord配置为true。

 |否，默认值为false。|
|partition|Kafka的一个topic有多个分区（partition），正常情况下数据同步任务是读取topic（多个分区）一个点位区间的数据。您也可以指定partition，仅读取一个分区点位区间的数据。|否，无默认值。|
|kafkaConfig|创建Kafka数据消费客户端KafkaConsumer可以指定扩展参数，例如bootstrap.servers、auto.commit.interval.ms、session.timeout.ms等，您可以基于kafkaConfig控制KafkaConsumer消费数据的行为。|否|

kafkaConfig参数说明如下：

-   fetch.min.bytes：指定消费者从broker获取消息的最小字节数，即等到有足够的数据时才把它返回给消费者。
-   fetch.max.wait.ms：等待broker返回数据的最大时间，默认500ms。fetch.min.bytes和fetch.max.wait.ms哪个条件先得到满足，便按照哪种方式返回数据。
-   max.partition.fetch.bytes：指定broker从每个partition中返回给消费者的最大字节数，默认1MB。
-   session.timeout.ms：指定消费者不再接收服务之前，可以与服务器断开连接的时间，默认是30s。
-   auto.offset.reset：消费者在读取没有偏移量或者偏移量无效的情况下（因为消费者长时间失效，包含偏移量的记录已经过时并被删除）的处理方式。默认为latest（消费者从最新的记录开始读取数据），可更改为earliest（消费者从起始位置读取partition的记录）。
-   max.poll.records：单次调用poll方法能够返回的消息数量。
-   key.deserializer：消息key的反序列化方法，例如org.apache.kafka.common.serialization.StringDeserializer。
-   value.deserializer：数据value的反序列化方法，例如org.apache.kafka.common.serialization.StringDeserializer。
-   ssl.truststore.location：SSL根证书的路径。
-   ssl.truststore.password：根证书store的密码，如果是Aliyun Kafka，则配置为KafkaOnsClient。
-   security.protocol：接入协议，目前支持使用SASL\_SSL协议接入。
-   sasl.mechanism：SASL鉴权方式，如果是Aliyun Kafka，使用PLAIN。

配置示例如下：

``` {#codeblock_liq_ge7_w4c}
{
    "group.id": "demo_test",
    "java.security.auth.login.config": "/home/admin/kafka_client_jaas.conf",
    "ssl.truststore.location": "/home/admin/kafka.client.truststore.jks",
    "ssl.truststore.password": "KafkaOnsClient",
    "security.protocol": "SASL_SSL",
    "sasl.mechanism": "PLAIN",
    "ssl.endpoint.identification.algorithm": ""
}
```

## 脚本开发示例 {#section_ssm_rcz_y3l .section}

从Kafka读取数据的JSON配置，如下所示。

``` {#codeblock_l79_h8g_04l}
{
    "type": "job",
    "steps": [
        {
            "stepType": "kafka",
            "parameter": {
                "server": "host:9093",
                "column": [
                    "__key__",
                    "__value__",
                    "__partition__",
                    "__offset__",
                    "__timestamp__",
                    "'123'",
                    "event_id",
                    "tag.desc"
                ],
                "kafkaConfig": {
                    "group.id": "demo_test"
                },
                "topic": "topicName",
                "keyType": "ByteArray",
                "valueType": "ByteArray",
                "beginDateTime": "20190416000000",
                "endDateTime": "20190416000006",
                "skipExceedRecord": "false"
            },
            "name": "Reader",
            "category": "reader"
        },
        {
            "stepType": "stream",
            "parameter": {
                "print": false,
                "fieldDelimiter": ","
            },
            "name": "Writer",
            "category": "writer"
        }
    ],
    "version": "2.0",
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
            "throttle": false,
            "concurrent": 1,
            "dmu": 1
        }
    }
}
```

