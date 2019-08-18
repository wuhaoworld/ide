# Hot code replacement {#concept_cwx_gdz_bhb .concept}

Using the hot code replacement feature, you can edit the running code of an app and make the edits effective without restarting the app.

For example, after you edit the code while debugging a Spring Boot-based app, you do not need to restart the app. The edited code takes effect once it is saved. App Studio supports this feature by default.

App Studio also supports hot code replacement while an app is running. To trigger hot code replacement, you only need to save the file without installing any plug-in or manually compiling the file.

If you are editing the code in Debug mode, App Studio automatically deletes the current running stack and returns to the function entry.

## Configure hot code replacement in Run mode {#section_ryp_jm2_chb .section}

1.  Enable hot code replacement on the Run/Debug Configurations page.

    After you click Run or Debug, the output information of the HotCode2 plug-in appears on the OUT tab.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/138072/156610792740831_en-US.png)

2.  Trigger hot code replacement.

    Save the file after editing it.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/138072/156610792740833_en-US.png)

3.  After the incremental code synchronization is completed, if the output of a reload class appears in the console, hot code replacement takes effect. The sample code is as follows:

    ``` {#codeblock_c46_6es_px0}
    public class IndexController {
        @RequestMapping("/")
        @ResponseBody
        public String index(){
            return "cccc";
        }
    }
    ```

    You can replace the return string with another string to make the edit effective immediately.


## Configure hot code replacement in Debug mode {#section_y3x_cq2_chb .section}

You can use the native Java Debug Interface \(JDI\) to enable hot code replacement in Debug mode. However, due to Java Virtual Machine \(JVM\) restrictions, hot code replacement is unavailable when a method is added to or deleted from a class. You can save the file to trigger hot code replacement.

**Note:** The native JVM supports hot code replacement for operations such as adding or deleting a class. However, hot code replacement is unavailable when you change the class structure.

