---
title: "aaaGet 啟動與 Azure IoT 中樞 (.NET) |Microsoft 文件"
description: "了解如何 toosend 裝置到雲端訊息 tooAzure 使用 IoT Sdk for.NET 的 IoT 中樞。 建立模擬的裝置和服務應用程式 tooregister 您的裝置、 傳送訊息，以及從 IoT 中樞讀取訊息。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: f40604ff-8fd6-4969-9e99-8574fbcf036c
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56cf14687411898ea0fa4ebb1782e18b3930809c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a><span data-ttu-id="08f68-104">連接您使用適用於.NET 的裝置 tooyour IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="08f68-104">Connect your device tooyour IoT hub using .NET</span></span>

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="08f68-105">在本教學課程的 hello 最後，您有三個.NET 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="08f68-105">At hello end of this tutorial, you have three .NET console apps:</span></span>

* <span data-ttu-id="08f68-106">**CreateDeviceIdentity**，這樣就可以建立裝置身分識別，以及相關聯的安全性金鑰 tooconnect 您裝置的應用程式。</span><span class="sxs-lookup"><span data-stu-id="08f68-106">**CreateDeviceIdentity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="08f68-107">**ReadDeviceToCloudMessages**，其中顯示您裝置的應用程式所傳送的 hello 遙測。</span><span class="sxs-lookup"><span data-stu-id="08f68-107">**ReadDeviceToCloudMessages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="08f68-108">**SimulatedDevice**，這會 tooyour IoT 中樞連接使用稍早建立的 hello 裝置身分識別，並使用 hello MQTT 通訊協定傳送遙測訊息每秒。</span><span class="sxs-lookup"><span data-stu-id="08f68-108">**SimulatedDevice**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second by using hello MQTT protocol.</span></span>

