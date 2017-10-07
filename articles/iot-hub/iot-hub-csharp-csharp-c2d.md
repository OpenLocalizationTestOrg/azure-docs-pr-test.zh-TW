---
title: "aaaCloud 到裝置訊息與 Azure IoT 中樞 (.NET) |Microsoft 文件"
description: "如何 toosend 雲端到裝置訊息 tooa 裝置使用 hello Azure IoT Sdk for.NET 的 Azure IoT 中樞。 您會修改裝置應用程式 tooreceive 雲端到裝置訊息，並修改後端應用程式 toosend hello 雲端到裝置訊息。"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: a31c05ed-6ec0-40f3-99ab-8fdd28b1a89a
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: f6a7618b164d95c8ddaf28943f244aeeb568217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="send-messages-from-hello-cloud-tooyour-device-with-iot-hub-net"></a>將訊息傳送 hello 雲端 tooyour 裝置與 IoT 中樞 (.NET)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a>簡介
Azure IoT 中樞是一項完全受管理的服務，有助於讓數百萬個裝置和一個解決方案後端進行可靠且安全的雙向通訊。 hello[開始使用 IoT 中樞]教學課程將說明如何 toocreate IoT 中樞，佈建裝置身分識別，並傳送裝置到雲端訊息的裝置應用程式的程式碼。

本教學課程是以 [開始使用 IoT 中樞]為基礎。 這會說明如何：

* 從您的方案後端，傳送到 IoT 中樞雲端到裝置訊息 tooa 單一裝置。
* 接收裝置上的雲端到裝置訊息。
* 從您的方案後端，要求傳遞通知 (*意見反應*) 的訊息傳送 tooa 裝置從 IoT 中樞。

您可以找到更多有關雲端到裝置訊息在 hello [IoT 中樞開發人員指南][IoT Hub developer guide - C2D]。

在本教學課程的 hello 最後，您可以執行兩個.NET 主控台應用程式：

* **SimulatedDevice**，hello 應用程式中建立的修改的版本[開始使用 IoT 中樞]，這會連接 tooyour IoT 中樞，並接收雲端到裝置訊息。
* **SendCloudToDevice**，這會傳送到 IoT 中樞雲端到裝置訊息 toohello 裝置應用程式，但收到其傳遞通知。

> [!NOTE]
> IoT 中樞會透過 [Azure IoT 裝置 SDK] 為許多裝置平台和語言 (包括 C、Java 及 Javascript) 提供 SDK 支援。 如需如何 tooconnect 裝置 toothis 教學課程的程式碼，以及通常 tooAzure IoT 中樞，請參閱逐步指示 hello [IoT 中樞開發人員指南]。
> 
> 

toocomplete 本教學課程中，您需要遵循的 hello:

* Visual Studio 2015 或 Visual Studio 2017
* 使用中的 Azure 帳戶。 (如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)

## <a name="receive-messages-in-hello-device-app"></a>在 hello 裝置應用程式中接收訊息
在本節中，您將修改 hello 裝置應用程式中建立[開始使用 IoT 中樞]tooreceive 雲端到裝置訊息從 hello IoT 中樞。

1. 在 Visual Studio，在 hello **SimulatedDevice**專案中，加入下列方法 toohello hello**程式**類別。
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud toodevice messages from service");
            while (true)
            {
                Message receivedMessage = await deviceClient.ReceiveAsync();
                if (receivedMessage == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received message: {0}", Encoding.ASCII.GetString(receivedMessage.GetBytes()));
                Console.ResetColor();
   
                await deviceClient.CompleteAsync(receivedMessage);
            }
        }
   
    hello`ReceiveAsync`方法以非同步方式在收到 hello 裝置 hello 時間傳回收到 hello 訊息。 它會傳回*null*可逾時期間之後 （在此情況下，會使用 hello 預設值是一分鐘）。 當收到 hello 應用程式*null*，則應繼續 toowait 新郵件。 這項需求是 hello hello 原因`if (receivedMessage == null) continue`列。
   
    太 hello 呼叫`CompleteAsync()`通知 IoT 中樞 hello 訊息已成功處理。 hello 訊息可以安全地移除 hello 裝置佇列。 如果發生無法完成處理 hello hello 訊息，予以防止的 hello 裝置應用程式，IoT 中樞將其傳遞一次。 然後是很重要的訊息處理 hello 裝置應用程式中的邏輯*等冪*，以便接收的 hello 會產生相同的訊息多次 hello 相同的結果。 應用程式也會暫時可以放棄的訊息，導致 IoT 中心保留供未來取用的 hello 佇列中的 hello 訊息。 或者，hello 應用程式可以拒絕的訊息，永久移除 hello 佇列中的 hello 訊息。 如需 hello 雲端到裝置訊息生命週期的詳細資訊，請參閱 hello [IoT 中樞開發人員指南][IoT Hub developer guide - C2D]。
   
   > [!NOTE]
   > 當使用 HTTP 而非 MQTT 或 AMQP 做為傳輸，hello`ReceiveAsync`方法會立即傳回。 雲端到裝置訊息的 HTTP 支援的 hello 模式是不常訊息 （小於每隔 25 分鐘） 檢查間斷連接的裝置。 發行多個 HTTP 接收 IoT 中樞節流 hello 要求中的結果。 如需 MQTT、 AMQP 和 HTTP 支援與 IoT 中樞節流的 hello 差異的詳細資訊，請參閱 hello [IoT 中樞開發人員指南][IoT Hub developer guide - C2D]。
   > 
   > 
