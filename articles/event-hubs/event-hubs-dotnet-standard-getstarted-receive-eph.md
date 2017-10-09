---
title: "從使用標準.NET 的 Azure 事件中樞 aaaReceive 事件 |Microsoft 文件"
description: "開始接收訊息以 hello EventProcessorHost.NET 標準"
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
ms.openlocfilehash: c3983f2668ac8f65522e44a1609dfd2eed31b7d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-receiving-messages-with-hello-event-processor-host-in-net-standard"></a><span data-ttu-id="6bd25-103">開始在標準.NET 中接收訊息以 hello 事件處理器主機</span><span class="sxs-lookup"><span data-stu-id="6bd25-103">Get started receiving messages with hello Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="6bd25-104">您可在 [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) 上取得此範例。</span><span class="sxs-lookup"><span data-stu-id="6bd25-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span></span>

<span data-ttu-id="6bd25-105">本教學課程示範如何 toowrite.NET Core 主控台應用程式從事件中心接收訊息，使用**EventProcessorHost**。</span><span class="sxs-lookup"><span data-stu-id="6bd25-105">This tutorial shows how toowrite a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="6bd25-106">您可以執行 hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver)做為方案的事件中樞與儲存體帳戶值，取代 hello 字串。</span><span class="sxs-lookup"><span data-stu-id="6bd25-106">You can run hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution as-is, replacing hello strings with your event hub and storage account values.</span></span> <span data-ttu-id="6bd25-107">您可以遵循 hello 步驟在本教學課程 toocreate 自己。</span><span class="sxs-lookup"><span data-stu-id="6bd25-107">Or you can follow hello steps in this tutorial toocreate your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bd25-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="6bd25-108">Prerequisites</span></span>

