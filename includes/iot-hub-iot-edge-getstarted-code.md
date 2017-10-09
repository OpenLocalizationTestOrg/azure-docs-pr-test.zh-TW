## <a name="typical-output"></a>典型輸出

hello 下列範例顯示 hello 輸出寫入 hello Hello World 範例 toohello 記錄檔。 可讀性格式化 hello 輸出：

```json
[{
    "time": "Mon Apr 11 13:48:07 2016",
    "content": "Log started"
}, {
    "time": "Mon Apr 11 13:48:48 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:48:55 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:01 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:04 2016",
    "content": "Log stopped"
}]
```

## <a name="code-snippets"></a>程式碼片段

本章節將討論 hello hello hello 中的程式碼某些索引鍵區段\_world 範例。

### <a name="iot-edge-gateway-creation"></a>建立 IoT Edge 閘道

您必須實作閘道程序。 此程式會建立 hello 內部基礎結構 （hello 代理人）、 載入 hello IoT 邊緣模組，並設定 hello 閘道處理程序。 IoT 邊緣提供 hello**閘道\_建立\_從\_JSON**函式 tooenable toobootstrap 閘道，以從 JSON 檔案。 toouse hello**閘道\_建立\_從\_JSON**函式中，將它傳遞 hello 路徑 tooa JSON 檔案，指定 hello IoT 邊緣模組 tooload。

您可以在 hello hello 閘道處理程序找到 hello 程式碼*Hello World* hello 範例[main.c] [ lnk-main-c]檔案。 以利閱讀，hello 下列程式碼片段顯示 hello 閘道處理程序程式碼的縮寫的版本。 這個範例程式建立閘道，並再等待 hello 使用者 toopress hello **ENTER**之前它瓦解 hello 閘道金鑰。

```c
int main(int argc, char** argv)
{
    GATEWAY_HANDLE gateway;
    if ((gateway = Gateway_Create_From_JSON(argv[1])) == NULL)
    {
        printf("failed toocreate hello gateway from JSON\n");
    }
    else
    {
        printf("gateway successfully created from JSON\n");
        printf("gateway shall run until ENTER is pressed\n");
        (void)getchar();
        Gateway_LL_Destroy(gateway);
    }
    return 0;
}
```

hello JSON 設定檔案包含一份 IoT 邊緣模組 tooload 的 hello hello 模組之間的連結。 每個 IoT Edge 模組都必須指定：

* **名稱**: hello 模組的唯一名稱。
* **載入器**： 知道如何 tooload hello 預期模組載入器。 載入器是一個用來載入不同模組類型的擴充點。 IoT Edge 提供可與以原生 C、Node.js、Java 和 .NET 撰寫的模組搭配使用的載入器。 hello Hello World 範例只會使用 hello 原生 C 載入器，因為在此範例中的所有 hello 模組都是以 c 撰寫動態程式庫如需有關如何以不同的語言撰寫的 toouse IoT 邊緣模組，請參閱 「 hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/)， [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample)，或[.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample)範例。
    * **名稱**: hello hello 載入器名稱使用 tooload hello 模組。
    * **entrypoint**: hello 路徑 toohello 程式庫包含 hello 模組。 在 Linux 上，此程式庫是 .so 檔案，在 Windows 上，此程式庫是 .dll 檔案。 hello 進入點是特定 toohello 的載入器所使用的型別。 hello Node.js 載入器進入點是.js 檔案。 hello Java 載入器進入點是 classpath 和類別名稱。 hello.NET 載入器進入點是組件名稱和類別名稱。

* **引數**： 需要任何組態資訊 hello 模組。

下列程式碼顯示 hello 使用 JSON toodeclare 所有 hello hello IoT 邊緣 hello Hello World 範例，在 Linux 上的模組。 模組是否需要任何引數取決於 hello 設計 hello 模組。 在此範例中，hello 記錄器模組會採用引數是 hello 路徑 toohello 輸出檔案而 hello hello\_世界模組沒有任何引數。

```json
"modules" :
[
    {
        "name" : "logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/logger/liblogger.so"
        }
        },
        "args" : {"filename":"log.txt"}
    },
    {
        "name" : "hello_world",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/hello_world/libhello_world.so"
        }
        },
        "args" : null
    }
]
```

hello JSON 檔案也包含 hello hello 模組傳遞 toohello broker 之間的連結。 連結有兩個屬性︰

* **來源**： 模組名稱從 hello `modules`  區段中，或`\*`。
* **接收**： 模組名稱從 hello `modules` > 一節。

每個連結都會定義訊息路由和方向。 從 hello 訊息**來源**模組傳遞 toohello**接收**模組。 您可以設定 hello**來源**模組太`\*`，表示該 hello**接收**模組會從任何模組接收訊息。

hello 下列程式碼示範 hello JSON 使用 tooconfigure 用於 hello hello hello 模組之間的連結\_Linux 上的 world 範例。 每個訊息所產生的 hello`hello_world`模組由 hello`logger`模組。

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a>Hello\_world 模組訊息發佈

