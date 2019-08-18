# DataService Studio {#concept_chw_x32_v2b .concept}

This topic describes how to check DataService Studio APIs that you have permissions to call in App Studio. This topic also describes how to generate code snippets to quickly access DataService Studio APIs through App Studio.

For more information about how to apply for and call DataService Studio APIs and SDKs, see [DataService Studio](intl.en-US/User Guide/DataService studio/DataService studio overview.md#).

## Prerequisites {#section_p4j_prf_hhb .section}

Before accessing DataService Studio, make sure that the following conditions are met:

-   You have created a workspace in DataService Studio and applied for permissions to call the APIs for the workspace.

    This topic is applicable to DataService Studio APIs that you have permissions to call. Therefore, you must first go to DataService Studio and check whether a workspace is available and whether the APIs that you have permissions to call exist in the workspace.

-   You have created a Java project in App Studio.

    The following section uses a Spring Boot-based project as an example to describe how to generate code snippets.

    1.  Log on to App Studio. On the Projects page, click **Create Project from Code**.
    2.  On the Create Project page, specify **Project Name** and **Project Description**, and set Runtime Environment to **springboot sample template**.
    3.  After the configuration is completed, click **Submit**.
    After the project is created, make sure that the pom.xml file contains the dependency of DataService Studio. For more information about the Maven coordinates, see [Nexus Repository Manager](https://oss.sonatype.org/#nexus-search;quick~aliyun-dataworks-dataservice-java-sdk).

    ``` {#codeblock_e71_um7_5ib}
    <dependency>
      <groupId>com.aliyun.dataworks</groupId>
      <artifactId>aliyun-dataworks-dataservice-java-sdk</artifactId>
      <version>0.0.1-aliyun</version>
    </dependency>
    ```


## Use DataService Studio APIs in App Studio {#section_zvk_htf_hhb .section}

You can use DataService Studio APIs through code or the WYSIWYG designer.

-   Use DataService Studio APIs through code.

    The following section describes how to view available DataService Studio APIs in App Studio by keyword, project, and service group. You can also use the feature of generating code snippets to quickly create the code to call a DataService Studio API.

    1.  View the list of DataService Studio APIs.

        Click the Data tab on the right. The list of DataService Studio APIs appears. You can filter the APIs by name, project, or service group.

    2.  Create an API on DataService Studio.

        You can click Create API in DataService Studio in the upper-right corner and create an API to call.

    3.  View details about DataService Studio APIs.

        Click **Details** in the Actions column of a DataService Studio API. The DataService Studio page appears, showing the details of the API.

    4.  Quickly generate the access code.

        App Studio allows you to create the access code with one click. It automatically enters the AppKey and AppSecret and generates the sample controller code, facilitating you to directly insert a project.

        Click **Select** in the Actions column of a DataService Studio API. The details page that includes the sample access code appears.

        The following section provides an example of the complete controller code. In the generated InvokeApi2252\(\) method, the path, host, AppKey, and AppSecret required for accessing the DataService Studio API are automatically entered. ApiRequest2252DTO contains all parameters required for accessing the DataService Studio API.

        ``` {#codeblock_6fb_fb4_sna}
        package com.alibaba.dataworks.dataservice;
        import com.aliyun.dataworks.dataservice.model.api.protocol.ApiProtocol;
        import com.aliyun.dataworks.dataservice.sdk.facade.DataApiClient;
        import com.aliyun.dataworks.dataservice.sdk.loader.http.Request;
        import org.slf4j.Logger;
        import org.slf4j.LoggerFactory;
        import org.springframework.beans.factory.annotation.Autowired;
        import org.springframework.web.bind.annotation.RequestBody;
        import org.springframework.web.bind.annotation.RequestMapping;
        import org.springframework.web.bind.annotation.RequestMethod;
        import org.springframework.web.bind.annotation.RestController;
        import java.lang.reflect.Field;
        import java.util.HashMap;
        /**
         * @author ****
         * @date 2019-03-21T17:23:17.040
         * - Before use, make sure that the pom.xml file contains the latest data-service-client dependency.
         *     <dependency>
         *         <groupId>com.alibaba.dataworks</groupId>
         *         <artifactId>data-service-client</artifactId>
         *         <version>${latest-data-service-version}</version>
         *     </dependency>
         * - Before use, make sure that the spring config class is separately configured and is not combined with other config classes.
         *     @Configuration
         *     @ComponentScan(basePackageClasses = { DsClientConfig.class })
         *     public class DsClientConfig {
         *         @Bean
         *         public BeanRegistryProcessor beanRegistryProcessor(){
         *             return new BeanRegistryProcessor();
         *         }
         *     }
         */
        @RestController
        public class Test2252Controller {
            private Logger logger = LoggerFactory.getLogger(Test2252Controller.class);
            @Autowired
            private DataApiClient dataApiClient;
            /**
             * Sample Result:
             * {
             *     "data": {
             *         "totalNum": 1000,
             *         "pageSize": 100,
             *         "rows": [
             *             {
             *                 "pageNum": "...", // The number of the page. This is a default pagination parameter. The value is an integer.
             *                 "pageSize": "...", // The number of entries on each page. This is a default pagination parameter. The value is an integer.
             *                 "totalNum": "...", // The total number of pages. This is a default pagination parameter. The value is an integer. 
             *                 "id": "...", // Integer.
             *                 "name": "...", // String.
             *                 "sex": "...", // String.
             *                 "age": "...", // Integer.
             *             }
             *             ......
             *         ],
             *         "pageNum": 1
             *     },
             *     "errCode": 0,
             *     "requestId": "478cae2f-0***-42fb-a439-c0***e6f",
             *     "errMsg": "success"
             * }
             */
            private HashMap InvokeApi2252(ApiRequest2252DTO dto) throws Exception {
                Request request = new Request();
                request.setMethod("GET");
                request.setAppKey("15810204");
                request.setAppSecret("*******************************");
                request.setHost("http://0e5e6cd70******5e64****hai.a***pi.com");
                request.setPath("/test");
                for (Field f : dto.getClass().getDeclaredFields()) {
                    try{
                        if(f.get(dto)! = null) {
                            request.getBodys().put(f.getName(), f.get(dto).toString());
                        }
                    }catch(Exception e){}
                }
                request.setApiProtocol(ApiProtocol.HTTP);
                return dataApiClient.dataLoad(request);
            }
            /**
             * Response:
             */
            @RequestMapping(value = "/sample/test2252", method = RequestMethod.POST)
            public HashMap testApi(@RequestBody ApiRequest2252DTO dto) throws Exception {
                return InvokeApi2252(dto);
            }
        }
        /**
         * Request
         */
        class ApiRequest2252DTO {
            public Integer pageNum;
            public Integer pageSize;
            public Integer id;
            public String name;
            public String sex;
            public Integer age;
        }
        ```

        **Note:** You can refer to the generated sample code in your code development. You can also click **Save** to add the code to the dataservice package in the current code directory.

-   Use DataService Studio APIs through the WYSIWYG designer.

    Components of the WYSIWYG designer are highly integrated with DataService Studio APIs and use the default format of data returned by DataService Studio. This means any configuration can take effect immediately. For more information, see [WYSIWYG designer](intl.en-US/User Guide/App Studio/Features/WYSIWYG designer/Overview of the WYSIWYG designer.md#).