* <span data-ttu-id="6bd25-109">[Microsoft Visual Studio 2015 或 2017](http://www.visualstudio.com)。</span><span class="sxs-lookup"><span data-stu-id="6bd25-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="6bd25-110">也支援在此教學課程使用 Visual Studio 2017，hello 範例，但 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="6bd25-110">hello examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="6bd25-111">[.NET Core Visual Studio 2015 或 2017 工具](http://www.microsoft.com/net/core)。</span><span class="sxs-lookup"><span data-stu-id="6bd25-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="6bd25-112">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6bd25-112">An Azure subscription.</span></span>
* <span data-ttu-id="6bd25-113">Azure 事件中樞命名空間。</span><span class="sxs-lookup"><span data-stu-id="6bd25-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="6bd25-114">一個 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6bd25-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="6bd25-115">建立事件中樞命名空間和事件中樞</span><span class="sxs-lookup"><span data-stu-id="6bd25-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="6bd25-116">hello 第一個步驟是 toouse hello [Azure 入口網站](https://portal.azure.com)toocreate hello 事件中心的命名空間類型，並取得 hello 應用程式需要 toocommunicate 與 hello 事件中心的管理認證。</span><span class="sxs-lookup"><span data-stu-id="6bd25-116">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace for hello Event Hubs type, and obtain hello management credentials that your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="6bd25-117">toocreate 命名空間和事件中心，請依照下列中的 hello 程序[本文](event-hubs-create.md)，再繼續執行步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="6bd25-117">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), and then proceed with hello following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="6bd25-118">建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="6bd25-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="6bd25-119">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="6bd25-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="6bd25-120">在 hello hello 入口網站的左側瀏覽窗格中按一下**新增**，按一下 **儲存體**，然後按一下**儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="6bd25-120">In hello left navigation pane of hello portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="6bd25-121">完成 hello 欄位在 hello 儲存體帳戶 刀鋒視窗，然後再按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="6bd25-121">Complete hello fields in hello storage account blade, and then click **Create**.</span></span>

    ![建立儲存體帳戶][1]

4. <span data-ttu-id="6bd25-123">Vez que aparezca hello**部署成功**訊息中，按一下 hello hello 新的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="6bd25-123">After you see hello **Deployments Succeeded** message, click hello name of hello new storage account.</span></span> <span data-ttu-id="6bd25-124">在 hello **Essentials**刀鋒視窗中，按一下  **Blob**。</span><span class="sxs-lookup"><span data-stu-id="6bd25-124">In hello **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="6bd25-125">當 hello **Blob 服務**開啟刀鋒視窗中，按一下**+ 容器**hello 頂端。</span><span class="sxs-lookup"><span data-stu-id="6bd25-125">When hello **Blob service** blade opens, click **+ Container** at hello top.</span></span> <span data-ttu-id="6bd25-126">指定的名稱，hello 容器，然後關閉 hello **Blob 服務**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6bd25-126">Give hello container a name, and then close hello **Blob service** blade.</span></span>  
5. <span data-ttu-id="6bd25-127">按一下**存取金鑰**hello 左刀鋒視窗，然後複製 hello 名稱中的 hello 儲存體容器、 hello 儲存體帳戶，以及 hello 值**key1**。</span><span class="sxs-lookup"><span data-stu-id="6bd25-127">Click **Access keys** in hello left blade and copy hello name of hello storage container, hello storage account, and hello value of **key1**.</span></span> <span data-ttu-id="6bd25-128">儲存這些值 tooNotepad 或一些其他的暫存位置。</span><span class="sxs-lookup"><span data-stu-id="6bd25-128">Save these values tooNotepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="6bd25-129">建立主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="6bd25-129">Create a console application</span></span>

<span data-ttu-id="6bd25-130">啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="6bd25-130">Start Visual Studio.</span></span> <span data-ttu-id="6bd25-131">從 hello**檔案**功能表上，按一下 **新增**，然後按一下**專案**。</span><span class="sxs-lookup"><span data-stu-id="6bd25-131">From hello **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="6bd25-132">建立 .NET Core 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bd25-132">Create a .NET Core console application.</span></span>

![新增專案][2]

## <a name="add-hello-event-hubs-nuget-package"></a><span data-ttu-id="6bd25-134">加入 hello 事件中心 NuGet 封裝</span><span class="sxs-lookup"><span data-stu-id="6bd25-134">Add hello Event Hubs NuGet package</span></span>

<span data-ttu-id="6bd25-135">新增 hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/)和[ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET 標準程式庫 NuGet 封裝 tooyour 專案依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6bd25-135">Add hello [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard library NuGet packages tooyour project by following these steps:</span></span> 

1. <span data-ttu-id="6bd25-136">Hello 新建立的專案上按一下滑鼠右鍵，然後選取**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="6bd25-136">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="6bd25-137">按一下 hello**瀏覽** 索引標籤，然後搜尋 「 Microsoft.Azure.EventHubs 」 和選取 hello **Microsoft.Azure.EventHubs**封裝。</span><span class="sxs-lookup"><span data-stu-id="6bd25-137">Click hello **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select hello **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="6bd25-138">按一下**安裝**toocomplete hello 安裝，然後關閉此對話方塊。</span><span class="sxs-lookup"><span data-stu-id="6bd25-138">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
3. <span data-ttu-id="6bd25-139">重複步驟 1 和 2，並安裝 hello **Microsoft.Azure.EventHubs.Processor**封裝。</span><span class="sxs-lookup"><span data-stu-id="6bd25-139">Repeat steps 1 and 2, and install hello **Microsoft.Azure.EventHubs.Processor** package.</span></span>

## <a name="implement-hello-ieventprocessor-interface"></a><span data-ttu-id="6bd25-140">實作 hello IEventProcessor 介面</span><span class="sxs-lookup"><span data-stu-id="6bd25-140">Implement hello IEventProcessor interface</span></span>

1. <span data-ttu-id="6bd25-141">在 方案總管 中，以滑鼠右鍵按一下 hello 專案中，按一下 **新增**，然後按一下**類別**。</span><span class="sxs-lookup"><span data-stu-id="6bd25-141">In Solution Explorer, right-click hello project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="6bd25-142">Hello 新類別命名**SimpleEventProcessor**。</span><span class="sxs-lookup"><span data-stu-id="6bd25-142">Name hello new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="6bd25-143">開啟 hello SimpleEventProcessor.cs 檔案並加入下列 hello `using` hello 檔案的陳述式 toohello 頂端。</span><span class="sxs-lookup"><span data-stu-id="6bd25-143">Open hello SimpleEventProcessor.cs file and add hello following `using` statements toohello top of hello file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="6bd25-144">實作 hello`IEventProcessor`介面。</span><span class="sxs-lookup"><span data-stu-id="6bd25-144">Implement hello `IEventProcessor` interface.</span></span> <span data-ttu-id="6bd25-145">取代 hello hello 整個內容`SimpleEventProcessor`類別以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="6bd25-145">Replace hello entire contents of hello `SimpleEventProcessor` class with hello following code:</span></span>

    ```csharp
    public class SimpleEventProcessor : IEventProcessor
    {
        public Task CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
            return Task.CompletedTask;
        }

        public Task OpenAsync(PartitionContext context)
        {
            Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
            return Task.CompletedTask;
        }

        public Task ProcessErrorAsync(PartitionContext context, Exception error)
        {
            Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
            return Task.CompletedTask;
        }

        public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (var eventData in messages)
            {
                var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
                Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
            }

            return context.CheckpointAsync();
        }
    }
    ```

## <a name="write-a-main-console-method-that-uses-hello-simpleeventprocessor-class-tooreceive-messages"></a><span data-ttu-id="6bd25-146">撰寫使用 hello SimpleEventProcessor 類別 tooreceive 訊息主控台方法</span><span class="sxs-lookup"><span data-stu-id="6bd25-146">Write a main console method that uses hello SimpleEventProcessor class tooreceive messages</span></span>

1. <span data-ttu-id="6bd25-147">新增下列 hello `using` hello Program.cs 檔案的陳述式 toohello 頂端。</span><span class="sxs-lookup"><span data-stu-id="6bd25-147">Add hello following `using` statements toohello top of hello Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="6bd25-148">新增常數 toohello `Program` hello 事件中樞連接字串、 事件中樞的名稱、 儲存體帳戶容器的名稱、 儲存體帳戶名稱，和儲存體帳戶金鑰的類別。</span><span class="sxs-lookup"><span data-stu-id="6bd25-148">Add constants toohello `Program` class for hello event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="6bd25-149">新增下列程式碼，其相對應值取代 hello 預留位置 hello。</span><span class="sxs-lookup"><span data-stu-id="6bd25-149">Add hello following code, replacing hello placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="6bd25-150">新增名為方法`MainAsync`toohello`Program`類別，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6bd25-150">Add a new method named `MainAsync` toohello `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        Console.WriteLine("Registering EventProcessor...");

        var eventProcessorHost = new EventProcessorHost(
            EhEntityPath,
            PartitionReceiver.DefaultConsumerGroupName,
            EhConnectionString,
            StorageConnectionString,
            StorageContainerName);

        // Registers hello Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER toostop worker.");
        Console.ReadLine();

        // Disposes of hello Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. <span data-ttu-id="6bd25-151">新增下列一行程式碼 toohello hello`Main`方法：</span><span class="sxs-lookup"><span data-stu-id="6bd25-151">Add hello following line of code toohello `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="6bd25-152">Program.cs 檔案看起來應該會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="6bd25-152">Here is what your Program.cs file should look like:</span></span>

    ```csharp
    namespace SampleEphReceiver
    {

        public class Program
        {
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";
            private const string StorageContainerName = "{Storage account container name}";
            private const string StorageAccountName = "{Storage account name}";
            private const string StorageAccountKey = "{Storage account key}";

            private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                Console.WriteLine("Registering EventProcessor...");

                var eventProcessorHost = new EventProcessorHost(
                    EhEntityPath,
                    PartitionReceiver.DefaultConsumerGroupName,
                    EhConnectionString,
                    StorageConnectionString,
                    StorageContainerName);

                // Registers hello Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER toostop worker.");
                Console.ReadLine();

                // Disposes of hello Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. <span data-ttu-id="6bd25-153">執行 hello 程式，並確定沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="6bd25-153">Run hello program, and ensure that there are no errors.</span></span>

<span data-ttu-id="6bd25-154">恭喜！</span><span class="sxs-lookup"><span data-stu-id="6bd25-154">Congratulations!</span></span> <span data-ttu-id="6bd25-155">您現在已從事件中心接收訊息，使用 hello 事件處理器主機。</span><span class="sxs-lookup"><span data-stu-id="6bd25-155">You have now received messages from an event hub by using hello Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bd25-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6bd25-156">Next steps</span></span>
<span data-ttu-id="6bd25-157">您可以進一步了解事件中心瀏覽下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="6bd25-157">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="6bd25-158">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="6bd25-158">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="6bd25-159">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="6bd25-159">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="6bd25-160">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="6bd25-160">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
