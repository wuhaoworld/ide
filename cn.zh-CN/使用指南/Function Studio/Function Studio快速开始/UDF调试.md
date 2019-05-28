# UDF调试 {#concept_ttg_zz3_5gb .concept}

UDF调试包括UDF（仅支持Java）、UDAF和UDTF的调试。

## UDF调试（目前仅支持Java） {#section_vl2_1fb_rfb .section}

1.  新建main函数。

    Function Studio目前支持通过main函数调用UDF，进行在线调试。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64980/155903259032986_zh-CN.png)

2.  设置Debug配置。

    单击右上角的**config**，进入配置页面。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64980/155903259032987_zh-CN.png)

    您只需要选择新建的main函数，其他的信息都是自动生成的。

    |配置|说明|
    |:-|:-|
    |**Main class**|选择需要调试的入口函数，必填项。|
    |**VM options**|需要启动的JVM参数，非必填项。|
    |**Program Variables**|启动参数，非必填项。|
    |**JRE**|目前仅支持JDK1.8。|
    |**PORT**|需要开放的HTTP端口，UDF/UDAF/UDTF类的项目此配置为非必填项。|
    |**机器**|机器规格。|
    |**开启HOTCODE**|是否需要支持热部署。|

3.  启动Debug。

    在Lower的evaluate函数上断点后，启动**Debug**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64980/155903259032988_zh-CN.png)

    启动成功后即可进行正常的调试。可通过step into进入到UDF方法内，并查看变量值。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64980/155903259032989_zh-CN.png)


## UDAF调试 {#section_kbf_m3b_rfb .section}

UDAF的调试需要自己构造相关数据，并且使用warehouse来模拟MaxCompute的数据。warehouse下会保存相关表的Schema以及Data，然后编写相关测试的main函数。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64980/155903259032991_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64980/155903259032992_zh-CN.png)

初始化warehouse后，调用相关的UDAF进行测试。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64980/155903259032993_zh-CN.png)

## UDTF的调试 {#section_ktp_t5t_xfb .section}

UDTF与UDAF的调试一样，初始化工程中已存在UDTF的测试类，直接执行该类，即可模拟真实数据对UDTF进行调试。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64980/155903259032995_zh-CN.png)

单击**执行**，如果程序没有抛异常，则表示运行通过。

