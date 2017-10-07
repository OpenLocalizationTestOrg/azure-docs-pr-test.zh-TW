---
title: "監視 aaaAzure IoT 中樞作業 |Microsoft 文件"
description: "如何監視 toomonitor toouse Azure IoT 中樞作業 hello 您即時的 IoT 中樞上的作業狀態。"
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a299f3a5-b14d-4586-9c3b-44aea14ed013
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.openlocfilehash: a0b233ef2d9bd0827e19fa30fdbdd49b2b61b813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-operations-monitoring"></a>IoT 中樞作業監視

IoT 中樞作業監視可讓您即時您 IoT 中樞上的作業 toomonitor hello 狀態。 IoT 中樞可追蹤橫跨數個作業類別的事件。 您可以選擇從您的 IoT 中樞進行處理的一或多個類別 tooan 端點傳送的事件。 您可以監視有錯誤的 hello 資料或設定根據資料模式更複雜的處理。

IoT 中樞會監視六個類別的事件：

* 裝置身分識別作業
* 裝置遙測
* 雲端到裝置的訊息
* 連線
* 檔案上傳
* 訊息路由

## <a name="how-tooenable-operations-monitoring"></a>如何 tooenable 作業監視

1. 建立 IoT 中樞。 您可以找到指示如何 toocreate hello IoT 中樞[開始][ lnk-get-started]指南。

1. 開啟您的 IoT 中樞的 hello 刀鋒視窗。 按一下其中的 [作業監視] 。

    ![監視 hello 入口網站中的設定的存取作業][1]

1. 監視您希望 toomonitor，，然後按一下類別目錄選取 hello**儲存**。 hello 事件可用來讀取 hello 事件中樞相容端點中所列**監視設定**。 hello IoT 中樞端點稱為`messages/operationsmonitoringevents`。

    ![在 IoT 中樞上設定作業監視][2]

> [!NOTE]
> 選取**Verbose**監視 hello**連線**類別目錄會造成 IoT 中樞 toogenerate 額外的診斷訊息。 對於所有其他分類，hello **Verbose** hello 數量資訊 IoT 中樞設定變更包含在每個錯誤訊息。

## <a name="event-categories-and-how-toouse-them"></a>事件類別目錄以及 toouse 它們

每個作業監視類別會各自追蹤與 IoT 中樞所進行的不同類型的互動，而每一個監視類別都有結構描述來定義該類別的事件要如何構成。

### <a name="device-identity-operations"></a>裝置身分識別作業

hello 裝置識別作業類別目錄會追蹤您嘗試 toocreate 時，發生錯誤、 更新或刪除您的 IoT 中樞身分識別登錄中的項目。 佈建案例就很適合追蹤此類別。

```json
{
    "time": "UTC timestamp",
        "operationName": "create",
        "category": "DeviceIdentityOperations",
        "level": "Error",
        "statusCode": 4XX,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "durationMs": 1234,
        "userAgent": "userAgent",
        "sharedAccessPolicy": "accessPolicy"
}
```

### <a name="device-telemetry"></a>裝置遙測

hello 裝置遙測類別會追蹤錯誤發生在 hello IoT 中樞，而且相關的 toohello 遙測管線。 此類別包括在傳送遙測事件 (例如節流) 和接收遙測事件 (例如未經授權的讀取器) 時所發生的錯誤。 此類別無法攔截 hello 裝置本身上執行的程式碼所造成的錯誤。

```json
{
        "messageSizeInBytes": 1234,
        "batching": 0,
        "protocol": "Amqp",
        "authType": "{\"scope\":\"device\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
        "time": "UTC timestamp",
        "operationName": "ingress",
        "category": "DeviceTelemetry",
        "level": "Error",
        "statusCode": 4XX,
        "statusType": 4XX001,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "EventProcessedUtcTime": "UTC timestamp",
        "PartitionId": 1,
        "EventEnqueuedUtcTime": "UTC timestamp"
}
```

### <a name="cloud-to-device-commands"></a>雲端到裝置的命令

hello 雲端到裝置命令類別會追蹤錯誤發生在 hello IoT 中樞，而且相關的 toohello 雲端到裝置訊息管線。 這個類別包括在傳送雲端到裝置訊息 (例如未經授權的寄件者)、接收雲端到裝置訊息 (例如超過傳遞計數) 和接收雲端到裝置訊息意見反應 (例如意見反應已過期) 時所發生的錯誤。 此類別不會攔截錯誤處理的雲端到裝置訊息如果 hello 雲端到裝置訊息已成功傳遞的裝置中的錯誤。

```json
{
    "messageSizeInBytes": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "deliveryAcknowledgement": 0,
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "C2DCommands",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "EventProcessedUtcTime": "UTC timestamp",
    "PartitionId": 1,
    "EventEnqueuedUtcTime": “UTC timestamp"
}
```

### <a name="connections"></a>連線

hello 連接類別目錄會追蹤裝置連線，或從 IoT 中樞中斷連線時，發生錯誤。 若想識別未經授權的連線嘗試，以及在連線品質不佳之區域內的裝置中斷連線時進行追蹤，就很適合追蹤此類別。

