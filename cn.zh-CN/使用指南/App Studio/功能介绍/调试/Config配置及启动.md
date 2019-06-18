# Config配置及启动 {#concept_enk_s3p_fhb .concept}

您可通过配置入口函数，单击调试、断点等步骤，进行程序的调试。

## 配置入口函数 {#section_j3h_y3p_fhb .section}

![](images/41761_zh-CN.gif)

|配置|说明|
|:-|:-|
|**MainClass**|您可以从多个配置中选择需要启动的main函数。|
|**VM options**|您可以配置在JVM启动时，例如-D -Xms -Xmx等配置。|
|**Program arguments**|您可以添加启动参数，此参数会被main函数的args参数接收。|
|**Environment**|环境变量参数。|
|**PORT**|端口，表示本程序需要暴露的端口信息，例如springboot经典的7001、8080等端口。|
|**机器**|您可以选择需要的机器配置进行调试。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/150118/156085274941765_zh-CN.png)

|
|**HotCode**|此配置仅在run模式下生效，默认使用公司的HotCode2插件进行启动。|

## 启动调试 {#section_qx3_kjp_fhb .section}

选择菜单栏中的**调试** \> **启动调试**。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/150118/156085274941766_zh-CN.png)

因为需要为您准备运行环境和下载mvn依赖，第一次启动时速度较慢。重启调试会跳过此步骤，启动速度逐渐接近本地编辑器的体验。

![](images/41768_zh-CN.gif)

