---
title: "通知中樞 - 企業推送架構"
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
ms.openlocfilehash: ae7c1c9644ecfe7fe4ad6e332cc0683a3b5df22f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-push-architectural-guidance"></a><span data-ttu-id="6dd5a-103">企業推送架構指引</span><span class="sxs-lookup"><span data-stu-id="6dd5a-103">Enterprise push architectural guidance</span></span>
<span data-ttu-id="6dd5a-104">當代的企業正逐漸朝著為使用者 (外部) 或員工 (內部) 建立行動應用程式的方向邁進。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-104">Enterprises today are gradually moving towards creating mobile applications for either their end users (external) or for the employees (internal).</span></span> <span data-ttu-id="6dd5a-105">他們擁有現成的後端系統 (大型主機或一些 LoB 應用程式)，而這些系統必須整合到行動應用程式架構中。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-105">They have existing backend systems in place be it mainframes or some LoB applications which must be integrated into the mobile application architecture.</span></span> <span data-ttu-id="6dd5a-106">本指南將討論如何以最佳方式進行整合，以及推薦常見案例適用的可行方案。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-106">This guide will talk about how best to do this integration recommending possible solution to common scenarios.</span></span>

<span data-ttu-id="6dd5a-107">常見的需求是當後端系統發生使用者感興趣的事件時，透過行動應用程式將推播通知傳送給使用者。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-107">A frequent requirement is for sending push notification to the users through their mobile application when an event of interest occurs in the backend systems.</span></span> <span data-ttu-id="6dd5a-108">例如</span><span class="sxs-lookup"><span data-stu-id="6dd5a-108">E.g.</span></span> <span data-ttu-id="6dd5a-109">在 iPhone 上安裝某家銀行之網路銀行應用程式的銀行客戶，想要在帳戶扣款金額超過一定數量時獲得通知，抑或是在 Windows Phone 安裝預算核准應用程式的財務部門員工，想要在收到核准要求時獲得通知的內部網路案例。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-109">a bank customer who has the bank's banking app on her iPhone wants to be notified when a debit is made above a certain amount from her account or an intranet scenario where an employee from finance department who has a budget approval app on his Windows Phone wants to be notified when he gets an approval request.</span></span>

<span data-ttu-id="6dd5a-110">銀行帳戶或核准處理有可能是在必須發出推播給使用者的後端系統中完成。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-110">The bank account or approval processing is likely to be done in some backend system which must initiate a push to the user.</span></span> <span data-ttu-id="6dd5a-111">若要在事件觸發通知時實作推播，企業必須具備多部建置相同邏輯的後端系統。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-111">There may be multiple such backend systems which must all build the same kind of logic to implement push when an event triggers a notification.</span></span> <span data-ttu-id="6dd5a-112">其複雜度在於利用一個推播系統將數個後端系統整合在一起，而在此案例中，使用者可能訂閱了不同的通知且甚至擁有多個行動應用程式。例如，在內部網路行動應用程式案例中，某個行動應用程式想要收到由多部上述後端系統所傳送的通知。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-112">The complexity here lies in integrating several backend systems together with a single push system where the end users may have subscribed to different notifications and there may even be multiple mobile applications e.g. in the case of intranet mobile apps where one mobile application may want to receive notifications from multiple such backend systems.</span></span> <span data-ttu-id="6dd5a-113">由於後端系統不知道 (或不需要知道) 推播語意/技術，因此在傳統上，常用方案是採用輪詢後端系統是否有任何使用者感興趣之事件的元件，並將傳送推播訊息給用戶端的職責交由它來完成。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-113">The backend systems do not know or need to know of push semantics/technology so a common solution here traditionally has been to introduce a component which polls the backend systems for any events of interest and is responsible for sending the push messages to the client.</span></span>
<span data-ttu-id="6dd5a-114">這裡我們將討論使用「Azure 服務匯流排 - 主題/訂用帳戶」模型這種甚至更好的解決方案，而此模型可降低複雜度，同時讓解決方案更具調整性。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-114">Here we will talk about an even better solution using Azure Service Bus - Topic/Subscription model which will reduce the complexity while making the solution scalable.</span></span>

<span data-ttu-id="6dd5a-115">以下是方案的一般架構 (我們已利用多個行動應用程式將其一般化，不過該架構亦適用於只有一個行動應用程式的案例)。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-115">Here is the general architecture of the solution (generalized with multiple mobile apps but equally applicable when there is only one mobile app)</span></span>

