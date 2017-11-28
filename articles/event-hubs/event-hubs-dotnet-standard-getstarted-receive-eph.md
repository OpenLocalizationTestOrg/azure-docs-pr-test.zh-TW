---
title: "使用 .NET Standard 從 Azure 事件中樞接收事件 | Microsoft Docs"
description: "開始使用 .NET Standard 中的 EventProcessorHost 接收訊息"
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
ms.openlocfilehash: cc62792dad0284f9514664795fdfb32e94a85943
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-receiving-messages-with-the-event-processor-host-in-net-standard"></a><span data-ttu-id="80a01-103">開始使用 .NET Standard 中的事件處理器主機來接收訊息</span><span class="sxs-lookup"><span data-stu-id="80a01-103">Get started receiving messages with the Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="80a01-104">您可在 [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) 上取得此範例。</span><span class="sxs-lookup"><span data-stu-id="80a01-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span></span>

<span data-ttu-id="80a01-105">本教學課程說明如何撰寫一個 .NET Core 主控台應用程式，以使用 **EventProcessorHost** 從事件中樞接收訊息。</span><span class="sxs-lookup"><span data-stu-id="80a01-105">This tutorial shows how to write a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="80a01-106">您可以依現狀執行 [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) 解決方案，其中以您事件中樞和儲存體帳戶的值來取代字串。</span><span class="sxs-lookup"><span data-stu-id="80a01-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution as-is, replacing the strings with your event hub and storage account values.</span></span> <span data-ttu-id="80a01-107">或者，您可以遵循本教學課程中的步驟，來建立自己的解決方案。</span><span class="sxs-lookup"><span data-stu-id="80a01-107">Or you can follow the steps in this tutorial to create your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80a01-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="80a01-108">Prerequisites</span></span>

