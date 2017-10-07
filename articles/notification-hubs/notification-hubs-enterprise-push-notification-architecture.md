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
# <a name="enterprise-push-architectural-guidance"></a><span data-ttu-id="12fe2-103">企業推送架構指引</span><span class="sxs-lookup"><span data-stu-id="12fe2-103">Enterprise push architectural guidance</span></span>
<span data-ttu-id="12fe2-104">企業現在正逐漸建立行動應用程式的使用者 （外部） 或 hello 員工 （內部）。</span><span class="sxs-lookup"><span data-stu-id="12fe2-104">Enterprises today are gradually moving towards creating mobile applications for either their end users (external) or for hello employees (internal).</span></span> <span data-ttu-id="12fe2-105">他們擁有現有後端系統，將是大型主機，或者有些 LoB 應用程式必須整合至其 hello 行動應用程式架構。</span><span class="sxs-lookup"><span data-stu-id="12fe2-105">They have existing backend systems in place be it mainframes or some LoB applications which must be integrated into hello mobile application architecture.</span></span> <span data-ttu-id="12fe2-106">本指南會討論如何最佳 toodo 這項整合 toocommon 案例建議可能的解決方案。</span><span class="sxs-lookup"><span data-stu-id="12fe2-106">This guide will talk about how best toodo this integration recommending possible solution toocommon scenarios.</span></span>

<span data-ttu-id="12fe2-107">常見的需求是用於傳送推播通知 toohello 使用者透過他們的行動應用程式時 hello 後端系統中發生感興趣的事件。</span><span class="sxs-lookup"><span data-stu-id="12fe2-107">A frequent requirement is for sending push notification toohello users through their mobile application when an event of interest occurs in hello backend systems.</span></span> <span data-ttu-id="12fe2-108">例如</span><span class="sxs-lookup"><span data-stu-id="12fe2-108">E.g.</span></span> <span data-ttu-id="12fe2-109">她的 iPhone 都有 hello 銀行銀行應用程式的銀行客戶想 toobe 高於特定從她的帳戶或內部網路案例，財務部門的員工在他的 Windows Phone 都有預算核准應用程式希望 toobe 進行付款時收到通知他取得核准要求時通知您。</span><span class="sxs-lookup"><span data-stu-id="12fe2-109">a bank customer who has hello bank's banking app on her iPhone wants toobe notified when a debit is made above a certain amount from her account or an intranet scenario where an employee from finance department who has a budget approval app on his Windows Phone wants toobe notified when he gets an approval request.</span></span>

<span data-ttu-id="12fe2-110">hello 銀行帳戶或核准程序不可能 toobe 必須啟動推入 toohello 使用者的某些後端系統中完成。</span><span class="sxs-lookup"><span data-stu-id="12fe2-110">hello bank account or approval processing is likely toobe done in some backend system which must initiate a push toohello user.</span></span> <span data-ttu-id="12fe2-111">可能有多個這類的後端事件觸發通知時，所有必須建置系統 hello 相同類型的邏輯 tooimplement 推入。</span><span class="sxs-lookup"><span data-stu-id="12fe2-111">There may be multiple such backend systems which must all build hello same kind of logic tooimplement push when an event triggers a notification.</span></span> <span data-ttu-id="12fe2-112">這裡 hello 複雜性在於整合數個後端系統，以及其中 hello 終端使用者可能已訂閱 toodifferent 通知，而且甚至可能是多個行動應用程式，例如在內部網路的行動裝置應用程式的 hello 案例中的單一發送系統其中一個行動裝置應用程式可能會想從多個這類的後端系統的 tooreceive 通知。</span><span class="sxs-lookup"><span data-stu-id="12fe2-112">hello complexity here lies in integrating several backend systems together with a single push system where hello end users may have subscribed toodifferent notifications and there may even be multiple mobile applications e.g. in hello case of intranet mobile apps where one mobile application may want tooreceive notifications from multiple such backend systems.</span></span> <span data-ttu-id="12fe2-113">不知道 hello 後端系統或需要 tooknow 的推入語意技術，因此這裡的常見解決方案一直都 toointroduce 元件，輪詢 hello 後端系統的任何感興趣的事件，並負責傳送嗨推播訊息toohello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="12fe2-113">hello backend systems do not know or need tooknow of push semantics/technology so a common solution here traditionally has been toointroduce a component which polls hello backend systems for any events of interest and is responsible for sending hello push messages toohello client.</span></span>
<span data-ttu-id="12fe2-114">這裡我們將討論使用 Azure 服務匯流排主題/訂閱模型可減少 hello 複雜時可擴充 hello 方案甚至更好的解決方案。</span><span class="sxs-lookup"><span data-stu-id="12fe2-114">Here we will talk about an even better solution using Azure Service Bus - Topic/Subscription model which will reduce hello complexity while making hello solution scalable.</span></span>

