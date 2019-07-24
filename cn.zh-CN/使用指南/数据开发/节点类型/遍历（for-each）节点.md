# 遍历（for-each）节点 {#concept_183549 .concept}

本文将为您介绍如何通过for-each节点实现循环2次，每次循环中把当前的循环次数打印出来的需求。

**说明：** 您需要购买DataWorks标准版及以上版本，方可使用for-each节点功能。

## 创建工作流 {#section_sj5_17z_kmo .section}

1.  进入DataStudio（数据开发）页面，选择**新建** \> **控制** \> **for-each**。

    ![for-each](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/157612/156397037644372_zh-CN.png)

    **说明：** 您也可以找到相应的业务流程，右键单击**控制**，选择**新建控制节点** \> **for-each**。

    ![for-each](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/157612/156397037652894_zh-CN.png)

2.  填写新建节点对话框中的配置，单击**提交**。

    ![for-each](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/157612/156397037644376_zh-CN.png)

3.  创建的工作流上游为赋值节点，下游为遍历节点。

    ![赋值节点](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/157612/156397037644381_zh-CN.png)

    上游赋值节点选择的是Shell节点，代码如下。

    ``` {#codeblock_9ye_wvg_5xb}
    echo 'this is name,ok';
    ```

    赋值节点默认一个outputs参数。

    ![output参数](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/157612/156397037744385_zh-CN.png)


**说明：** 

-   遍历节点的start节点和end节点不能编辑，其逻辑是固定的。
-   Shell节点中的代码修改后一定要保存，提交时不会提示您进行保存，如果没有保存，最新的代码便不能及时更新。

Shell节点的代码为：

``` {#codeblock_q7w_51t_ksy}
echo ${dag.loopTimes}  ----打印循环的次数。
```

遍历节点支持以下四种环境变量。

-   $\{dag.foreach.current\}：当前遍历到的数据行。
-   $\{dag.loopDataArray\}：输入的数据集。
-   $\{dag.offset\}：偏移量。
-   $\{dag.loopTimes\}：当前循环次数，值为$\{dag.offset\}+1。

``` {#codeblock_e20_ayj_czj}
// 以常见的for循环代码进行类比
data=[]  // 相当于${dag.loopDataArray}
// i相当于${dag.offset}
for(int i=0;i<data.length;i++) {
  print(data[i]);  // data[i]相当于${dag.foreach.current}
}
```

遍历节点默认参数名为loopDataArray，取值来源是上游赋值节点的outputs参数，需要手动添加，如果没有添加，提交时会报错。

![loopDataArray](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/157612/156397037744387_zh-CN.png)

提交后发布，进入运维中心页面查看相应结果。

![运维中心](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/157612/156397037744388_zh-CN.png)

遍历节点的结果如下图所示。

![遍历结果](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/157612/156397037744389_zh-CN.png)

![遍历结果](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/157612/156397037744391_zh-CN.png)

![遍历结果](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/157612/156397037744392_zh-CN.png)

