---
title: "使用路由 (.Net) aaaProcess Azure IoT Hub 裝置到雲端訊息 |Microsoft 文件"
description: "如何使用路由規則和自訂端點 toodispatch IoT 中樞裝置到雲端訊息 tooprocess 訊息 tooother 後端服務。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 5177bac9-722f-47ef-8a14-b201142ba4bc
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: c1dd5be04ca30c65af2be466ba6c8c1858333154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a>使用路由處理 Azure IoT 中樞的裝置到雲端訊息 (.NET)

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

本教學課程是 hello[開始使用 IoT 中樞]教學課程。 hello 教學課程：

* 顯示如何 toouse 路由規則 toodispatch 裝置到雲端訊息以簡單、 以組態為基礎的方式。
* 說明 tooisolate 互動式訊息需要立即採取行動 hello 方案從傳回的進一步處理結束的方式。 例如，裝置可能會傳送一則警示訊息，以觸發將票證插入 CRM 系統的作業。 相較之下，資料點訊息 (例如溫度遙測) 只會饋送至分析引擎。

在本教學課程的 hello 最後，您可以執行三個.NET 主控台應用程式：

* **SimulatedDevice**，hello hello 中建立的應用程式的修改的版本[開始使用 IoT 中樞]教學課程傳送的資料點裝置到雲端訊息每秒，而互動式裝置到雲端訊息每隔 10秒數。
* **ReadDeviceToCloudMessages**顯示 hello 裝置之應用程式所傳送的非關鍵遙測。
* **ReadCriticalQueue**取消佇列 hello 重大裝置之應用程式所傳送來自服務匯流排佇列的訊息。 此佇列為附加的 toohello IoT 中樞。

> [!NOTE]
> IoT 中樞對於許多裝置平台和語言 (包括 C、Java 和 JavaScript) 提供 SDK 支援。 toolearn 如何 tooreplace 本教學課程中模擬的裝置 hello 與實體裝置，請參閱 hello [Azure IoT 開發人員中心]。

toocomplete 本教學課程中，您需要遵循的 hello:

