---
title: "開始使用佇列儲存體和 Visual Studio 已連線的服務 （雲端服務） 的 aaaGet |Microsoft 文件"
description: "Tooget 啟動連接 tooa 儲存體帳戶，使用 Visual Studio 已連接服務之後，在 Visual Studio 中的雲端服務專案中使用 Azure 佇列儲存體的方式"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: da587aac-5e64-4e9a-8405-44cc1924881d
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 1e90eeb826131cadca90dcb720c931fff5fedcb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="b8f8c-103">開始使用 Azure 佇列儲存體和 Visual Studio 已連接服務 (雲端服務專案)</span><span class="sxs-lookup"><span data-stu-id="b8f8c-103">Getting started with Azure Queue storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="b8f8c-104">概觀</span><span class="sxs-lookup"><span data-stu-id="b8f8c-104">Overview</span></span>
<span data-ttu-id="b8f8c-105">本文說明如何 tooget 啟動後您建立或使用 Visual Studio hello 參考 Azure 儲存體帳戶中的雲端服務專案，Visual Studio 中使用 Azure 佇列儲存體**加入已連接服務**對話方塊.</span><span class="sxs-lookup"><span data-stu-id="b8f8c-105">This article describes how tooget started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using hello  Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="b8f8c-106">我們將為您示範如何 toocreate 程式碼中的佇列。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-106">We'll show you how toocreate a queue in code.</span></span> <span data-ttu-id="b8f8c-107">我們也會顯示您如何 tooperform 基本佇列作業，例如加入、 修改、 讀取以及移除佇列的訊息。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-107">We'll also show you how tooperform basic queue operations, such as adding, modifying, reading and removing queue messages.</span></span> <span data-ttu-id="b8f8c-108">hello 範例以 C# 程式碼撰寫和使用 hello [Microsoft Azure 儲存體用戶端程式庫適用於.NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-108">hello samples are written in C# code and use hello [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="b8f8c-109">hello**加入已連接服務**作業安裝在您的專案中的適當 NuGet 封裝 tooaccess hello Azure 儲存體，並新增 hello 連接字串，hello 儲存體帳戶 tooyour 專案組態檔。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-109">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