<span data-ttu-id="08f68-109">您可以下載或複製 hello Visual Studio 方案，其中包含從 Github 的 hello 三個應用程式。</span><span class="sxs-lookup"><span data-stu-id="08f68-109">You can download or clone hello Visual Studio solution, which contains hello three apps from Github.</span></span>

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> <span data-ttu-id="08f68-110">如需有關資訊 hello Azure IoT Sdk，您可以使用 toobuild 在裝置上，應用程式 toorun 和您的方案後端，請參閱[Azure IoT Sdk][lnk-hub-sdks]。</span><span class="sxs-lookup"><span data-stu-id="08f68-110">For information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="08f68-111">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="08f68-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="08f68-112">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="08f68-112">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="08f68-113">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="08f68-113">An active Azure account.</span></span> <span data-ttu-id="08f68-114">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="08f68-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="08f68-115">您現在已建立您的 IoT 中樞，而且您擁有 hello 主機名稱和您需要 toocomplete hello rest 本教學課程的 IoT 中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="08f68-115">You have now created your IoT hub, and you have hello host name and IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="08f68-116">接收裝置到雲端的訊息</span><span class="sxs-lookup"><span data-stu-id="08f68-116">Receive device-to-cloud messages</span></span>
<span data-ttu-id="08f68-117">在本節中，您會建立 .NET 主控台應用程式，以讀取來自 IoT 中樞的裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="08f68-117">In this section, you create a .NET console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="08f68-118">IoT 中樞公開[Azure 事件中心][lnk-event-hubs-overview]-相容的端點 tooenable 您 tooread 裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="08f68-118">An IoT hub exposes an [Azure Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="08f68-119">簡單 tookeep 方面，本教學課程會建立基本的讀取器不是適用於高輸送量部署。</span><span class="sxs-lookup"><span data-stu-id="08f68-119">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="08f68-120">toolearn 如何 tooprocess 裝置到雲端訊息小數位數，請參閱 hello[處理裝置到雲端訊息][ lnk-process-d2c-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="08f68-120">toolearn how tooprocess device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span> <span data-ttu-id="08f68-121">如需如何 tooprocess 訊息從事件中心的詳細資訊，請參閱 hello[開始使用事件中心][ lnk-eventhubs-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="08f68-121">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span> <span data-ttu-id="08f68-122">（本教學課程是適用 toohello IoT 中樞事件中樞相容的端點）。</span><span class="sxs-lookup"><span data-stu-id="08f68-122">(This tutorial is applicable toohello IoT Hub Event Hub-compatible endpoints.)</span></span>

> [!NOTE]
> <span data-ttu-id="08f68-123">hello 一律讀取裝置到雲端訊息的事件中樞相容端點使用 hello AMQP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="08f68-123">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="08f68-124">在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 toohello 目前方案，使用 hello**主控台應用程式 (.NET Framework)**專案範本。</span><span class="sxs-lookup"><span data-stu-id="08f68-124">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="08f68-125">請確定 hello.NET Framework 版本 4.5.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="08f68-125">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="08f68-126">名稱 hello 專案**ReadDeviceToCloudMessages**。</span><span class="sxs-lookup"><span data-stu-id="08f68-126">Name hello project **ReadDeviceToCloudMessages**.</span></span>

    ![新的 Visual C# Windows 傳統桌面專案][10a]

2. <span data-ttu-id="08f68-128">在 [方案總管] 中，以滑鼠右鍵按一下 hello **ReadDeviceToCloudMessages**專案，然後再按一下**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="08f68-128">In Solution Explorer, right-click hello **ReadDeviceToCloudMessages** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="08f68-129">在 hello **NuGet 套件管理員**視窗中，搜尋**WindowsAzure.ServiceBus**，選取**安裝**，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="08f68-129">In hello **NuGet Package Manager** window, search for **WindowsAzure.ServiceBus**, select **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="08f68-130">此程序下載、 安裝，並將參考加入太[Azure 服務匯流排][lnk-servicebus-nuget]，所有相依性。</span><span class="sxs-lookup"><span data-stu-id="08f68-130">This procedure downloads, installs, and adds a reference too[Azure Service Bus][lnk-servicebus-nuget], with all its dependencies.</span></span> <span data-ttu-id="08f68-131">此套件可讓 hello 應用程式 tooconnect toohello 事件中樞相容端點 IoT 中樞上。</span><span class="sxs-lookup"><span data-stu-id="08f68-131">This package enables hello application tooconnect toohello Event Hub-compatible endpoint on your IoT hub.</span></span>

4. <span data-ttu-id="08f68-132">新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：</span><span class="sxs-lookup"><span data-stu-id="08f68-132">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. <span data-ttu-id="08f68-133">新增下列欄位 toohello hello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="08f68-133">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="08f68-134">取代 hello hello 中樞在 hello 「 建立 IoT 中樞 」 一節中所建立的 IoT 中樞連接字串中的 hello 預留位置的值。</span><span class="sxs-lookup"><span data-stu-id="08f68-134">Replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello "Create an IoT hub" section.</span></span>

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. <span data-ttu-id="08f68-135">新增下列方法 toohello hello**程式**類別：</span><span class="sxs-lookup"><span data-stu-id="08f68-135">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested) break;
            EventData eventData = await eventHubReceiver.ReceiveAsync();
            if (eventData == null) continue;

            string data = Encoding.UTF8.GetString(eventData.GetBytes());
            Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
        }
    }
    ```

    <span data-ttu-id="08f68-136">這個方法會使用**EventHubReceiver**從所有 hello IoT 中樞裝置到雲端的執行個體 tooreceive 訊息接收的資料分割。</span><span class="sxs-lookup"><span data-stu-id="08f68-136">This method uses an **EventHubReceiver** instance tooreceive messages from all hello IoT hub device-to-cloud receive partitions.</span></span> <span data-ttu-id="08f68-137">請注意您的傳遞方式`DateTime.Now`參數，當您建立 hello **EventHubReceiver**物件，使它只會接收啟動後所傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="08f68-137">Notice how you pass a `DateTime.Now` parameter when you create hello **EventHubReceiver** object, so that it only receives messages sent after it starts.</span></span> <span data-ttu-id="08f68-138">此篩選器是適用於測試環境，因此您可以看到 hello 訊息的目前資料集。</span><span class="sxs-lookup"><span data-stu-id="08f68-138">This filter is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="08f68-139">在實際執行環境中，您的程式碼應該要確定在處理所有的 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="08f68-139">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="08f68-140">如需詳細資訊，請參閱 hello 教學課程[如何 tooprocess IoT 中樞裝置到雲端訊息][lnk-process-d2c-tutorial]。</span><span class="sxs-lookup"><span data-stu-id="08f68-140">For more information, see hello tutorial [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial].</span></span>

7. <span data-ttu-id="08f68-141">最後，加入下列行 toohello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="08f68-141">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive messages. Ctrl-C tooexit.\n");
    eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, iotHubD2cEndpoint);

    var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;

    CancellationTokenSource cts = new CancellationTokenSource();

    System.Console.CancelKeyPress += (s, e) =>
    {
        e.Cancel = true;
        cts.Cancel();
        Console.WriteLine("Exiting...");
    };

    var tasks = new List<Task>();
    foreach (string partition in d2cPartitions)
    {
        tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
    }  
    Task.WaitAll(tasks.ToArray());
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="08f68-142">建立裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="08f68-142">Create a device app</span></span>

<span data-ttu-id="08f68-143">在本節中，您可以建立.NET 主控台應用程式中，可以模擬傳送裝置到雲端訊息 tooan IoT 中樞的裝置。</span><span class="sxs-lookup"><span data-stu-id="08f68-143">In this section, you create a .NET console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="08f68-144">在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 toohello 目前方案，使用 hello**主控台應用程式 (.NET Framework)**專案範本。</span><span class="sxs-lookup"><span data-stu-id="08f68-144">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="08f68-145">請確定 hello.NET Framework 版本 4.5.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="08f68-145">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="08f68-146">名稱 hello 專案**SimulatedDevice**。</span><span class="sxs-lookup"><span data-stu-id="08f68-146">Name hello project **SimulatedDevice**.</span></span>

    ![新的 Visual C# Windows 傳統桌面專案][10b]

2. <span data-ttu-id="08f68-148">在 [方案總管] 中，以滑鼠右鍵按一下 hello **SimulatedDevice**專案，然後再按一下**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="08f68-148">In Solution Explorer, right-click hello **SimulatedDevice** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="08f68-149">在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**，搜尋**Microsoft.Azure.Devices.Client**，選取**安裝**tooinstall hello **Microsoft.Azure.Devices.Client**封裝，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="08f68-149">In hello **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Client**, select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="08f68-150">此程序下載、 安裝，並新增參考 toohello [Azure IoT 裝置 SDK 的 NuGet 套件][ lnk-device-nuget]及其相依項目。</span><span class="sxs-lookup"><span data-stu-id="08f68-150">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK NuGet package][lnk-device-nuget] and its dependencies.</span></span>

4. <span data-ttu-id="08f68-151">新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：</span><span class="sxs-lookup"><span data-stu-id="08f68-151">Add hello following `using` statement at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. <span data-ttu-id="08f68-152">新增下列欄位 toohello hello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="08f68-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="08f68-153">替代`{iot hub hostname}`使用您擷取 hello 「 建立 IoT 中樞 」 一節中的 hello IoT 中樞的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="08f68-153">Substitute `{iot hub hostname}` with hello IoT hub host name you retrieved in hello "Create an IoT hub" section.</span></span> <span data-ttu-id="08f68-154">替代`{device key}`與 hello 裝置索引鍵擷取 hello 「 建立裝置身分識別 」 一節中。</span><span class="sxs-lookup"><span data-stu-id="08f68-154">Substitute `{device key}` with hello device key you retrieved in hello "Create a device identity" section.</span></span>

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. <span data-ttu-id="08f68-155">新增下列方法 toohello hello**程式**類別：</span><span class="sxs-lookup"><span data-stu-id="08f68-155">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    private static async void SendDeviceToCloudMessagesAsync()
    {
        double minTemperature = 20;
        double minHumidity = 60;
        int messageId = 1;
        Random rand = new Random();

        while (true)
        {
            double currentTemperature = minTemperature + rand.NextDouble() * 15;
            double currentHumidity = minHumidity + rand.NextDouble() * 20;

            var telemetryDataPoint = new
            {
                messageId = messageId++,
                deviceId = "myFirstDevice",
                temperature = currentTemperature,
                humidity = currentHumidity
            };
            var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
            var message = new Message(Encoding.ASCII.GetBytes(messageString));
            message.Properties.Add("temperatureAlert", (currentTemperature > 30) ? "true" : "false");

            await deviceClient.SendEventAsync(message);
            Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, messageString);

            await Task.Delay(1000);
        }
    }
    ```

    <span data-ttu-id="08f68-156">這個方法會每秒傳送新的裝置對雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="08f68-156">This method sends a new device-to-cloud message every second.</span></span> <span data-ttu-id="08f68-157">hello 訊息包含 JSON 序列化物件，與 hello 裝置識別碼和隨機產生的數字 toosimulate 溫度感應器和溼度感應器。</span><span class="sxs-lookup"><span data-stu-id="08f68-157">hello message contains a JSON-serialized object, with hello device ID and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

7. <span data-ttu-id="08f68-158">最後，加入下列行 toohello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="08f68-158">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    <span data-ttu-id="08f68-159">根據預設，hello**建立**方法在.NET Framework 應用程式會建立**DeviceClient**使用 hello AMQP 通訊協定 toocommunicate 與 IoT 中樞執行個體。</span><span class="sxs-lookup"><span data-stu-id="08f68-159">By default, hello **Create** method in a .NET Framework app creates a **DeviceClient** instance that uses hello AMQP protocol toocommunicate with IoT Hub.</span></span> <span data-ttu-id="08f68-160">toouse hello MQTT 或 HTTP 通訊協定，使用覆寫 hello hello**建立**方法可讓您 toospecify hello 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="08f68-160">toouse hello MQTT or HTTP protocol, use hello override of hello **Create** method that enables you toospecify hello protocol.</span></span> <span data-ttu-id="08f68-161">UWP 和 PCL 用戶端預設使用 hello HTTP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="08f68-161">UWP and PCL clients use hello HTTP protocol by default.</span></span> <span data-ttu-id="08f68-162">如果您使用 hello HTTP 通訊協定，您也應該加入 hello **Microsoft.AspNet.WebApi.Client** NuGet 封裝 tooyour 專案 tooinclude hello **System.Net.Http.Formatting**命名空間。</span><span class="sxs-lookup"><span data-stu-id="08f68-162">If you use hello HTTP protocol, you should also add hello **Microsoft.AspNet.WebApi.Client** NuGet package tooyour project tooinclude hello **System.Net.Http.Formatting** namespace.</span></span>

<span data-ttu-id="08f68-163">本教學課程中引導您完成 hello 步驟 toocreate IoT 中樞裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="08f68-163">This tutorial takes you through hello steps toocreate an IoT Hub device app.</span></span> <span data-ttu-id="08f68-164">您也可以使用 hello[已連接服務的 Azure IoT 中樞][ lnk-connected-service] Visual Studio 擴充功能 tooadd hello 必要的程式碼 tooyour 裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="08f68-164">You can also use hello [Connected Service for Azure IoT Hub][lnk-connected-service] Visual Studio extension tooadd hello necessary code tooyour device app.</span></span>

> [!NOTE]
> <span data-ttu-id="08f68-165">簡單 tookeep 方面，本教學課程未實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="08f68-165">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="08f68-166">在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理][lnk-transient-faults]。</span><span class="sxs-lookup"><span data-stu-id="08f68-166">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="08f68-167">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="08f68-167">Run hello apps</span></span>

