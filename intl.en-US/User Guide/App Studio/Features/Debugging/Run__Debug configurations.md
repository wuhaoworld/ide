# Run/Debug configurations {#concept_enk_s3p_fhb .concept}

You can configure the entry function, start debugging, and set breakpoints to debug an app.

## Configure the entry function {#section_j3h_y3p_fhb .section}

|Parameter|Description|
|:--------|:----------|
|**Main class**|The class of the main function to be started. Select a value from the drop-down list.|
|**VM options**|The parameters for starting a Java Virtual Machine \(JVM\), for example, -D, -Xms, and -Xmx.|
|**Program arguments**|The startup parameter, which is obtained by the args parameter in the main function.|
|**Environment Variables**|The environment variable parameters.|
|**PORT**|The port to be exposed in the app, for example, classic port 7001 or port 8080 for Spring Boot-based projects.|
|**Machine**|The type of the ECS instance used for debugging.|
|**HotCode**|This configuration takes effect only in Run mode. Alibaba Cloud's HotCode2 plug-in is used by default.|

## Start debugging {#section_qx3_kjp_fhb .section}

In the top navigation bar, choose **Debug** \> **Start Debugging**.

The initial startup process takes a longer time because App Studio needs to prepare the runtime environment and download Maven dependencies. When you restart debugging, App Studio skips this process and provides user experience similar to that in a local IDE.

