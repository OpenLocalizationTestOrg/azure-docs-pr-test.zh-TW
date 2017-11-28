## <a name="typical-output"></a><span data-ttu-id="ba376-101">典型輸出</span><span class="sxs-lookup"><span data-stu-id="ba376-101">Typical output</span></span>

<span data-ttu-id="ba376-102">下列範例顯示 Hello World 範例寫入記錄檔中的輸出。</span><span class="sxs-lookup"><span data-stu-id="ba376-102">The following example shows the output written to the log file by the Hello World sample.</span></span> <span data-ttu-id="ba376-103">已針對易讀性將輸出格式化︰</span><span class="sxs-lookup"><span data-stu-id="ba376-103">The output is formatted for legibility:</span></span>

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

## <a name="code-snippets"></a><span data-ttu-id="ba376-104">程式碼片段</span><span class="sxs-lookup"><span data-stu-id="ba376-104">Code snippets</span></span>

<span data-ttu-id="ba376-105">本節探討 hello\_world 範例中程式碼的一些重要區段。</span><span class="sxs-lookup"><span data-stu-id="ba376-105">This section discusses some key sections of the code in the hello\_world sample.</span></span>

### <a name="iot-edge-gateway-creation"></a><span data-ttu-id="ba376-106">建立 IoT Edge 閘道</span><span class="sxs-lookup"><span data-stu-id="ba376-106">IoT Edge gateway creation</span></span>

<span data-ttu-id="ba376-107">您必須實作閘道程序。</span><span class="sxs-lookup"><span data-stu-id="ba376-107">You must implement a *gateway process*.</span></span> <span data-ttu-id="ba376-108">此程式會建立內部基礎結構 (訊息代理程式)、載入 IoT Edge 模組，以及設定閘道程序。</span><span class="sxs-lookup"><span data-stu-id="ba376-108">This program creates the internal infrastructure (the broker), loads the IoT Edge modules, and configures the gateway process.</span></span> <span data-ttu-id="ba376-109">IoT Edge 提供的 **Gateway\_Create\_From\_JSON** 函式可讓您從 JSON 檔案啟動閘道。</span><span class="sxs-lookup"><span data-stu-id="ba376-109">IoT Edge provides the **Gateway\_Create\_From\_JSON** function to enable you to bootstrap a gateway from a JSON file.</span></span> <span data-ttu-id="ba376-110">若要使用 **Gateway\_Create\_From\_JSON** 函式，請將它傳遞到 JSON 檔案的路徑，以指定要載入的 IoT Edge 模組。</span><span class="sxs-lookup"><span data-stu-id="ba376-110">To use the **Gateway\_Create\_From\_JSON** function, pass it the path to a JSON file that specifies the IoT Edge modules to load.</span></span>

<span data-ttu-id="ba376-111">在 [main.c][lnk-main-c] 檔案中，您可以找到 Hello World 範例中閘道程序的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ba376-111">You can find the code for the gateway process in the *Hello World* sample in the [main.c][lnk-main-c] file.</span></span> <span data-ttu-id="ba376-112">下列程式碼片段顯示精簡版本的閘道程序程式碼，以利閱讀。</span><span class="sxs-lookup"><span data-stu-id="ba376-112">For legibility, the following snippet shows an abbreviated version of the gateway process code.</span></span> <span data-ttu-id="ba376-113">此範例會建立閘道，然後先等待使用者按下 **ENTER** 鍵，再終止閘道。</span><span class="sxs-lookup"><span data-stu-id="ba376-113">This example program creates a gateway and then waits for the user to press the **ENTER** key before it tears down the gateway.</span></span>

