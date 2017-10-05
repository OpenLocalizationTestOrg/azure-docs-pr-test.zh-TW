---
title: "使用 .NET Standard 傳送事件至 Azure 事件中樞 | Microsoft Docs"
description: "開始在 .NET Standard 中傳送事件至事件中樞"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: 8af9d70965c1c9ad8c49b7d2bb04244fc207058d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-sending-messages-to-azure-event-hubs-in-net-standard"></a><span data-ttu-id="c4f85-103">開始在 .NET Standard 中傳送訊息至 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="c4f85-103">Get started sending messages to Azure Event Hubs in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="c4f85-104">您可在 [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) 上取得此範例。</span><span class="sxs-lookup"><span data-stu-id="c4f85-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span></span>

<span data-ttu-id="c4f85-105">本教學課程說明如何撰寫一個 .NET Core 主控台應用程式，以將一組訊息傳送到事件中樞。</span><span class="sxs-lookup"><span data-stu-id="c4f85-105">This tutorial shows how to write a .NET Core console application that sends a set of messages to an event hub.</span></span> <span data-ttu-id="c4f85-106">您可以依現狀執行 [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) 解決方案，其中以您事件中樞的值來取代 `EhConnectionString` 和 `EhEntityPath` 字串。</span><span class="sxs-lookup"><span data-stu-id="c4f85-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solution as-is, replacing the `EhConnectionString` and `EhEntityPath` strings with your event hub values.</span></span> <span data-ttu-id="c4f85-107">或者，您可以遵循本教學課程中的步驟，來建立自己的解決方案。</span><span class="sxs-lookup"><span data-stu-id="c4f85-107">Or you can follow the steps in this tutorial to create your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4f85-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="c4f85-108">Prerequisites</span></span>