* Visual Studio 2015 或 Visual Studio 2017。
* 使用中的 Azure 帳戶。 <br/>如果您沒有帳戶，只需要幾分鐘的時間就可以建立 [免費帳戶](https://azure.microsoft.com/free/) 。

您應具備 [Azure 儲存體]和 [Azure 服務匯流排]的基本知識。

## <a name="send-interactive-messages"></a>傳送互動式訊息

修改 hello 裝置應用程式，您可以在 hello[開始使用 IoT 中樞]教學課程 toooccasionally 傳送互動的訊息。

在 Visual Studio，在 hello **SimulatedDevice**專案中，取代 hello`SendDeviceToCloudMessagesAsync`方法，以下列程式碼的 hello:

```csharp
private static async void SendDeviceToCloudMessagesAsync()
{
    double minTemperature = 20;
    double minHumidity = 60;
    Random rand = new Random();

    while (true)
    {
        double currentTemperature = minTemperature + rand.NextDouble() * 15;
        double currentHumidity = minHumidity + rand.NextDouble() * 20;

        var telemetryDataPoint = new
        {
            deviceId = "myFirstDevice",
            temperature = currentTemperature,
            humidity = currentHumidity
        };
        var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
        string levelValue;

        if (rand.NextDouble() > 0.7)
        {
            messageString = "This is a critical message";
            levelValue = "critical";
        }
        else
        {
            levelValue = "normal";
        }
        
        var message = new Message(Encoding.ASCII.GetBytes(messageString));
        message.Properties.Add("level", levelValue);
        
        await deviceClient.SendEventAsync(message);
        Console.WriteLine("{0} > Sent message: {1}", DateTime.Now, messageString);

        await Task.Delay(1000);
    }
}
```

此方法會隨機將 hello 屬性`"level": "critical"`toomessages 傳送 hello 裝置，這將模擬 hello 方案後端時，需要立即採取行動的訊息。 hello 裝置應用程式將此資訊傳遞在 hello 訊息內容中，而不是在 hello 訊息主體中，因此該 IoT 中樞可以路由傳送 hello 訊息 toohello 適當訊息目的地。

> [!NOTE]
> 您可以使用訊息內容 tooroute 訊息各種案例，包括冷路徑的處理，此外 toohello 熱路徑範例所示。

> [!NOTE]
> 為了簡化的 hello 起見，本教學課程未實作任何重試原則。 在實際執行程式碼，您應該實作重試原則，例如 hello MSDN 文章中建議的指數型撤退[暫時性錯誤處理]。

## <a name="route-messages-tooa-queue-in-your-iot-hub"></a>路由的郵件 tooa 佇列在 IoT 中樞

在本節中，您可：

* 建立服務匯流排佇列。
* 連接 tooyour IoT 中樞。
* 設定您 IoT 中樞 toosend 訊息 toohello 佇列根據 hello hello 訊息上的屬性存在。

如需如何 tooprocess 訊息從服務匯流排佇列的詳細資訊，請參閱[開始使用佇列][Service Bus queue]。

1. 如[開始使用佇列][Service Bus queue]所述，建立服務匯流排佇列。 hello hello 佇列必須是相同的訂用帳戶和與 IoT 中樞區域。 記下 hello 命名空間和佇列名稱。

    > [!NOTE]
    > 做為 IoT 中樞端點的服務匯流排佇列和主題不能啟用 [工作階段] 或 [重複偵測]。 如果這些選項的其中一個已啟用，以顯示 hello 端點**連線**hello Azure 入口網站中。

2. 在 hello Azure 入口網站，開啟您的 IoT 中樞，然後按一下**端點**。
    
    ![IoT 中樞端點][30]

3. 在 hello**端點**刀鋒視窗中，按一下 **新增**在 hello 頂端 tooadd 佇列 tooyour IoT 中樞。 名稱 hello 端點**CriticalQueue**並用 hello 下拉式清單 tooselect **Service Bus 佇列**、 hello 佇列所在的服務匯流排命名空間和 hello 您的佇列名稱。 當您完成之後時，按一下 **儲存**hello 底部。
    
    ![新增端點][31]
    
4. 現在按一下 IoT 中樞中的 [路由]。 按一下**新增**頂端 hello hello 刀鋒視窗 toocreate 加入路由傳送訊息 toohello 佇列只路由規則。 選取**DeviceTelemetry** hello 的資料來源。 輸入`level="critical"`做為 hello 條件，然後選擇您剛才加入做為自訂的端點，如 hello 路由規則端點 hello 佇列。 當您完成之後時，按一下 **儲存**hello 底部。
    
    ![新增路由][32]
    
    請確定 hello 後援路由設定得**ON**。 此值為 hello IoT 中樞的預設組態。
    
    ![後援路由][33]

## <a name="read-from-hello-queue-endpoint"></a>讀取 hello 佇列端點

在本節中，您會從 hello 佇列端點讀取 hello 訊息。

1. 在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 toohello 目前方案，使用 hello**主控台應用程式 (.NET Framework)**專案範本。 名稱 hello 專案**ReadCriticalQueue**。

2. 在 [方案總管] 中，以滑鼠右鍵按一下 hello **ReadCriticalQueue**專案，然後再按一下**管理 NuGet 封裝**。 這項作業會顯示 hello **NuGet 套件管理員**視窗。

3. 搜尋**WindowsAzure.ServiceBus**，按一下 **安裝**，並接受使用規定 hello。 這項作業會下載、 安裝，並新增參考 toohello Azure 服務匯流排，所有相依性。

4. 新增下列 hello**使用**在 hello hello 最上方的陳述式**Program.cs**檔案：
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. 最後，加入下列行 toohello hello **Main**方法。 取代連接字串 hello**接聽**hello 佇列的權限：
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C tooexit.\n");
    var connectionString = "{service bus listen string}";
    var queueName = "{queue name}";
    
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);

    client.OnMessage(message =>
        {
            Stream stream = message.GetBody<Stream>();
            StreamReader reader = new StreamReader(stream, Encoding.ASCII);
            string s = reader.ReadToEnd();
            Console.WriteLine(String.Format("Message body: {0}", s));
        });
        
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a>執行 hello 應用程式
現在您已準備好 toorun hello 應用程式。

1. 在 Visual Studio 的方案總管中，以滑鼠右鍵按一下您的方案，然後選取 [設定啟始專案]。 選取**多個啟始專案**，然後選取**啟動**hello hello 動作**ReadDeviceToCloudMessages**， **SimulatedDevice**，和**ReadCriticalQueue**專案。
2. 按**F5** toostart hello 三個主控台應用程式。 hello **ReadDeviceToCloudMessages**應用程式必須僅非重大訊息寄件者 hello **SimulatedDevice**應用程式，以及 hello **ReadCriticalQueue**只剩應用程式重要訊息。
   
   ![三個主控台應用程式][50]

## <a name="next-steps"></a>後續步驟
在本教學課程中，您學會如何 tooreliably 裝置到雲端訊息分派使用 IoT 中樞的 hello 訊息路由功能。

hello [toosend 雲端到裝置與 IoT 中樞的訊息][ lnk-c2d]顯示 toosend 訊息從您的方案後端 tooyour 裝置的方式。

完整的端對端解決方案使用 IoT 中樞 toosee 範例請參閱[Azure IoT 套件][lnk-suite]。

toolearn 進一步了解開發與 IoT 中樞的解決方案，請參閱 「 hello [IoT 中樞開發人員指南]。

請參閱詳細訊息路由在 IoT 中樞 toolearn[傳送和接收訊息與 IoT 中樞][lnk-devguide-messaging]。

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[Azure 儲存體]: https://azure.microsoft.com/documentation/services/storage/
[Azure 服務匯流排]: https://azure.microsoft.com/documentation/services/service-bus/
[IoT 中樞開發人員指南]: iot-hub-devguide.md
[開始使用 IoT 中樞]: iot-hub-csharp-csharp-getstarted.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[Azure IoT 開發人員中心]: https://azure.microsoft.com/develop/iot
[暫時性錯誤處理]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
