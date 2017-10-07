---
title: "aaaSend 事件 tooAzure 使用標準.NET 的事件中心 |Microsoft 文件"
description: "以.NET 標準 tooEvent 中樞傳送事件開始"
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
ms.openlocfilehash: caa9747a8a72aa8e7aea1348a116f6e4b406460e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-sending-messages-tooazure-event-hubs-in-net-standard"></a><span data-ttu-id="3bf4c-103">開始傳送訊息的.NET 標準 tooAzure 事件中心</span><span class="sxs-lookup"><span data-stu-id="3bf4c-103">Get started sending messages tooAzure Event Hubs in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="3bf4c-104">您可在 [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) 上取得此範例。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span></span>

<span data-ttu-id="3bf4c-105">本教學課程會示範如何 toowrite.NET Core 主控台應用程式所傳送的一組訊息 tooan 事件中心。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-105">This tutorial shows how toowrite a .NET Core console application that sends a set of messages tooan event hub.</span></span> <span data-ttu-id="3bf4c-106">您可以執行 hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender)做為方案層，就取代 hello`EhConnectionString`和`EhEntityPath`字串以您的事件中樞值。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-106">You can run hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solution as-is, replacing hello `EhConnectionString` and `EhEntityPath` strings with your event hub values.</span></span> <span data-ttu-id="3bf4c-107">您可以遵循 hello 步驟在本教學課程 toocreate 自己。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-107">Or you can follow hello steps in this tutorial toocreate your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3bf4c-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="3bf4c-108">Prerequisites</span></span>

* <span data-ttu-id="3bf4c-109">[Microsoft Visual Studio 2015 或 2017](http://www.visualstudio.com)。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="3bf4c-110">也支援在此教學課程使用 Visual Studio 2017，hello 範例，但 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-110">hello examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="3bf4c-111">[.NET Core Visual Studio 2015 或 2017 工具](http://www.microsoft.com/net/core)。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="3bf4c-112">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-112">An Azure subscription.</span></span>
* <span data-ttu-id="3bf4c-113">事件中樞命名空間。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-113">An event hub namespace.</span></span>

<span data-ttu-id="3bf4c-114">toosend 訊息 tooan 事件中樞，我們將使用 Visual Studio toowrite C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-114">toosend messages tooan event hub, we will use Visual Studio toowrite a C# console application.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="3bf4c-115">建立事件中樞命名空間和事件中樞</span><span class="sxs-lookup"><span data-stu-id="3bf4c-115">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="3bf4c-116">hello 第一個步驟是 toouse hello [Azure 入口網站](https://portal.azure.com)toocreate hello 事件中樞的類型、 命名空間，並取得 hello 應用程式需要 toocommunicate 與 hello 事件中心的管理認證。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-116">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace for hello event hub type, and obtain hello management credentials that your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="3bf4c-117">toocreate 的命名空間和事件中心，請依照下列中的 hello 程序[本文](event-hubs-create.md)，再繼續執行步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-117">toocreate a namespace and an event hub, follow hello procedure in [this article](event-hubs-create.md), and then proceed with hello following steps.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="3bf4c-118">建立主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="3bf4c-118">Create a console application</span></span>

<span data-ttu-id="3bf4c-119">啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-119">Start Visual Studio.</span></span> <span data-ttu-id="3bf4c-120">從 hello**檔案**功能表上，按一下 **新增**，然後按一下**專案**。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-120">From hello **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="3bf4c-121">建立 .NET Core 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-121">Create a .NET Core console application.</span></span>

![新增專案][1]

## <a name="add-hello-event-hubs-nuget-package"></a><span data-ttu-id="3bf4c-123">加入 hello 事件中心 NuGet 封裝</span><span class="sxs-lookup"><span data-stu-id="3bf4c-123">Add hello Event Hubs NuGet package</span></span>

<span data-ttu-id="3bf4c-124">新增 hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET 標準程式庫 NuGet 封裝 tooyour 專案依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3bf4c-124">Add hello [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard library NuGet package tooyour project by following these steps:</span></span> 

1. <span data-ttu-id="3bf4c-125">Hello 新建立的專案上按一下滑鼠右鍵，然後選取**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-125">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="3bf4c-126">按一下 hello**瀏覽** 索引標籤，然後搜尋 「 Microsoft.Azure.EventHubs 」 和選取 hello **Microsoft.Azure.EventHubs**封裝。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-126">Click hello **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select hello **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="3bf4c-127">按一下**安裝**toocomplete hello 安裝，然後關閉此對話方塊。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-127">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>

## <a name="write-some-code-toosend-messages-toohello-event-hub"></a><span data-ttu-id="3bf4c-128">撰寫一些程式碼 toosend 訊息 toohello 事件中樞</span><span class="sxs-lookup"><span data-stu-id="3bf4c-128">Write some code toosend messages toohello event hub</span></span>

1. <span data-ttu-id="3bf4c-129">新增下列 hello `using` hello Program.cs 檔案的陳述式 toohello 頂端。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-129">Add hello following `using` statements toohello top of hello Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="3bf4c-130">新增常數 toohello `Program` hello 事件中樞連接字串和實體路徑 （個別的事件中樞名稱） 的類別。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-130">Add constants toohello `Program` class for hello Event Hubs connection string and entity path (individual event hub name).</span></span> <span data-ttu-id="3bf4c-131">方括號中的 hello 預留位置取代為 hello 建立 hello 事件中心時取得的適當值。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-131">Replace hello placeholders in brackets with hello proper values that were obtained when creating hello event hub.</span></span>

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. <span data-ttu-id="3bf4c-132">新增名為方法`MainAsync`toohello`Program`類別，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3bf4c-132">Add a new method named `MainAsync` toohello `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
        // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
        // we are using hello connection string from hello namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
    }
    ```

4. <span data-ttu-id="3bf4c-133">新增名為方法`SendMessagesToEventHub`toohello`Program`類別，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3bf4c-133">Add a new method named `SendMessagesToEventHub` toohello `Program` class, as follows:</span></span>

    ```csharp
    // Creates an event hub client and sends 100 messages toohello event hub.
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

5. <span data-ttu-id="3bf4c-134">新增下列程式碼 toohello hello`Main`方法在 hello`Program`類別。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-134">Add hello following code toohello `Main` method in hello `Program` class.</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   <span data-ttu-id="3bf4c-135">Program.cs 看起來應該會像下面這樣。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-135">Here is what your Program.cs should look like.</span></span>

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
                // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
                // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
                // we are using hello connection string from hello namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER tooexit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages toohello event hub.
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

6. <span data-ttu-id="3bf4c-136">執行 hello 程式，並確定沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-136">Run hello program, and ensure that there are no errors.</span></span>

<span data-ttu-id="3bf4c-137">恭喜！</span><span class="sxs-lookup"><span data-stu-id="3bf4c-137">Congratulations!</span></span> <span data-ttu-id="3bf4c-138">現在您已送出訊息 tooan 事件中心。</span><span class="sxs-lookup"><span data-stu-id="3bf4c-138">You have now sent messages tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bf4c-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3bf4c-139">Next steps</span></span>
<span data-ttu-id="3bf4c-140">您可以進一步了解事件中心瀏覽下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="3bf4c-140">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="3bf4c-141">從事件中樞接收事件</span><span class="sxs-lookup"><span data-stu-id="3bf4c-141">Receive events from Event Hubs</span></span>](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [<span data-ttu-id="3bf4c-142">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="3bf4c-142">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="3bf4c-143">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="3bf4c-143">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="3bf4c-144">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="3bf4c-144">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
