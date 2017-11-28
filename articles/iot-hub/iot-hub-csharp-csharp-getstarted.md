---
title: "開始使用 Azure IoT 中樞 (.NET) | Microsoft Docs"
description: "了解如何使用適用於 .NET 的 IoT SDK 將裝置到雲端訊息傳送至 Azure IoT 中樞。 建立模擬裝置和服務應用程式來註冊您的裝置、傳送訊息，並從 IoT 中樞讀取訊息。"
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
ms.openlocfilehash: 69296eb9ac2a74a97b632d27733a6a06500b4abd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="connect-your-device-to-your-iot-hub-using-net"></a><span data-ttu-id="10e65-104">使用 .NET 將您的裝置連線至 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="10e65-104">Connect your device to your IoT hub using .NET</span></span>

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="10e65-105">在本教學課程結尾處，您會有三個 .NET 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="10e65-105">At the end of this tutorial, you have three .NET console apps:</span></span>

* <span data-ttu-id="10e65-106">**CreateDeviceIdentity**，這會建立裝置身分識別與相關聯的安全性金鑰，以連線到您的裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="10e65-106">**CreateDeviceIdentity**, which creates a device identity and associated security key to connect your device app.</span></span>
* <span data-ttu-id="10e65-107">**ReadDeviceToCloudMessages**，其中顯示裝置應用程式所傳送的遙測。</span><span class="sxs-lookup"><span data-stu-id="10e65-107">**ReadDeviceToCloudMessages**, which displays the telemetry sent by your device app.</span></span>
* <span data-ttu-id="10e65-108">**SimulatedDevice**，這會使用先前建立的裝置識別連接到您的 IoT 中樞，並使用 MQTT 通訊協定每秒傳送遙測訊息。</span><span class="sxs-lookup"><span data-stu-id="10e65-108">**SimulatedDevice**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second by using the MQTT protocol.</span></span>