2. 新增下列方法在 hello hello **Main**方法中的前 hello,`Console.ReadLine()`行：
   
        ReceiveC2dAsync();

> [!NOTE]
> 為了簡單起見，本教學課程不會實作任何重試原則。 在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理]。
> 
> 

## <a name="send-a-cloud-to-device-message"></a>傳送雲端到裝置訊息
在本節中，您可以撰寫.NET 主控台應用程式中傳送雲端到裝置訊息 toohello 裝置應用程式。

1. Hello 目前 Visual Studio 方案中建立 Visual C# 桌面應用程式專案使用 hello**主控台應用程式**專案範本。 名稱 hello 專案**SendCloudToDevice**。
   
    ![Visual Studio 中的新專案][20]
2. 在 方案總管 hello 方案上按一下滑鼠右鍵，然後按一下**管理方案的 NuGet 套件...**. 
   
    這個動作會開啟 hello**管理 NuGet 封裝**視窗。
3. 搜尋**Microsoft.Azure.Devices**，按一下 **安裝**，並接受使用規定 hello。 
   
    此下載、 安裝，並新增參考 toohello [Azure IoT 服務 SDK 的 NuGet 封裝]。

4. 新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：
   
        using Microsoft.Azure.Devices;
5. 新增下列欄位 toohello hello**程式**類別。 替代 hello 預留位置的值與 hello IoT 中樞連接字串從[開始使用 IoT 中樞]:
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. 新增下列方法 toohello hello**程式**類別：
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud toodevice message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    這個方法會傳送新的雲端到裝置訊息 toohello 裝置 hello 識別碼`myFirstDevice`。 變更此參數只有當您修改過它從一個用於 hello[開始使用 IoT 中樞]。
7. 最後，加入下列行 toohello hello **Main**方法：
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key toosend a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. 從 Visual Studio 中，在您的方案上按一下滑鼠右鍵，然後選取 [設定啟始專案...]。選取**多個啟始專案**，然後選取 hello**啟動**動作**ReadDeviceToCloudMessages**， **SimulatedDevice**，和**SendCloudToDevice**。
9. 按 **F5**。 三個應用程式應該全部都會啟動。 選取 hello **SendCloudToDevice**視窗，然後按**Enter**。 您應該會看到所接收的 hello 裝置應用程式的 hello 訊息。
   
   ![正在接收訊息的應用程式][21]

## <a name="receive-delivery-feedback"></a>接收傳遞意見反應
很可能 toorequest 傳遞 （或到期） 通知從 IoT 中樞的每個雲端到裝置的訊息。 此選項可讓 hello 方案後端 tooeasily 通知重試或補償邏輯。 如需有關雲端到裝置的意見反應的詳細資訊，請參閱 hello [IoT 中樞開發人員指南][IoT Hub developer guide - C2D]。

在本節中，您將修改 hello **SendCloudToDevice**應用程式 toorequest 意見反應，並接收來自 IoT 中樞。

1. 在 Visual Studio，在 hello **SendCloudToDevice**專案中，加入下列方法 toohello hello**程式**類別。
   
        private async static void ReceiveFeedbackAsync()
        {
            var feedbackReceiver = serviceClient.GetFeedbackReceiver();
   
            Console.WriteLine("\nReceiving c2d feedback from service");
            while (true)
            {
                var feedbackBatch = await feedbackReceiver.ReceiveAsync();
                if (feedbackBatch == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received feedback: {0}", string.Join(", ", feedbackBatch.Records.Select(f => f.StatusCode)));
                Console.ResetColor();
   
                await feedbackReceiver.CompleteAsync(feedbackBatch);
            }
        }
   
    請注意此接收模式是 hello hello 裝置應用程式來自相同一個使用的 tooreceive 雲端到裝置訊息。
2. 新增下列方法在 hello hello **Main**方法，在完成後立即 hello`serviceClient = ServiceClient.CreateFromConnectionString(connectionString)`行：
   
        ReceiveFeedbackAsync();
3. hello 雲端到裝置訊息傳遞的 toorequest 意見反應，您在 toospecify 屬性 hello **SendCloudToDeviceMessageAsync**方法。 新增下列一行，權限之後 hello hello`var commandMessage = new Message(...);`行：
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. 執行 hello 應用程式按**F5**。 您應該會看到三個應用程式全部都啟動。 選取 hello **SendCloudToDevice**視窗，然後按**Enter**。 您應該會看見 hello 訊息所收到 hello 裝置的應用程式，並於幾秒後，hello 所接收的回應訊息您**SendCloudToDevice**應用程式。
   
   ![正在接收訊息的應用程式][22]

> [!NOTE]
> 為了簡單起見，本教學課程不會實作任何重試原則。 在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理]。
> 
> 

## <a name="next-steps"></a>後續步驟
在本教學課程中，您學到如何 toosend 和接收雲端到裝置訊息。 

完整的端對端解決方案使用 IoT 中樞 toosee 範例請參閱[Azure IoT 套件]。

toolearn 進一步了解開發與 IoT 中樞的解決方案，請參閱 「 hello [IoT 中樞開發人員指南]。

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[Azure IoT 服務 SDK 的 NuGet 封裝]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[暫時性錯誤處理]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[IoT 中樞開發人員指南]: iot-hub-devguide.md
[開始使用 IoT 中樞]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure IoT 套件]: https://docs.microsoft.com/en-us/azure/iot-suite/
[Azure IoT 裝置 SDK]: iot-hub-devguide-sdks.md