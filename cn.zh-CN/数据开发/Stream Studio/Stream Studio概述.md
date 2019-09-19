# Stream Studio概述 {#concept_ltf_j3j_wgb .concept}

Stream Studio是DataWorks旗下的一站式实时计算开发平台，请加入钉钉DataWorks Stream Studio交流群（群号：23359532）获取更多支持。

Stream Studio基于阿里云[实时计算引擎](../../../../cn.zh-CN/产品简介/什么是阿里云实时计算.md#)（基于Flink）构建，集DAG和SQL两种开发模式为一体，并且支持DAG与SQL两种模式互相转换，通过可视化拖拽您就可以轻松实现实时计算作业开发。

Stream Studio是您开发实时计算作业的理想平台，核心功能特性如下：

-   支持DAG模式，通过可视化拖拽即可实现实时计算作业开发。
-   支持[Flink SQL](../../../../cn.zh-CN/Flink SQL开发指南/Flink SQL/Flink SQL概述.md#)模式，您可以选择单纯通过SQL开发实时计算作业。
-   支持DAG与Flink SQL互转，方便查看SQL的算子结构。
-   支持Function Studio在线开发UDF，支持一键发布UDF（仅独享模式支持）。
-   支持作业智能诊断，方便排查线上作业问题。

## 实时计算任务开发流程 {#section_hta_gq4_6mk .section}

通常情况下，通过Stream Studio实现实时计算任务的开发和运维，包含以下操作：

1.  数据采集

    数据需要经过采集，方可进入大数据系统。为最大化利用您现有的流式存储系统，阿里云实时计算对接了多种上游的流式存储，让您无需额外进行数据的采集，即可享受现有的数据流式存储。详情请参见[数据存储概述](../../../../cn.zh-CN/Flink SQL开发指南/数据存储/数据存储概述.md#)。

2.  新建实时计算任务

    完成数据的采集后，新建实时计算任务并通过Stream Studio进行数据开发，详情请参见[新建实时计算任务](cn.zh-CN/数据开发/Stream Studio/新建实时计算任务.md#)。

3.  任务运维

    完成任务的开发和发布后，单击Stream Studio页面右上角的**运维**，即可进入任务运维页面。目前Stream Studio的任务运维功能直接对接原有实时计算开发平台（Bayes），详情请参见[数据运维](../../../../cn.zh-CN/Flink SQL开发指南/作业运维/运行信息.md#)。