<span data-ttu-id="08f68-168">現在您已經準備就緒 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="08f68-168">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="08f68-169">在 Visual Studio 的 方案總管 中以滑鼠右鍵按一下您的方案，然後按一下設定啟始專案。</span><span class="sxs-lookup"><span data-stu-id="08f68-169">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="08f68-170">選取**多個啟始專案**，然後選取**啟動**hello 動作這兩個 hello **ReadDeviceToCloudMessages**和**SimulatedDevice**專案。</span><span class="sxs-lookup"><span data-stu-id="08f68-170">Select **Multiple startup projects**, and then select **Start** as hello action for both hello **ReadDeviceToCloudMessages** and **SimulatedDevice** projects.</span></span>

    ![啟動專案屬性 ][41]

2. <span data-ttu-id="08f68-172">按**F5** toostart 這兩個執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="08f68-172">Press **F5** toostart both apps running.</span></span> <span data-ttu-id="08f68-173">hello hello 從主控台輸出**SimulatedDevice**您裝置的應用程式傳送 tooyour IoT 中樞應用程式顯示 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="08f68-173">hello console output from hello **SimulatedDevice** app shows hello messages your device app sends tooyour IoT hub.</span></span> <span data-ttu-id="08f68-174">hello hello 從主控台輸出**ReadDeviceToCloudMessages**應用程式會顯示您的 IoT 中樞接收的 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="08f68-174">hello console output from hello **ReadDeviceToCloudMessages** app shows hello messages that your IoT hub receives.</span></span>

    ![來自應用程式的主控台輸出][42]

