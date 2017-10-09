## <a name="typical-output"></a><span data-ttu-id="7cdd9-101">典型輸出</span><span class="sxs-lookup"><span data-stu-id="7cdd9-101">Typical output</span></span>

<span data-ttu-id="7cdd9-102">hello 下列範例顯示 hello 輸出寫入 hello Hello World 範例 toohello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-102">hello following example shows hello output written toohello log file by hello Hello World sample.</span></span> <span data-ttu-id="7cdd9-103">可讀性格式化 hello 輸出：</span><span class="sxs-lookup"><span data-stu-id="7cdd9-103">hello output is formatted for legibility:</span></span>

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

## <a name="code-snippets"></a><span data-ttu-id="7cdd9-104">程式碼片段</span><span class="sxs-lookup"><span data-stu-id="7cdd9-104">Code snippets</span></span>

<span data-ttu-id="7cdd9-105">本章節將討論 hello hello hello 中的程式碼某些索引鍵區段\_world 範例。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-105">This section discusses some key sections of hello code in hello hello\_world sample.</span></span>

### <a name="iot-edge-gateway-creation"></a><span data-ttu-id="7cdd9-106">建立 IoT Edge 閘道</span><span class="sxs-lookup"><span data-stu-id="7cdd9-106">IoT Edge gateway creation</span></span>

<span data-ttu-id="7cdd9-107">您必須實作閘道程序。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-107">You must implement a *gateway process*.</span></span> <span data-ttu-id="7cdd9-108">此程式會建立 hello 內部基礎結構 （hello 代理人）、 載入 hello IoT 邊緣模組，並設定 hello 閘道處理程序。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-108">This program creates hello internal infrastructure (hello broker), loads hello IoT Edge modules, and configures hello gateway process.</span></span> <span data-ttu-id="7cdd9-109">IoT 邊緣提供 hello**閘道\_建立\_從\_JSON**函式 tooenable toobootstrap 閘道，以從 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-109">IoT Edge provides hello **Gateway\_Create\_From\_JSON** function tooenable you toobootstrap a gateway from a JSON file.</span></span> <span data-ttu-id="7cdd9-110">toouse hello**閘道\_建立\_從\_JSON**函式中，將它傳遞 hello 路徑 tooa JSON 檔案，指定 hello IoT 邊緣模組 tooload。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-110">toouse hello **Gateway\_Create\_From\_JSON** function, pass it hello path tooa JSON file that specifies hello IoT Edge modules tooload.</span></span>

<span data-ttu-id="7cdd9-111">您可以在 hello hello 閘道處理程序找到 hello 程式碼*Hello World* hello 範例[main.c] [ lnk-main-c]檔案。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-111">You can find hello code for hello gateway process in hello *Hello World* sample in hello [main.c][lnk-main-c] file.</span></span> <span data-ttu-id="7cdd9-112">以利閱讀，hello 下列程式碼片段顯示 hello 閘道處理程序程式碼的縮寫的版本。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-112">For legibility, hello following snippet shows an abbreviated version of hello gateway process code.</span></span> <span data-ttu-id="7cdd9-113">這個範例程式建立閘道，並再等待 hello 使用者 toopress hello **ENTER**之前它瓦解 hello 閘道金鑰。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-113">This example program creates a gateway and then waits for hello user toopress hello **ENTER** key before it tears down hello gateway.</span></span>

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

<span data-ttu-id="7cdd9-114">hello JSON 設定檔案包含一份 IoT 邊緣模組 tooload 的 hello hello 模組之間的連結。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-114">hello JSON settings file contains a list of IoT Edge modules tooload and hello links between hello modules.</span></span> <span data-ttu-id="7cdd9-115">每個 IoT Edge 模組都必須指定：</span><span class="sxs-lookup"><span data-stu-id="7cdd9-115">Each IoT Edge module must specify a:</span></span>