* <span data-ttu-id="c4f85-109">[Microsoft Visual Studio 2015 或 2017](http://www.visualstudio.com)。</span><span class="sxs-lookup"><span data-stu-id="c4f85-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="c4f85-110">本教學課程中的範例使用 Visual Studio 2017，但也支援 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="c4f85-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="c4f85-111">[.NET Core Visual Studio 2015 或 2017 工具](http://www.microsoft.com/net/core)。</span><span class="sxs-lookup"><span data-stu-id="c4f85-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="c4f85-112">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c4f85-112">An Azure subscription.</span></span>
* <span data-ttu-id="c4f85-113">事件中樞命名空間。</span><span class="sxs-lookup"><span data-stu-id="c4f85-113">An event hub namespace.</span></span>

<span data-ttu-id="c4f85-114">為了將訊息傳送到事件中樞，我們將使用 Visual Studio 來撰寫一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4f85-114">To send messages to an event hub, we will use Visual Studio to write a C# console application.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="c4f85-115">建立事件中樞命名空間和事件中樞</span><span class="sxs-lookup"><span data-stu-id="c4f85-115">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="c4f85-116">第一個步驟是使用 [Azure 入口網站](https://portal.azure.com)來建立事件中樞類型的命名空間，然後取得您應用程式與事件中樞進行通訊所需的管理認證。</span><span class="sxs-lookup"><span data-stu-id="c4f85-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the event hub type, and obtain the management credentials that your application needs to communicate with the event hub.</span></span> <span data-ttu-id="c4f85-117">若要建立命名空間和事件中樞，請依照[這篇文章](event-hubs-create.md)中的程序操作，然後繼續進行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="c4f85-117">To create a namespace and an event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="c4f85-118">建立主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="c4f85-118">Create a console application</span></span>

<span data-ttu-id="c4f85-119">啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="c4f85-119">Start Visual Studio.</span></span> <span data-ttu-id="c4f85-120">從 [檔案] 功能表中，按一下 [新增]，再按 [專案]。</span><span class="sxs-lookup"><span data-stu-id="c4f85-120">From the **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="c4f85-121">建立 .NET Core 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4f85-121">Create a .NET Core console application.</span></span>

![新增專案][1]

## <a name="add-the-event-hubs-nuget-package"></a><span data-ttu-id="c4f85-123">新增事件中樞 NuGet 封裝</span><span class="sxs-lookup"><span data-stu-id="c4f85-123">Add the Event Hubs NuGet package</span></span>

<span data-ttu-id="c4f85-124">遵循下列幾個步驟，將 [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET 標準程式庫 NuGet 套件新增至您的專案：</span><span class="sxs-lookup"><span data-stu-id="c4f85-124">Add the [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard library NuGet package to your project by following these steps:</span></span> 

1. <span data-ttu-id="c4f85-125">以滑鼠右鍵按一下新建立的專案，然後選取 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="c4f85-125">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="c4f85-126">按一下 [瀏覽] 索引標籤，然後搜尋「Microsoft.Azure.EventHubs」並選取 [Microsoft.Azure.EventHubs] 套件。</span><span class="sxs-lookup"><span data-stu-id="c4f85-126">Click the **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select the **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="c4f85-127">按一下 [安裝]  完成安裝作業，然後關閉此對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c4f85-127">Click **Install** to complete the installation, then close this dialog box.</span></span>

## <a name="write-some-code-to-send-messages-to-the-event-hub"></a><span data-ttu-id="c4f85-128">撰寫一些程式碼以將訊息傳送到事件中樞</span><span class="sxs-lookup"><span data-stu-id="c4f85-128">Write some code to send messages to the event hub</span></span>

1. <span data-ttu-id="c4f85-129">在 Program.cs 檔案開頭處加入 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="c4f85-129">Add the following `using` statements to the top of the Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="c4f85-130">針對「事件中樞」連接字串和實體路徑 (個別事件中樞名稱)，將常數新增到 `Program` 類別。</span><span class="sxs-lookup"><span data-stu-id="c4f85-130">Add constants to the `Program` class for the Event Hubs connection string and entity path (individual event hub name).</span></span> <span data-ttu-id="c4f85-131">以建立事件中樞時所取得的適當值取代方括號中的預留位置。</span><span class="sxs-lookup"><span data-stu-id="c4f85-131">Replace the placeholders in brackets with the proper values that were obtained when creating the event hub.</span></span>

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. <span data-ttu-id="c4f85-132">將名為 `MainAsync` 的新方法新增到 `Program` 類別，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c4f85-132">Add a new method named `MainAsync` to the `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from the connection string, and sets the EntityPath.
        // Typically, the connection string should have the entity path in it, but for the sake of this simple scenario
        // we are using the connection string from the namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
    }
    ```

4. <span data-ttu-id="c4f85-133">將名為 `SendMessagesToEventHub` 的新方法新增到 `Program` 類別，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c4f85-133">Add a new method named `SendMessagesToEventHub` to the `Program` class, as follows:</span></span>

    ```csharp
    // Creates an event hub client and sends 100 messages to the event hub.
    private static async Task SendMessagesToEventHub(int numMessagesToSend)
    {
        for (var i = 0; i < numMessagesToSend; i++)
        {
            try
            {
                var message = $"Message {i}";
                Console.WriteLine($"Sending message: {message}");
                await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
            }
            catch (Exception exception)
            {
                Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
            }

            await Task.Delay(10);
        }

        Console.WriteLine($"{numMessagesToSend} messages sent.");
    }
    ```

5. <span data-ttu-id="c4f85-134">將下列程式碼行新增至 `Program` 類別中的 `Main` 方法。</span><span class="sxs-lookup"><span data-stu-id="c4f85-134">Add the following code to the `Main` method in the `Program` class.</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   <span data-ttu-id="c4f85-135">Program.cs 看起來應該會像下面這樣。</span><span class="sxs-lookup"><span data-stu-id="c4f85-135">Here is what your Program.cs should look like.</span></span>

    ```csharp
    namespace SampleSender
    {
        using System;
        using System.Text;
        using System.Threading.Tasks;
        using Microsoft.Azure.EventHubs;

        public class Program
        {
            private static EventHubClient eventHubClient;
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                // Creates an EventHubsConnectionStringBuilder object from the connection string, and sets the EntityPath.
                // Typically, the connection string should have the entity path in it, but for the sake of this simple scenario
                // we are using the connection string from the namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER to exit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages to the event hub.
            private static async Task SendMessagesToEventHub(int numMessagesToSend)
            {
                for (var i = 0; i < numMessagesToSend; i++)
                {
                    try
                    {
                        var message = $"Message {i}";
                        Console.WriteLine($"Sending message: {message}");
                        await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
                    }
                    catch (Exception exception)
                    {
                        Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
                    }

                    await Task.Delay(10);
                }

                Console.WriteLine($"{numMessagesToSend} messages sent.");
            }
        }
    }
    ```

6. <span data-ttu-id="c4f85-136">執行程式，並確定沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="c4f85-136">Run the program, and ensure that there are no errors.</span></span>

<span data-ttu-id="c4f85-137">恭喜！</span><span class="sxs-lookup"><span data-stu-id="c4f85-137">Congratulations!</span></span> <span data-ttu-id="c4f85-138">您現在已將傳送訊息到事件中樞。</span><span class="sxs-lookup"><span data-stu-id="c4f85-138">You have now sent messages to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4f85-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c4f85-139">Next steps</span></span>
<span data-ttu-id="c4f85-140">您可以造訪下列連結以深入了解事件中樞︰</span><span class="sxs-lookup"><span data-stu-id="c4f85-140">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="c4f85-141">從事件中樞接收事件</span><span class="sxs-lookup"><span data-stu-id="c4f85-141">Receive events from Event Hubs</span></span>](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [<span data-ttu-id="c4f85-142">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="c4f85-142">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="c4f85-143">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="c4f85-143">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="c4f85-144">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="c4f85-144">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
