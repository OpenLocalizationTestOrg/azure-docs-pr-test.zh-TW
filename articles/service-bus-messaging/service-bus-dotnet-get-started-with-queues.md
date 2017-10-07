---
title: "開始使用 Azure Service Bus 佇列的 aaaGet |Microsoft 文件"
description: "撰寫使用服務匯流排傳訊佇列的 C# 主控台應用程式。"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68a34c00-5600-43f6-bbcc-fea599d500da
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/26/2017
ms.author: sethm
ms.openlocfilehash: eaa362ab0eabd2427977398c1deab5dc00105ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-queues"></a><span data-ttu-id="472b0-103">開始使用服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="472b0-103">Get started with Service Bus queues</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="472b0-104">將會完成的工作</span><span class="sxs-lookup"><span data-stu-id="472b0-104">What will be accomplished</span></span>
<span data-ttu-id="472b0-105">本教學課程涵蓋 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="472b0-105">This tutorial covers hello following steps:</span></span>

1. <span data-ttu-id="472b0-106">建立服務匯流排命名空間，使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="472b0-106">Create a Service Bus namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="472b0-107">建立服務匯流排佇列，使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="472b0-107">Create a Service Bus queue, using hello Azure portal.</span></span>
3. <span data-ttu-id="472b0-108">訊息寫入主控台應用程式 toosend。</span><span class="sxs-lookup"><span data-stu-id="472b0-108">Write a console application toosend a message.</span></span>
4. <span data-ttu-id="472b0-109">撰寫主控台應用程式 tooreceive hello hello 上一個步驟中傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="472b0-109">Write a console application tooreceive hello messages sent in hello previous step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="472b0-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="472b0-110">Prerequisites</span></span>
1. <span data-ttu-id="472b0-111">[Visual Studio 2015 或更新版本](http://www.visualstudio.com)。</span><span class="sxs-lookup"><span data-stu-id="472b0-111">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="472b0-112">在此教學課程中的 hello 範例會使用 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="472b0-112">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="472b0-113">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="472b0-113">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="472b0-114">1.建立命名空間使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="472b0-114">1. Create a namespace using hello Azure portal</span></span>
<span data-ttu-id="472b0-115">如果您已經建立 Service Bus 訊息的命名空間，跳 toohello[建立佇列，使用 Azure 入口網站 hello](#2-create-a-queue-using-the-azure-portal) > 一節。</span><span class="sxs-lookup"><span data-stu-id="472b0-115">If you've already created a Service Bus Messaging namespace, jump toohello [Create a queue using hello Azure portal](#2-create-a-queue-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-hello-azure-portal"></a><span data-ttu-id="472b0-116">2.建立佇列，使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="472b0-116">2. Create a queue using hello Azure portal</span></span>
<span data-ttu-id="472b0-117">如果您已經建立 Service Bus 佇列，跳 toohello[傳送訊息 toohello 佇列](#3-send-messages-to-the-queue)> 一節。</span><span class="sxs-lookup"><span data-stu-id="472b0-117">If you have already created a Service Bus queue, jump toohello [Send messages toohello queue](#3-send-messages-to-the-queue) section.</span></span>

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-toohello-queue"></a><span data-ttu-id="472b0-118">3.傳送訊息 toohello 佇列</span><span class="sxs-lookup"><span data-stu-id="472b0-118">3. Send messages toohello queue</span></span>
<span data-ttu-id="472b0-119">toosend 訊息 toohello 佇列中，我們會撰寫 C# 主控台應用程式使用 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="472b0-119">toosend messages toohello queue, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="472b0-120">建立主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="472b0-120">Create a console application</span></span>

<span data-ttu-id="472b0-121">啟動 Visual Studio，並建立新的**主控台應用程式 (.NET Framework)** 專案。</span><span class="sxs-lookup"><span data-stu-id="472b0-121">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-hello-service-bus-nuget-package"></a><span data-ttu-id="472b0-122">加入 hello 服務匯流排 NuGet 封裝</span><span class="sxs-lookup"><span data-stu-id="472b0-122">Add hello Service Bus NuGet package</span></span>
1. <span data-ttu-id="472b0-123">Hello 新建立的專案上按一下滑鼠右鍵，然後選取**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="472b0-123">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="472b0-124">按一下 hello**瀏覽**索引標籤上，搜尋**Microsoft Azure 服務匯流排**，然後選取 hello **WindowsAzure.ServiceBus**項目。</span><span class="sxs-lookup"><span data-stu-id="472b0-124">Click hello **Browse** tab, search for **Microsoft Azure Service Bus**, and then select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="472b0-125">按一下**安裝**toocomplete hello 安裝，然後關閉此對話方塊。</span><span class="sxs-lookup"><span data-stu-id="472b0-125">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
   
    ![選取 NuGet 封裝][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-queue"></a><span data-ttu-id="472b0-127">撰寫一些程式碼 toosend 訊息 toohello 佇列</span><span class="sxs-lookup"><span data-stu-id="472b0-127">Write some code toosend a message toohello queue</span></span>
1. <span data-ttu-id="472b0-128">新增下列 hello `using` hello Program.cs 檔案的陳述式 toohello 頂端。</span><span class="sxs-lookup"><span data-stu-id="472b0-128">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="472b0-129">新增下列程式碼 toohello hello`Main`方法。</span><span class="sxs-lookup"><span data-stu-id="472b0-129">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="472b0-130">設定 hello`connectionString`變數 toohello 連接字串時建立 hello 命名空間中，取得及設定`queueName`toohello 建立 hello 佇列時所使用的佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="472b0-130">Set hello `connectionString` variable toohello connection string that you obtained when creating hello namespace, and set `queueName` toohello queue name that you used when creating hello queue.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="472b0-131">Program.cs 檔案看起來應該會像下面這樣。</span><span class="sxs-lookup"><span data-stu-id="472b0-131">Here is what your Program.cs file should look like.</span></span>
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.ServiceBus.Messaging;

    namespace qsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var queueName = "<your queue name>";

                var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. <span data-ttu-id="472b0-132">執行 hello 程式並檢查 hello Azure 入口網站： 按一下您的佇列 hello 命名空間中的 hello 名稱**概觀**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="472b0-132">Run hello program, and check hello Azure portal: click hello name of your queue in hello namespace **Overview** blade.</span></span> <span data-ttu-id="472b0-133">hello 佇列**Essentials**刀鋒視窗會顯示。</span><span class="sxs-lookup"><span data-stu-id="472b0-133">hello queue **Essentials** blade is displayed.</span></span> <span data-ttu-id="472b0-134">請注意該 hello**作用中的訊息計數**值現在應該是 1。</span><span class="sxs-lookup"><span data-stu-id="472b0-134">Notice that hello **Active Message Count** value should now be 1.</span></span> <span data-ttu-id="472b0-135">每的次您執行 hello 寄件者應用程式而不擷取 hello 訊息，這個值會增加 1。</span><span class="sxs-lookup"><span data-stu-id="472b0-135">Each time you run hello sender application without retrieving hello messages, this value increases by 1.</span></span> <span data-ttu-id="472b0-136">也請注意 hello hello 佇列的目前的大小遞增每個時間 hello 應用程式會加入訊息 toohello 佇列。</span><span class="sxs-lookup"><span data-stu-id="472b0-136">Also note that hello current size of hello queue increments each time hello app adds a message toohello queue.</span></span>
   
      ![訊息大小][queue-message]

## <a name="4-receive-messages-from-hello-queue"></a><span data-ttu-id="472b0-138">4.從 hello 佇列接收訊息</span><span class="sxs-lookup"><span data-stu-id="472b0-138">4. Receive messages from hello queue</span></span>

1. <span data-ttu-id="472b0-139">只傳送 tooreceive hello 訊息建立新的主控台應用程式，並加入參考 toohello 服務匯流排 NuGet 封裝，類似 toohello 先前寄件者應用程式。</span><span class="sxs-lookup"><span data-stu-id="472b0-139">tooreceive hello messages you just sent, create a new console application and add a reference toohello Service Bus NuGet package, similar toohello previous sender application.</span></span>
2. <span data-ttu-id="472b0-140">新增下列 hello `using` hello Program.cs 檔案的陳述式 toohello 頂端。</span><span class="sxs-lookup"><span data-stu-id="472b0-140">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="472b0-141">新增下列程式碼 toohello hello`Main`方法。</span><span class="sxs-lookup"><span data-stu-id="472b0-141">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="472b0-142">設定 hello`connectionString`變數 toohello 連接字串時建立 hello 命名空間、 取得和設定`queueName`toohello 建立 hello 佇列時所使用的佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="472b0-142">Set hello `connectionString` variable toohello connection string that was obtained when creating hello namespace, and set `queueName` toohello queue name that you used when creating hello queue.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="472b0-143">Program.cs 檔案看起來應該會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="472b0-143">Here is what your Program.cs file should look like:</span></span>
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithQueues
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var queueName = "<your queue name>";
   
          var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
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
4. <span data-ttu-id="472b0-144">執行 hello 程式並再次檢查 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="472b0-144">Run hello program, and check hello portal again.</span></span> <span data-ttu-id="472b0-145">請注意該 hello**作用中的訊息計數**和**目前**值現在是 0。</span><span class="sxs-lookup"><span data-stu-id="472b0-145">Notice that hello **Active Message Count** and **Current** values are now 0.</span></span>
   
    ![佇列長度][queue-message-receive]

<span data-ttu-id="472b0-147">恭喜！</span><span class="sxs-lookup"><span data-stu-id="472b0-147">Congratulations!</span></span> <span data-ttu-id="472b0-148">您現已建立佇列、傳送訊息和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="472b0-148">You have now created a queue, sent a message, and received a message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="472b0-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="472b0-149">Next steps</span></span>

<span data-ttu-id="472b0-150">請查看我們[範例 GitHub 儲存機制](https://github.com/Azure/azure-service-bus/tree/master/samples)，示範一些更進階的功能的服務匯流排傳訊的 hello。</span><span class="sxs-lookup"><span data-stu-id="472b0-150">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of hello more advanced features of Service Bus messaging.</span></span>

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