<span data-ttu-id="12fe2-115">以下是 hello 的 hello 方案的一般架構 （多個行動應用程式與通用但同樣適用於只有一個行動裝置應用程式時）</span><span class="sxs-lookup"><span data-stu-id="12fe2-115">Here is hello general architecture of hello solution (generalized with multiple mobile apps but equally applicable when there is only one mobile app)</span></span>

## <a name="architecture"></a><span data-ttu-id="12fe2-116">架構</span><span class="sxs-lookup"><span data-stu-id="12fe2-116">Architecture</span></span>
![][1]

<span data-ttu-id="12fe2-117">這個架構的圖表中的 hello 主要片段為 Azure 服務匯流排提供程式設計模型的主題/訂閱 (它在多個[服務匯流排 Pub/Sub 程式設計])。</span><span class="sxs-lookup"><span data-stu-id="12fe2-117">hello key piece in this architectural diagram is Azure Service Bus which provides a topics/subscriptions programming model (more on it at [Service Bus Pub/Sub programming]).</span></span> <span data-ttu-id="12fe2-118">hello 收件者，在此情況下，是 hello 行動後端 (通常[Azure 行動服務]，這會起始發送 toohello 行動裝置應用程式) 不會收到訊息直接 hello 後端系統但改為我們有所提供的中繼抽象層[Azure 服務匯流排]可讓行動後端 tooreceive 訊息從一個或多個後端系統。</span><span class="sxs-lookup"><span data-stu-id="12fe2-118">hello receiver, which in this case, is hello Mobile backend (typically [Azure Mobile Service], which will initiate a push toohello mobile apps) does not receive messages directly from hello backend systems but instead we have an intermediate abstraction layer provided by [Azure Service Bus] which enables mobile backend tooreceive messages from one or more backend systems.</span></span> <span data-ttu-id="12fe2-119">服務匯流排主題需要 toobe 針對每個 hello 後端系統例如帳戶 HR、 財務基本上是 「 主題 」，這會起始訊息 toobe 傳送為推播通知感興趣的建立。</span><span class="sxs-lookup"><span data-stu-id="12fe2-119">A Service Bus Topic needs toobe created for each of hello backend systems e.g. Account, HR, Finance which are basically "topics" of interest which will initiate messages toobe sent as push notification.</span></span> <span data-ttu-id="12fe2-120">hello 後端系統會傳送訊息 toothese 主題。</span><span class="sxs-lookup"><span data-stu-id="12fe2-120">hello backend systems will send messages toothese topics.</span></span> <span data-ttu-id="12fe2-121">行動裝置後端可以藉由建立 Service Bus 訂閱訂閱 tooone 或更多這類的主題。</span><span class="sxs-lookup"><span data-stu-id="12fe2-121">A Mobile Backend can subscribe tooone or more such topics by creating a Service Bus subscription.</span></span> <span data-ttu-id="12fe2-122">這將贊成 hello 行動後端 tooreceive 來自 hello 對應的後端系統的通知。</span><span class="sxs-lookup"><span data-stu-id="12fe2-122">This will entitle hello mobile backend tooreceive a notification from hello corresponding backend system.</span></span> <span data-ttu-id="12fe2-123">行動後端會 toolisten 訊息繼續其訂用帳戶上，而且只要在訊息到達時，它會開啟上一步，並將它傳送為通知 tooits 通知中樞。</span><span class="sxs-lookup"><span data-stu-id="12fe2-123">Mobile backend continues toolisten for messages on their subscriptions and as soon as a message arrives, it turns back and sends it as notification tooits notification hub.</span></span> <span data-ttu-id="12fe2-124">通知中樞時，然後最終傳送 hello 訊息 toohello 行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="12fe2-124">Notification hubs then eventually delivers hello message toohello mobile app.</span></span> <span data-ttu-id="12fe2-125">因此 toosummarize hello 主要元件，我們有：</span><span class="sxs-lookup"><span data-stu-id="12fe2-125">So toosummarize hello key components, we have:</span></span>