```json
{
    "durationMs": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "deviceConnect",
    "category": "Connections",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID"
}
```

### <a name="file-uploads"></a>檔案上傳

hello 檔案上傳類別會追蹤錯誤發生在 hello IoT 中樞，而且相關的 toofile 上傳功能。 此類別包括︰

* 以 hello SAS URI，例如過期之前裝置通知 hello 中樞的已完成上傳時所發生的錯誤。
* 無法上傳 hello 裝置所報告。
* IoT 中樞通知訊息建立期間在儲存體中找不到檔案時所發生的錯誤。

此類別無法攔截 hello 裝置上傳檔案 toostorage，直接時發生的錯誤。

```json
{
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "HTTP",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "fileUpload",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "blobUri": "http//bloburi.com",
    "durationMs": 1234
}
```

### <a name="message-routing"></a>訊息路由

hello 訊息路由類別會追蹤訊息路由評估與端點健全狀況觀察得到的 IoT 中樞期間發生的錯誤。 此類別包含事件，例如當規則評估太"未定義 」，當 IoT 中樞將標示端點為寄不出，並收到來自端點的其他錯誤。 此類別不包含有關 hello 訊息本身 （例如裝置節流錯誤），報告 hello 「 裝置遙測 」 類別下的特定錯誤。

```json
{
    "messageSizeInBytes": 1234,
    "time": "UTC timestamp",
    "operationName": "ingress",
    "category": "routes",
    "level": "Error",
    "deviceId": "device-ID",
    "messageId": "ID of message",
    "routeName": "myroute",
    "endpointName": "myendpoint",
    "details": "ExternalEndpointDisabled"
}
```

## <a name="view-events"></a>檢視事件

您可以使用 hello *iot 中樞總管*工具 tooquickly 測試您的 IoT 中樞產生監視的事件。 tooinstall hello 工具，請參閱 hello hello 指示[iot 中樞總管][ lnk-iothub-explorer] GitHub 儲存機制。

1. 請確定 hello**連線**監視類別設定太**Verbose** hello 入口網站中。

1. 在命令提示字元中執行 hello 監視端點中的下列命令 tooread hello:

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. 在另一個命令提示字元，執行下列命令 toosimulate hello 傳送裝置到雲端訊息的裝置：

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. hello 第一個命令提示字元會顯示 hello 監視事件 hello 模擬的裝置連線 tooyour IoT 中樞。

## <a name="connect-toohello-monitoring-endpoint"></a>連接 toohello 監視端點

hello 監視上 IoT 中樞端點是事件中樞相容端點。 您可以使用任何機制可搭配事件中心 tooread 監視郵件從這個端點。 hello 下列範例會建立基本的讀取器不是適用於高輸送量部署。 如需如何 tooprocess 訊息從事件中心的詳細資訊，請參閱 hello[開始使用事件中心][ lnk-eventhubs-tutorial]教學課程。

tooconnect toohello 監視端點，您需要的連接字串和 hello 端點的名稱。 hello 步驟會告訴您如何 toofind hello hello 入口網站中的必要值：

1. 在 [hello 入口網站中，瀏覽 tooyour IoT 中樞資源刀鋒視窗。

1. 選擇**作業監視**，並記下的 hello**事件中樞相容名稱**和**事件中樞相容端點**值：

    ![事件中樞相容端點值][img-endpoints]

1. 選擇 [共用存取原則]，然後選擇 [服務]。 請記下 hello**主索引鍵**值：

    ![服務共用存取原則主要金鑰][img-service-key]

hello 下列 C# 程式碼範例取自 Visual Studio**的傳統 Windows 桌面**C# 主控台應用程式。 hello 專案具有 hello **WindowsAzure.ServiceBus**安裝的 NuGet 套件。

* Hello 連接字串預留位置取代為連接字串使用 hello**事件中樞相容端點**和服務**主索引鍵**記下 hello 下列所示的先前值範例：

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* 取代 hello 監視端點名稱預留位置 hello**事件中樞相容名稱**先前所述的值。

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key tooexit.\n");

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, monitoringEndpointName);
        var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;
        CancellationTokenSource cts = new CancellationTokenSource();
        var tasks = new List<Task>();

        foreach (string partition in d2cPartitions)
        {
            tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
        }

        Console.ReadLine();
        Console.WriteLine("Exiting...");
        cts.Cancel();
        Task.WaitAll(tasks.ToArray());
    }

    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested)
            {
                await eventHubReceiver.CloseAsync();
                break;
            }

            EventData eventData = await eventHubReceiver.ReceiveAsync(new TimeSpan(0,0,10));

            if (eventData != null)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
            }
        }
    }
}
```

## <a name="next-steps"></a>後續步驟
toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

* [IoT 中樞開發人員指南][lnk-devguide]
* [使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]

<!-- Links and images -->
[1]: media/iot-hub-operations-monitoring/enable-OM-1.png
[2]: media/iot-hub-operations-monitoring/enable-OM-2.png
[img-endpoints]: media/iot-hub-operations-monitoring/monitoring-endpoint.png
[img-service-key]: media/iot-hub-operations-monitoring/service-key.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-diagnostic-metrics]: iot-hub-metrics.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer
[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md