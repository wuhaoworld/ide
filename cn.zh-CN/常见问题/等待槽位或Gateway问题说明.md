# 等待槽位或Gateway问题说明 {#concept_kz4_kvv_1gb .concept}

本文将为您介绍任务运行等待槽位或Gateway的原因与解决方案。

## 问题描述 {#section_xvz_nvv_1gb .section}

DataWorks任务未按时调度运行，运行日志中显示：**槽位等待**、**正在等待在云端的gateway资源**等信息。

## 问题原因 {#section_ptt_nvv_1gb .section}

DataWorks免费为您提供了一定的任务调度能力，但如果达到一定的任务并发量，则需等待运行中的任务结束后，方可继续运行等待中的任务。

## 解决方案 {#section_hhk_nvv_1gb .section}

在可满足业务诉求的前提下，建议您合理安排任务错峰运行，以便在各个时间段，充分利用已购买的计算资源。 如果需要获得更高任务并发调度能力，请将如下内容[提交工单](https://workorder.console.aliyun.com/console.htm#/ticket/add?productCode=ide&commonQuestionId=1421&isSmart=true)以进行评估。

1.  业务场景。
2.  期望的高峰期DataWorks任务并发量。
3.  任务无法错峰运行的原因。

我们将根据实际情况为您制定解决方案。

**说明：** 后续出现上述问题，可购买DataWorks独享资源，详情请参见[DataWorks独享资源](../../../../cn.zh-CN/产品定价/预付费（包年包月）/DataWorks独享资源.md#)。

-   独享调度资源可解决等待Gateway的资源。
-   独享数据集成资源可解决同步任务的资源。

如果您要保障数据集成任务的顺利运行，两种独享资源均需购买。