1. <span data-ttu-id="12fe2-126">後端系統 (LoB/舊版系統)</span><span class="sxs-lookup"><span data-stu-id="12fe2-126">Backend systems (LoB/Legacy systems)</span></span>
   * <span data-ttu-id="12fe2-127">建立服務匯流排主題</span><span class="sxs-lookup"><span data-stu-id="12fe2-127">Creates Service Bus Topic</span></span>
   * <span data-ttu-id="12fe2-128">傳送訊息</span><span class="sxs-lookup"><span data-stu-id="12fe2-128">Sends Message</span></span>
2. <span data-ttu-id="12fe2-129">行動後端</span><span class="sxs-lookup"><span data-stu-id="12fe2-129">Mobile backend</span></span>
   * <span data-ttu-id="12fe2-130">建立服務訂閱</span><span class="sxs-lookup"><span data-stu-id="12fe2-130">Creates Service Subscription</span></span>
   * <span data-ttu-id="12fe2-131">接收訊息 (來自後端系統)</span><span class="sxs-lookup"><span data-stu-id="12fe2-131">Receives Message (from Backend system)</span></span>
   * <span data-ttu-id="12fe2-132">傳送通知 tooclients （透過 Azure 通知中樞）</span><span class="sxs-lookup"><span data-stu-id="12fe2-132">Sends notification tooclients (via Azure Notification Hub)</span></span>
3. <span data-ttu-id="12fe2-133">行動應用程式</span><span class="sxs-lookup"><span data-stu-id="12fe2-133">Mobile Application</span></span>
   * <span data-ttu-id="12fe2-134">接收及顯示通知</span><span class="sxs-lookup"><span data-stu-id="12fe2-134">Receives and display notification</span></span>

### <a name="benefits"></a><span data-ttu-id="12fe2-135">優點：</span><span class="sxs-lookup"><span data-stu-id="12fe2-135">Benefits:</span></span>
1. <span data-ttu-id="12fe2-136">hello 接收者 （行動應用程式/透過通知中樞服務） 寄件者 （後端系統） 之間的去耦合 hello 可讓您少的變更要整合的其他後端系統。</span><span class="sxs-lookup"><span data-stu-id="12fe2-136">hello decoupling between hello receiver (mobile app/service via Notification Hub) and sender (backend systems) enables additional backend systems being integrated with minimal change.</span></span>
2. <span data-ttu-id="12fe2-137">這也能讓多個行動應用程式正在從一或多個後端系統能夠 tooreceive 事件 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="12fe2-137">This also makes hello scenario of multiple mobile apps being able tooreceive events from one or more backend systems.</span></span>  

## <a name="sample"></a><span data-ttu-id="12fe2-138">範例：</span><span class="sxs-lookup"><span data-stu-id="12fe2-138">Sample:</span></span>
### <a name="prerequisites"></a><span data-ttu-id="12fe2-139">必要條件</span><span class="sxs-lookup"><span data-stu-id="12fe2-139">Prerequisites</span></span>
<span data-ttu-id="12fe2-140">您應該先完成下列與 hello 概念，以及一般的建立與組態步驟的教學課程 toofamiliarize hello:</span><span class="sxs-lookup"><span data-stu-id="12fe2-140">You should complete hello following tutorials toofamiliarize with hello concepts as well as common creation & configuration steps:</span></span>

1. <span data-ttu-id="12fe2-141">[服務匯流排 Pub/Sub 程式設計]-這如何解釋 hello 詳細資料的使用與服務匯流排主題/訂閱 toocreate 命名空間 toocontain 主題/訂閱方式 toosend （& s) 從中接收訊息。</span><span class="sxs-lookup"><span data-stu-id="12fe2-141">[Service Bus Pub/Sub programming] - This explains hello details of working with Service Bus Topics/Subscriptions, how toocreate a namespace toocontain topics/subscriptions, how toosend & receive messages from them.</span></span>
2. <span data-ttu-id="12fe2-142">[通知中樞-Windows 通用的教學課程]-本節將說明如何 tooset Windows 市集應用程式和使用通知中樞 tooregister，然後接收通知。</span><span class="sxs-lookup"><span data-stu-id="12fe2-142">[Notification Hubs - Windows Universal tutorial] - This explains how tooset up a Windows Store app and use Notification Hubs tooregister and then receive notifications.</span></span>

