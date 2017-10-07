---
title: "aaaNotification 中樞-企業發送架構"
description: "在企業環境中使用 Azure 通知中樞的指引"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 903023e9-9347-442a-924b-663af85e05c6
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c3afb83de1ba0882bf99e10f38cca40cb42d07a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-push-architectural-guidance"></a>企業推送架構指引
企業現在正逐漸建立行動應用程式的使用者 （外部） 或 hello 員工 （內部）。 他們擁有現有後端系統，將是大型主機，或者有些 LoB 應用程式必須整合至其 hello 行動應用程式架構。 本指南會討論如何最佳 toodo 這項整合 toocommon 案例建議可能的解決方案。

常見的需求是用於傳送推播通知 toohello 使用者透過他們的行動應用程式時 hello 後端系統中發生感興趣的事件。 例如 她的 iPhone 都有 hello 銀行銀行應用程式的銀行客戶想 toobe 高於特定從她的帳戶或內部網路案例，財務部門的員工在他的 Windows Phone 都有預算核准應用程式希望 toobe 進行付款時收到通知他取得核准要求時通知您。

hello 銀行帳戶或核准程序不可能 toobe 必須啟動推入 toohello 使用者的某些後端系統中完成。 可能有多個這類的後端事件觸發通知時，所有必須建置系統 hello 相同類型的邏輯 tooimplement 推入。 這裡 hello 複雜性在於整合數個後端系統，以及其中 hello 終端使用者可能已訂閱 toodifferent 通知，而且甚至可能是多個行動應用程式，例如在內部網路的行動裝置應用程式的 hello 案例中的單一發送系統其中一個行動裝置應用程式可能會想從多個這類的後端系統的 tooreceive 通知。 不知道 hello 後端系統或需要 tooknow 的推入語意技術，因此這裡的常見解決方案一直都 toointroduce 元件，輪詢 hello 後端系統的任何感興趣的事件，並負責傳送嗨推播訊息toohello 用戶端。
這裡我們將討論使用 Azure 服務匯流排主題/訂閱模型可減少 hello 複雜時可擴充 hello 方案甚至更好的解決方案。

以下是 hello 的 hello 方案的一般架構 （多個行動應用程式與通用但同樣適用於只有一個行動裝置應用程式時）

## <a name="architecture"></a>架構
![][1]

這個架構的圖表中的 hello 主要片段為 Azure 服務匯流排提供程式設計模型的主題/訂閱 (它在多個[服務匯流排 Pub/Sub 程式設計])。 hello 收件者，在此情況下，是 hello 行動後端 (通常[Azure 行動服務]，這會起始發送 toohello 行動裝置應用程式) 不會收到訊息直接 hello 後端系統但改為我們有所提供的中繼抽象層[Azure 服務匯流排]可讓行動後端 tooreceive 訊息從一個或多個後端系統。 服務匯流排主題需要 toobe 針對每個 hello 後端系統例如帳戶 HR、 財務基本上是 「 主題 」，這會起始訊息 toobe 傳送為推播通知感興趣的建立。 hello 後端系統會傳送訊息 toothese 主題。 行動裝置後端可以藉由建立 Service Bus 訂閱訂閱 tooone 或更多這類的主題。 這將贊成 hello 行動後端 tooreceive 來自 hello 對應的後端系統的通知。 行動後端會 toolisten 訊息繼續其訂用帳戶上，而且只要在訊息到達時，它會開啟上一步，並將它傳送為通知 tooits 通知中樞。 通知中樞時，然後最終傳送 hello 訊息 toohello 行動裝置應用程式。 因此 toosummarize hello 主要元件，我們有：

1. 後端系統 (LoB/舊版系統)
   * 建立服務匯流排主題
   * 傳送訊息
2. 行動後端
   * 建立服務訂閱
   * 接收訊息 (來自後端系統)
   * 傳送通知 tooclients （透過 Azure 通知中樞）
3. 行動應用程式
   * 接收及顯示通知

### <a name="benefits"></a>優點：
1. hello 接收者 （行動應用程式/透過通知中樞服務） 寄件者 （後端系統） 之間的去耦合 hello 可讓您少的變更要整合的其他後端系統。
2. 這也能讓多個行動應用程式正在從一或多個後端系統能夠 tooreceive 事件 hello 案例。  