## <a name="architecture"></a><span data-ttu-id="6dd5a-116">架構</span><span class="sxs-lookup"><span data-stu-id="6dd5a-116">Architecture</span></span>
![][1]

<span data-ttu-id="6dd5a-117">本架構圖中的關鍵是提供主題/訂用帳戶程式撰寫模型的 Azure 服務匯流排 (如需詳細資料，請參閱 [服務匯流排發佈/訂用帳戶程式撰寫])。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-117">The key piece in this architectural diagram is Azure Service Bus which provides a topics/subscriptions programming model (more on it at [Service Bus Pub/Sub programming]).</span></span> <span data-ttu-id="6dd5a-118">本案例中的接收器是行動後端 (通常是 [Azure 行動服務]，它會將推播發送給行動裝置)，它不會直接接收來自後端系統的訊息，反之，我們會加入由 [Azure 服務匯流排]提供的中繼抽象層，讓行動後端得以接收來自一或多個後端系統的訊息。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-118">The receiver, which in this case, is the Mobile backend (typically [Azure Mobile Service], which will initiate a push to the mobile apps) does not receive messages directly from the backend systems but instead we have an intermediate abstraction layer provided by [Azure Service Bus] which enables mobile backend to receive messages from one or more backend systems.</span></span> <span data-ttu-id="6dd5a-119">您需要為每個後端系統建立服務匯流排主題 (如客戶、人事、財務)，基本上它們是讓訊息能以推播通知形式傳送的興趣「主題」。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-119">A Service Bus Topic needs to be created for each of the backend systems e.g. Account, HR, Finance which are basically "topics" of interest which will initiate messages to be sent as push notification.</span></span> <span data-ttu-id="6dd5a-120">後端系統會將訊息傳送到這些主題。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-120">The backend systems will send messages to these topics.</span></span> <span data-ttu-id="6dd5a-121">藉由建立服務匯流排訂閱，行動後端能訂閱一或多個這類型的主題。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-121">A Mobile Backend can subscribe to one or more such topics by creating a Service Bus subscription.</span></span> <span data-ttu-id="6dd5a-122">如此一來，行動後端便能接收由對應後端系統所傳送的通知。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-122">This will entitle the mobile backend to receive a notification from the corresponding backend system.</span></span> <span data-ttu-id="6dd5a-123">行動後端會持續接聽與其訂閱相關的訊息，待訊息抵達後，它會立即轉向並以通知形式將訊息傳送到通知匯流排。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-123">Mobile backend continues to listen for messages on their subscriptions and as soon as a message arrives, it turns back and sends it as notification to its notification hub.</span></span> <span data-ttu-id="6dd5a-124">通知匯流排再接著將訊息傳遞給行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-124">Notification hubs then eventually delivers the message to the mobile app.</span></span> <span data-ttu-id="6dd5a-125">總結以上關鍵元件，我們可以得出：</span><span class="sxs-lookup"><span data-stu-id="6dd5a-125">So to summarize the key components, we have:</span></span>

1. <span data-ttu-id="6dd5a-126">後端系統 (LoB/舊版系統)</span><span class="sxs-lookup"><span data-stu-id="6dd5a-126">Backend systems (LoB/Legacy systems)</span></span>
   * <span data-ttu-id="6dd5a-127">建立服務匯流排主題</span><span class="sxs-lookup"><span data-stu-id="6dd5a-127">Creates Service Bus Topic</span></span>
   * <span data-ttu-id="6dd5a-128">傳送訊息</span><span class="sxs-lookup"><span data-stu-id="6dd5a-128">Sends Message</span></span>
2. <span data-ttu-id="6dd5a-129">行動後端</span><span class="sxs-lookup"><span data-stu-id="6dd5a-129">Mobile backend</span></span>
   * <span data-ttu-id="6dd5a-130">建立服務訂閱</span><span class="sxs-lookup"><span data-stu-id="6dd5a-130">Creates Service Subscription</span></span>
   * <span data-ttu-id="6dd5a-131">接收訊息 (來自後端系統)</span><span class="sxs-lookup"><span data-stu-id="6dd5a-131">Receives Message (from Backend system)</span></span>
   * <span data-ttu-id="6dd5a-132">將通知傳送給用戶端 (透過 Azure 通知中樞)</span><span class="sxs-lookup"><span data-stu-id="6dd5a-132">Sends notification to clients (via Azure Notification Hub)</span></span>