```c
int main(int argc, char** argv)
{
    GATEWAY_HANDLE gateway;
    if ((gateway = Gateway_Create_From_JSON(argv[1])) == NULL)
    {
        printf("failed to create the gateway from JSON\n");
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

<span data-ttu-id="ba376-114">JSON 設定檔案包含要載入的 IoT Edge 模組清單以及模組之間的連結。</span><span class="sxs-lookup"><span data-stu-id="ba376-114">The JSON settings file contains a list of IoT Edge modules to load and the links between the modules.</span></span> <span data-ttu-id="ba376-115">每個 IoT Edge 模組都必須指定：</span><span class="sxs-lookup"><span data-stu-id="ba376-115">Each IoT Edge module must specify a:</span></span>

* <span data-ttu-id="ba376-116">**名稱**：模組的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="ba376-116">**name**: a unique name for the module.</span></span>
* <span data-ttu-id="ba376-117">**載入器**︰知道如何載入所需模組的載入器。</span><span class="sxs-lookup"><span data-stu-id="ba376-117">**loader**: a loader that knows how to load the desired module.</span></span> <span data-ttu-id="ba376-118">載入器是一個用來載入不同模組類型的擴充點。</span><span class="sxs-lookup"><span data-stu-id="ba376-118">Loaders are an extension point for loading different types of modules.</span></span> <span data-ttu-id="ba376-119">IoT Edge 提供可與以原生 C、Node.js、Java 和 .NET 撰寫的模組搭配使用的載入器。</span><span class="sxs-lookup"><span data-stu-id="ba376-119">IoT Edge provides loaders for use with modules written in native C, Node.js, Java, and .NET.</span></span> <span data-ttu-id="ba376-120">Hello World 範例只會使用原生 C 載入器，因為此範例中的所有模組都是以 C 撰寫的動態程式庫。如需有關如何使用以不同語言撰寫之 IoT Edge 模組的詳細資訊，請參閱 [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/)、[Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample) 或 [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) 範例。</span><span class="sxs-lookup"><span data-stu-id="ba376-120">The Hello World sample only uses the native C loader because all the modules in this sample are dynamic libraries written in C. For more information about how to use IoT Edge modules written in different languages, see the [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), or [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) samples.</span></span>
    * <span data-ttu-id="ba376-121">**名稱**︰用來載入模組的載入器名稱。</span><span class="sxs-lookup"><span data-stu-id="ba376-121">**name**: the name of the loader used to load the module.</span></span>
    * <span data-ttu-id="ba376-122">**進入點**：包含模組之程式庫的路徑。</span><span class="sxs-lookup"><span data-stu-id="ba376-122">**entrypoint**: the path to the library containing the module.</span></span> <span data-ttu-id="ba376-123">在 Linux 上，此程式庫是 .so 檔案，在 Windows 上，此程式庫是 .dll 檔案。</span><span class="sxs-lookup"><span data-stu-id="ba376-123">On Linux this library is a .so file, on Windows this library is a .dll file.</span></span> <span data-ttu-id="ba376-124">此進入點是要使用的載入器類型特定的。</span><span class="sxs-lookup"><span data-stu-id="ba376-124">The entry point is specific to the type of loader being used.</span></span> <span data-ttu-id="ba376-125">Node.js 載入器的進入點是 .js 檔案。</span><span class="sxs-lookup"><span data-stu-id="ba376-125">The Node.js loader entry point is a .js file.</span></span> <span data-ttu-id="ba376-126">Java 載入器的進入點是 classpath 與類別名稱。</span><span class="sxs-lookup"><span data-stu-id="ba376-126">The Java loader entry point is a classpath and a class name.</span></span> <span data-ttu-id="ba376-127">.NET 載入器的進入點是組件名稱與類別名稱。</span><span class="sxs-lookup"><span data-stu-id="ba376-127">The .NET loader entry point is an assembly name and a class name.</span></span>

* <span data-ttu-id="ba376-128">**args**：模組所需的任何組態資訊。</span><span class="sxs-lookup"><span data-stu-id="ba376-128">**args**: any configuration information the module needs.</span></span>

<span data-ttu-id="ba376-129">下列程式碼所示範的 JSON 可用來在 Linux 上宣告適用於 Hello World 範例的所有 IoT Edge 模組。</span><span class="sxs-lookup"><span data-stu-id="ba376-129">The following code shows the JSON used to declare all the IoT Edge modules for the Hello World sample on Linux.</span></span> <span data-ttu-id="ba376-130">模組是否需要引數取決於模組的設計。</span><span class="sxs-lookup"><span data-stu-id="ba376-130">Whether a module requires any arguments depends on the design of the module.</span></span> <span data-ttu-id="ba376-131">在此範例中，Logger 模組所採用的引數是輸出檔的路徑，而 hello\_world 模組沒有任何引數。</span><span class="sxs-lookup"><span data-stu-id="ba376-131">In this example, the logger module takes an argument that is the path to the output file and the hello\_world module has no arguments.</span></span>

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

<span data-ttu-id="ba376-132">JSON 檔案也包含會傳遞給訊息代理程式之模組之間的連結。</span><span class="sxs-lookup"><span data-stu-id="ba376-132">The JSON file also contains the links between the modules that are passed to the broker.</span></span> <span data-ttu-id="ba376-133">連結有兩個屬性︰</span><span class="sxs-lookup"><span data-stu-id="ba376-133">A link has two properties:</span></span>

* <span data-ttu-id="ba376-134">**來源**：來自 `modules` 區段的模組名稱，或 `\*`。</span><span class="sxs-lookup"><span data-stu-id="ba376-134">**source**: a module name from the `modules` section, or `\*`.</span></span>
* <span data-ttu-id="ba376-135">**接收**：來自 `modules` 區段的模組名稱。</span><span class="sxs-lookup"><span data-stu-id="ba376-135">**sink**: a module name from the `modules` section.</span></span>

<span data-ttu-id="ba376-136">每個連結都會定義訊息路由和方向。</span><span class="sxs-lookup"><span data-stu-id="ba376-136">Each link defines a message route and direction.</span></span> <span data-ttu-id="ba376-137">來自**來源**模組的訊息會傳遞給**接收**模組。</span><span class="sxs-lookup"><span data-stu-id="ba376-137">Messages from the **source** module are delivered to the **sink** module.</span></span> <span data-ttu-id="ba376-138">您可以將**來源**模組設定為 `\*`，這表示**接收**模組會從任何模組接收訊息。</span><span class="sxs-lookup"><span data-stu-id="ba376-138">You can set the **source** module to `\*`, which indicates that the **sink** module receives messages from any module.</span></span>

<span data-ttu-id="ba376-139">下列程式碼所示範的 JSON 可用來在 Linux 上設定在 hello\_world 範例所使用之模組間的連結。</span><span class="sxs-lookup"><span data-stu-id="ba376-139">The following code shows the JSON used to configure links between the modules used in the hello\_world sample on Linux.</span></span> <span data-ttu-id="ba376-140">`hello_world` 模組所產生的每則訊息都是由 `logger` 模組取用。</span><span class="sxs-lookup"><span data-stu-id="ba376-140">Every message produced by the `hello_world` module is consumed by the `logger` module.</span></span>

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a><span data-ttu-id="ba376-141">Hello\_world 模組訊息發佈</span><span class="sxs-lookup"><span data-stu-id="ba376-141">Hello\_world module message publishing</span></span>

<span data-ttu-id="ba376-142">您可以在 ['hello_world.c'][lnk-helloworld-c] 檔案中找到 hello\_world 模組所使用的程式碼來發佈訊息。</span><span class="sxs-lookup"><span data-stu-id="ba376-142">You can find the code used by the hello\_world module to publish messages in the ['hello_world.c'][lnk-helloworld-c] file.</span></span> <span data-ttu-id="ba376-143">下列程式碼片段所示範的修改過程式碼版本已新增註解並移除一些錯誤處理程式碼，以利閱讀︰</span><span class="sxs-lookup"><span data-stu-id="ba376-143">The following snippet shows an amended version of the code with comments added and some error handling code removed for legibility:</span></span>

```c
int helloWorldThread(void *param)
{
    // create data structures used in function.
    HELLOWORLD_HANDLE_DATA* handleData = param;
    MESSAGE_CONFIG msgConfig;
    MAP_HANDLE propertiesMap = Map_Create(NULL);

    // add a property named "helloWorld" with a value of "from Azure IoT
    // Gateway SDK simple sample!" to a set of message properties that
    // will be appended to the message before publishing it. 
    Map_AddOrUpdate(propertiesMap, "helloWorld", "from Azure IoT Gateway SDK simple sample!")

    // set the content for the message
    msgConfig.size = strlen(HELLOWORLD_MESSAGE);
    msgConfig.source = HELLOWORLD_MESSAGE;

    // set the properties for the message
    msgConfig.sourceProperties = propertiesMap;

    // create a message based on the msgConfig structure
    MESSAGE_HANDLE helloWorldMessage = Message_Create(&msgConfig);

    while (1)
    {
        if (handleData->stopThread)
        {
            (void)Unlock(handleData->lockHandle);
            break; /*gets out of the thread*/
        }
        else
        {
            // publish the message to the broker
            (void)Broker_Publish(handleData->brokerHandle, helloWorldMessage);
            (void)Unlock(handleData->lockHandle);
        }

        (void)ThreadAPI_Sleep(5000); /*every 5 seconds*/
    }

    Message_Destroy(helloWorldMessage);

    return 0;
}
```

### <a name="helloworld-module-message-processing"></a><span data-ttu-id="ba376-144">Hello\_world 模組訊息處理</span><span class="sxs-lookup"><span data-stu-id="ba376-144">Hello\_world module message processing</span></span>

<span data-ttu-id="ba376-145">Hello\_world 模組永遠不會處理其他 IoT Edge 模組發佈至訊息代理程式的訊息。</span><span class="sxs-lookup"><span data-stu-id="ba376-145">The hello\_world module never processes messages that other IoT Edge modules publish to the broker.</span></span> <span data-ttu-id="ba376-146">因此，hello\_world 模組中的訊息回呼實作為無作業函式。</span><span class="sxs-lookup"><span data-stu-id="ba376-146">Therefore, the implementation of the message callback in the hello\_world module is a no-op function.</span></span>

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a><span data-ttu-id="ba376-147">Logger 模組訊息發佈和處理</span><span class="sxs-lookup"><span data-stu-id="ba376-147">Logger module message publishing and processing</span></span>

<span data-ttu-id="ba376-148">Logger 模組會接收來自訊息代理程式的訊息，並將它們寫入檔案。</span><span class="sxs-lookup"><span data-stu-id="ba376-148">The logger module receives messages from the broker and writes them to a file.</span></span> <span data-ttu-id="ba376-149">此模組永遠不會發佈任何訊息。</span><span class="sxs-lookup"><span data-stu-id="ba376-149">It never publishes any messages.</span></span> <span data-ttu-id="ba376-150">因此，Logger 模組的程式碼永遠不會呼叫 **Broker_Publish** 函式。</span><span class="sxs-lookup"><span data-stu-id="ba376-150">Therefore, the code of the logger module never calls the **Broker_Publish** function.</span></span>

<span data-ttu-id="ba376-151">[logger.c][lnk-logger-c] 檔案中的 **Logger_Receive** 函式是訊息代理程式所叫用的回呼，以將訊息傳遞到 Logger 模組。</span><span class="sxs-lookup"><span data-stu-id="ba376-151">The **Logger_Receive** function in the [logger.c][lnk-logger-c] file is the callback the broker invokes to deliver messages to the logger module.</span></span> <span data-ttu-id="ba376-152">下列程式碼片段所示範的修改過版本已新增註解並移除一些錯誤處理程式碼，以利閱讀︰</span><span class="sxs-lookup"><span data-stu-id="ba376-152">The following snippet shows an amended version with comments added and some error handling code removed for legibility:</span></span>

```c
static void Logger_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{

    time_t temp = time(NULL);
    struct tm* t = localtime(&temp);
    char timetemp[80] = { 0 };

    // Get the message properties from the message
    CONSTMAP_HANDLE originalProperties = Message_GetProperties(messageHandle); 
    MAP_HANDLE propertiesAsMap = ConstMap_CloneWriteable(originalProperties);

    // Convert the collection of properties into a JSON string
    STRING_HANDLE jsonProperties = Map_ToJSON(propertiesAsMap);

    //  base64 encode the message content
    const CONSTBUFFER * content = Message_GetContent(messageHandle);
    STRING_HANDLE contentAsJSON = Base64_Encode_Bytes(content->buffer, content->size);

    // Start the construction of the final string to be logged by adding
    // the timestamp
    STRING_HANDLE jsonToBeAppended = STRING_construct(",{\"time\":\"");
    STRING_concat(jsonToBeAppended, timetemp);

    // Add the message properties
    STRING_concat(jsonToBeAppended, "\",\"properties\":"); 
    STRING_concat_with_STRING(jsonToBeAppended, jsonProperties);

    // Add the content
    STRING_concat(jsonToBeAppended, ",\"content\":\"");
    STRING_concat_with_STRING(jsonToBeAppended, contentAsJSON);
    STRING_concat(jsonToBeAppended, "\"}]");

    // Write the formatted string
    LOGGER_HANDLE_DATA *handleData = (LOGGER_HANDLE_DATA *)moduleHandle;
    addJSONString(handleData->fout, STRING_c_str(jsonToBeAppended);
}
```

## <a name="next-steps"></a><span data-ttu-id="ba376-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba376-153">Next steps</span></span>

<span data-ttu-id="ba376-154">在本文中，您所執行的簡單 IoT Edge 閘道可將訊息寫入記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="ba376-154">In this article, you ran a simple IoT Edge gateway that writes messages to a log file.</span></span> <span data-ttu-id="ba376-155">若要執行可將訊息傳送到 IoT 中樞的範例，請參閱 [IoT Edge – 使用 Linux 透過模擬的裝置傳送裝置對雲端訊息][lnk-gateway-simulated-linux]或 [IoT Edge – 使用 Windows 透過模擬的裝置傳送裝置對雲端訊息][lnk-gateway-simulated-windows]。</span><span class="sxs-lookup"><span data-stu-id="ba376-155">To run a sample that sends messages to IoT Hub, see [IoT Edge – send device-to-cloud messages with a simulated device using Linux][lnk-gateway-simulated-linux] or [IoT Edge – send device-to-cloud messages with a simulated device using Windows][lnk-gateway-simulated-windows].</span></span>


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md