* <span data-ttu-id="7cdd9-116">**名稱**: hello 模組的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-116">**name**: a unique name for hello module.</span></span>
* <span data-ttu-id="7cdd9-117">**載入器**： 知道如何 tooload hello 預期模組載入器。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-117">**loader**: a loader that knows how tooload hello desired module.</span></span> <span data-ttu-id="7cdd9-118">載入器是一個用來載入不同模組類型的擴充點。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-118">Loaders are an extension point for loading different types of modules.</span></span> <span data-ttu-id="7cdd9-119">IoT Edge 提供可與以原生 C、Node.js、Java 和 .NET 撰寫的模組搭配使用的載入器。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-119">IoT Edge provides loaders for use with modules written in native C, Node.js, Java, and .NET.</span></span> <span data-ttu-id="7cdd9-120">hello Hello World 範例只會使用 hello 原生 C 載入器，因為在此範例中的所有 hello 模組都是以 c 撰寫動態程式庫如需有關如何以不同的語言撰寫的 toouse IoT 邊緣模組，請參閱 「 hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/)， [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample)，或[.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample)範例。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-120">hello Hello World sample only uses hello native C loader because all hello modules in this sample are dynamic libraries written in C. For more information about how toouse IoT Edge modules written in different languages, see hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), or [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) samples.</span></span>
    * <span data-ttu-id="7cdd9-121">**名稱**: hello hello 載入器名稱使用 tooload hello 模組。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-121">**name**: hello name of hello loader used tooload hello module.</span></span>
    * <span data-ttu-id="7cdd9-122">**entrypoint**: hello 路徑 toohello 程式庫包含 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-122">**entrypoint**: hello path toohello library containing hello module.</span></span> <span data-ttu-id="7cdd9-123">在 Linux 上，此程式庫是 .so 檔案，在 Windows 上，此程式庫是 .dll 檔案。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-123">On Linux this library is a .so file, on Windows this library is a .dll file.</span></span> <span data-ttu-id="7cdd9-124">hello 進入點是特定 toohello 的載入器所使用的型別。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-124">hello entry point is specific toohello type of loader being used.</span></span> <span data-ttu-id="7cdd9-125">hello Node.js 載入器進入點是.js 檔案。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-125">hello Node.js loader entry point is a .js file.</span></span> <span data-ttu-id="7cdd9-126">hello Java 載入器進入點是 classpath 和類別名稱。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-126">hello Java loader entry point is a classpath and a class name.</span></span> <span data-ttu-id="7cdd9-127">hello.NET 載入器進入點是組件名稱和類別名稱。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-127">hello .NET loader entry point is an assembly name and a class name.</span></span>

* <span data-ttu-id="7cdd9-128">**引數**： 需要任何組態資訊 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-128">**args**: any configuration information hello module needs.</span></span>

<span data-ttu-id="7cdd9-129">下列程式碼顯示 hello 使用 JSON toodeclare 所有 hello hello IoT 邊緣 hello Hello World 範例，在 Linux 上的模組。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-129">hello following code shows hello JSON used toodeclare all hello IoT Edge modules for hello Hello World sample on Linux.</span></span> <span data-ttu-id="7cdd9-130">模組是否需要任何引數取決於 hello 設計 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-130">Whether a module requires any arguments depends on hello design of hello module.</span></span> <span data-ttu-id="7cdd9-131">在此範例中，hello 記錄器模組會採用引數是 hello 路徑 toohello 輸出檔案而 hello hello\_世界模組沒有任何引數。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-131">In this example, hello logger module takes an argument that is hello path toohello output file and hello hello\_world module has no arguments.</span></span>

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

<span data-ttu-id="7cdd9-132">hello JSON 檔案也包含 hello hello 模組傳遞 toohello broker 之間的連結。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-132">hello JSON file also contains hello links between hello modules that are passed toohello broker.</span></span> <span data-ttu-id="7cdd9-133">連結有兩個屬性︰</span><span class="sxs-lookup"><span data-stu-id="7cdd9-133">A link has two properties:</span></span>

* <span data-ttu-id="7cdd9-134">**來源**： 模組名稱從 hello `modules`  區段中，或`\*`。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-134">**source**: a module name from hello `modules` section, or `\*`.</span></span>
* <span data-ttu-id="7cdd9-135">**接收**： 模組名稱從 hello `modules` > 一節。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-135">**sink**: a module name from hello `modules` section.</span></span>

<span data-ttu-id="7cdd9-136">每個連結都會定義訊息路由和方向。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-136">Each link defines a message route and direction.</span></span> <span data-ttu-id="7cdd9-137">從 hello 訊息**來源**模組傳遞 toohello**接收**模組。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-137">Messages from hello **source** module are delivered toohello **sink** module.</span></span> <span data-ttu-id="7cdd9-138">您可以設定 hello**來源**模組太`\*`，表示該 hello**接收**模組會從任何模組接收訊息。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-138">You can set hello **source** module too`\*`, which indicates that hello **sink** module receives messages from any module.</span></span>