* <span data-ttu-id="80a01-109">[Microsoft Visual Studio 2015 或 2017](http://www.visualstudio.com)。</span><span class="sxs-lookup"><span data-stu-id="80a01-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="80a01-110">本教學課程中的範例使用 Visual Studio 2017，但也支援 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="80a01-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="80a01-111">[.NET Core Visual Studio 2015 或 2017 工具](http://www.microsoft.com/net/core)。</span><span class="sxs-lookup"><span data-stu-id="80a01-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="80a01-112">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="80a01-112">An Azure subscription.</span></span>
* <span data-ttu-id="80a01-113">Azure 事件中樞命名空間。</span><span class="sxs-lookup"><span data-stu-id="80a01-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="80a01-114">一個 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="80a01-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="80a01-115">建立事件中樞命名空間和事件中樞</span><span class="sxs-lookup"><span data-stu-id="80a01-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="80a01-116">第一個步驟是使用 [Azure 入口網站](https://portal.azure.com)來建立「事件中樞」類型的命名空間，然後取得您應用程式與事件中樞進行通訊所需的管理認證。</span><span class="sxs-lookup"><span data-stu-id="80a01-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the Event Hubs type, and obtain the management credentials that your application needs to communicate with the event hub.</span></span> <span data-ttu-id="80a01-117">若要建立命名空間和事件中樞，請依照[這篇文章](event-hubs-create.md)中的程序操作，然後繼續進行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="80a01-117">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="80a01-118">建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="80a01-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="80a01-119">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="80a01-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="80a01-120">在入口網站的左方瀏覽窗格中，依序按一下 [新增]、[儲存體] 及 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="80a01-120">In the left navigation pane of the portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="80a01-121">完成 [儲存體帳戶] 刀鋒視窗中的欄位，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="80a01-121">Complete the fields in the storage account blade, and then click **Create**.</span></span>

    ![建立儲存體帳戶][1]

4. <span data-ttu-id="80a01-123">在看到「部署成功」訊息之後，按一下新儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="80a01-123">After you see the **Deployments Succeeded** message, click the name of the new storage account.</span></span> <span data-ttu-id="80a01-124">在 [基本資訊] 刀鋒視窗中，按一下 [Blob]。</span><span class="sxs-lookup"><span data-stu-id="80a01-124">In the **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="80a01-125">當 [Blob 服務] 刀鋒視窗開啟時，按一下頂端的 [+ 容器]。</span><span class="sxs-lookup"><span data-stu-id="80a01-125">When the **Blob service** blade opens, click **+ Container** at the top.</span></span> <span data-ttu-id="80a01-126">為容器命名，然後關閉 [Blob 服務] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="80a01-126">Give the container a name, and then close the **Blob service** blade.</span></span>  
5. <span data-ttu-id="80a01-127">按一下左側刀鋒視窗中的 [存取金鑰]，然後複製儲存體容器的名稱、儲存體帳戶及 **key1** 的值。</span><span class="sxs-lookup"><span data-stu-id="80a01-127">Click **Access keys** in the left blade and copy the name of the storage container, the storage account, and the value of **key1**.</span></span> <span data-ttu-id="80a01-128">將這些值儲存到記事本或一些其他暫存位置。</span><span class="sxs-lookup"><span data-stu-id="80a01-128">Save these values to Notepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="80a01-129">建立主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="80a01-129">Create a console application</span></span>

<span data-ttu-id="80a01-130">啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="80a01-130">Start Visual Studio.</span></span> <span data-ttu-id="80a01-131">從 [檔案] 功能表中，按一下 [新增]，再按 [專案]。</span><span class="sxs-lookup"><span data-stu-id="80a01-131">From the **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="80a01-132">建立 .NET Core 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="80a01-132">Create a .NET Core console application.</span></span>

![新增專案][2]

## <a name="add-the-event-hubs-nuget-package"></a><span data-ttu-id="80a01-134">新增事件中樞 NuGet 封裝</span><span class="sxs-lookup"><span data-stu-id="80a01-134">Add the Event Hubs NuGet package</span></span>

<span data-ttu-id="80a01-135">遵循下列幾個步驟，將 [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) 和 [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET 標準程式庫 NuGet 套件新增至您的專案：</span><span class="sxs-lookup"><span data-stu-id="80a01-135">Add the [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard library NuGet packages to your project by following these steps:</span></span> 

1. <span data-ttu-id="80a01-136">以滑鼠右鍵按一下新建立的專案，然後選取 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="80a01-136">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="80a01-137">按一下 [瀏覽] 索引標籤，然後搜尋「Microsoft.Azure.EventHubs」並選取 [Microsoft.Azure.EventHubs] 套件。</span><span class="sxs-lookup"><span data-stu-id="80a01-137">Click the **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select the **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="80a01-138">按一下 [安裝]  完成安裝作業，然後關閉此對話方塊。</span><span class="sxs-lookup"><span data-stu-id="80a01-138">Click **Install** to complete the installation, then close this dialog box.</span></span>
3. <span data-ttu-id="80a01-139">重複步驟 1 和 2，並安裝 **Microsoft.Azure.EventHubs.Processor** 套件。</span><span class="sxs-lookup"><span data-stu-id="80a01-139">Repeat steps 1 and 2, and install the **Microsoft.Azure.EventHubs.Processor** package.</span></span>

## <a name="implement-the-ieventprocessor-interface"></a><span data-ttu-id="80a01-140">實作 IEventProcessor 介面</span><span class="sxs-lookup"><span data-stu-id="80a01-140">Implement the IEventProcessor interface</span></span>

1. <span data-ttu-id="80a01-141">在 [方案總管] 中，於專案上按一下滑鼠右鍵，按一下 [新增]，然後按一下 [類別]。</span><span class="sxs-lookup"><span data-stu-id="80a01-141">In Solution Explorer, right-click the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="80a01-142">將新類別命名為 **SimpleEventProcessor**。</span><span class="sxs-lookup"><span data-stu-id="80a01-142">Name the new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="80a01-143">開啟 SimpleEventProcessor.cs 檔案，然後在檔案開頭新增下列 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="80a01-143">Open the SimpleEventProcessor.cs file and add the following `using` statements to the top of the file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="80a01-144">實作 `IEventProcessor` 介面。</span><span class="sxs-lookup"><span data-stu-id="80a01-144">Implement the `IEventProcessor` interface.</span></span> <span data-ttu-id="80a01-145">以下列程式碼取代 `SimpleEventProcessor` 類別的整個內容：</span><span class="sxs-lookup"><span data-stu-id="80a01-145">Replace the entire contents of the `SimpleEventProcessor` class with the following code:</span></span>

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

## <a name="write-a-main-console-method-that-uses-the-simpleeventprocessor-class-to-receive-messages"></a><span data-ttu-id="80a01-146">撰寫使用 SimpleEventProcessor 類別來接收訊息的主要主控台方法</span><span class="sxs-lookup"><span data-stu-id="80a01-146">Write a main console method that uses the SimpleEventProcessor class to receive messages</span></span>

1. <span data-ttu-id="80a01-147">在 Program.cs 檔案開頭處加入 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="80a01-147">Add the following `using` statements to the top of the Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="80a01-148">針對事件中樞連接字串、事件中樞名稱、儲存體帳戶容器名稱、儲存體帳戶名稱及儲存體帳戶金鑰，將常數新增到 `Program` 類別。</span><span class="sxs-lookup"><span data-stu-id="80a01-148">Add constants to the `Program` class for the event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="80a01-149">新增下列程式碼，其中將預留位置取代成其對應的值。</span><span class="sxs-lookup"><span data-stu-id="80a01-149">Add the following code, replacing the placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="80a01-150">將名為 `MainAsync` 的新方法新增到 `Program` 類別，如下所示：</span><span class="sxs-lookup"><span data-stu-id="80a01-150">Add a new method named `MainAsync` to the `Program` class, as follows:</span></span>

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

        // Registers the Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER to stop worker.");
        Console.ReadLine();

        // Disposes of the Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. <span data-ttu-id="80a01-151">將下列程式碼行新增至 `Main` 方法：</span><span class="sxs-lookup"><span data-stu-id="80a01-151">Add the following line of code to the `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="80a01-152">Program.cs 檔案看起來應該會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="80a01-152">Here is what your Program.cs file should look like:</span></span>

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

                // Registers the Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER to stop worker.");
                Console.ReadLine();

                // Disposes of the Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. <span data-ttu-id="80a01-153">執行程式，並確定沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="80a01-153">Run the program, and ensure that there are no errors.</span></span>

<span data-ttu-id="80a01-154">恭喜！</span><span class="sxs-lookup"><span data-stu-id="80a01-154">Congratulations!</span></span> <span data-ttu-id="80a01-155">您現在已使用「事件處理器主機」從事件中樞接收訊息。</span><span class="sxs-lookup"><span data-stu-id="80a01-155">You have now received messages from an event hub by using the Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80a01-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="80a01-156">Next steps</span></span>
<span data-ttu-id="80a01-157">您可以造訪下列連結以深入了解事件中樞︰</span><span class="sxs-lookup"><span data-stu-id="80a01-157">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="80a01-158">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="80a01-158">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="80a01-159">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="80a01-159">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="80a01-160">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="80a01-160">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
