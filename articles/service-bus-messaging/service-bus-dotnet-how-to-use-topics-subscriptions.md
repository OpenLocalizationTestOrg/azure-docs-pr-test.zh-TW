---
title: "開始使用 Azure 服務匯流排主題和訂用帳戶 | Microsoft Docs"
description: "撰寫使用服務匯流排傳訊主題和訂用帳戶的 C# 主控台應用程式。"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/30/2017
ms.author: sethm
ms.openlocfilehash: 9401ada519f600b0d2817f06a396e16607a24129
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-service-bus-topics"></a><span data-ttu-id="a9a37-103">開始使用服務匯流排主題</span><span class="sxs-lookup"><span data-stu-id="a9a37-103">Get started with Service Bus topics</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="a9a37-104">將會完成的工作</span><span class="sxs-lookup"><span data-stu-id="a9a37-104">What will be accomplished</span></span>

<span data-ttu-id="a9a37-105">本教學課程涵蓋下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a9a37-105">This tutorial covers the following steps:</span></span>

1. <span data-ttu-id="a9a37-106">使用 Azure 入口網站建立服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="a9a37-106">Create a Service Bus namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="a9a37-107">使用 Azure 入口網站建立服務匯流排主題。</span><span class="sxs-lookup"><span data-stu-id="a9a37-107">Create a Service Bus topic, using the Azure portal.</span></span>
3. <span data-ttu-id="a9a37-108">使用 Azure 入口網站，針對該主題建立服務匯流排訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a9a37-108">Create a Service Bus subscription to that topic, using the Azure portal.</span></span>
4. <span data-ttu-id="a9a37-109">撰寫主控台應用程式以傳送訊息至主題。</span><span class="sxs-lookup"><span data-stu-id="a9a37-109">Write a console application to send a message to the topic.</span></span>
5. <span data-ttu-id="a9a37-110">撰寫主控台應用程式以從訂用帳戶接收該訊息。</span><span class="sxs-lookup"><span data-stu-id="a9a37-110">Write a console application to receive that message from the subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9a37-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="a9a37-111">Prerequisites</span></span>

