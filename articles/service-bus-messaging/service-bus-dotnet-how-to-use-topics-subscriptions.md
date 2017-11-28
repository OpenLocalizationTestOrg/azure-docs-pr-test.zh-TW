---
title: "aaaGet 開始使用 Azure 服務匯流排主題和訂用帳戶 |Microsoft 文件"
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
ms.openlocfilehash: 619d602599d97ecff2ded0681a383b19f1a8b7ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-topics"></a><span data-ttu-id="afa66-103">開始使用服務匯流排主題</span><span class="sxs-lookup"><span data-stu-id="afa66-103">Get started with Service Bus topics</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="afa66-104">將會完成的工作</span><span class="sxs-lookup"><span data-stu-id="afa66-104">What will be accomplished</span></span>

<span data-ttu-id="afa66-105">本教學課程涵蓋 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="afa66-105">This tutorial covers hello following steps:</span></span>

1. <span data-ttu-id="afa66-106">建立服務匯流排命名空間，使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="afa66-106">Create a Service Bus namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="afa66-107">建立服務匯流排主題，使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="afa66-107">Create a Service Bus topic, using hello Azure portal.</span></span>
3. <span data-ttu-id="afa66-108">建立服務匯流排訂用帳戶 toothat 主題，使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="afa66-108">Create a Service Bus subscription toothat topic, using hello Azure portal.</span></span>
4. <span data-ttu-id="afa66-109">撰寫主控台應用程式 toosend 訊息 toohello 主題。</span><span class="sxs-lookup"><span data-stu-id="afa66-109">Write a console application toosend a message toohello topic.</span></span>
5. <span data-ttu-id="afa66-110">撰寫從 hello 訂用帳戶的主控台應用程式 tooreceive 該訊息。</span><span class="sxs-lookup"><span data-stu-id="afa66-110">Write a console application tooreceive that message from hello subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afa66-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="afa66-111">Prerequisites</span></span>