3. <span data-ttu-id="6dd5a-133">行動應用程式</span><span class="sxs-lookup"><span data-stu-id="6dd5a-133">Mobile Application</span></span>
   * <span data-ttu-id="6dd5a-134">接收及顯示通知</span><span class="sxs-lookup"><span data-stu-id="6dd5a-134">Receives and display notification</span></span>

### <a name="benefits"></a><span data-ttu-id="6dd5a-135">優點：</span><span class="sxs-lookup"><span data-stu-id="6dd5a-135">Benefits:</span></span>
1. <span data-ttu-id="6dd5a-136">接收器 (行動應用程式/透過通知中樞傳送的服務) 與傳送器 (後端系統) 的解離可讓您在變更少量架構的情況下整合額外的後端系統。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-136">The decoupling between the receiver (mobile app/service via Notification Hub) and sender (backend systems) enables additional backend systems being integrated with minimal change.</span></span>
2. <span data-ttu-id="6dd5a-137">含有多個行動應用程式的案例也能藉此接收來自一或多個後端系統的事件。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-137">This also makes the scenario of multiple mobile apps being able to receive events from one or more backend systems.</span></span>  

## <a name="sample"></a><span data-ttu-id="6dd5a-138">範例：</span><span class="sxs-lookup"><span data-stu-id="6dd5a-138">Sample:</span></span>
### <a name="prerequisites"></a><span data-ttu-id="6dd5a-139">必要條件</span><span class="sxs-lookup"><span data-stu-id="6dd5a-139">Prerequisites</span></span>
<span data-ttu-id="6dd5a-140">您應該先完成下列教學課程以熟悉概念，以及常用的建立和組態步驟：</span><span class="sxs-lookup"><span data-stu-id="6dd5a-140">You should complete the following tutorials to familiarize with the concepts as well as common creation & configuration steps:</span></span>

1. <span data-ttu-id="6dd5a-141">[服務匯流排發佈/訂用帳戶程式撰寫] - 這說明使用服務匯流排主題/訂用帳戶的詳細資料、如何建立命名空間來包含主題/訂用帳戶、如何傳送和接收來自它們的訊息。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-141">[Service Bus Pub/Sub programming] - This explains the details of working with Service Bus Topics/Subscriptions, how to create a namespace to contain topics/subscriptions, how to send & receive messages from them.</span></span>
2. <span data-ttu-id="6dd5a-142">[通知中樞 - Windows Universal 教學課程] - 說明如何設定 Windows 市集應用程式，以及使用通知中樞來註冊和接收通知。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-142">[Notification Hubs - Windows Universal tutorial] - This explains how to set up a Windows Store app and use Notification Hubs to register and then receive notifications.</span></span>

### <a name="sample-code"></a><span data-ttu-id="6dd5a-143">範例程式碼</span><span class="sxs-lookup"><span data-stu-id="6dd5a-143">Sample code</span></span>
<span data-ttu-id="6dd5a-144">如需完整範例程式碼，請參閱 [通知中樞範例]。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-144">The full sample code is available at [Notification Hub Samples].</span></span> <span data-ttu-id="6dd5a-145">其可劃分為三個元件：</span><span class="sxs-lookup"><span data-stu-id="6dd5a-145">It is split into three components:</span></span>

