# 通过数据集成导入数据到Elasticsearch {#concept_ckd_32b_pfb .concept}

本文将为您介绍如何通过数据集成对离线Elasticsearch进行数据导入的操作。

## 准备工作 {#section_0q7_szp_y0u .section}

1.  准备阿里云账号，并创建账号的访问密钥，即AccessID和AccessKey。详情请参见[准备阿里云账号](../../../../intl.zh-CN/准备工作/管理员使用云账号/准备阿里云账号.md#)。
2.  开通MaxCompute，自动产生一个默认的MaxCompute数据源，并使用主账号登录DataWorks。
3.  创建工作空间，您可以在工作空间中协作完成业务流程，共同维护数据和任务等，因此使用DataWorks之前需要先创建一个工作空间。详情请参见[创建工作空间](../../../../intl.zh-CN/准备工作/管理员使用云账号/创建工作空间.md#)。

    **说明：** 如果您想通过子账号创建数据集成任务，可以赋予其相应的权限。详情请参见[准备RAM用户](../../../../intl.zh-CN/准备工作/管理员使用云账号/准备RAM用户.md#)和[成员管理](intl.zh-CN/使用指南/工作空间管理/成员管理.md#)。

4.  配置好相关的数据源，详情请参见[数据源配置](https://www.alibabacloud.com/help/faq-list/72788.htm)。

## 新建数据同步节点 {#section_ky2_x5f_svq .section}

1.  以开发者身份登录[DataWorks控制台](https://workbench.data.aliyun.com/console)，单击相应工作空间后的**进入数据开发**。
2.  新建业务流程。
    1.  右键单击**业务流程**，选择**新建业务流程**。

        ![新建业务流程](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16288/15677413087643_zh-CN.png)

    2.  在新建业务流程对话框中，填写**业务流程名称**和**描述**。

        ![新建业务流程](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16288/156774130913575_zh-CN.png)

    3.  单击**新建**，即可完成业务流程的创建。
3.  展开业务流程，右键单击**数据集成**，选择**新建数据集成节点** \> **数据同步**。

    ![数据同步](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16216/15677413097612_zh-CN.png)

4.  填写新建节点对话框中的配置，单击**提交**。

    ![配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/24565/156774130914346_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**节点类型**|默认数据同步类型。|
    |**节点名称**|填写该节点名称。|
    |**目标文件夹**|默认放在相应的业务流程下。|


## 配置数据同步节点 {#section_q2s_hv2_4fb .section}

1.  成功创建数据同步节点后，单击工具栏中的**转换脚本**。

    ![转换脚本](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16217/156774130951386_zh-CN.png)

2.  单击提示对话框中的**确认**，即可进入脚本模式进行开发。

    ![转换脚本](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16217/15677413097631_zh-CN.png)

3.  单击工具栏中的**导入模板**。

    ![导入模板](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16217/156774130951385_zh-CN.png)

4.  填写导入模板对话框中的配置。

    ![导入模板](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/24565/156774130914348_zh-CN.png)

    |配置|说明|
    |:-|:-|
    |**来源类型**|此处选择**MySQL**类型。|
    |**数据源**|选择配置好的MySQL数据源。|
    |**目标类型**|此处选择**Elasticsearch**类型。|
    |**数据源**|选择配置好的Elasticsearch数据源。|

5.  单击**确认**，根据自身情况进行配置。

    ``` {#codeblock_kwd_1vx_wsv}
    {
    "configuration": {
    "setting": {
      "speed": {
        "concurrent": "1", //作业并发数。
        "mbps": "1" //作业速率上限。
      }
    },
    "reader": {
      "parameter": {
        "connection": [
          {
            "table": [
              "`es_table`" //源端表名。
            ],
            "datasource": "px_mysql_OK" //数据源名，建议和添加的数据源名保持一致。
          }
        ],
        "column": [ //源端表的列名。
          "col_ip",
          "col_double",
          "col_long",
          "col_integer",
          "col_keyword",
          "col_text",
          "col_geo_point",
          "col_date"
        ],
        "where": "", //过滤条件。
      },
      "plugin": "mysql"
    },
    "writer": {
      "parameter": {
        "cleanup": true, //是否在每次导入数据到Elasticsearch时清空原有数据，全量导入/重建索引的时候需要设置为true，同步增量的时候必须为false。此处为同步增量，需要设置为false。
        "accessKey": "nimda", //如果使用了X-PACK插件，需要填写password；如果未使用，则填空字符串即可。阿里云Elasticsearch使用了X-PACK插件，需要填写password。
        "index": "datax_test", // Elasticsearch的索引名称，如果之前没有，插件会自动创建。
        "alias": "test-1-alias", //数据导入完成后写入别名。
        "settings": {
          "index": {
            "number_of_replicas": 0,
            "number_of_shards": 1
          }
        },
        "batchSize": 1000, //每次批量数据的条数。
        "accessId": "default", //如果使用了X-PACK插件，需要填写username；如果未使用，则填空字符串即可。阿里云Elasticsearch使用了X-PACK插件，需要填写username。
        "endpoint": "http://xxx.xxxx.xxx:xxxx", //Elasticsearch的连接地址，可以在控制台查看。
        "splitter": ",", //如果插入数据是array，则使用指定分隔符。
        "indexType": "default", //Elasticsearch中相应索引下的类型名称。
        "aliasMode": "append", //数据导入完成后增加别名的模式，append（增加模式），exclusive（只留这一个）。
        "column": [ //Elasticsearch中的列名，顺序和Reader中的Column顺序一致。
          {
            "name": "col_ip",//对应于TableStore中的属性列：name。
            "type": "ip"//文本类型，采用默认分词。
          },
          {
            "name": "col_double",
            "type": "string"
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
            "type": "text"
          },
          {
            "name": "col_geo_point",
            "type": "geo_point"
          },
          {
            "name": "col_date",
            "type": "date"
          }
        ],
        "discovery": false//是否自动发现，设置为true。
      },
      "plugin": "elasticsearch"//Writer插件的名称：ElasticsearchWriter，不需要修改。
    }
    },
    "type": "job",
    "version": "1.0"
    }
    ```

6.  配置完成后，单击**保存**并**运行**。

    **说明：** 

    -   Elasticsearch仅支持以脚本模式导入数据。
    -   如果想选择新模板，可以单击工具栏中的**导入模板**。一旦导入新模板，原有内容将会被全部覆盖。
    -   同步任务保存后，直接单击**运行**，任务会立刻运行。您也可以单击**提交**，提交同步任务至调度系统中，调度系统会按照配置属性在从第二天开始自动定时执行。

## 参考文档 {#section_cvw_n2b_pfb .section}

其它类型的数据源配置同步任务的详情，请参见下述文档：

-   [配置Reader插件](https://www.alibabacloud.com/help/faq-list/74300.htm)。
-   [配置Writer插件](https://www.alibabacloud.com/help/faq-list/74301.htm)。

