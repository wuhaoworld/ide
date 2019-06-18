# UT测试 {#concept_ebn_zf1_dhb .concept}

App Studio目前支持自动生成UT代码、检测UT测试入口、运行UT代码和展示运行结果等功能。

## 自动生成UT代码 {#section_xd2_hv4_fhb .section}

打开相应文件后，右键单击代码编辑区，选择**Generate** \> **Create Test**，即可在Test目录下自动生成测试类和测试代码。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/139469/156085253741735_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/139469/156085253741736_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/139469/156085253841744_zh-CN.png)

## 检测UT测试入口 {#section_ojt_hg1_dhb .section}

**说明：** 

-   UT类需要写在src/test/java目录下。如果Java UT类文件不在该目录下，将无法被正常识别成Java UT类。
-   @Test注解下的方法会出现Run Test的UT运行入口。

完成Java类的创建后，在对应的测试用例方法上添加`org.junit.Test`的**@Test**注解即可。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/139469/156085253840893_zh-CN.png)

## 运行UT代码 {#section_ycf_wg1_dhb .section}

单击右上角的运行按钮，即可运行UT的测试用例。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/139469/156085253940894_zh-CN.png)

## 展示UT运行结果 {#section_4xo_ukd_7yd .section}

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/139469/156085253940895_zh-CN.png)

