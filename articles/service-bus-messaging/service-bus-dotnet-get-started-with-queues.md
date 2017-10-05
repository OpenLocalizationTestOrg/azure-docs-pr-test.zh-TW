---
title: "開始使用 Azure 服務匯流排佇列 | Microsoft Docs"
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
ms.openlocfilehash: 99a377db6341d90d263b98e14227db61dd9beabd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-service-bus-queues"></a><span data-ttu-id="363a3-103">開始使用服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="363a3-103">Get started with Service Bus queues</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="363a3-104">將會完成的工作</span><span class="sxs-lookup"><span data-stu-id="363a3-104">What will be accomplished</span></span>
<span data-ttu-id="363a3-105">本教學課程涵蓋下列步驟：</span><span class="sxs-lookup"><span data-stu-id="363a3-105">This tutorial covers the following steps:</span></span>

1. <span data-ttu-id="363a3-106">使用 Azure 入口網站建立服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="363a3-106">Create a Service Bus namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="363a3-107">使用 Azure 入口網站建立服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="363a3-107">Create a Service Bus queue, using the Azure portal.</span></span>
3. <span data-ttu-id="363a3-108">撰寫主控台應用程式來傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="363a3-108">Write a console application to send a message.</span></span>
4. <span data-ttu-id="363a3-109">撰寫主控台應用程式以接收上一個步驟中傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="363a3-109">Write a console application to receive the messages sent in the previous step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="363a3-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="363a3-110">Prerequisites</span></span>
1. <span data-ttu-id="363a3-111">[Visual Studio 2015 或更新版本](http://www.visualstudio.com)。</span><span class="sxs-lookup"><span data-stu-id="363a3-111">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="363a3-112">本教學課程中的範例使用 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="363a3-112">The examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="363a3-113">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="363a3-113">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="363a3-114">1.使用 Azure 入口網站建立命名空間</span><span class="sxs-lookup"><span data-stu-id="363a3-114">1. Create a namespace using the Azure portal</span></span>
<span data-ttu-id="363a3-115">如果您已建立服務匯流排傳訊命名空間，請跳至[使用 Azure 入口網站建立佇列](#2-create-a-queue-using-the-azure-portal)一節。</span><span class="sxs-lookup"><span data-stu-id="363a3-115">If you've already created a Service Bus Messaging namespace, jump to the [Create a queue using the Azure portal](#2-create-a-queue-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-the-azure-portal"></a><span data-ttu-id="363a3-116">2.使用 Azure 入口網站建立佇列</span><span class="sxs-lookup"><span data-stu-id="363a3-116">2. Create a queue using the Azure portal</span></span>
<span data-ttu-id="363a3-117">如果您已經建立服務匯流排佇列，請跳至[將訊息傳送至佇列](#3-send-messages-to-the-queue)一節。</span><span class="sxs-lookup"><span data-stu-id="363a3-117">If you have already created a Service Bus queue, jump to the [Send messages to the queue](#3-send-messages-to-the-queue) section.</span></span>

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-to-the-queue"></a><span data-ttu-id="363a3-118">3.將訊息傳送到佇列</span><span class="sxs-lookup"><span data-stu-id="363a3-118">3. Send messages to the queue</span></span>
<span data-ttu-id="363a3-119">為了將訊息傳送到佇列，我們使用 Visual Studio 撰寫 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="363a3-119">To send messages to the queue, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="363a3-120">建立主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="363a3-120">Create a console application</span></span>

<span data-ttu-id="363a3-121">啟動 Visual Studio，並建立新的**主控台應用程式 (.NET Framework)** 專案。</span><span class="sxs-lookup"><span data-stu-id="363a3-121">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-the-service-bus-nuget-package"></a><span data-ttu-id="363a3-122">新增服務匯流排 NuGet 封裝</span><span class="sxs-lookup"><span data-stu-id="363a3-122">Add the Service Bus NuGet package</span></span>
1. <span data-ttu-id="363a3-123">以滑鼠右鍵按一下新建立的專案，然後選取 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="363a3-123">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="363a3-124">按一下 [瀏覽] 索引標籤，搜尋 [Microsoft Azure 服務匯流排]，然後選取 [WindowsAzure.ServiceBus] 項目。</span><span class="sxs-lookup"><span data-stu-id="363a3-124">Click the **Browse** tab, search for **Microsoft Azure Service Bus**, and then select the **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="363a3-125">按一下 [安裝]  完成安裝作業，然後關閉此對話方塊。</span><span class="sxs-lookup"><span data-stu-id="363a3-125">Click **Install** to complete the installation, then close this dialog box.</span></span>
   
    ![選取 NuGet 封裝][nuget-pkg]

### <a name="write-some-code-to-send-a-message-to-the-queue"></a><span data-ttu-id="363a3-127">撰寫一些程式碼來將訊息傳送到佇列</span><span class="sxs-lookup"><span data-stu-id="363a3-127">Write some code to send a message to the queue</span></span>
1. <span data-ttu-id="363a3-128">在 Program.cs 檔案開頭處新增以下 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="363a3-128">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="363a3-129">將下列程式碼新增至 `Main` 方法。</span><span class="sxs-lookup"><span data-stu-id="363a3-129">Add the following code to the `Main` method.</span></span> <span data-ttu-id="363a3-130">將 `connectionString` 變數設定為建立命名空間時取得的連接字串，並將 `queueName` 設定為建立佇列時使用的佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="363a3-130">Set the `connectionString` variable to the connection string that you obtained when creating the namespace, and set `queueName` to the queue name that you used when creating the queue.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER to exit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="363a3-131">Program.cs 檔案看起來應該會像下面這樣。</span><span class="sxs-lookup"><span data-stu-id="363a3-131">Here is what your Program.cs file should look like.</span></span>
   
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

                Console.WriteLine("Message successfully sent! Press ENTER to exit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. <span data-ttu-id="363a3-132">執行程式，並檢查 Azure 入口網站：按一下命名空間 [概觀] 刀鋒視窗中的佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="363a3-132">Run the program, and check the Azure portal: click the name of your queue in the namespace **Overview** blade.</span></span> <span data-ttu-id="363a3-133">佇列 [Essentials] 刀鋒視窗即會顯示。</span><span class="sxs-lookup"><span data-stu-id="363a3-133">The queue **Essentials** blade is displayed.</span></span> <span data-ttu-id="363a3-134">請注意，**使用中訊息計數**值現在應該是 1。</span><span class="sxs-lookup"><span data-stu-id="363a3-134">Notice that the **Active Message Count** value should now be 1.</span></span> <span data-ttu-id="363a3-135">每次執行傳送者應用程式而未擷取訊息時，這個值就會增加 1。</span><span class="sxs-lookup"><span data-stu-id="363a3-135">Each time you run the sender application without retrieving the messages, this value increases by 1.</span></span> <span data-ttu-id="363a3-136">也請注意，每當應用程式在佇列中新增訊息時，佇列目前的大小就會增加。</span><span class="sxs-lookup"><span data-stu-id="363a3-136">Also note that the current size of the queue increments each time the app adds a message to the queue.</span></span>
   
      ![訊息大小][queue-message]

## <a name="4-receive-messages-from-the-queue"></a><span data-ttu-id="363a3-138">4.從佇列接收訊息</span><span class="sxs-lookup"><span data-stu-id="363a3-138">4. Receive messages from the queue</span></span>

1. <span data-ttu-id="363a3-139">若要接收您剛傳送的訊息，請建立新的主控台應用程式，並和上面的傳送者應用程式類似，新增服務匯流排 NuGet 套件的參考。</span><span class="sxs-lookup"><span data-stu-id="363a3-139">To receive the messages you just sent, create a new console application and add a reference to the Service Bus NuGet package, similar to the previous sender application.</span></span>
2. <span data-ttu-id="363a3-140">在 Program.cs 檔案開頭處新增以下 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="363a3-140">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="363a3-141">將下列程式碼新增至 `Main` 方法。</span><span class="sxs-lookup"><span data-stu-id="363a3-141">Add the following code to the `Main` method.</span></span> <span data-ttu-id="363a3-142">將 `connectionString` 變數設定為建立命名空間時取得的連接字串，並將 `queueName` 設定為建立佇列時使用的佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="363a3-142">Set the `connectionString` variable to the connection string that was obtained when creating the namespace, and set `queueName` to the queue name that you used when creating the queue.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER to exit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="363a3-143">Program.cs 檔案看起來應該會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="363a3-143">Here is what your Program.cs file should look like:</span></span>
   
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

          Console.WriteLine("Press ENTER to exit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. <span data-ttu-id="363a3-144">執行程式，並再次檢查入口網站。</span><span class="sxs-lookup"><span data-stu-id="363a3-144">Run the program, and check the portal again.</span></span> <span data-ttu-id="363a3-145">請注意，**使用中訊息計數**和**目前**值現在是 0。</span><span class="sxs-lookup"><span data-stu-id="363a3-145">Notice that the **Active Message Count** and **Current** values are now 0.</span></span>
   
    ![佇列長度][queue-message-receive]

<span data-ttu-id="363a3-147">恭喜！</span><span class="sxs-lookup"><span data-stu-id="363a3-147">Congratulations!</span></span> <span data-ttu-id="363a3-148">您現已建立佇列、傳送訊息和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="363a3-148">You have now created a queue, sent a message, and received a message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="363a3-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="363a3-149">Next steps</span></span>

<span data-ttu-id="363a3-150">查看 [GitHub 存放庫以及範例](https://github.com/Azure/azure-service-bus/tree/master/samples)，其中會展示一些更進階的服務匯流排傳訊功能。</span><span class="sxs-lookup"><span data-stu-id="363a3-150">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of the more advanced features of Service Bus messaging.</span></span>

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