### <a name="sample-code"></a><span data-ttu-id="12fe2-143">範例程式碼</span><span class="sxs-lookup"><span data-stu-id="12fe2-143">Sample code</span></span>
<span data-ttu-id="12fe2-144">hello 完整的範例程式碼將會位於[通知中樞範例]。</span><span class="sxs-lookup"><span data-stu-id="12fe2-144">hello full sample code is available at [Notification Hub Samples].</span></span> <span data-ttu-id="12fe2-145">其可劃分為三個元件：</span><span class="sxs-lookup"><span data-stu-id="12fe2-145">It is split into three components:</span></span>

1. <span data-ttu-id="12fe2-146">**EnterprisePushBackendSystem**</span><span class="sxs-lookup"><span data-stu-id="12fe2-146">**EnterprisePushBackendSystem**</span></span>
   
    <span data-ttu-id="12fe2-147">a.</span><span class="sxs-lookup"><span data-stu-id="12fe2-147">a.</span></span> <span data-ttu-id="12fe2-148">此專案使用 hello *WindowsAzure.ServiceBus* Nuget 封裝，並且根據[服務匯流排 Pub/Sub 程式設計]。</span><span class="sxs-lookup"><span data-stu-id="12fe2-148">This project uses hello *WindowsAzure.ServiceBus* Nuget package and is  based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="12fe2-149">b.</span><span class="sxs-lookup"><span data-stu-id="12fe2-149">b.</span></span> <span data-ttu-id="12fe2-150">這是簡單 C# 主控台應用程式 toosimulate LoB 系統，後者再起始 hello 訊息 toobe 傳遞 toohello 行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="12fe2-150">This is a simple C# console app toosimulate an LoB system which initiates hello message toobe delivered toohello mobile app.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    <span data-ttu-id="12fe2-151">c.</span><span class="sxs-lookup"><span data-stu-id="12fe2-151">c.</span></span> <span data-ttu-id="12fe2-152">`CreateTopic`是使用的 toocreate hello Service Bus 主題，我們會傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="12fe2-152">`CreateTopic` is used toocreate hello Service Bus topic where we will send messages.</span></span>
   
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
   
    <span data-ttu-id="12fe2-153">d.</span><span class="sxs-lookup"><span data-stu-id="12fe2-153">d.</span></span> <span data-ttu-id="12fe2-154">`SendMessage`會使用的 toosend hello 訊息 toothis 服務匯流排主題。</span><span class="sxs-lookup"><span data-stu-id="12fe2-154">`SendMessage` is used toosend hello messages toothis Service Bus Topic.</span></span> <span data-ttu-id="12fe2-155">這裡我們只會傳送一組隨機訊息 toohello 主題定期的 hello hello 範例的目的。</span><span class="sxs-lookup"><span data-stu-id="12fe2-155">Here we are simply sending a set of random messages toohello topic periodically for hello purpose of hello sample.</span></span> <span data-ttu-id="12fe2-156">在一般情況下，我們會有在事件發生時傳送訊息的後端系統。</span><span class="sxs-lookup"><span data-stu-id="12fe2-156">Normally there will be a backend system which will send messages when an event occurs.</span></span>
   
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
2. <span data-ttu-id="12fe2-157">**ReceiveAndSendNotification**</span><span class="sxs-lookup"><span data-stu-id="12fe2-157">**ReceiveAndSendNotification**</span></span>
   
    <span data-ttu-id="12fe2-158">a.</span><span class="sxs-lookup"><span data-stu-id="12fe2-158">a.</span></span> <span data-ttu-id="12fe2-159">此專案使用 hello *WindowsAzure.ServiceBus*和*Microsoft.Web.WebJobs.Publish* Nuget 封裝，並且根據[服務匯流排 Pub/Sub 程式設計]。</span><span class="sxs-lookup"><span data-stu-id="12fe2-159">This project uses hello *WindowsAzure.ServiceBus* and *Microsoft.Web.WebJobs.Publish* Nuget packages and is based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="12fe2-160">b.</span><span class="sxs-lookup"><span data-stu-id="12fe2-160">b.</span></span> <span data-ttu-id="12fe2-161">這是另一個 C# 主控台應用程式，我們將會當做執行[Azure WebJob]因為它有連續 toorun toolisten 的訊息從 hello LoB/後端系統。</span><span class="sxs-lookup"><span data-stu-id="12fe2-161">This is another C# console app which we will run as an [Azure WebJob] since it has toorun continuously toolisten for messages from hello LoB/backend systems.</span></span> <span data-ttu-id="12fe2-162">它將會是行動後端的一部分。</span><span class="sxs-lookup"><span data-stu-id="12fe2-162">This will be part of your Mobile backend.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    <span data-ttu-id="12fe2-163">c.</span><span class="sxs-lookup"><span data-stu-id="12fe2-163">c.</span></span> <span data-ttu-id="12fe2-164">`CreateSubscription`是使用的 toocreate hello 主題的服務匯流排訂閱 hello 後端系統傳送訊息的位置。</span><span class="sxs-lookup"><span data-stu-id="12fe2-164">`CreateSubscription` is used toocreate a Service Bus subscription for hello topic where hello backend system will send messages.</span></span> <span data-ttu-id="12fe2-165">根據 hello 的商務案例，此元件將會建立一個或多個訂閱 toocorresponding 主題 （例如某些可接收的訊息從 HR 系統中，有些來自財務系統等等）</span><span class="sxs-lookup"><span data-stu-id="12fe2-165">Depending on hello business scenario, this component will create one or more subscriptions toocorresponding topics (e.g. some may be receiving messages from HR system, some from Finance system, and so on)</span></span>
   
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
   
    <span data-ttu-id="12fe2-166">d.</span><span class="sxs-lookup"><span data-stu-id="12fe2-166">d.</span></span> <span data-ttu-id="12fe2-167">ReceiveMessageAndSendNotification 是透過使用其訂用帳戶的 hello 主題使用的 tooread hello 訊息，並成功讀取的 hello 時再製作 （在 Windows 原生快顯通知 hello 範例案例） 的通知傳送的 toobe toohello 行動使用 Azure 通知中樞應用程式。</span><span class="sxs-lookup"><span data-stu-id="12fe2-167">ReceiveMessageAndSendNotification is used tooread hello message from hello topic using its subscription and if hello read is successful then craft a notification (in hello sample scenario a Windows native toast notification) toobe sent toohello mobile application using Azure Notification Hubs.</span></span>
   
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
   
    <span data-ttu-id="12fe2-168">e.</span><span class="sxs-lookup"><span data-stu-id="12fe2-168">e.</span></span> <span data-ttu-id="12fe2-169">發行為**WebJob**，Visual Studio 中的 hello 方案上按一下滑鼠右鍵，然後選取**發佈為 web 工作**</span><span class="sxs-lookup"><span data-stu-id="12fe2-169">For publishing this as a **WebJob**, right click on hello solution in Visual Studio and select **Publish as WebJob**</span></span>
   
    ![][2]
   
    <span data-ttu-id="12fe2-170">f.</span><span class="sxs-lookup"><span data-stu-id="12fe2-170">f.</span></span> <span data-ttu-id="12fe2-171">選取您的發行設定檔，並建立新的 Azure 網站，如果不存在已經它將裝載此 WebJob 和一旦 hello 網站然後**發行**。</span><span class="sxs-lookup"><span data-stu-id="12fe2-171">Select your publishing profile and create a new Azure WebSite if it doesnt exist already which will host this WebJob and once you have hello WebSite then **Publish**.</span></span>
   
    ![][3]
   
    <span data-ttu-id="12fe2-172">g.</span><span class="sxs-lookup"><span data-stu-id="12fe2-172">g.</span></span> <span data-ttu-id="12fe2-173">設定 「 持續執行"hello 作業 toobe 時登入 toohello [Azure 傳統入口網站]您應該會看到類似下列 hello:</span><span class="sxs-lookup"><span data-stu-id="12fe2-173">Configure hello job toobe "Run Continuously" so that when you log in toohello [Azure Classic Portal] you should see something like hello following:</span></span>
   
    ![][4]
