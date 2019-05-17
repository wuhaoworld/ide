# ETL文档 {#concept_186695 .concept}

## 表总览 {#section_m52_k3l_b7e .section}

|表名|说明|
|--|--|
|ods\_raw\_log\_d|离源ODS层最近的数据|
|dwd\_user\_info\_d|用户公共明细表|
|dws\_user\_info\_d|用户公共汇总表|
|dim\_user\_info\_d|用户数据集市表|
|rpt\_user\_info\_d|用户分析汇总表|

## 节点dwd\_user\_info\_d {#section_o7q_3m8_okc .section}

|任务（节点）名称 dwd\_user\_info\_d|
|字段名称|目标表字段|字段说明|源表|涉及源表字段|算法说明|备注|
|---------------------------|
|----|-----|----|--|------|----|--|
|uid|用户id|用户id|ods\_log\_info\_d|uid|抽取汇总| |
|gender|性别|性别|ods\_log\_info\_d|time|抽取| |
|age\_range|年龄段|年龄段|ods\_log\_info\_d|status|抽取| |
|zodiac|星座|星座|ods\_log\_info\_d|bytes|抽取| |
|region|地域，根据IP获取|地域，根据IP|ods\_log\_info\_d|region|转换| |
|device|终端类型|终端类型|ods\_log\_info\_d|method|抽取| |
|identity|访问类型 crawler feed user unknown|访问类型 crawler feed user unknown|ods\_log\_info\_d|url|抽取| |
|method|http请求类型|http请求类型|ods\_log\_info\_d|protocol|抽取| |
|url|url|url|ods\_log\_info\_d|referer|截取引用IP| |
|referer|来源url|来源url|ods\_log\_info\_d|device|截取设备名称| |
|time|时间yyyymmddhh:mi:ss|时间yyyymmddhh:mi:ss|ods\_log\_info\_d|identity| | |

