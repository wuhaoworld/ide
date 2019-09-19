# UDTF {#concept_gxj_lwf_xgb .concept}

UDTF组件即自定义函数组件，相当于SQL中的UDTF子句。

**说明：** 仅实时计算服务的独享模式支持UDTF组件，详情请参见[UDTF使用说明](../../../../../cn.zh-CN/开发/SQL及函数/UDF/UDTF使用说明.md#)。

## 配置面板说明 {#section_ws5_qwf_xgb .section}

![配置面板](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/131687/156888006639597_zh-CN.png)

|参数|注释说明|
|--|----|
|**Join模式**|支持INNER JOIN和LEFT OUTER JOIN两种模式。 -   INNER JOIN：UDTF有结果才返回。
-   LEFT OUTER JOIN：UDTF无结果补NULL。

 |
|**选择函数**|选择函数名称。您需要先在资源引用中上传程序包，然后在资源引用面板中勾选程序包，以表明当前任务引用了此程序包。|
|**参数表达式**|选择函数后填写对应的输入、输出参数。|
|**选择输出字段**|选择要输出的字段，此处可以定义字段名、字段别名和字段表达式。|

