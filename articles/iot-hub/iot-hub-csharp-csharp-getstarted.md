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
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a>連接您使用適用於.NET 的裝置 tooyour IoT 中樞

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

在本教學課程的 hello 最後，您有三個.NET 主控台應用程式：

* **CreateDeviceIdentity**，這樣就可以建立裝置身分識別，以及相關聯的安全性金鑰 tooconnect 您裝置的應用程式。
* **ReadDeviceToCloudMessages**，其中顯示您裝置的應用程式所傳送的 hello 遙測。
* **SimulatedDevice**，這會 tooyour IoT 中樞連接使用稍早建立的 hello 裝置身分識別，並使用 hello MQTT 通訊協定傳送遙測訊息每秒。

您可以下載或複製 hello Visual Studio 方案，其中包含從 Github 的 hello 三個應用程式。

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> 如需有關資訊 hello Azure IoT Sdk，您可以使用 toobuild 在裝置上，應用程式 toorun 和您的方案後端，請參閱[Azure IoT Sdk][lnk-hub-sdks]。

toocomplete 本教學課程中，您需要遵循的 hello:

* Visual Studio 2015 或 Visual Studio 2017。
* 使用中的 Azure 帳戶。 (如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

您現在已建立您的 IoT 中樞，而且您擁有 hello 主機名稱和您需要 toocomplete hello rest 本教學課程的 IoT 中樞連接字串。

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a>接收裝置到雲端的訊息
在本節中，您會建立 .NET 主控台應用程式，以讀取來自 IoT 中樞的裝置到雲端訊息。 IoT 中樞公開[Azure 事件中心][lnk-event-hubs-overview]-相容的端點 tooenable 您 tooread 裝置到雲端訊息。 簡單 tookeep 方面，本教學課程會建立基本的讀取器不是適用於高輸送量部署。 toolearn 如何 tooprocess 裝置到雲端訊息小數位數，請參閱 hello[處理裝置到雲端訊息][ lnk-process-d2c-tutorial]教學課程。 如需如何 tooprocess 訊息從事件中心的詳細資訊，請參閱 hello[開始使用事件中心][ lnk-eventhubs-tutorial]教學課程。 （本教學課程是適用 toohello IoT 中樞事件中樞相容的端點）。

> [!NOTE]
> hello 一律讀取裝置到雲端訊息的事件中樞相容端點使用 hello AMQP 通訊協定。

1. 在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 toohello 目前方案，使用 hello**主控台應用程式 (.NET Framework)**專案範本。 請確定 hello.NET Framework 版本 4.5.1 或更新版本。 名稱 hello 專案**ReadDeviceToCloudMessages**。

    ![新的 Visual C# Windows 傳統桌面專案][10a]

2. 在 [方案總管] 中，以滑鼠右鍵按一下 hello **ReadDeviceToCloudMessages**專案，然後再按一下**管理 NuGet 封裝**。

3. 在 hello **NuGet 套件管理員**視窗中，搜尋**WindowsAzure.ServiceBus**，選取**安裝**，並接受使用規定 hello。 此程序下載、 安裝，並將參考加入太[Azure 服務匯流排][lnk-servicebus-nuget]，所有相依性。 此套件可讓 hello 應用程式 tooconnect toohello 事件中樞相容端點 IoT 中樞上。

4. 新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. 新增下列欄位 toohello hello**程式**類別。 取代 hello hello 中樞在 hello 「 建立 IoT 中樞 」 一節中所建立的 IoT 中樞連接字串中的 hello 預留位置的值。

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. 新增下列方法 toohello hello**程式**類別：

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

    這個方法會使用**EventHubReceiver**從所有 hello IoT 中樞裝置到雲端的執行個體 tooreceive 訊息接收的資料分割。 請注意您的傳遞方式`DateTime.Now`參數，當您建立 hello **EventHubReceiver**物件，使它只會接收啟動後所傳送的訊息。 此篩選器是適用於測試環境，因此您可以看到 hello 訊息的目前資料集。 在實際執行環境中，您的程式碼應該要確定在處理所有的 hello 訊息。 如需詳細資訊，請參閱 hello 教學課程[如何 tooprocess IoT 中樞裝置到雲端訊息][lnk-process-d2c-tutorial]。

7. 最後，加入下列行 toohello hello **Main**方法：

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

## <a name="create-a-device-app"></a>建立裝置應用程式

在本節中，您可以建立.NET 主控台應用程式中，可以模擬傳送裝置到雲端訊息 tooan IoT 中樞的裝置。

1. 在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 toohello 目前方案，使用 hello**主控台應用程式 (.NET Framework)**專案範本。 請確定 hello.NET Framework 版本 4.5.1 或更新版本。 名稱 hello 專案**SimulatedDevice**。

    ![新的 Visual C# Windows 傳統桌面專案][10b]

2. 在 [方案總管] 中，以滑鼠右鍵按一下 hello **SimulatedDevice**專案，然後再按一下**管理 NuGet 封裝**。

3. 在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**，搜尋**Microsoft.Azure.Devices.Client**，選取**安裝**tooinstall hello **Microsoft.Azure.Devices.Client**封裝，並接受使用規定 hello。 此程序下載、 安裝，並新增參考 toohello [Azure IoT 裝置 SDK 的 NuGet 套件][ lnk-device-nuget]及其相依項目。

4. 新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. 新增下列欄位 toohello hello**程式**類別。 替代`{iot hub hostname}`使用您擷取 hello 「 建立 IoT 中樞 」 一節中的 hello IoT 中樞的主機名稱。 替代`{device key}`與 hello 裝置索引鍵擷取 hello 「 建立裝置身分識別 」 一節中。

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. 新增下列方法 toohello hello**程式**類別：

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

    這個方法會每秒傳送新的裝置對雲端訊息。 hello 訊息包含 JSON 序列化物件，與 hello 裝置識別碼和隨機產生的數字 toosimulate 溫度感應器和溼度感應器。

7. 最後，加入下列行 toohello hello **Main**方法：

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    根據預設，hello**建立**方法在.NET Framework 應用程式會建立**DeviceClient**使用 hello AMQP 通訊協定 toocommunicate 與 IoT 中樞執行個體。 toouse hello MQTT 或 HTTP 通訊協定，使用覆寫 hello hello**建立**方法可讓您 toospecify hello 通訊協定。 UWP 和 PCL 用戶端預設使用 hello HTTP 通訊協定。 如果您使用 hello HTTP 通訊協定，您也應該加入 hello **Microsoft.AspNet.WebApi.Client** NuGet 封裝 tooyour 專案 tooinclude hello **System.Net.Http.Formatting**命名空間。

本教學課程中引導您完成 hello 步驟 toocreate IoT 中樞裝置應用程式。 您也可以使用 hello[已連接服務的 Azure IoT 中樞][ lnk-connected-service] Visual Studio 擴充功能 tooadd hello 必要的程式碼 tooyour 裝置應用程式。

> [!NOTE]
> 簡單 tookeep 方面，本教學課程未實作任何重試原則。 在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理][lnk-transient-faults]。

## <a name="run-hello-apps"></a>執行 hello 應用程式

現在您已經準備就緒 toorun hello 應用程式。

1. 在 Visual Studio 的 方案總管 中以滑鼠右鍵按一下您的方案，然後按一下設定啟始專案。 選取**多個啟始專案**，然後選取**啟動**hello 動作這兩個 hello **ReadDeviceToCloudMessages**和**SimulatedDevice**專案。

    ![啟動專案屬性 ][41]

2. 按**F5** toostart 這兩個執行的應用程式。 hello hello 從主控台輸出**SimulatedDevice**您裝置的應用程式傳送 tooyour IoT 中樞應用程式顯示 hello 訊息。 hello hello 從主控台輸出**ReadDeviceToCloudMessages**應用程式會顯示您的 IoT 中樞接收的 hello 訊息。

    ![來自應用程式的主控台輸出][42]

3. hello**使用量**磚中 hello [Azure 入口網站][ lnk-portal]顯示 hello 訊息傳送 toohello IoT 中樞的數目：

    ![Azure 入口網站的使用量圖格][43]

## <a name="next-steps"></a>後續步驟

在本教學課程中，您可以設定 hello Azure 入口網站中的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。 您已經使用此裝置身分識別 tooenable hello 裝置應用程式 toosend 裝置到雲端訊息 toohello IoT 中樞。 您也會建立會顯示 hello IoT 中樞收到 hello 訊息的應用程式。

使用者入門 toocontinue tooexplore IoT 中樞與其他 IoT 案例，請參閱：

* [連接您的裝置][lnk-connect-device]
* [開始使用裝置管理][lnk-device-management]
* [開始使用 IoT Edge][lnk-iot-edge]

toolearn 如何 tooextend 您 IoT 方案和程序裝置到雲端訊息在小數位數，請參閱 hello[處理裝置到雲端訊息][ lnk-process-d2c-tutorial]教學課程。

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