3. <span data-ttu-id="08f68-176">hello**使用量**磚中 hello [Azure 入口網站][ lnk-portal]顯示 hello 訊息傳送 toohello IoT 中樞的數目：</span><span class="sxs-lookup"><span data-stu-id="08f68-176">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Azure 入口網站的使用量圖格][43]

## <a name="next-steps"></a><span data-ttu-id="08f68-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="08f68-178">Next steps</span></span>

<span data-ttu-id="08f68-179">在本教學課程中，您可以設定 hello Azure 入口網站中的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="08f68-179">In this tutorial, you configured an IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="08f68-180">您已經使用此裝置身分識別 tooenable hello 裝置應用程式 toosend 裝置到雲端訊息 toohello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="08f68-180">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="08f68-181">您也會建立會顯示 hello IoT 中樞收到 hello 訊息的應用程式。</span><span class="sxs-lookup"><span data-stu-id="08f68-181">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="08f68-182">使用者入門 toocontinue tooexplore IoT 中樞與其他 IoT 案例，請參閱：</span><span class="sxs-lookup"><span data-stu-id="08f68-182">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="08f68-183">[連接您的裝置][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="08f68-183">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="08f68-184">[開始使用裝置管理][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="08f68-184">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="08f68-185">[開始使用 IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="08f68-185">[Getting started with IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="08f68-186">toolearn 如何 tooextend 您 IoT 方案和程序裝置到雲端訊息在小數位數，請參閱 hello[處理裝置到雲端訊息][ lnk-process-d2c-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="08f68-186">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[41]: ./media/iot-hub-csharp-csharp-getstarted/run-apps1.png
[42]: ./media/iot-hub-csharp-csharp-getstarted/run-apps2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png
[10a]: ./media/iot-hub-csharp-csharp-getstarted/create-receive-csharp1.png
[10b]: ./media/iot-hub-csharp-csharp-getstarted/create-device-csharp1.png


<!-- Links -->
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-servicebus-nuget]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-device-nuget]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-connected-service]: https://visualstudiogallery.msdn.microsoft.com/e254a3a5-d72e-488e-9bd3-8fee8e0cd1d6
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