您可以找到 hello hello hello 所使用的程式碼\_hello world 模組 toopublish 訊息['hello_world.c'] [ lnk-helloworld-c]檔案。 hello 下列程式碼片段顯示 hello 程式碼的修改的版本與註解加入一些錯誤處理程式碼，以利閱讀移除：

```c
int helloWorldThread(void *param)
{
    // create data structures used in function.
    HELLOWORLD_HANDLE_DATA* handleData = param;
    MESSAGE_CONFIG msgConfig;
    MAP_HANDLE propertiesMap = Map_Create(NULL);

    // add a property named "helloWorld" with a value of "from Azure IoT
    // Gateway SDK simple sample!" tooa set of message properties that
    // will be appended toohello message before publishing it. 
    Map_AddOrUpdate(propertiesMap, "helloWorld", "from Azure IoT Gateway SDK simple sample!")

    // set hello content for hello message
    msgConfig.size = strlen(HELLOWORLD_MESSAGE);
    msgConfig.source = HELLOWORLD_MESSAGE;

    // set hello properties for hello message
    msgConfig.sourceProperties = propertiesMap;

    // create a message based on hello msgConfig structure
    MESSAGE_HANDLE helloWorldMessage = Message_Create(&msgConfig);

    while (1)
    {
        if (handleData->stopThread)
        {
            (void)Unlock(handleData->lockHandle);
            break; /*gets out of hello thread*/
        }
        else
        {
            // publish hello message toohello broker
            (void)Broker_Publish(handleData->brokerHandle, helloWorldMessage);
            (void)Unlock(handleData->lockHandle);
        }

        (void)ThreadAPI_Sleep(5000); /*every 5 seconds*/
    }

    Message_Destroy(helloWorldMessage);

    return 0;
}
```

### <a name="helloworld-module-message-processing"></a>Hello\_world 模組訊息處理

hello hello\_世界模組永遠不會處理其他 IoT 邊緣模組發佈 toohello broker 的訊息。 因此，hello hello hello 中的 hello 訊息回呼實作\_世界模組是無作業函式。

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a>Logger 模組訊息發佈和處理

hello 記錄器模組會從 hello broker 接收訊息，並將它們 tooa 檔案。 此模組永遠不會發佈任何訊息。 因此，hello 程式碼的 hello 記錄器模組從未呼叫 hello **Broker_Publish**函式。

hello **Logger_Receive**函式在 hello [logger.c] [ lnk-logger-c]檔案是 hello 回呼 hello broker 會叫用 toodeliver 訊息 toohello 記錄器模組。 hello 下列程式碼片段顯示修改過的版本註解加入與某些錯誤處理程式碼，以利閱讀移除：

```c
static void Logger_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{

    time_t temp = time(NULL);
    struct tm* t = localtime(&temp);
    char timetemp[80] = { 0 };

    // Get hello message properties from hello message
    CONSTMAP_HANDLE originalProperties = Message_GetProperties(messageHandle); 
    MAP_HANDLE propertiesAsMap = ConstMap_CloneWriteable(originalProperties);

    // Convert hello collection of properties into a JSON string
    STRING_HANDLE jsonProperties = Map_ToJSON(propertiesAsMap);

    //  base64 encode hello message content
    const CONSTBUFFER * content = Message_GetContent(messageHandle);
    STRING_HANDLE contentAsJSON = Base64_Encode_Bytes(content->buffer, content->size);

    // Start hello construction of hello final string toobe logged by adding
    // hello timestamp
    STRING_HANDLE jsonToBeAppended = STRING_construct(",{\"time\":\"");
    STRING_concat(jsonToBeAppended, timetemp);

    // Add hello message properties
    STRING_concat(jsonToBeAppended, "\",\"properties\":"); 
    STRING_concat_with_STRING(jsonToBeAppended, jsonProperties);

    // Add hello content
    STRING_concat(jsonToBeAppended, ",\"content\":\"");
    STRING_concat_with_STRING(jsonToBeAppended, contentAsJSON);
    STRING_concat(jsonToBeAppended, "\"}]");

    // Write hello formatted string
    LOGGER_HANDLE_DATA *handleData = (LOGGER_HANDLE_DATA *)moduleHandle;
    addJSONString(handleData->fout, STRING_c_str(jsonToBeAppended);
}
```

## <a name="next-steps"></a>後續步驟

在本文中，您可以執行簡單的 IoT 邊緣閘道會寫入訊息 tooa 記錄檔。 toorun 範例傳送訊息 tooIoT 集線器，請參閱[IoT 邊緣 – 傳送裝置到雲端訊息與模擬的裝置使用 Linux] [ lnk-gateway-simulated-linux]或[IoT 邊緣裝置到雲端以傳送訊息使用 Windows 模擬的裝置][lnk-gateway-simulated-windows]。


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md