* <span data-ttu-id="b8f8c-110">如需以程式碼處理佇列的詳細資訊，請參閱 [以 .NET 開始使用 Azure 佇列儲存體](../storage/queues/storage-dotnet-how-to-use-queues.md) 。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-110">See [Get started with Azure Queue storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information on manipulating queues in code.</span></span>
* <span data-ttu-id="b8f8c-111">如需 Azure 儲存體的一般資訊，請參閱 [儲存體文件](https://azure.microsoft.com/documentation/services/storage/) 。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-111">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="b8f8c-112">如需 Azure 雲端服務的一般資訊，請參閱 [雲端服務文件](https://azure.microsoft.com/documentation/services/cloud-services/) 。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-112">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="b8f8c-113">若需要如何編寫 ASP.NET 應用程式的詳細資訊，請參閱 [ASP.NET](http://www.asp.net) 。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-113">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

<span data-ttu-id="b8f8c-114">Azure 佇列儲存體是用於儲存大量訊息，可透過使用 HTTP 或 HTTPS 驗證呼叫的 hello world 中從任何地方存取服務。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-114">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="b8f8c-115">單一佇列訊息可以是總 too64 KB 的大小，並佇列可以包含數百萬個訊息，向上 toohello 總容量限制的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-115">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="b8f8c-116">在程式碼中存取佇列</span><span class="sxs-lookup"><span data-stu-id="b8f8c-116">Access queues in code</span></span>
<span data-ttu-id="b8f8c-117">tooaccess 佇列中的 Visual Studio 雲端服務專案，您需要 tooinclude hello 下列存取 Azure 佇列儲存體的項目 tooany C# 原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-117">tooaccess queues in Visual Studio Cloud Services projects, you need tooinclude hello following items tooany C# source file that access Azure Queue storage.</span></span>

1. <span data-ttu-id="b8f8c-118">請確定在 hello hello C# 檔案最上方的 hello 命名空間宣告包括**使用**陳述式。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-118">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. <span data-ttu-id="b8f8c-119">取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-119">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b8f8c-120">下列程式碼 tooget 使用 hello hello 您的儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-120">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="b8f8c-121">取得**CloudQueueClient** tooreference hello 佇列物件儲存體帳戶中的物件。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-121">Get a **CloudQueueClient** object tooreference hello queue objects in your storage account.</span></span>  
   
        // Create hello queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="b8f8c-122">取得**CloudQueue** tooreference 特定佇列的物件。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-122">Get a **CloudQueue** object tooreference a specific queue.</span></span>
   
        // Get a reference tooa queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="b8f8c-123">**注意：** hello 遵循範例中使用所有 hello hello 程式碼前面的程式碼上方。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-123">**NOTE:** Use all of hello above code in front of hello code in hello following samples.</span></span>

## <a name="create-a-queue-in-code"></a><span data-ttu-id="b8f8c-124">在程式碼中建立佇列</span><span class="sxs-lookup"><span data-stu-id="b8f8c-124">Create a queue in code</span></span>
<span data-ttu-id="b8f8c-125">toocreate hello 佇列中的程式碼，只要加入呼叫太**CreateIfNotExists**。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-125">toocreate hello queue in code, just add a call too**CreateIfNotExists**.</span></span>

    // Create hello CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="b8f8c-126">新增訊息 tooa 佇列</span><span class="sxs-lookup"><span data-stu-id="b8f8c-126">Add a message tooa queue</span></span>
<span data-ttu-id="b8f8c-127">tooinsert 將訊息插入現有佇列，建立新**CloudQueueMessage**物件，然後呼叫 hello **AddMessage**方法。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-127">tooinsert a message into an existing queue, create a new **CloudQueueMessage** object, then call hello **AddMessage** method.</span></span>

<span data-ttu-id="b8f8c-128">您可以從字串 (採用 UTF-8 格式) 或位元組陣列建立 **CloudQueueMessage** 物件。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-128">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="b8f8c-129">以下是範例插入 'Hello World' hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-129">Here is an example which inserts hello message 'Hello, World'.</span></span>

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="b8f8c-130">讀取佇列中的訊息</span><span class="sxs-lookup"><span data-stu-id="b8f8c-130">Read a message in a queue</span></span>
<span data-ttu-id="b8f8c-131">您可以查看 hello 前方的佇列中的 hello 訊息而不需移除 hello 佇列中所呼叫的 hello **PeekMessage**方法。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-131">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessage** method.</span></span>

    // Peek at hello next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="b8f8c-132">讀取並移除佇列中的訊息</span><span class="sxs-lookup"><span data-stu-id="b8f8c-132">Read and remove a message in a queue</span></span>
<span data-ttu-id="b8f8c-133">您的程式碼可以使用兩個步驟將訊息從佇列中移除 (清除佇列)。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-133">Your code can remove (de-queue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="b8f8c-134">呼叫**GetMessage** tooget hello 中的下一個訊息佇列。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-134">Call **GetMessage** tooget hello next message in a queue.</span></span> <span data-ttu-id="b8f8c-135">傳回訊息**GetMessage**變成不可見的 tooany 從此佇列讀取訊息的其他程式碼。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-135">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="b8f8c-136">依預設，此訊息會維持 30 秒的不可見狀態。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-136">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="b8f8c-137">移除 hello 佇列、 呼叫 hello 訊息 toofinish **DeleteMessage**。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-137">toofinish removing hello message from hello queue, call **DeleteMessage**.</span></span>

<span data-ttu-id="b8f8c-138">這兩個步驟的程序中移除訊息可確保，如果您的程式碼失敗的 tooprocess 到期 toohardware 或軟體失敗，您的程式碼的另一個執行個體訊息可以取得 hello 相同的訊息並再試一次。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-138">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="b8f8c-139">hello 下列程式碼呼叫**DeleteMessage**處理 hello 訊息之後，以滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-139">hello following code calls **DeleteMessage** right after hello message has been processed.</span></span>

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process hello message in less than 30 seconds

    // Then delete hello message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-tooprocess-and-remove-queue-messages"></a><span data-ttu-id="b8f8c-140">使用其他選項 tooprocess 並移除佇列的訊息</span><span class="sxs-lookup"><span data-stu-id="b8f8c-140">Use additional options tooprocess and remove queue messages</span></span>
<span data-ttu-id="b8f8c-141">自訂從佇列中擷取訊息的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-141">There are two ways you can customize message retrieval from a queue.</span></span>

* <span data-ttu-id="b8f8c-142">您可以取得一批訊息 （向上 too32)。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-142">You can get a batch of messages (up too32).</span></span>
* <span data-ttu-id="b8f8c-143">您可以設定長或短過了隱藏逾時，可讓您的程式碼更多或較少時間 toofully 處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-143">You can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="b8f8c-144">hello 下列程式碼範例使用**GetMessages**方法 tooget 20 訊息在單一呼叫中的。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-144">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="b8f8c-145">接著它會使用 **foreach** 迴圈處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-145">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="b8f8c-146">它也會設定 hello 過了隱藏逾時 toofive 分鐘數的每個訊息。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-146">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="b8f8c-147">請注意該 hello 5 分鐘所有 hello 訊息啟動相同的時間，因此後 5 分鐘自以來已經過 hello 呼叫太**GetMessages**，任何已被刪除的訊息一次將變成可見。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-147">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**GetMessages**, any messages which have not been deleted will become visible again.</span></span>

