---
title: "開始使用佇列儲存體和 Visual Studio 已連接服務 (ASP.NET Core) | Microsoft Docs"
description: "如何開始在 Visual Studio 的 ASP.NET Core 專案中使用 Azure 佇列儲存體"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 04977069-5b2d-4cba-84ae-9fb2f5eb1006
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 4622496544ce6e1057ac68a2e9946917573e997e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="8ce85-103">開始使用佇列儲存體和 Visual Studio 已連接服務 (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="8ce85-103">Get started with queue storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="8ce85-104">概觀</span><span class="sxs-lookup"><span data-stu-id="8ce85-104">Overview</span></span>
<span data-ttu-id="8ce85-105">本文說明如何在您使用 Visual Studio 的 [新增已連接服務]  對話方塊建立或參考了 ASP.NET Core 專案中的 Azure 儲存體帳戶之後，開始在 Visual Studio 使用 Azure 佇列儲存體。</span><span class="sxs-lookup"><span data-stu-id="8ce85-105">This article describes how to get started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="8ce85-106">[新增連接的服務]  作業會安裝適當的 NuGet 套件，以存取專案中的 Azure 儲存體，並將儲存體帳戶的連接字串新增至您的專案設定檔。</span><span class="sxs-lookup"><span data-stu-id="8ce85-106">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="8ce85-107">Azure 佇列儲存體是一項儲存大量訊息的服務，全球任何地方都可利用 HTTP 或 HTTPS 並透過驗證的呼叫來存取這些訊息。</span><span class="sxs-lookup"><span data-stu-id="8ce85-107">Azure queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="8ce85-108">單一佇列訊息的大小上限為 64 KB，而一個佇列可以包含數百萬個訊息，以儲存體帳戶的總容量為限。</span><span class="sxs-lookup"><span data-stu-id="8ce85-108">A single queue message can be up to 64 kilobytes (KB) in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

<span data-ttu-id="8ce85-109">若要開始，首先您必須在儲存體帳戶中建立 Azure 佇列。</span><span class="sxs-lookup"><span data-stu-id="8ce85-109">To get started, you first need to create an Azure queue in your storage account.</span></span> <span data-ttu-id="8ce85-110">我們將會示範如何在程式碼中建立佇列。</span><span class="sxs-lookup"><span data-stu-id="8ce85-110">We'll show you how to create a queue in code.</span></span> <span data-ttu-id="8ce85-111">我們也將顯示如何執行基本的佇列作業，例如新增、修改、讀取和移除佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="8ce85-111">We'll also show you how to perform basic queue operations, such as adding, modifying, reading, and removing queue messages.</span></span> <span data-ttu-id="8ce85-112">這些範例均以 C\# 程式碼撰寫，並使用 Azure Storage Client Library for .NET。</span><span class="sxs-lookup"><span data-stu-id="8ce85-112">The samples are written in C\# code and use the Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="8ce85-113">如需 ASP.NET 的詳細資訊，請參閱 [ASP.NET](http://www.asp.net)。</span><span class="sxs-lookup"><span data-stu-id="8ce85-113">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

<span data-ttu-id="8ce85-114">**注意：**對 ASP.NET Core 中的 Azure 儲存體執行呼叫的部分 API 是非同步的。</span><span class="sxs-lookup"><span data-stu-id="8ce85-114">**NOTE:** Some of the APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="8ce85-115">如需詳細資訊，請參閱 [使用 Async 和 Await 進行非同步程式設計](http://msdn.microsoft.com/library/hh191443.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="8ce85-115">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="8ce85-116">以下程式碼假設使用非同步程式設計方法。</span><span class="sxs-lookup"><span data-stu-id="8ce85-116">The code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="8ce85-117">如需以程式設計方式處理佇列的詳細資訊，請參閱 [以 .NET 開始使用 Azure 佇列儲存體](storage-dotnet-how-to-use-queues.md) 。</span><span class="sxs-lookup"><span data-stu-id="8ce85-117">See [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md) for more information on programmatically manipulating queues.</span></span>
* <span data-ttu-id="8ce85-118">如需 Azure 儲存體的一般資訊，請參閱 [儲存體文件](https://azure.microsoft.com/documentation/services/storage/) 。</span><span class="sxs-lookup"><span data-stu-id="8ce85-118">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="8ce85-119">如需 Azure 雲端服務的一般資訊，請參閱 [雲端服務文件](https://azure.microsoft.com/documentation/services/cloud-services/) 。</span><span class="sxs-lookup"><span data-stu-id="8ce85-119">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="8ce85-120">若需要如何編寫 ASP.NET 應用程式的詳細資訊，請參閱 [ASP.NET](http://www.asp.net) 。</span><span class="sxs-lookup"><span data-stu-id="8ce85-120">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="8ce85-121">在程式碼中存取佇列</span><span class="sxs-lookup"><span data-stu-id="8ce85-121">Access queues in code</span></span>
<span data-ttu-id="8ce85-122">若要存取 ASP.NET Core 專案中的佇列，您需要將下列項目包含在存取 Azure 佇列儲存體的任何 C# 原始程式檔中。</span><span class="sxs-lookup"><span data-stu-id="8ce85-122">To access queues in ASP.NET Core projects, you need to include the following items to any C# source file that accesses Azure queue storage.</span></span>

1. <span data-ttu-id="8ce85-123">請確定 C# 檔案頂端的命名空間宣告包含這些 **using** 陳述式。</span><span class="sxs-lookup"><span data-stu-id="8ce85-123">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="8ce85-124">取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="8ce85-124">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8ce85-125">使用下列程式碼，從 Azure 服務組態取得您的儲存體連接字串和儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="8ce85-125">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="8ce85-126">取得 **CloudQueueClient** 物件以參考儲存體帳戶中的佇列物件。</span><span class="sxs-lookup"><span data-stu-id="8ce85-126">Get a **CloudQueueClient** object to reference the queue objects in your storage account.</span></span>  
   
        // Create the CloudQueueClient object for the storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="8ce85-127">取得 **CloudQueue** 物件以參考特定的佇列。</span><span class="sxs-lookup"><span data-stu-id="8ce85-127">Get a **CloudQueue** object to reference a specific queue.</span></span>
   
        // Get a reference to the CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="8ce85-128">**注意：** 請在下列範例中的程式碼前面使用上述所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="8ce85-128">**NOTE:** Use all of the above code in front of the code in the following samples.</span></span>

### <a name="create-a-queue-in-code"></a><span data-ttu-id="8ce85-129">在程式碼中建立佇列</span><span class="sxs-lookup"><span data-stu-id="8ce85-129">Create a queue in code</span></span>
<span data-ttu-id="8ce85-130">若要在程式碼中建立 Azure 佇列，請加入 **CreateIfNotExistsAsync**呼叫。</span><span class="sxs-lookup"><span data-stu-id="8ce85-130">To create the Azure queue in code, just add a call to **CreateIfNotExistsAsync**.</span></span>

    // Create the CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="8ce85-131">將訊息新增至佇列</span><span class="sxs-lookup"><span data-stu-id="8ce85-131">Add a message to a queue</span></span>
<span data-ttu-id="8ce85-132">若要將訊息插入現有佇列中，請建立新的 **CloudQueueMessage** 物件，然後呼叫 **AddMessageAsync** 方法。</span><span class="sxs-lookup"><span data-stu-id="8ce85-132">To insert a message into an existing queue, create a new **CloudQueueMessage** object, then call the **AddMessageAsync** method.</span></span>

<span data-ttu-id="8ce85-133">您可以從字串 (採用 UTF-8 格式) 或位元組陣列建立 **CloudQueueMessage** 物件。</span><span class="sxs-lookup"><span data-stu-id="8ce85-133">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="8ce85-134">以下是插入訊息 'Hello, World' 的範例。</span><span class="sxs-lookup"><span data-stu-id="8ce85-134">Here is an example which inserts the message 'Hello, World'.</span></span>

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="8ce85-135">讀取佇列中的訊息</span><span class="sxs-lookup"><span data-stu-id="8ce85-135">Read a message in a queue</span></span>
<span data-ttu-id="8ce85-136">您只要呼叫 **PeekMessageAsync** 方法，就能在佇列前查看訊息，而無須將其從佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="8ce85-136">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessageAsync** method.</span></span>

    // Peek the next message in the queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="8ce85-137">讀取並移除佇列中的訊息</span><span class="sxs-lookup"><span data-stu-id="8ce85-137">Read and remove a message in a queue</span></span>
<span data-ttu-id="8ce85-138">您的程式碼可以使用兩個步驟將訊息從佇列中移除 (清除佇列)。</span><span class="sxs-lookup"><span data-stu-id="8ce85-138">Your code can remove (dequeue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="8ce85-139">呼叫 **GetMessageAsync** ，以取得佇列中的下一則訊息。</span><span class="sxs-lookup"><span data-stu-id="8ce85-139">Call **GetMessageAsync** to get the next message in a queue.</span></span> <span data-ttu-id="8ce85-140">任何從此佇列讀取訊息的其他程式碼，將無法看到從 **GetMessageAsync** 傳回的訊息。</span><span class="sxs-lookup"><span data-stu-id="8ce85-140">A message returned from **GetMessageAsync** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="8ce85-141">依預設，此訊息會維持 30 秒的不可見狀態。</span><span class="sxs-lookup"><span data-stu-id="8ce85-141">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="8ce85-142">若要完成從佇列中移除訊息，請呼叫 **DeleteMessageAsync**。</span><span class="sxs-lookup"><span data-stu-id="8ce85-142">To finish removing the message from the queue, call **DeleteMessageAsync**.</span></span>

<span data-ttu-id="8ce85-143">這個移除訊息的兩步驟程序可確保您的程式碼因為硬體或軟體故障而無法處理訊息時，另一個程式碼的執行個體可以取得相同訊息並再試一次。</span><span class="sxs-lookup"><span data-stu-id="8ce85-143">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="8ce85-144">下列程式碼會在處理完訊息之後隨即呼叫 **DeleteMessageAsync** 。</span><span class="sxs-lookup"><span data-stu-id="8ce85-144">The following code calls **DeleteMessageAsync** right after the message has been processed.</span></span>

    // Get the next message in the queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process the message in less than 30 seconds.

    // Then delete the message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a><span data-ttu-id="8ce85-145">運用清除佇列訊息的其他選項</span><span class="sxs-lookup"><span data-stu-id="8ce85-145">Leverage additional options for dequeuing messages</span></span>
<span data-ttu-id="8ce85-146">自訂從佇列中擷取訊息的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="8ce85-146">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="8ce85-147">首先，您可以取得一批訊息 (最多 32 個)。</span><span class="sxs-lookup"><span data-stu-id="8ce85-147">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="8ce85-148">其次，您可以設定較長或較短的可見度逾時，讓您的程式碼有較長或較短的時間可以完全處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="8ce85-148">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="8ce85-149">下列程式碼範例將使用 **GetMessages** 方法，在一次呼叫中取得 20 個訊息。</span><span class="sxs-lookup"><span data-stu-id="8ce85-149">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="8ce85-150">接著它會使用 **foreach** 迴圈處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="8ce85-150">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="8ce85-151">它也會將可見度逾時設定為每個訊息 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="8ce85-151">It also sets the invisibility timeout to 5 minutes for each message.</span></span> <span data-ttu-id="8ce85-152">請注意，所有訊息皆會同時開始計時 5 分鐘，當呼叫 **GetMessages**後的 5 分鐘一到，所有尚未刪除的訊息皆會重新出現。</span><span class="sxs-lookup"><span data-stu-id="8ce85-152">Note that the 5 minutes start for all messages at the same time, so after 5 minutes have passed after the call to **GetMessages**, any messages which have not been deleted become visible again.</span></span>

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-the-queue-length"></a><span data-ttu-id="8ce85-153">取得佇列長度</span><span class="sxs-lookup"><span data-stu-id="8ce85-153">Get the queue length</span></span>
<span data-ttu-id="8ce85-154">您可以取得佇列中的估計訊息數目。</span><span class="sxs-lookup"><span data-stu-id="8ce85-154">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="8ce85-155">**FetchAttributes** 方法會要求佇列服務擷取佇列屬性，其中包含訊息計數。</span><span class="sxs-lookup"><span data-stu-id="8ce85-155">The **FetchAttributes** method asks the queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="8ce85-156">**ApproximateMethodCount** 屬性會傳回 **FetchAttributes** 方法所擷取的最後一個值，而無需呼叫佇列服務。</span><span class="sxs-lookup"><span data-stu-id="8ce85-156">The **ApproximateMethodCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the queue service.</span></span>

    // Fetch the queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve the cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display the number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-the-async-await-pattern-with-common-queue-apis"></a><span data-ttu-id="8ce85-157">搭配使用 Async-Await 模式和通用佇列 API</span><span class="sxs-lookup"><span data-stu-id="8ce85-157">Use the Async-Await pattern with common queue APIs</span></span>
<span data-ttu-id="8ce85-158">這個範例示範如何搭配使用 Async-Await 模式和通用佇列 API。</span><span class="sxs-lookup"><span data-stu-id="8ce85-158">This example shows how to use the Async-Await pattern with common queue APIs.</span></span> <span data-ttu-id="8ce85-159">此範例會呼叫每個特定方法的非同步版本。</span><span class="sxs-lookup"><span data-stu-id="8ce85-159">The sample calls the async version of each of the given methods.</span></span> <span data-ttu-id="8ce85-160">這可以透過每個方法的非同步 Postfix 看到。</span><span class="sxs-lookup"><span data-stu-id="8ce85-160">This can be seen by the Async post-fix of each method.</span></span> <span data-ttu-id="8ce85-161">使用非同步方法時，async-await 模式會暫停本機執行，直到呼叫完成為止。</span><span class="sxs-lookup"><span data-stu-id="8ce85-161">When an async method is used, the Async-Await pattern suspends local execution until the call is completed.</span></span> <span data-ttu-id="8ce85-162">這種行為可讓目前的執行緒執行其他工作，有助於避免發生效能瓶頸並提升應用程式的整體回應。</span><span class="sxs-lookup"><span data-stu-id="8ce85-162">This behavior allows the current thread to do other work which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="8ce85-163">如需如何在 .NET 中使用 Async-Await 模式的詳細資訊，請參閱 [Async 和 Await (C# 和 Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="8ce85-163">For more details on using the Async-Await pattern in .NET, see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message to add to the queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue the message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue the message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete the message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a><span data-ttu-id="8ce85-164">刪除佇列</span><span class="sxs-lookup"><span data-stu-id="8ce85-164">Delete a queue</span></span>
<span data-ttu-id="8ce85-165">若要刪除佇列及其內含的所有訊息，請在佇列物件上呼叫 **Delete** 方法。</span><span class="sxs-lookup"><span data-stu-id="8ce85-165">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

    // Delete the queue.
    messageQueue.Delete();


## <a name="next-steps"></a><span data-ttu-id="8ce85-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8ce85-166">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

