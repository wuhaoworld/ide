# Supported data sources {#concept_uzy_hgv_42b .concept}

Data Integration is a stable, efficient, and elastically scalable data synchronization platform provided by the Alibaba Group to external users. It provides offline \(batch\) data access channels for Alibaba Cloud's big data computing engines \(including MaxCompute, AnalyticDB, and OSS\).

The following table lists the data source types supported by Data Synchronization:

|Data Source category|Data source type|Extraction \(Reader\)|Import \(Writer\)|Support Methods|Supported types:|
|:-------------------|:---------------|:--------------------|:----------------|:--------------|:---------------|
|Relational Databases|[MySQL](reseller.en-US/User Guide/Data integration/Data source configuration/Configure MySQL data source.md#)|Yes, see [Configure MySQL Reader](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Reader plug-in/Configure MySQL Reader.md#) for details.|Yes, see [Configure MySQL Writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configure MySQL Writer.md#) for details.|Wizard/script|Alibaba Cloud/self-built|
|Relational Databases|[SQL Server](reseller.en-US/User Guide/Data integration/Data source configuration/Configuring SQL server data source.md#)|Yes, see [Configuring SQL server Reader](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Reader plug-in/Configuring SQL server Reader.md#) for details.|Yes, see [Configure SQL Server Writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configure SQL Server Writer.md#) for details.|Wizard/script|Alibaba Cloud/self-built|
|Relational Database|[PostgreSQL](reseller.en-US/User Guide/Data integration/Data source configuration/Configure PostgreSQL data source.md#)|Yes, see [Configuring PostgreSQL Reader](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Reader plug-in/Configuring PostgreSQL Reader.md#) for details.|Yes, see [Configure PostgreSQL Writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configure PostgreSQL Writer.md#) for details.|Wizard/script|Alibaba Cloud/self-built|
|Relational Databases|[Oracle](reseller.en-US/User Guide/Data integration/Data source configuration/Configure Oracle data source.md#)|Yes, see [Configure Oracle Reader](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Reader plug-in/Configure Oracle Reader.md#) for details.|Yes, see [Configuring Oracle Writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configuring Oracle Writer.md#) for details.|Wizard/script|Self-developed|
|Relational Databases|[DRDS](reseller.en-US/User Guide/Data integration/Data source configuration/Configure DRDS data sources.md#)|Yes, see [Configure DRDS Reader](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Reader plug-in/Configure DRDS Reader.md#) for details.|Yes, see [Configure DRDS Writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configure DRDS Writer.md#) for details.|Wizard/script|Alibaba Cloud|
|Relational Databases-|DB2|Yes, see [Configure DB2 Reader](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Reader plug-in/Configure DB2 Reader.md#) for details.|Yes, see [Configure DB2 writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configure DB2 writer.md#) for details.|script|Self-developed-|
|Relational Databases|[DM](reseller.en-US/User Guide/Data integration/Data source configuration/Configure the DM data source.md#)|Yes|Yes|script|Self-developed|
|Relational Databases|RDS for PPAS|Yes|Yes|script|Alibaba Cloud|
|MPP|HybridDB for MySQL|Yes|Yes|Wizard/script|Alibaba Cloud|
|MPP|HybridDB for PostgreSQL released|Yes|Yes|Wizard/script|Alibaba Cloud|
|Big data storage|[Maxcompute](reseller.en-US/User Guide/Data integration/Data source configuration/Configure MaxCompute data source.md#) \(corresponding data source name: ODPS\)|Yes, see [Configure MaxCompute Reader](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Reader plug-in/Configure MaxCompute Reader.md#) for details.|Yes, see [Configure MaxCompute Writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configure MaxCompute Writer.md#) for details.|Wizard/script|Alibaba Cloud|
|Big data storage|[DataHub](reseller.en-US/User Guide/Data integration/Data source configuration/DataHub data source.md#)|No|Yes, see [Configure DataHub Writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configure DataHub Writer.md#) for details.|script|Alibaba Cloud|
|Big data storage|ElasticSearch|No|Yes, see [Configure ElasticSearch Writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configure ElasticSearch Writer.md#) for details.|script|Alibaba Cloud|
|Big data storage|[Analyticdb](reseller.en-US/User Guide/Data integration/Data source configuration/Configure the AnalyticDB data source.md#) \(corresponding data source name: ADS\)|No|Yes, see [Configure AnalyticDB Writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configure AnalyticDB(ADS) Writer.md#) for details.|Wizard/script|Alibaba Cloud|
|Unstructured storage|[OSS](reseller.en-US/User Guide/Data integration/Data source configuration/Configure OSS data source.md#)|Yes, see [Configure OSS Reader](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Reader plug-in/Configure OSS Reader.md#) for details.|Yes, see [Configure OSS Writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configure OSS Writer.md#) for details.|Wizard/script|Alibaba Cloud|
|Unstructured storage|[HDFS](reseller.en-US/User Guide/Data integration/Data source configuration/Configuring HDFS data source.md#)|Yes, see [Configuring HDFS Reader](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Reader plug-in/Configuring HDFS Reader.md#) for details.|Yes, see [Configure HDFS Writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configure HDFS Writer.md#) for details.|script|Self-developed|
|Unstructured storage|[FTP](reseller.en-US/User Guide/Data integration/Data source configuration/Configure the FTP data source.md#)|Yes, see [Configuring FTP Reader](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Reader plug-in/Configuring FTP Reader.md#) for details.|Yes, see [Configure FTP Writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configure FTP Writer.md#) for details.|Wizard/script|Self-developed|
|Message Queue|[LogHub](reseller.en-US/User Guide/Data integration/Data source configuration/Add LogHub data source.md#)|Yes, see [Configure LogHub Reader](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Reader plug-in/Configure LogHub Reader.md#) for details.|Yes, see [Configure LogHub Writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configure LogHub Writer.md#) for details.|Wizard/script|Alibaba Cloud|
|NoSQL|HBase|Yes, see [Configure HBase Reader](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Reader plug-in/Configure HBase Reader.md#) for details.|Yes, see [Configure HBase Writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configure HBase Writer.md#) for details.|script|Alibaba Cloud/self-built|
|NoSQL|[MongoDB](reseller.en-US/User Guide/Data integration/Data source configuration/Configure MongoDB data source.md#)|Yes, see [Configure MongoDB Reader](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Reader plug-in/Configure MongoDB Reader.md#) for details.|Yes, see [Configure MongoDB Writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configure MongoDB Writer.md#) for details.|script|Alibaba Cloud/self-built|
|NoSQL|[Memcache](reseller.en-US/User Guide/Data integration/Data source configuration/Configure Memcached data source.md#)|No|Yes, see [Configure Memcache \(OCS\) Writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configure Memcache (OCS) Writer.md#) for details.|script|Alibaba Cloud/self-built memcached|
|NoSQL|[Table store](reseller.en-US/User Guide/Data integration/Data source configuration/SConfigure OTS data source.md#) \(corresponding data source name: OTS\)|Yes, see [Configure Table Store\(OTS\) Reader](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Reader plug-in/Configure Table Store(OTS) Reader.md#) for detaials.|Yes, see [Configure Table Store \(OTS\) Writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configure Table Store (OTS) Writer.md#) for details.|script|Alibaba Cloud|
|NoSQL|OpenSearch|No|Yes, see [Configure OpenSearch Writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configure OpenSearch Writer.md#) for details|script|Alibaba Cloud|
|NoSQL|[Redis](reseller.en-US/User Guide/Data integration/Data source configuration/Configure Redis data source.md#)|No|Yes, see [Configure Redis Writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configure Redis Writer.md#) for details.|script|Alibaba Cloud/self-built|
|Performance Testing|Stream|Yes, see [Configure Stream Reader](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Reader plug-in/Configure Stream Reader.md#) for details.|Yes, see [Configure Stream Writer](reseller.en-US/User Guide/Data integration/Task Configuration/Configure Writer plug-in/Configure Stream Writer.md#) for details.|script|-|