<span data-ttu-id="10e65-109">您可以下載或複製 Visual Studio 方案，其中包含來自 Github 的三個應用程式。</span><span class="sxs-lookup"><span data-stu-id="10e65-109">You can download or clone the Visual Studio solution, which contains the three apps from Github.</span></span>

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> <span data-ttu-id="10e65-110">如需可用來建置兩個應用程式，以在裝置與您的解決方案後端執行之 Azure IoT SDK 的相關資訊，請參閱 [Azure IoT SDK][lnk-hub-sdks]。</span><span class="sxs-lookup"><span data-stu-id="10e65-110">For information about the Azure IoT SDKs that you can use to build both applications to run on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="10e65-111">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="10e65-111">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="10e65-112">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="10e65-112">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="10e65-113">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="10e65-113">An active Azure account.</span></span> <span data-ttu-id="10e65-114">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="10e65-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="10e65-115">您現在已經建立 IoT 中樞，因此您已具有完成本教學課程的其餘部分所需的主機名稱和 IoT 中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="10e65-115">You have now created your IoT hub, and you have the host name and IoT Hub connection string that you need to complete the rest of this tutorial.</span></span>

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="10e65-116">接收裝置到雲端的訊息</span><span class="sxs-lookup"><span data-stu-id="10e65-116">Receive device-to-cloud messages</span></span>
<span data-ttu-id="10e65-117">在本節中，您會建立 .NET 主控台應用程式，以讀取來自 IoT 中樞的裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="10e65-117">In this section, you create a .NET console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="10e65-118">IoT 中樞會公開與 [Azure 事件中樞][lnk-event-hubs-overview]相容的端點以讓您讀取裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="10e65-118">An IoT hub exposes an [Azure Event Hubs][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="10e65-119">為了簡單起見，本教學課程會建立的基本讀取器不適合用於高輸送量部署。</span><span class="sxs-lookup"><span data-stu-id="10e65-119">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="10e65-120">若要了解如何大規模處理裝置到雲端訊息，請參閱[處理裝置到雲端訊息][lnk-process-d2c-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="10e65-120">To learn how to process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span> <span data-ttu-id="10e65-121">如需有關如何處理來自「事件中樞」之訊息的詳細資訊，請參閱[開始使用事件中樞][lnk-eventhubs-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="10e65-121">For more information about how to process messages from Event Hubs, see the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span> <span data-ttu-id="10e65-122">(本教學課程適用於 IoT 中樞的事件中樞相容端點)。</span><span class="sxs-lookup"><span data-stu-id="10e65-122">(This tutorial is applicable to the IoT Hub Event Hub-compatible endpoints.)</span></span>

> [!NOTE]
> <span data-ttu-id="10e65-123">用於讀取裝置到雲端訊息的事件中樞相容端點一律會使用 AMQP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="10e65-123">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>

1. <span data-ttu-id="10e65-124">在 Visual Studio 中，使用 [主控台應用程式 (.NET Framework)] 專案範本，將 Visual C# Windows 傳統桌面專案新增至目前的解決方案。</span><span class="sxs-lookup"><span data-stu-id="10e65-124">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="10e65-125">確定 .NET Framework 為 4.5.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="10e65-125">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="10e65-126">將專案命名為 **ReadDeviceToCloudMessages**。</span><span class="sxs-lookup"><span data-stu-id="10e65-126">Name the project **ReadDeviceToCloudMessages**.</span></span>

    ![新的 Visual C# Windows 傳統桌面專案][10a]

2. <span data-ttu-id="10e65-128">在 [方案總管] 中，以滑鼠右鍵按一下 **ReadDeviceToCloudMessages** 專案，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="10e65-128">In Solution Explorer, right-click the **ReadDeviceToCloudMessages** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="10e65-129">在 [NuGet 套件管理員] 視窗中，搜尋 **WindowsAzure.ServiceBus**，選取 [安裝] 並接受使用規定。</span><span class="sxs-lookup"><span data-stu-id="10e65-129">In the **NuGet Package Manager** window, search for **WindowsAzure.ServiceBus**, select **Install**, and accept the terms of use.</span></span> <span data-ttu-id="10e65-130">此程序會下載及安裝 [Azure 服務匯流排][lnk-servicebus-nuget]，並新增對它的參考與其所有相依項目。</span><span class="sxs-lookup"><span data-stu-id="10e65-130">This procedure downloads, installs, and adds a reference to [Azure Service Bus][lnk-servicebus-nuget], with all its dependencies.</span></span> <span data-ttu-id="10e65-131">此套件可讓應用程式連接到 IoT 中樞上的事件中樞相容端點。</span><span class="sxs-lookup"><span data-stu-id="10e65-131">This package enables the application to connect to the Event Hub-compatible endpoint on your IoT hub.</span></span>

4. <span data-ttu-id="10e65-132">在 **Program.cs** 檔案開頭處新增下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="10e65-132">Add the following `using` statements at the top of the **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. <span data-ttu-id="10e65-133">將下列欄位新增到 **Program** 類別。</span><span class="sxs-lookup"><span data-stu-id="10e65-133">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="10e65-134">將預留位置的值替換為您在＜建立 IoT 中樞＞一節中為中樞所建立的 IoT 中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="10e65-134">Replace the placeholder value with the IoT Hub connection string for the hub you created in the "Create an IoT hub" section.</span></span>

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. <span data-ttu-id="10e65-135">將下列方法新增至 **Program** 類別：</span><span class="sxs-lookup"><span data-stu-id="10e65-135">Add the following method to the **Program** class:</span></span>

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

    <span data-ttu-id="10e65-136">這個方法會使用 **EventHubReceiver** 執行個體接收來自所有 IoT 中樞裝置對雲端接收資料分割的訊息。</span><span class="sxs-lookup"><span data-stu-id="10e65-136">This method uses an **EventHubReceiver** instance to receive messages from all the IoT hub device-to-cloud receive partitions.</span></span> <span data-ttu-id="10e65-137">請注意當您建立 **EventHubReceiver** 物件時如何傳遞 `DateTime.Now` 參數，使它只會收到它啟動後傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="10e65-137">Notice how you pass a `DateTime.Now` parameter when you create the **EventHubReceiver** object, so that it only receives messages sent after it starts.</span></span> <span data-ttu-id="10e65-138">此篩選器很適合測試環境，因為如此一來您就可以看到目前的訊息集。</span><span class="sxs-lookup"><span data-stu-id="10e65-138">This filter is useful in a test environment so you can see the current set of messages.</span></span> <span data-ttu-id="10e65-139">在生產環境中，您的程式碼應該要確定它能處理所有訊息。</span><span class="sxs-lookup"><span data-stu-id="10e65-139">In a production environment, your code should make sure that it processes all the messages.</span></span> <span data-ttu-id="10e65-140">如需詳細資訊，請參閱[如何處理 IoT 中樞裝置到雲端訊息][lnk-process-d2c-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="10e65-140">For more information, see the tutorial [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial].</span></span>

7. <span data-ttu-id="10e65-141">最後，將下列幾行新增至 **Main** 方法：</span><span class="sxs-lookup"><span data-stu-id="10e65-141">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive messages. Ctrl-C to exit.\n");
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

## <a name="create-a-device-app"></a><span data-ttu-id="10e65-142">建立裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="10e65-142">Create a device app</span></span>

<span data-ttu-id="10e65-143">在本節中，您會撰寫 .NET 主控台應用程式，模擬裝置傳送裝置對雲端訊息至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="10e65-143">In this section, you create a .NET console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="10e65-144">在 Visual Studio 中，使用 [主控台應用程式 (.NET Framework)] 專案範本，將 Visual C# Windows 傳統桌面專案新增至目前的解決方案。</span><span class="sxs-lookup"><span data-stu-id="10e65-144">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="10e65-145">確定 .NET Framework 為 4.5.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="10e65-145">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="10e65-146">將專案命名為 **SimulatedDevice**。</span><span class="sxs-lookup"><span data-stu-id="10e65-146">Name the project **SimulatedDevice**.</span></span>

    ![新的 Visual C# Windows 傳統桌面專案][10b]

2. <span data-ttu-id="10e65-148">在 [方案總管] 中，以滑鼠右鍵按一下 **SimulatedDevice** 專案，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="10e65-148">In Solution Explorer, right-click the **SimulatedDevice** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="10e65-149">在 [NuGet 套件管理員] 視窗中選取 [瀏覽]、搜尋 **Microsoft.Azure.Devices.Client**、選取 [安裝] 以安裝 **Microsoft.Azure.Devices.Client** 套件，並接受使用規定。</span><span class="sxs-lookup"><span data-stu-id="10e65-149">In the **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Client**, select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="10e65-150">此程序會下載及安裝 [Azure IoT 裝置 SDK NuGet 套件][lnk-device-nuget]與其相依項目，並新增對它的參考。</span><span class="sxs-lookup"><span data-stu-id="10e65-150">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK NuGet package][lnk-device-nuget] and its dependencies.</span></span>

4. <span data-ttu-id="10e65-151">在 **Program.cs** 檔案開頭處新增下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="10e65-151">Add the following `using` statement at the top of the **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. <span data-ttu-id="10e65-152">將下列欄位新增到 **Program** 類別。</span><span class="sxs-lookup"><span data-stu-id="10e65-152">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="10e65-153">以您在「建立 IoT 中樞」一節中擷取的 IoT 中樞主機名稱替代 `{iot hub hostname}`。</span><span class="sxs-lookup"><span data-stu-id="10e65-153">Substitute `{iot hub hostname}` with the IoT hub host name you retrieved in the "Create an IoT hub" section.</span></span> <span data-ttu-id="10e65-154">以您在「建立裝置身分識別」一節中擷取的裝置金鑰替代 `{device key}`。</span><span class="sxs-lookup"><span data-stu-id="10e65-154">Substitute `{device key}` with the device key you retrieved in the "Create a device identity" section.</span></span>

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. <span data-ttu-id="10e65-155">將下列方法加入至 **Program** 類別：</span><span class="sxs-lookup"><span data-stu-id="10e65-155">Add the following method to the **Program** class:</span></span>

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

    <span data-ttu-id="10e65-156">這個方法會每秒傳送新的裝置對雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="10e65-156">This method sends a new device-to-cloud message every second.</span></span> <span data-ttu-id="10e65-157">此訊息包含 JSON 序列化物件及裝置識別碼與隨機產生的數字，以模擬溫度感應器和溼度感應器。</span><span class="sxs-lookup"><span data-stu-id="10e65-157">The message contains a JSON-serialized object, with the device ID and randomly generated numbers to simulate a temperature sensor, and a humidity sensor.</span></span>

7. <span data-ttu-id="10e65-158">最後，將下列幾行加入至 **Main** 方法：</span><span class="sxs-lookup"><span data-stu-id="10e65-158">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    <span data-ttu-id="10e65-159">根據預設，**Create** 方法會在 .NET Framework 應用程式中建立一個使用 AMQP 通訊協定的 **DeviceClient** 執行個體來與 IoT 中樞通訊。</span><span class="sxs-lookup"><span data-stu-id="10e65-159">By default, the **Create** method in a .NET Framework app creates a **DeviceClient** instance that uses the AMQP protocol to communicate with IoT Hub.</span></span> <span data-ttu-id="10e65-160">若要使用 MQTT 或 HTTP 通訊協定，請使用可讓您指定通訊協定的 **Create** 方法的覆寫。</span><span class="sxs-lookup"><span data-stu-id="10e65-160">To use the MQTT or HTTP protocol, use the override of the **Create** method that enables you to specify the protocol.</span></span> <span data-ttu-id="10e65-161">UWP 和 PCL 用戶端預設使用 HTTP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="10e65-161">UWP and PCL clients use the HTTP protocol by default.</span></span> <span data-ttu-id="10e65-162">若您使用 HTTP 通訊協定，您也應該將 **Microsoft.AspNet.WebApi.Client** NuGet 套件新增至您的專案，以包含 **System.Net.Http.Formatting** 命名空間。</span><span class="sxs-lookup"><span data-stu-id="10e65-162">If you use the HTTP protocol, you should also add the **Microsoft.AspNet.WebApi.Client** NuGet package to your project to include the **System.Net.Http.Formatting** namespace.</span></span>

<span data-ttu-id="10e65-163">本教學課程會逐步引導您完成建立 IoT 中樞裝置應用程式的步驟。</span><span class="sxs-lookup"><span data-stu-id="10e65-163">This tutorial takes you through the steps to create an IoT Hub device app.</span></span> <span data-ttu-id="10e65-164">您也可以使用 [Azure IoT 中樞的已連結服務][lnk-connected-service] Visual Studio 擴充功能，將必要的程式碼新增至裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="10e65-164">You can also use the [Connected Service for Azure IoT Hub][lnk-connected-service] Visual Studio extension to add the necessary code to your device app.</span></span>

> [!NOTE]
> <span data-ttu-id="10e65-165">為了簡單起見，本教學課程不會實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="10e65-165">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="10e65-166">在實際程式碼中，您應該如 MSDN 文章[暫時性錯誤處理][lnk-transient-faults]所建議，實作重試原則 (例如指數型輪詢)。</span><span class="sxs-lookup"><span data-stu-id="10e65-166">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="10e65-167">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="10e65-167">Run the apps</span></span>

<span data-ttu-id="10e65-168">您現在可以開始執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="10e65-168">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="10e65-169">在 Visual Studio 的 [方案總管] 中以滑鼠右鍵按一下您的方案，然後按一下 [設定啟始專案]。</span><span class="sxs-lookup"><span data-stu-id="10e65-169">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="10e65-170">選取 [多個啟始專案]，然後同時針對 **ReadDeviceToCloudMessages** 和 **SimulatedDevice** 專案選取 **Start** 作為動作。</span><span class="sxs-lookup"><span data-stu-id="10e65-170">Select **Multiple startup projects**, and then select **Start** as the action for both the **ReadDeviceToCloudMessages** and **SimulatedDevice** projects.</span></span>

    ![啟動專案屬性 ][41]

2. <span data-ttu-id="10e65-172">按下 **F5** 來啟動這兩個執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="10e65-172">Press **F5** to start both apps running.</span></span> <span data-ttu-id="10e65-173">來自 **SimulatedDevice** 應用程式的主控台輸出會顯示裝置應用程式傳送給您的 IoT 中樞的訊息。</span><span class="sxs-lookup"><span data-stu-id="10e65-173">The console output from the **SimulatedDevice** app shows the messages your device app sends to your IoT hub.</span></span> <span data-ttu-id="10e65-174">來自 **ReadDeviceToCloudMessages** 應用程式的主控台輸出則會顯示您的 IoT 中樞接收的訊息。</span><span class="sxs-lookup"><span data-stu-id="10e65-174">The console output from the **ReadDeviceToCloudMessages** app shows the messages that your IoT hub receives.</span></span>

    ![來自應用程式的主控台輸出][42]

3. <span data-ttu-id="10e65-176">[Azure 入口網站][lnk-portal]中的 [使用量] 圖格會顯示傳送至 IoT 中樞的訊息數目︰</span><span class="sxs-lookup"><span data-stu-id="10e65-176">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>

    ![Azure 入口網站的使用量圖格][43]

## <a name="next-steps"></a><span data-ttu-id="10e65-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="10e65-178">Next steps</span></span>

<span data-ttu-id="10e65-179">在此教學課程中，您在 Azure 入口網站中設定了 IoT 中樞，然後在 IoT 中樞的身分識別登錄中建立了裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="10e65-179">In this tutorial, you configured an IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="10e65-180">您會將此裝置身分識別用於啟用裝置應用程式，以將裝置到雲端訊息傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="10e65-180">You used this device identity to enable the device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="10e65-181">您也會建立一個應用程式來顯示 IoT 中樞所接收的訊息。</span><span class="sxs-lookup"><span data-stu-id="10e65-181">You also created an app that displays the messages received by the IoT hub.</span></span>

<span data-ttu-id="10e65-182">若要繼續開始使用 IoT 中樞並瀏覽其他 IoT 案例，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="10e65-182">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="10e65-183">[連接您的裝置][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="10e65-183">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="10e65-184">[開始使用裝置管理][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="10e65-184">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="10e65-185">[開始使用 IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="10e65-185">[Getting started with IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="10e65-186">若要了解如何擴充您的 IoT 解決方案及大規模處理裝置到雲端訊息，請參閱[處理裝置到雲端訊息][lnk-process-d2c-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="10e65-186">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

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