1. <span data-ttu-id="6dd5a-146">**EnterprisePushBackendSystem**</span><span class="sxs-lookup"><span data-stu-id="6dd5a-146">**EnterprisePushBackendSystem**</span></span>
   
    <span data-ttu-id="6dd5a-147">a.</span><span class="sxs-lookup"><span data-stu-id="6dd5a-147">a.</span></span> <span data-ttu-id="6dd5a-148">本專案使用 *WindowsAzure.ServiceBus* Nuget 套件，並以[服務匯流排發佈/訂用帳戶程式撰寫]為依據。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-148">This project uses the *WindowsAzure.ServiceBus* Nuget package and is  based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="6dd5a-149">b.</span><span class="sxs-lookup"><span data-stu-id="6dd5a-149">b.</span></span> <span data-ttu-id="6dd5a-150">此為簡易的 C# 主控台應用程式，可用來模擬讓訊息得以傳遞到行動應用程式的 LoB 系統。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-150">This is a simple C# console app to simulate an LoB system which initiates the message to be delivered to the mobile app.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create the topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    <span data-ttu-id="6dd5a-151">c.</span><span class="sxs-lookup"><span data-stu-id="6dd5a-151">c.</span></span> <span data-ttu-id="6dd5a-152">`CreateTopic` 可用來建立傳送訊息的服務匯流排主題。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-152">`CreateTopic` is used to create the Service Bus topic where we will send messages.</span></span>
   
        public static void CreateTopic(string connectionString)
        {
            // Create the topic if it does not exist already
   
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.TopicExists(sampleTopic))
            {
                namespaceManager.CreateTopic(sampleTopic);
            }
        }
   
    <span data-ttu-id="6dd5a-153">d.</span><span class="sxs-lookup"><span data-stu-id="6dd5a-153">d.</span></span> <span data-ttu-id="6dd5a-154">`SendMessage` 可用來將訊息傳送到此服務匯流排主題。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-154">`SendMessage` is used to send the messages to this Service Bus Topic.</span></span> <span data-ttu-id="6dd5a-155">基於示範目的，在這裡我們只定期傳送一組隨機訊息給主題。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-155">Here we are simply sending a set of random messages to the topic periodically for the purpose of the sample.</span></span> <span data-ttu-id="6dd5a-156">在一般情況下，我們會有在事件發生時傳送訊息的後端系統。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-156">Normally there will be a backend system which will send messages when an event occurs.</span></span>
   
        public static void SendMessage(string connectionString)
        {
            TopicClient client =
                TopicClient.CreateFromConnectionString(connectionString, sampleTopic);
   
            // Sends random messages every 10 seconds to the topic
            string[] messages =
            {
                "Employee Id '{0}' has joined.",
                "Employee Id '{0}' has left.",
                "Employee Id '{0}' has switched to a different team."
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
2. <span data-ttu-id="6dd5a-157">**ReceiveAndSendNotification**</span><span class="sxs-lookup"><span data-stu-id="6dd5a-157">**ReceiveAndSendNotification**</span></span>
   
    <span data-ttu-id="6dd5a-158">a.</span><span class="sxs-lookup"><span data-stu-id="6dd5a-158">a.</span></span> <span data-ttu-id="6dd5a-159">本專案使用 *WindowsAzure.ServiceBus* 和 *Microsoft.Web.WebJobs.Publish* Nuget 套件，並以[服務匯流排發佈/訂用帳戶程式撰寫]為依據。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-159">This project uses the *WindowsAzure.ServiceBus* and *Microsoft.Web.WebJobs.Publish* Nuget packages and is based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="6dd5a-160">b.</span><span class="sxs-lookup"><span data-stu-id="6dd5a-160">b.</span></span> <span data-ttu-id="6dd5a-161">由於它必須連續執行以便接聽來自 LoB/後端系統的訊息，因此我們會以 [Azure WebJob] 的形式予以執行。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-161">This is another C# console app which we will run as an [Azure WebJob] since it has to run continuously to listen for messages from the LoB/backend systems.</span></span> <span data-ttu-id="6dd5a-162">它將會是行動後端的一部分。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-162">This will be part of your Mobile backend.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create the subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    <span data-ttu-id="6dd5a-163">c.</span><span class="sxs-lookup"><span data-stu-id="6dd5a-163">c.</span></span> <span data-ttu-id="6dd5a-164">`CreateSubscription` 可用來為後端系統傳送訊息的主題建立服務匯流排訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-164">`CreateSubscription` is used to create a Service Bus subscription for the topic where the backend system will send messages.</span></span> <span data-ttu-id="6dd5a-165">由於商務案例不盡相同，此元件將會建立一或多個對應主題的訂閱 (例如，有些訂閱會接收來自人事系統的訊息，有些則接收來自財務系統的訊息等)。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-165">Depending on the business scenario, this component will create one or more subscriptions to corresponding topics (e.g. some may be receiving messages from HR system, some from Finance system, and so on)</span></span>
   
        static void CreateSubscription(string connectionString)
        {
            // Create the subscription if it does not exist already
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.SubscriptionExists(sampleTopic, sampleSubscription))
            {
                namespaceManager.CreateSubscription(sampleTopic, sampleSubscription);
            }
        }
   
    <span data-ttu-id="6dd5a-166">d.</span><span class="sxs-lookup"><span data-stu-id="6dd5a-166">d.</span></span> <span data-ttu-id="6dd5a-167">使用 ReceiveMessageAndSendNotification，以使用訂用帳戶來讀取主題中的訊息，如果讀取成功，則會使用 Azure 通知中樞製作通知 (在範例案例中，即 Windows 原生快顯通知) 以傳送給行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-167">ReceiveMessageAndSendNotification is used to read the message from the topic using its subscription and if the read is successful then craft a notification (in the sample scenario a Windows native toast notification) to be sent to the mobile application using Azure Notification Hubs.</span></span>
   
        static void ReceiveMessageAndSendNotification(string connectionString)
        {
            // Initialize the Notification Hub
            string hubConnectionString = CloudConfigurationManager.GetSetting
                    ("Microsoft.NotificationHub.ConnectionString");
            hub = NotificationHubClient.CreateClientFromConnectionString
                    (hubConnectionString, "enterprisepushservicehub");
   
            SubscriptionClient Client =
                SubscriptionClient.CreateFromConnectionString
                        (connectionString, sampleTopic, sampleSubscription);
   
            Client.Receive();
   
            // Continuously process messages received from the subscription
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
   
    <span data-ttu-id="6dd5a-168">e.</span><span class="sxs-lookup"><span data-stu-id="6dd5a-168">e.</span></span> <span data-ttu-id="6dd5a-169">若要將其發佈為 **WebJob**，請在 Visual Studio 中於解決方案上按一下滑鼠右鍵，然後選取 [發佈為 WebJob]。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-169">For publishing this as a **WebJob**, right click on the solution in Visual Studio and select **Publish as WebJob**</span></span>
   
    ![][2]
   
    <span data-ttu-id="6dd5a-170">f.</span><span class="sxs-lookup"><span data-stu-id="6dd5a-170">f.</span></span> <span data-ttu-id="6dd5a-171">選取發佈設定檔並建立新的 Azure 網站 (如果網站不存在，其可用來裝載此 WebJob)，待備妥網站後，請予以 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-171">Select your publishing profile and create a new Azure WebSite if it doesnt exist already which will host this WebJob and once you have the WebSite then **Publish**.</span></span>
   
    ![][3]
   
    <span data-ttu-id="6dd5a-172">g.</span><span class="sxs-lookup"><span data-stu-id="6dd5a-172">g.</span></span> <span data-ttu-id="6dd5a-173">將作業設定為 [連續執行]，如此一來，當您登入 [Azure 傳統入口網站]時，應能看見與以下範例相似的內容：</span><span class="sxs-lookup"><span data-stu-id="6dd5a-173">Configure the job to be "Run Continuously" so that when you log in to the [Azure Classic Portal] you should see something like the following:</span></span>
   
    ![][4]
3. <span data-ttu-id="6dd5a-174">**EnterprisePushMobileApp**</span><span class="sxs-lookup"><span data-stu-id="6dd5a-174">**EnterprisePushMobileApp**</span></span>
   
    <span data-ttu-id="6dd5a-175">a.</span><span class="sxs-lookup"><span data-stu-id="6dd5a-175">a.</span></span> <span data-ttu-id="6dd5a-176">此為 Windows 市集應用程式，它能接收隨附於行動後端運作之 WebJob 發出的快顯通知並加以顯示。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-176">This is a Windows Store application which will receive toast notifications from the WebJob running as part of your Mobile backend and display it.</span></span> <span data-ttu-id="6dd5a-177">其乃依據[通知中樞 - Windows Universal 教學課程]。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-177">This is based on [Notification Hubs - Windows Universal tutorial].</span></span>  
   
    <span data-ttu-id="6dd5a-178">b.</span><span class="sxs-lookup"><span data-stu-id="6dd5a-178">b.</span></span> <span data-ttu-id="6dd5a-179">確認應用程式可接收快顯通知。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-179">Ensure that your application is enabled to receive toast notifications.</span></span>
   
    <span data-ttu-id="6dd5a-180">c.</span><span class="sxs-lookup"><span data-stu-id="6dd5a-180">c.</span></span> <span data-ttu-id="6dd5a-181">確認應用程式啟動時會呼叫以下通知中樞註冊程式碼 (取代 *HubName* 和 *DefaultListenSharedAccessSignature* 之後)：</span><span class="sxs-lookup"><span data-stu-id="6dd5a-181">Ensure that the following Notification Hubs registration code is being called at the App start up (after replacing the *HubName* and *DefaultListenSharedAccessSignature*:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("[HubName]", "[DefaultListenSharedAccessSignature]");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

### <a name="running-sample"></a><span data-ttu-id="6dd5a-182">執行範例：</span><span class="sxs-lookup"><span data-stu-id="6dd5a-182">Running sample:</span></span>
1. <span data-ttu-id="6dd5a-183">確認 WebJob 成功執行，並已排定為 [連續執行]。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-183">Ensure that your WebJob is running successfully and scheduled to "Run Continuously".</span></span>
2. <span data-ttu-id="6dd5a-184">執行 **EnterprisePushMobileApp** 以啟動 Windows 市集應用程式。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-184">Run the **EnterprisePushMobileApp** which will start the Windows Store app.</span></span>
3. <span data-ttu-id="6dd5a-185">執行 **EnterprisePushBackendSystem** 主控台應用程式以模擬 LoB 後端。它會開始傳送訊息，因此您應該會看見與以下範例相似的快顯通知：</span><span class="sxs-lookup"><span data-stu-id="6dd5a-185">Run the **EnterprisePushBackendSystem** console application which will simulate the LoB backend and will start sending messages and you should see toast notifications appearing like the following:</span></span>
   
    ![][5]
4. <span data-ttu-id="6dd5a-186">這些訊息最初是傳送給受到 WebJob 中服務匯流排訂閱監視的服務匯流排主題。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-186">The messages were originally sent to Service Bus topics which was being monitored by Service Bus subscriptions in your Web Job.</span></span> <span data-ttu-id="6dd5a-187">待服務匯流排主題接收到訊息後，它會建立通知並傳送給行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="6dd5a-187">Once a message was received, a notification was created and sent to the mobile app.</span></span> <span data-ttu-id="6dd5a-188">在 [Azure 傳統入口網站] 中，當您前往 WebJob 的 [記錄檔] 連結時，可以瀏覽 WebJob 記錄檔來確認處理狀態：</span><span class="sxs-lookup"><span data-stu-id="6dd5a-188">You can look through the WebJob logs to confirm the processing when you go to the Logs link in [Azure Classic Portal] for your Web Job:</span></span>
   
    ![][6]

<!-- Images -->
[1]: ./media/notification-hubs-enterprise-push-architecture/architecture.png
[2]: ./media/notification-hubs-enterprise-push-architecture/WebJobsContextMenu.png
[3]: ./media/notification-hubs-enterprise-push-architecture/PublishAsWebJob.png
[4]: ./media/notification-hubs-enterprise-push-architecture/WebJob.png
[5]: ./media/notification-hubs-enterprise-push-architecture/Notifications.png
[6]: ./media/notification-hubs-enterprise-push-architecture/WebJobsLog.png

<!-- Links -->
<span data-ttu-id="6dd5a-189">[通知中樞範例]: https://github.com/Azure/azure-notificationhubs-samples</span><span class="sxs-lookup"><span data-stu-id="6dd5a-189">[Notification Hub Samples]: https://github.com/Azure/azure-notificationhubs-samples</span></span>
<span data-ttu-id="6dd5a-190">[Azure 行動服務]: http://azure.microsoft.com/documentation/services/mobile-services/</span><span class="sxs-lookup"><span data-stu-id="6dd5a-190">[Azure Mobile Service]: http://azure.microsoft.com/documentation/services/mobile-services/</span></span>
<span data-ttu-id="6dd5a-191">[Azure 服務匯流排]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/</span><span class="sxs-lookup"><span data-stu-id="6dd5a-191">[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/</span></span>
<span data-ttu-id="6dd5a-192">[服務匯流排發佈/訂用帳戶程式撰寫]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/</span><span class="sxs-lookup"><span data-stu-id="6dd5a-192">[Service Bus Pub/Sub programming]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/</span></span>
<span data-ttu-id="6dd5a-193">[Azure WebJob]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/</span><span class="sxs-lookup"><span data-stu-id="6dd5a-193">[Azure WebJob]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/</span></span>
<span data-ttu-id="6dd5a-194">[通知中樞 - Windows Universal 教學課程]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span><span class="sxs-lookup"><span data-stu-id="6dd5a-194">[Notification Hubs - Windows Universal tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span></span>
<span data-ttu-id="6dd5a-195">[Azure 傳統入口網站]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="6dd5a-195">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