1. <span data-ttu-id="afa66-112">[Visual Studio 2015 或更新版本](http://www.visualstudio.com)。</span><span class="sxs-lookup"><span data-stu-id="afa66-112">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="afa66-113">在此教學課程中的 hello 範例會使用 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="afa66-113">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="afa66-114">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="afa66-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="afa66-115">1.建立命名空間使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="afa66-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="afa66-116">如果您已經建立 Service Bus 訊息的命名空間，跳 toohello[建立使用 hello Azure 入口網站主題](#2-create-a-topic-using-the-azure-portal)> 一節。</span><span class="sxs-lookup"><span data-stu-id="afa66-116">If you have already created a Service Bus Messaging namespace, jump toohello [Create a topic using hello Azure portal](#2-create-a-topic-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-hello-azure-portal"></a><span data-ttu-id="afa66-117">2.建立使用 hello Azure 入口網站主題</span><span class="sxs-lookup"><span data-stu-id="afa66-117">2. Create a topic using hello Azure portal</span></span>

1. <span data-ttu-id="afa66-118">登入 toohello [Azure 入口網站][azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="afa66-118">Log on toohello [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="afa66-119">在 hello hello 入口網站的左側瀏覽窗格中按一下**Service Bus** (如果您沒有看到**Service Bus**，按一下 **更多服務**)。</span><span class="sxs-lookup"><span data-stu-id="afa66-119">In hello left navigation pane of hello portal, click **Service Bus** (if you don't see **Service Bus**, click **More services**).</span></span>
3. <span data-ttu-id="afa66-120">按一下您想在其中要 toocreate hello 主題 hello 命名空間。</span><span class="sxs-lookup"><span data-stu-id="afa66-120">Click hello namespace in which you would like toocreate hello topic.</span></span> <span data-ttu-id="afa66-121">hello 命名空間概觀刀鋒視窗會出現：</span><span class="sxs-lookup"><span data-stu-id="afa66-121">hello namespace overview blade appears:</span></span>
   
    ![建立主題][createtopic1]
4. <span data-ttu-id="afa66-123">在 hello**服務匯流排命名空間**刀鋒視窗中，按一下 **主題**，然後按一下 **新增主題**。</span><span class="sxs-lookup"><span data-stu-id="afa66-123">In hello **Service Bus namespace** blade, click **Topics**, then click **Add topic**.</span></span>
   
    ![選取主題][createtopic2]
5. <span data-ttu-id="afa66-125">輸入 hello 主題的名稱，然後取消選取 hello**啟用資料分割**選項。</span><span class="sxs-lookup"><span data-stu-id="afa66-125">Enter a name for hello topic, and uncheck hello **Enable partitioning** option.</span></span> <span data-ttu-id="afa66-126">將 hello 保留其預設值與其他選項。</span><span class="sxs-lookup"><span data-stu-id="afa66-126">Leave hello other options with their default values.</span></span>
   
    ![選取新增][createtopic3]
6. <span data-ttu-id="afa66-128">在 hello hello 刀鋒視窗底部，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="afa66-128">At hello bottom of hello blade, click **Create**.</span></span>

## <a name="3-create-a-subscription-toohello-topic"></a><span data-ttu-id="afa66-129">3.建立訂用帳戶 toohello 主題</span><span class="sxs-lookup"><span data-stu-id="afa66-129">3. Create a subscription toohello topic</span></span>

1. <span data-ttu-id="afa66-130">在 hello 入口網站的資源 窗格中，按一下您在步驟 1 所建立的 hello 命名空間然後按一下您在步驟 2 中建立的 hello 主題的名稱。</span><span class="sxs-lookup"><span data-stu-id="afa66-130">In hello portal resources pane, click hello namespace you created in step 1, then click name of hello topic you created in step 2.</span></span>
2. <span data-ttu-id="afa66-131">Hello 頂端 hello 概觀窗格中，按一下 hello 加上登入接著太**訂用帳戶**tooadd 訂用帳戶 toothis 主題。</span><span class="sxs-lookup"><span data-stu-id="afa66-131">A hello top of hello overview pane, click hello plus sign next too**Subscription** tooadd a subscription toothis topic.</span></span>

    ![建立訂用帳戶][createtopic4]

3. <span data-ttu-id="afa66-133">輸入 hello 訂用帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="afa66-133">Enter a name for hello subscription.</span></span> <span data-ttu-id="afa66-134">將 hello 保留其預設值與其他選項。</span><span class="sxs-lookup"><span data-stu-id="afa66-134">Leave hello other options with their default values.</span></span>

## <a name="4-send-messages-toohello-topic"></a><span data-ttu-id="afa66-135">4.傳送訊息 toohello 主題</span><span class="sxs-lookup"><span data-stu-id="afa66-135">4. Send messages toohello topic</span></span>

<span data-ttu-id="afa66-136">toosend 訊息 toohello 主題中，我們會撰寫 C# 主控台應用程式使用 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="afa66-136">toosend messages toohello topic, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="afa66-137">建立主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="afa66-137">Create a console application</span></span>

<span data-ttu-id="afa66-138">啟動 Visual Studio，並建立新的**主控台應用程式 (.NET Framework)** 專案。</span><span class="sxs-lookup"><span data-stu-id="afa66-138">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-hello-service-bus-nuget-package"></a><span data-ttu-id="afa66-139">加入 hello 服務匯流排 NuGet 封裝</span><span class="sxs-lookup"><span data-stu-id="afa66-139">Add hello Service Bus NuGet package</span></span>

1. <span data-ttu-id="afa66-140">Hello 新建立的專案上按一下滑鼠右鍵，然後選取**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="afa66-140">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="afa66-141">按一下 hello**瀏覽**索引標籤上，搜尋**Microsoft Azure 服務匯流排**，然後選取 hello **WindowsAzure.ServiceBus**項目。</span><span class="sxs-lookup"><span data-stu-id="afa66-141">Click hello **Browse** tab, search for **Microsoft Azure Service Bus**, and then select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="afa66-142">按一下**安裝**toocomplete hello 安裝，然後關閉此對話方塊。</span><span class="sxs-lookup"><span data-stu-id="afa66-142">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
   
    ![選取 NuGet 封裝][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-topic"></a><span data-ttu-id="afa66-144">撰寫一些程式碼 toosend 訊息 toohello 主題</span><span class="sxs-lookup"><span data-stu-id="afa66-144">Write some code toosend a message toohello topic</span></span>

1. <span data-ttu-id="afa66-145">新增下列 hello `using` hello Program.cs 檔案的陳述式 toohello 頂端。</span><span class="sxs-lookup"><span data-stu-id="afa66-145">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="afa66-146">新增下列程式碼 toohello hello`Main`方法。</span><span class="sxs-lookup"><span data-stu-id="afa66-146">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="afa66-147">設定 hello`connectionString`變數 toohello 連接字串時建立 hello 命名空間中，取得及設定`topicName`toohello 建立 hello 主題時，您所使用的名稱。</span><span class="sxs-lookup"><span data-stu-id="afa66-147">Set hello `connectionString` variable toohello connection string that you obtained when creating hello namespace, and set `topicName` toohello name that you used when creating hello topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="afa66-148">Program.cs 檔案看起來應該會像下面這樣。</span><span class="sxs-lookup"><span data-stu-id="afa66-148">Here is what your Program.cs file should look like.</span></span>
   
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

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. <span data-ttu-id="afa66-149">執行 hello 程式並檢查 hello Azure 入口網站： 按一下主題 hello 命名空間中的 hello 名稱**概觀**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="afa66-149">Run hello program, and check hello Azure portal: click hello name of your topic in hello namespace **Overview** blade.</span></span> <span data-ttu-id="afa66-150">hello 主題**Essentials**刀鋒視窗會顯示。</span><span class="sxs-lookup"><span data-stu-id="afa66-150">hello topic **Essentials** blade is displayed.</span></span> <span data-ttu-id="afa66-151">在 hello 訂閱 hello hello 刀鋒視窗的底部列，請注意該 hello**訊息計數**每個訂用帳戶現在應該為 1 的值。</span><span class="sxs-lookup"><span data-stu-id="afa66-151">In hello subscription(s) listed near hello bottom of hello blade, notice that hello **Message Count** value for each subscription should now be 1.</span></span> <span data-ttu-id="afa66-152">每次執行 hello 寄件者應用程式，而不擷取 hello 訊息 （如 hello 下一節中所述），這個值會增加 1。</span><span class="sxs-lookup"><span data-stu-id="afa66-152">Each time you run hello sender application without retrieving hello messages (as described in hello next section), this value increases by 1.</span></span> <span data-ttu-id="afa66-153">也請注意該 hello 的目前大小的 hello 主題遞增 hello**目前**上 hello 值**Essentials**刀鋒視窗每次 hello 應用程式加入訊息的 toohello 主題/訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="afa66-153">Also note that hello current size of hello topic increments hello **Current** value on hello **Essentials** blade each time hello app adds a message toohello topic/subscription.</span></span>
   
      ![訊息大小][topic-message]

## <a name="5-receive-messages-from-hello-subscription"></a><span data-ttu-id="afa66-155">5.從 hello 訂閱接收訊息</span><span class="sxs-lookup"><span data-stu-id="afa66-155">5. Receive messages from hello subscription</span></span>

1. <span data-ttu-id="afa66-156">tooreceive hello 訊息或只傳送的訊息建立新的主控台應用程式，並加入參考 toohello 服務匯流排 NuGet 封裝，類似 toohello 先前寄件者應用程式。</span><span class="sxs-lookup"><span data-stu-id="afa66-156">tooreceive hello message or messages you just sent, create a new console application and add a reference toohello Service Bus NuGet package, similar toohello previous sender application.</span></span>
2. <span data-ttu-id="afa66-157">新增下列 hello `using` hello Program.cs 檔案的陳述式 toohello 頂端。</span><span class="sxs-lookup"><span data-stu-id="afa66-157">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="afa66-158">新增下列程式碼 toohello hello`Main`方法。</span><span class="sxs-lookup"><span data-stu-id="afa66-158">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="afa66-159">設定 hello`connectionString`變數 toohello 連接字串時建立 hello 命名空間中，取得並設定您`topicName`toohello 建立 hello 主題時，您所使用的名稱。</span><span class="sxs-lookup"><span data-stu-id="afa66-159">Set hello `connectionString` variable toohello connection string you obtained when creating hello namespace, and set `topicName` toohello name that you used when creating hello topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="afa66-160">Program.cs 檔案看起來應該會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="afa66-160">Here is what your Program.cs file should look like:</span></span>
   
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

          Console.WriteLine("Press ENTER tooexit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. <span data-ttu-id="afa66-161">執行 hello 程式並再次檢查 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="afa66-161">Run hello program, and check hello portal again.</span></span> <span data-ttu-id="afa66-162">請注意該 hello**訊息計數**和**目前**值現在是 0。</span><span class="sxs-lookup"><span data-stu-id="afa66-162">Notice that hello **Message Count** and **Current** values are now 0.</span></span>
   
    ![主題長度][topic-message-receive]

<span data-ttu-id="afa66-164">恭喜！</span><span class="sxs-lookup"><span data-stu-id="afa66-164">Congratulations!</span></span> <span data-ttu-id="afa66-165">您現在已建立主題和訂用帳戶，傳送一則訊息並接收該訊息。</span><span class="sxs-lookup"><span data-stu-id="afa66-165">You have now created a topic and subscription, sent a message, and received that message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afa66-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="afa66-166">Next steps</span></span>

<span data-ttu-id="afa66-167">請查看我們[範例 GitHub 儲存機制](https://github.com/Azure/azure-service-bus/tree/master/samples)，示範一些更進階的功能的服務匯流排傳訊的 hello。</span><span class="sxs-lookup"><span data-stu-id="afa66-167">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of hello more advanced features of Service Bus messaging.</span></span>

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