## <a name="sample"></a>範例：
### <a name="prerequisites"></a>必要條件
您應該先完成下列與 hello 概念，以及一般的建立與組態步驟的教學課程 toofamiliarize hello:

1. [服務匯流排 Pub/Sub 程式設計]-這如何解釋 hello 詳細資料的使用與服務匯流排主題/訂閱 toocreate 命名空間 toocontain 主題/訂閱方式 toosend （& s) 從中接收訊息。
2. [通知中樞-Windows 通用的教學課程]-本節將說明如何 tooset Windows 市集應用程式和使用通知中樞 tooregister，然後接收通知。

### <a name="sample-code"></a>範例程式碼
hello 完整的範例程式碼將會位於[通知中樞範例]。 其可劃分為三個元件：

1. **EnterprisePushBackendSystem**
   
    a. 此專案使用 hello *WindowsAzure.ServiceBus* Nuget 封裝，並且根據[服務匯流排 Pub/Sub 程式設計]。
   
    b. 這是簡單 C# 主控台應用程式 toosimulate LoB 系統，後者再起始 hello 訊息 toobe 傳遞 toohello 行動裝置應用程式。
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    c. `CreateTopic`是使用的 toocreate hello Service Bus 主題，我們會傳送訊息。
   
        public static void CreateTopic(string connectionString)
        {
            // Create hello topic if it does not exist already
   
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.TopicExists(sampleTopic))
            {
                namespaceManager.CreateTopic(sampleTopic);
            }
        }
   
    d. `SendMessage`會使用的 toosend hello 訊息 toothis 服務匯流排主題。 這裡我們只會傳送一組隨機訊息 toohello 主題定期的 hello hello 範例的目的。 在一般情況下，我們會有在事件發生時傳送訊息的後端系統。
   
        public static void SendMessage(string connectionString)
        {
            TopicClient client =
                TopicClient.CreateFromConnectionString(connectionString, sampleTopic);
   
            // Sends random messages every 10 seconds toohello topic
            string[] messages =
            {
                "Employee Id '{0}' has joined.",
                "Employee Id '{0}' has left.",
                "Employee Id '{0}' has switched tooa different team."
            };
   
            while (true)
            {
                Random rnd = new Random();
                string employeeId = rnd.Next(10000, 99999).ToString();
                string notification = String.Format(messages[rnd.Next(0,messages.Length)], employeeId);
   
                // Send Notification
                BrokeredMessage message = new BrokeredMessage(notification);
                client.Send(message);
   
                Console.WriteLine("{0} Message sent - '{1}'", DateTime.Now, notification);
   
                System.Threading.Thread.Sleep(new TimeSpan(0, 0, 10));
            }
        }