<span data-ttu-id="b8f8c-148">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="b8f8c-148">Here's an example:</span></span>

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete hello message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-hello-queue-length"></a><span data-ttu-id="b8f8c-149">取得 hello 佇列長度</span><span class="sxs-lookup"><span data-stu-id="b8f8c-149">Get hello queue length</span></span>
<span data-ttu-id="b8f8c-150">您可以在佇列中取得估計的 hello 訊息數目。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-150">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="b8f8c-151">**FetchAttributes**方法會要求 hello 佇列服務，以擷取 hello 佇列屬性，包括 hello 訊息計數。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-151">The **FetchAttributes** method asks hello Queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="b8f8c-152">hello **ApproximateMethodCount**屬性會傳回 hello 所擷取的最後一個值**FetchAttributes**方法，而不需要呼叫 hello 佇列服務。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-152">hello **ApproximateMethodCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello Queue service.</span></span>

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-azure-queue-apis"></a><span data-ttu-id="b8f8c-153">使用一般 Azure 佇列應用程式開發介面中的 hello 非同步等候模式</span><span class="sxs-lookup"><span data-stu-id="b8f8c-153">Use hello Async-Await Pattern with common Azure Queue APIs</span></span>
<span data-ttu-id="b8f8c-154">這個範例會示範如何 toouse hello 非同步等候模式與一般 Azure 佇列應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-154">This example shows how toouse hello Async-Await pattern with common Azure Queue APIs.</span></span> <span data-ttu-id="b8f8c-155">hello 範例會呼叫每個指定方法的 hello hello 非同步版本，這可以看見 hello**非同步**後修正每個方法。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-155">hello sample calls hello async version of each of hello given methods, this can be seen by hello **Async** post-fix of each method.</span></span> <span data-ttu-id="b8f8c-156">非同步方法時使用的 hello 非同步-await 模式會暫停本機執行，直到 hello 呼叫完成。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-156">When an async method is used hello async-await pattern suspends local execution until hello call completes.</span></span> <span data-ttu-id="b8f8c-157">此行為可讓目前的執行緒 toodo hello 其他工作，這有助於避免效能瓶頸並改善 hello 應用程式的整體回應性。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-157">This behavior allows hello current thread toodo other work which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="b8f8c-158">如需有關使用 hello.NET 中的非同步 Await 模式請參閱 < [Async 和 Await （C# 和 Visual Basic）](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="b8f8c-158">For more details on using hello Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message tooput in hello queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add hello message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete hello message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a><span data-ttu-id="b8f8c-159">刪除佇列</span><span class="sxs-lookup"><span data-stu-id="b8f8c-159">Delete a queue</span></span>
<span data-ttu-id="b8f8c-160">佇列和所有 hello 訊息包含在它呼叫 hello toodelete**刪除**hello 佇列物件上的方法。</span><span class="sxs-lookup"><span data-stu-id="b8f8c-160">toodelete a queue and all hello messages contained in it, call hello **Delete** method on hello queue object.</span></span>

    // Delete hello queue.
    messageQueue.Delete();

## <a name="next-steps"></a><span data-ttu-id="b8f8c-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8f8c-161">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