1. <span data-ttu-id="a9a37-112">[Visual Studio 2015 或更新版本](http://www.visualstudio.com)。</span><span class="sxs-lookup"><span data-stu-id="a9a37-112">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="a9a37-113">本教學課程中的範例使用 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="a9a37-113">The examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="a9a37-114">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a9a37-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="a9a37-115">1.使用 Azure 入口網站建立命名空間</span><span class="sxs-lookup"><span data-stu-id="a9a37-115">1. Create a namespace using the Azure portal</span></span>

<span data-ttu-id="a9a37-116">如果您已建立服務匯流排傳訊命名空間，請跳至[使用 Azure 入口網站建立主題](#2-create-a-topic-using-the-azure-portal)一節。</span><span class="sxs-lookup"><span data-stu-id="a9a37-116">If you have already created a Service Bus Messaging namespace, jump to the [Create a topic using the Azure portal](#2-create-a-topic-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-the-azure-portal"></a><span data-ttu-id="a9a37-117">2.使用 Azure 入口網站建立主題</span><span class="sxs-lookup"><span data-stu-id="a9a37-117">2. Create a topic using the Azure portal</span></span>

1. <span data-ttu-id="a9a37-118">登入 [Azure 入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="a9a37-118">Log on to the [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="a9a37-119">在入口網站的左方瀏覽窗格中，按一下 [服務匯流排] \(如果您未看見 [服務匯流排]，請按一下 [更多服務])。</span><span class="sxs-lookup"><span data-stu-id="a9a37-119">In the left navigation pane of the portal, click **Service Bus** (if you don't see **Service Bus**, click **More services**).</span></span>
3. <span data-ttu-id="a9a37-120">按一下要在其中建立主題的命名空間。</span><span class="sxs-lookup"><span data-stu-id="a9a37-120">Click the namespace in which you would like to create the topic.</span></span> <span data-ttu-id="a9a37-121">命名空間概觀的刀鋒視窗即會出現：</span><span class="sxs-lookup"><span data-stu-id="a9a37-121">The namespace overview blade appears:</span></span>
   
    ![建立主題][createtopic1]
4. <span data-ttu-id="a9a37-123">在 [服務匯流排命名空間] 刀鋒視窗中，按一下 [主題]，然後按一下 [新增主題]。</span><span class="sxs-lookup"><span data-stu-id="a9a37-123">In the **Service Bus namespace** blade, click **Topics**, then click **Add topic**.</span></span>
   
    ![選取主題][createtopic2]
5. <span data-ttu-id="a9a37-125">輸入主題名稱，然後取消核取 [啟用資料分割] 選項。</span><span class="sxs-lookup"><span data-stu-id="a9a37-125">Enter a name for the topic, and uncheck the **Enable partitioning** option.</span></span> <span data-ttu-id="a9a37-126">保留其他選項的預設值。</span><span class="sxs-lookup"><span data-stu-id="a9a37-126">Leave the other options with their default values.</span></span>
   
    ![選取新增][createtopic3]
6. <span data-ttu-id="a9a37-128">按一下刀鋒視窗底部的 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a9a37-128">At the bottom of the blade, click **Create**.</span></span>

## <a name="3-create-a-subscription-to-the-topic"></a><span data-ttu-id="a9a37-129">3.針對主題建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a9a37-129">3. Create a subscription to the topic</span></span>

1. <span data-ttu-id="a9a37-130">在入口網站的資源窗格中，按一下在步驟 1 所建立的命名空間，接著按一下在步驟 2 所建立的主題名稱。</span><span class="sxs-lookup"><span data-stu-id="a9a37-130">In the portal resources pane, click the namespace you created in step 1, then click name of the topic you created in step 2.</span></span>
2. <span data-ttu-id="a9a37-131">在概觀窗格頂端，按一下 [訂用帳戶] 旁的加號，將訂用帳戶新增至主題。</span><span class="sxs-lookup"><span data-stu-id="a9a37-131">A the top of the overview pane, click the plus sign next to **Subscription** to add a subscription to this topic.</span></span>

    ![建立訂用帳戶][createtopic4]

3. <span data-ttu-id="a9a37-133">輸入訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="a9a37-133">Enter a name for the subscription.</span></span> <span data-ttu-id="a9a37-134">保留其他選項的預設值。</span><span class="sxs-lookup"><span data-stu-id="a9a37-134">Leave the other options with their default values.</span></span>

## <a name="4-send-messages-to-the-topic"></a><span data-ttu-id="a9a37-135">4.將訊息傳送到主題</span><span class="sxs-lookup"><span data-stu-id="a9a37-135">4. Send messages to the topic</span></span>

<span data-ttu-id="a9a37-136">為了將訊息傳送至主題，我們使用 Visual Studio 撰寫 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="a9a37-136">To send messages to the topic, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="a9a37-137">建立主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="a9a37-137">Create a console application</span></span>

<span data-ttu-id="a9a37-138">啟動 Visual Studio，並建立新的**主控台應用程式 (.NET Framework)** 專案。</span><span class="sxs-lookup"><span data-stu-id="a9a37-138">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-the-service-bus-nuget-package"></a><span data-ttu-id="a9a37-139">新增服務匯流排 NuGet 封裝</span><span class="sxs-lookup"><span data-stu-id="a9a37-139">Add the Service Bus NuGet package</span></span>

1. <span data-ttu-id="a9a37-140">以滑鼠右鍵按一下新建立的專案，然後選取 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="a9a37-140">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="a9a37-141">按一下 [瀏覽] 索引標籤，搜尋 [Microsoft Azure 服務匯流排]，然後選取 [WindowsAzure.ServiceBus] 項目。</span><span class="sxs-lookup"><span data-stu-id="a9a37-141">Click the **Browse** tab, search for **Microsoft Azure Service Bus**, and then select the **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="a9a37-142">按一下 [安裝]  完成安裝作業，然後關閉此對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a9a37-142">Click **Install** to complete the installation, then close this dialog box.</span></span>
   
    ![選取 NuGet 封裝][nuget-pkg]

### <a name="write-some-code-to-send-a-message-to-the-topic"></a><span data-ttu-id="a9a37-144">撰寫一些程式碼以將訊息傳送至主題</span><span class="sxs-lookup"><span data-stu-id="a9a37-144">Write some code to send a message to the topic</span></span>

1. <span data-ttu-id="a9a37-145">在 Program.cs 檔案開頭處新增以下 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="a9a37-145">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="a9a37-146">將下列程式碼新增至 `Main` 方法。</span><span class="sxs-lookup"><span data-stu-id="a9a37-146">Add the following code to the `Main` method.</span></span> <span data-ttu-id="a9a37-147">將 `connectionString` 變數設定為建立命名空間時取得的連接字串，並將 `topicName` 設定為建立主題時使用的名稱。</span><span class="sxs-lookup"><span data-stu-id="a9a37-147">Set the `connectionString` variable to the connection string that you obtained when creating the namespace, and set `topicName` to the name that you used when creating the topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER to exit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="a9a37-148">Program.cs 檔案看起來應該會像下面這樣。</span><span class="sxs-lookup"><span data-stu-id="a9a37-148">Here is what your Program.cs file should look like.</span></span>
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.ServiceBus.Messaging;

    namespace tsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var topicName = "<your topic name>";

                var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER to exit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. <span data-ttu-id="a9a37-149">執行程式，並檢查 Azure 入口網站：按一下命名空間 [概觀] 刀鋒視窗中的主題名稱。</span><span class="sxs-lookup"><span data-stu-id="a9a37-149">Run the program, and check the Azure portal: click the name of your topic in the namespace **Overview** blade.</span></span> <span data-ttu-id="a9a37-150">主題 [Essentials] 刀鋒視窗即會顯示。</span><span class="sxs-lookup"><span data-stu-id="a9a37-150">The topic **Essentials** blade is displayed.</span></span> <span data-ttu-id="a9a37-151">請注意，在靠近刀鋒視窗底部所列的訂用帳戶中，每個訂用帳戶的**訊息計數**值現在應該是 1。</span><span class="sxs-lookup"><span data-stu-id="a9a37-151">In the subscription(s) listed near the bottom of the blade, notice that the **Message Count** value for each subscription should now be 1.</span></span> <span data-ttu-id="a9a37-152">每次執行傳送者應用程式而未擷取訊息 (如下一節所述)，這個值就會增加 1。</span><span class="sxs-lookup"><span data-stu-id="a9a37-152">Each time you run the sender application without retrieving the messages (as described in the next section), this value increases by 1.</span></span> <span data-ttu-id="a9a37-153">也請注意，每當應用程式新增訊息至主題/訂用帳戶，主題目前的大小就會讓 [Essentials] 刀鋒視窗上的**目前**值增加。</span><span class="sxs-lookup"><span data-stu-id="a9a37-153">Also note that the current size of the topic increments the **Current** value on the **Essentials** blade each time the app adds a message to the topic/subscription.</span></span>
   
      ![訊息大小][topic-message]

## <a name="5-receive-messages-from-the-subscription"></a><span data-ttu-id="a9a37-155">5.自訂用帳戶接收訊息</span><span class="sxs-lookup"><span data-stu-id="a9a37-155">5. Receive messages from the subscription</span></span>

1. <span data-ttu-id="a9a37-156">若要接收您剛傳送的訊息，請建立新的主控台應用程式，並和上面的傳送者應用程式類似，新增服務匯流排 NuGet 套件的參考。</span><span class="sxs-lookup"><span data-stu-id="a9a37-156">To receive the message or messages you just sent, create a new console application and add a reference to the Service Bus NuGet package, similar to the previous sender application.</span></span>
2. <span data-ttu-id="a9a37-157">在 Program.cs 檔案開頭處新增以下 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="a9a37-157">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="a9a37-158">將下列程式碼新增至 `Main` 方法。</span><span class="sxs-lookup"><span data-stu-id="a9a37-158">Add the following code to the `Main` method.</span></span> <span data-ttu-id="a9a37-159">將 `connectionString` 變數設定為建立命名空間時取得的連接字串，並將 `topicName` 設定為建立主題時使用的名稱。</span><span class="sxs-lookup"><span data-stu-id="a9a37-159">Set the `connectionString` variable to the connection string you obtained when creating the namespace, and set `topicName` to the name that you used when creating the topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER to exit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="a9a37-160">Program.cs 檔案看起來應該會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="a9a37-160">Here is what your Program.cs file should look like:</span></span>
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithTopics
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var topicName = "<your topic name>";
   
          var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
          client.OnMessage(message =>
          {
            Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
            Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
          });

          Console.WriteLine("Press ENTER to exit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. <span data-ttu-id="a9a37-161">執行程式，並再次檢查入口網站。</span><span class="sxs-lookup"><span data-stu-id="a9a37-161">Run the program, and check the portal again.</span></span> <span data-ttu-id="a9a37-162">請注意，**訊息計數**和**目前**值現在是 0。</span><span class="sxs-lookup"><span data-stu-id="a9a37-162">Notice that the **Message Count** and **Current** values are now 0.</span></span>
   
    ![主題長度][topic-message-receive]

<span data-ttu-id="a9a37-164">恭喜！</span><span class="sxs-lookup"><span data-stu-id="a9a37-164">Congratulations!</span></span> <span data-ttu-id="a9a37-165">您現在已建立主題和訂用帳戶，傳送一則訊息並接收該訊息。</span><span class="sxs-lookup"><span data-stu-id="a9a37-165">You have now created a topic and subscription, sent a message, and received that message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9a37-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a9a37-166">Next steps</span></span>

<span data-ttu-id="a9a37-167">查看 [GitHub 存放庫以及範例](https://github.com/Azure/azure-service-bus/tree/master/samples)，其中會展示一些更進階的服務匯流排傳訊功能。</span><span class="sxs-lookup"><span data-stu-id="a9a37-167">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of the more advanced features of Service Bus messaging.</span></span>

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/nuget-package.png
[topic-message]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message.png
[topic-message-receive]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message-receive.png
[createtopic1]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic1.png
[createtopic2]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic2.png
[createtopic3]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic3.png
[createtopic4]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic4.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
[azure-portal]: https://portal.azure.com