<span data-ttu-id="7cdd9-139">hello 下列程式碼示範 hello JSON 使用 tooconfigure 用於 hello hello hello 模組之間的連結\_Linux 上的 world 範例。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-139">hello following code shows hello JSON used tooconfigure links between hello modules used in hello hello\_world sample on Linux.</span></span> <span data-ttu-id="7cdd9-140">每個訊息所產生的 hello`hello_world`模組由 hello`logger`模組。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-140">Every message produced by hello `hello_world` module is consumed by hello `logger` module.</span></span>

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a><span data-ttu-id="7cdd9-141">Hello\_world 模組訊息發佈</span><span class="sxs-lookup"><span data-stu-id="7cdd9-141">Hello\_world module message publishing</span></span>

<span data-ttu-id="7cdd9-142">您可以找到 hello hello hello 所使用的程式碼\_hello world 模組 toopublish 訊息['hello_world.c'] [ lnk-helloworld-c]檔案。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-142">You can find hello code used by hello hello\_world module toopublish messages in hello ['hello_world.c'][lnk-helloworld-c] file.</span></span> <span data-ttu-id="7cdd9-143">hello 下列程式碼片段顯示 hello 程式碼的修改的版本與註解加入一些錯誤處理程式碼，以利閱讀移除：</span><span class="sxs-lookup"><span data-stu-id="7cdd9-143">hello following snippet shows an amended version of hello code with comments added and some error handling code removed for legibility:</span></span>

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

### <a name="helloworld-module-message-processing"></a><span data-ttu-id="7cdd9-144">Hello\_world 模組訊息處理</span><span class="sxs-lookup"><span data-stu-id="7cdd9-144">Hello\_world module message processing</span></span>

<span data-ttu-id="7cdd9-145">hello hello\_世界模組永遠不會處理其他 IoT 邊緣模組發佈 toohello broker 的訊息。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-145">hello hello\_world module never processes messages that other IoT Edge modules publish toohello broker.</span></span> <span data-ttu-id="7cdd9-146">因此，hello hello hello 中的 hello 訊息回呼實作\_世界模組是無作業函式。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-146">Therefore, hello implementation of hello message callback in hello hello\_world module is a no-op function.</span></span>

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a><span data-ttu-id="7cdd9-147">Logger 模組訊息發佈和處理</span><span class="sxs-lookup"><span data-stu-id="7cdd9-147">Logger module message publishing and processing</span></span>

<span data-ttu-id="7cdd9-148">hello 記錄器模組會從 hello broker 接收訊息，並將它們 tooa 檔案。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-148">hello logger module receives messages from hello broker and writes them tooa file.</span></span> <span data-ttu-id="7cdd9-149">此模組永遠不會發佈任何訊息。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-149">It never publishes any messages.</span></span> <span data-ttu-id="7cdd9-150">因此，hello 程式碼的 hello 記錄器模組從未呼叫 hello **Broker_Publish**函式。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-150">Therefore, hello code of hello logger module never calls hello **Broker_Publish** function.</span></span>

<span data-ttu-id="7cdd9-151">hello **Logger_Receive**函式在 hello [logger.c] [ lnk-logger-c]檔案是 hello 回呼 hello broker 會叫用 toodeliver 訊息 toohello 記錄器模組。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-151">hello **Logger_Receive** function in hello [logger.c][lnk-logger-c] file is hello callback hello broker invokes toodeliver messages toohello logger module.</span></span> <span data-ttu-id="7cdd9-152">hello 下列程式碼片段顯示修改過的版本註解加入與某些錯誤處理程式碼，以利閱讀移除：</span><span class="sxs-lookup"><span data-stu-id="7cdd9-152">hello following snippet shows an amended version with comments added and some error handling code removed for legibility:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7cdd9-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7cdd9-153">Next steps</span></span>

<span data-ttu-id="7cdd9-154">在本文中，您可以執行簡單的 IoT 邊緣閘道會寫入訊息 tooa 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-154">In this article, you ran a simple IoT Edge gateway that writes messages tooa log file.</span></span> <span data-ttu-id="7cdd9-155">toorun 範例傳送訊息 tooIoT 集線器，請參閱[IoT 邊緣 – 傳送裝置到雲端訊息與模擬的裝置使用 Linux] [ lnk-gateway-simulated-linux]或[IoT 邊緣裝置到雲端以傳送訊息使用 Windows 模擬的裝置][lnk-gateway-simulated-windows]。</span><span class="sxs-lookup"><span data-stu-id="7cdd9-155">toorun a sample that sends messages tooIoT Hub, see [IoT Edge – send device-to-cloud messages with a simulated device using Linux][lnk-gateway-simulated-linux] or [IoT Edge – send device-to-cloud messages with a simulated device using Windows][lnk-gateway-simulated-windows].</span></span>


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md