2. **ReceiveAndSendNotification**
   
    a. 此專案使用 hello *WindowsAzure.ServiceBus*和*Microsoft.Web.WebJobs.Publish* Nuget 封裝，並且根據[服務匯流排 Pub/Sub 程式設計]。
   
    b. 這是另一個 C# 主控台應用程式，我們將會當做執行[Azure WebJob]因為它有連續 toorun toolisten 的訊息從 hello LoB/後端系統。 它將會是行動後端的一部分。
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    c. `CreateSubscription`是使用的 toocreate hello 主題的服務匯流排訂閱 hello 後端系統傳送訊息的位置。 根據 hello 的商務案例，此元件將會建立一個或多個訂閱 toocorresponding 主題 （例如某些可接收的訊息從 HR 系統中，有些來自財務系統等等）
   
        static void CreateSubscription(string connectionString)
        {
            // Create hello subscription if it does not exist already
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.SubscriptionExists(sampleTopic, sampleSubscription))
            {
                namespaceManager.CreateSubscription(sampleTopic, sampleSubscription);
            }
        }
   
    d. ReceiveMessageAndSendNotification 是透過使用其訂用帳戶的 hello 主題使用的 tooread hello 訊息，並成功讀取的 hello 時再製作 （在 Windows 原生快顯通知 hello 範例案例） 的通知傳送的 toobe toohello 行動使用 Azure 通知中樞應用程式。
   
        static void ReceiveMessageAndSendNotification(string connectionString)
        {
            // Initialize hello Notification Hub
            string hubConnectionString = CloudConfigurationManager.GetSetting
                    ("Microsoft.NotificationHub.ConnectionString");
            hub = NotificationHubClient.CreateClientFromConnectionString
                    (hubConnectionString, "enterprisepushservicehub");
   
            SubscriptionClient Client =
                SubscriptionClient.CreateFromConnectionString
                        (connectionString, sampleTopic, sampleSubscription);
   
            Client.Receive();
   
            // Continuously process messages received from hello subscription
            while (true)
            {
                BrokeredMessage message = Client.Receive();
                var toastMessage = @"<toast><visual><binding template=""ToastText01""><text id=""1"">{messagepayload}</text></binding></visual></toast>";
   
                if (message != null)
                {
                    try
                    {
                        Console.WriteLine(message.MessageId);
                        Console.WriteLine(message.SequenceNumber);
                        string messageBody = message.GetBody<string>();
                        Console.WriteLine("Body: " + messageBody + "\n");
   
                        toastMessage = toastMessage.Replace("{messagepayload}", messageBody);
                        SendNotificationAsync(toastMessage);
   
                        // Remove message from subscription
                        message.Complete();
                    }
                    catch (Exception)
                    {
                        // Indicate a problem, unlock message in subscription
                        message.Abandon();
                    }
                }
            }
        }
        static async void SendNotificationAsync(string message)
        {
            await hub.SendWindowsNativeNotificationAsync(message);
        }
   
    e. 發行為**WebJob**，Visual Studio 中的 hello 方案上按一下滑鼠右鍵，然後選取**發佈為 web 工作**
   
    ![][2]
   
    f. 選取您的發行設定檔，並建立新的 Azure 網站，如果不存在已經它將裝載此 WebJob 和一旦 hello 網站然後**發行**。
   
    ![][3]
   
    g. 設定 「 持續執行"hello 作業 toobe 時登入 toohello [Azure 傳統入口網站]您應該會看到類似下列 hello:
   
    ![][4]
3. **EnterprisePushMobileApp**
   
    a. 這是接收快顯通知的 hello WebJob 執行您的行動裝置後端的一部分，並顯示 Windows 市集應用程式。 其乃依據[通知中樞-Windows 通用的教學課程]。  
   
    b. 請確定您的應用程式啟用的 tooreceive 快顯通知。
   
    c. 請確定在 hello 應用程式啟動時呼叫該 hello 下列通知中樞註冊程式碼 (取代 hello 後*HubName*和*DefaultListenSharedAccessSignature*:
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("[HubName]", "[DefaultListenSharedAccessSignature]");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

### <a name="running-sample"></a>執行範例：
1. 確定您 WebJob 順利執行，並排程太 「 執行持續 」。
2. 執行 hello **EnterprisePushMobileApp**這會啟動 hello Windows 市集應用程式。
3. 執行 hello **EnterprisePushBackendSystem**主控台應用程式，會模擬 hello LoB 後端，便會開始傳送訊息，以及您應該會看到快顯通知出現 hello 如下：
   
    ![][5]
4. hello 訊息原始傳送 tooService 匯流排主題在受監視服務匯流排訂用帳戶中的 Web 工作。 一旦收到的訊息，通知所建立及傳送 toohello 行動裝置應用程式。 您可以查看 WebJob 記錄 tooconfirm hello 處理，當您移的 toohello 記錄檔中連結的 hello [Azure 傳統入口網站]Web 工作：
   
    ![][6]

<!-- Images -->
[1]: ./media/notification-hubs-enterprise-push-architecture/architecture.png
[2]: ./media/notification-hubs-enterprise-push-architecture/WebJobsContextMenu.png
[3]: ./media/notification-hubs-enterprise-push-architecture/PublishAsWebJob.png
[4]: ./media/notification-hubs-enterprise-push-architecture/WebJob.png
[5]: ./media/notification-hubs-enterprise-push-architecture/Notifications.png
[6]: ./media/notification-hubs-enterprise-push-architecture/WebJobsLog.png

<!-- Links -->
[通知中樞範例]: https://github.com/Azure/azure-notificationhubs-samples
[Azure 行動服務]: http://azure.microsoft.com/documentation/services/mobile-services/
[Azure 服務匯流排]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/
[服務匯流排 Pub/Sub 程式設計]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/
[Azure WebJob]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/
[通知中樞-Windows 通用的教學課程]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[Azure 傳統入口網站]: https://manage.windowsazure.com/