3. <span data-ttu-id="12fe2-174">**EnterprisePushMobileApp**</span><span class="sxs-lookup"><span data-stu-id="12fe2-174">**EnterprisePushMobileApp**</span></span>
   
    <span data-ttu-id="12fe2-175">a.</span><span class="sxs-lookup"><span data-stu-id="12fe2-175">a.</span></span> <span data-ttu-id="12fe2-176">這是接收快顯通知的 hello WebJob 執行您的行動裝置後端的一部分，並顯示 Windows 市集應用程式。</span><span class="sxs-lookup"><span data-stu-id="12fe2-176">This is a Windows Store application which will receive toast notifications from hello WebJob running as part of your Mobile backend and display it.</span></span> <span data-ttu-id="12fe2-177">其乃依據[通知中樞-Windows 通用的教學課程]。</span><span class="sxs-lookup"><span data-stu-id="12fe2-177">This is based on [Notification Hubs - Windows Universal tutorial].</span></span>  
   
    <span data-ttu-id="12fe2-178">b.</span><span class="sxs-lookup"><span data-stu-id="12fe2-178">b.</span></span> <span data-ttu-id="12fe2-179">請確定您的應用程式啟用的 tooreceive 快顯通知。</span><span class="sxs-lookup"><span data-stu-id="12fe2-179">Ensure that your application is enabled tooreceive toast notifications.</span></span>
   
    <span data-ttu-id="12fe2-180">c.</span><span class="sxs-lookup"><span data-stu-id="12fe2-180">c.</span></span> <span data-ttu-id="12fe2-181">請確定在 hello 應用程式啟動時呼叫該 hello 下列通知中樞註冊程式碼 (取代 hello 後*HubName*和*DefaultListenSharedAccessSignature*:</span><span class="sxs-lookup"><span data-stu-id="12fe2-181">Ensure that hello following Notification Hubs registration code is being called at hello App start up (after replacing hello *HubName* and *DefaultListenSharedAccessSignature*:</span></span>
   
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

### <a name="running-sample"></a><span data-ttu-id="12fe2-182">執行範例：</span><span class="sxs-lookup"><span data-stu-id="12fe2-182">Running sample:</span></span>
1. <span data-ttu-id="12fe2-183">確定您 WebJob 順利執行，並排程太 「 執行持續 」。</span><span class="sxs-lookup"><span data-stu-id="12fe2-183">Ensure that your WebJob is running successfully and scheduled too"Run Continuously".</span></span>
2. <span data-ttu-id="12fe2-184">執行 hello **EnterprisePushMobileApp**這會啟動 hello Windows 市集應用程式。</span><span class="sxs-lookup"><span data-stu-id="12fe2-184">Run hello **EnterprisePushMobileApp** which will start hello Windows Store app.</span></span>
3. <span data-ttu-id="12fe2-185">執行 hello **EnterprisePushBackendSystem**主控台應用程式，會模擬 hello LoB 後端，便會開始傳送訊息，以及您應該會看到快顯通知出現 hello 如下：</span><span class="sxs-lookup"><span data-stu-id="12fe2-185">Run hello **EnterprisePushBackendSystem** console application which will simulate hello LoB backend and will start sending messages and you should see toast notifications appearing like hello following:</span></span>
   
    ![][5]
4. <span data-ttu-id="12fe2-186">hello 訊息原始傳送 tooService 匯流排主題在受監視服務匯流排訂用帳戶中的 Web 工作。</span><span class="sxs-lookup"><span data-stu-id="12fe2-186">hello messages were originally sent tooService Bus topics which was being monitored by Service Bus subscriptions in your Web Job.</span></span> <span data-ttu-id="12fe2-187">一旦收到的訊息，通知所建立及傳送 toohello 行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="12fe2-187">Once a message was received, a notification was created and sent toohello mobile app.</span></span> <span data-ttu-id="12fe2-188">您可以查看 WebJob 記錄 tooconfirm hello 處理，當您移的 toohello 記錄檔中連結的 hello [Azure 傳統入口網站]Web 工作：</span><span class="sxs-lookup"><span data-stu-id="12fe2-188">You can look through hello WebJob logs tooconfirm hello processing when you go toohello Logs link in [Azure Classic Portal] for your Web Job:</span></span>
   
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
