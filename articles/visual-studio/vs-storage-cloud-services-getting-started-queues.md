---
title: "開始使用佇列儲存體和 Visual Studio 已連接服務 (雲端服務) | Microsoft Docs"
description: "在使用 Visual Studio 已連接服務連接到儲存體帳戶之後，如何在 Visual Studio 雲端服務專案中開始使用 Azure 佇列儲存體"
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
ms.openlocfilehash: 7a6e58a62b4cfbf99641559363dd0c860cdf8af2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="14649-103">開始使用 Azure 佇列儲存體和 Visual Studio 已連接服務 (雲端服務專案)</span><span class="sxs-lookup"><span data-stu-id="14649-103">Getting started with Azure Queue storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="14649-104">Overview</span><span class="sxs-lookup"><span data-stu-id="14649-104">Overview</span></span>
<span data-ttu-id="14649-105">本文描述當您在雲端服務專案中建立或參考 Azure 儲存體帳戶之後，如何在 Visual Studio 中使用 [加入已連接服務] 對話方塊，開始使用 Azure 佇列儲存體。</span><span class="sxs-lookup"><span data-stu-id="14649-105">This article describes how to get started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using the  Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="14649-106">我們將會示範如何在程式碼中建立佇列。</span><span class="sxs-lookup"><span data-stu-id="14649-106">We'll show you how to create a queue in code.</span></span> <span data-ttu-id="14649-107">我們也將顯示如何執行基本的佇列作業，例如新增、修改、讀取和讀取佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="14649-107">We'll also show you how to perform basic queue operations, such as adding, modifying, reading and removing queue messages.</span></span> <span data-ttu-id="14649-108">這些範例均以 C# 程式碼撰寫，並使用 [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)。</span><span class="sxs-lookup"><span data-stu-id="14649-108">The samples are written in C# code and use the [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="14649-109">[ **新增連接的服務** ] 作業會安裝適當的 NuGet 封裝，以存取專案中的 Azure 儲存體，並將儲存體帳戶的連接字串新增至您的專案組態檔。</span><span class="sxs-lookup"><span data-stu-id="14649-109">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

* <span data-ttu-id="14649-110">如需以程式碼處理佇列的詳細資訊，請參閱 [以 .NET 開始使用 Azure 佇列儲存體](../storage/queues/storage-dotnet-how-to-use-queues.md) 。</span><span class="sxs-lookup"><span data-stu-id="14649-110">See [Get started with Azure Queue storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information on manipulating queues in code.</span></span>
* <span data-ttu-id="14649-111">如需 Azure 儲存體的一般資訊，請參閱 [儲存體文件](https://azure.microsoft.com/documentation/services/storage/) 。</span><span class="sxs-lookup"><span data-stu-id="14649-111">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="14649-112">如需 Azure 雲端服務的一般資訊，請參閱 [雲端服務文件](https://azure.microsoft.com/documentation/services/cloud-services/) 。</span><span class="sxs-lookup"><span data-stu-id="14649-112">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="14649-113">如需 ASP.NET 應用程式設計的詳細資訊，請參閱 [ASP.NET](http://www.asp.net) 。</span><span class="sxs-lookup"><span data-stu-id="14649-113">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

<span data-ttu-id="14649-114">Azure 佇列儲存體是一項儲存大量訊息的服務，全球任何地方都可利用 HTTP 或 HTTPS 並透過驗證的呼叫來存取這些訊息。</span><span class="sxs-lookup"><span data-stu-id="14649-114">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="14649-115">單一佇列訊息的大小上限為 64 KB，而一個佇列可以包含數百萬個訊息，以儲存體帳戶的總容量為限。</span><span class="sxs-lookup"><span data-stu-id="14649-115">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="14649-116">在程式碼中存取佇列</span><span class="sxs-lookup"><span data-stu-id="14649-116">Access queues in code</span></span>
<span data-ttu-id="14649-117">若要在 Visual Studio 雲端服務專案中存取佇列，您需要將下列項目加入至任何 C# 原始程式檔，以存取 Azure 佇列儲存體。</span><span class="sxs-lookup"><span data-stu-id="14649-117">To access queues in Visual Studio Cloud Services projects, you need to include the following items to any C# source file that access Azure Queue storage.</span></span>

1. <span data-ttu-id="14649-118">請確定 C# 檔案頂端的命名空間宣告包含這些 **using** 陳述式。</span><span class="sxs-lookup"><span data-stu-id="14649-118">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. <span data-ttu-id="14649-119">取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="14649-119">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="14649-120">使用下列程式碼，從 Azure 服務組態取得您的儲存體連接字串和儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="14649-120">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="14649-121">取得 **CloudQueueClient** 物件以參考儲存體帳戶中的佇列物件。</span><span class="sxs-lookup"><span data-stu-id="14649-121">Get a **CloudQueueClient** object to reference the queue objects in your storage account.</span></span>  
   
        // Create the queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="14649-122">取得 **CloudQueue** 物件以參考特定的佇列。</span><span class="sxs-lookup"><span data-stu-id="14649-122">Get a **CloudQueue** object to reference a specific queue.</span></span>
   
        // Get a reference to a queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="14649-123">**注意：** 請在下列範例中的程式碼前面使用上述所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="14649-123">**NOTE:** Use all of the above code in front of the code in the following samples.</span></span>

## <a name="create-a-queue-in-code"></a><span data-ttu-id="14649-124">在程式碼中建立佇列</span><span class="sxs-lookup"><span data-stu-id="14649-124">Create a queue in code</span></span>
<span data-ttu-id="14649-125">若要在程式碼中建立佇列，請加入 **CreateIfNotExists**呼叫。</span><span class="sxs-lookup"><span data-stu-id="14649-125">To create the queue in code, just add a call to **CreateIfNotExists**.</span></span>

    // Create the CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="14649-126">將訊息新增至佇列</span><span class="sxs-lookup"><span data-stu-id="14649-126">Add a message to a queue</span></span>
<span data-ttu-id="14649-127">若要將訊息插入現有佇列，請建立新的 **CloudQueueMessage** 物件，然後呼叫 **AddMessage** 方法。</span><span class="sxs-lookup"><span data-stu-id="14649-127">To insert a message into an existing queue, create a new **CloudQueueMessage** object, then call the **AddMessage** method.</span></span>

<span data-ttu-id="14649-128">您可以從字串 (採用 UTF-8 格式) 或位元組陣列建立 **CloudQueueMessage** 物件。</span><span class="sxs-lookup"><span data-stu-id="14649-128">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="14649-129">以下是插入訊息 'Hello, World' 的範例。</span><span class="sxs-lookup"><span data-stu-id="14649-129">Here is an example which inserts the message 'Hello, World'.</span></span>

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="14649-130">讀取佇列中的訊息</span><span class="sxs-lookup"><span data-stu-id="14649-130">Read a message in a queue</span></span>
<span data-ttu-id="14649-131">透過呼叫 **PeekMessage** 方法，您可以在佇列前面查看訊息，而無需將它從佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="14649-131">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessage** method.</span></span>

    // Peek at the next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="14649-132">讀取並移除佇列中的訊息</span><span class="sxs-lookup"><span data-stu-id="14649-132">Read and remove a message in a queue</span></span>
<span data-ttu-id="14649-133">您的程式碼可以使用兩個步驟將訊息從佇列中移除 (清除佇列)。</span><span class="sxs-lookup"><span data-stu-id="14649-133">Your code can remove (de-queue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="14649-134">呼叫 **GetMessage** 以取得佇列中的下一個訊息。</span><span class="sxs-lookup"><span data-stu-id="14649-134">Call **GetMessage** to get the next message in a queue.</span></span> <span data-ttu-id="14649-135">從 **GetMessage** 傳回的訊息，對於從此佇列讀取訊息的任何其他程式碼而言將會是不可見的。</span><span class="sxs-lookup"><span data-stu-id="14649-135">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="14649-136">依預設，此訊息會維持 30 秒的不可見狀態。</span><span class="sxs-lookup"><span data-stu-id="14649-136">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="14649-137">若要完成從佇列中移除訊息，請呼叫 **DeleteMessage**。</span><span class="sxs-lookup"><span data-stu-id="14649-137">To finish removing the message from the queue, call **DeleteMessage**.</span></span>

<span data-ttu-id="14649-138">這個移除訊息的兩步驟程序可確保您的程式碼因為硬體或軟體故障而無法處理訊息時，另一個程式碼的執行個體可以取得相同訊息並再試一次。</span><span class="sxs-lookup"><span data-stu-id="14649-138">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="14649-139">下列程式碼會在處理完訊息之後立即呼叫 **DeleteMessage** 。</span><span class="sxs-lookup"><span data-stu-id="14649-139">The following code calls **DeleteMessage** right after the message has been processed.</span></span>

    // Get the next message in the queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process the message in less than 30 seconds

    // Then delete the message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-to-process-and-remove-queue-messages"></a><span data-ttu-id="14649-140">使用其他選項來處理和移除佇列訊息</span><span class="sxs-lookup"><span data-stu-id="14649-140">Use additional options to process and remove queue messages</span></span>
<span data-ttu-id="14649-141">自訂從佇列中擷取訊息的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="14649-141">There are two ways you can customize message retrieval from a queue.</span></span>

* <span data-ttu-id="14649-142">您可以取得一批訊息 (最多 32 個)。</span><span class="sxs-lookup"><span data-stu-id="14649-142">You can get a batch of messages (up to 32).</span></span>
* <span data-ttu-id="14649-143">您可以設定較長或較短的可見度逾時，讓您的程式碼有較長或較短的時間可以完全處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="14649-143">You can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="14649-144">下列程式碼範例將使用 **GetMessages** 方法，在一次呼叫中取得 20 個訊息。</span><span class="sxs-lookup"><span data-stu-id="14649-144">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="14649-145">接著它會使用 **foreach** 迴圈處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="14649-145">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="14649-146">它也會將可見度逾時設定為每個訊息五分鐘。</span><span class="sxs-lookup"><span data-stu-id="14649-146">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="14649-147">請注意，系統會針對所有訊息同時開始計時 5 分鐘，所以從呼叫 **GetMessages**開始的 5 分鐘後，任何尚未刪除的訊息都會重新出現。</span><span class="sxs-lookup"><span data-stu-id="14649-147">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **GetMessages**, any messages which have not been deleted will become visible again.</span></span>

<span data-ttu-id="14649-148">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="14649-148">Here's an example:</span></span>

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete the message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-the-queue-length"></a><span data-ttu-id="14649-149">取得佇列長度</span><span class="sxs-lookup"><span data-stu-id="14649-149">Get the queue length</span></span>
<span data-ttu-id="14649-150">您可以取得佇列中的估計訊息數目。</span><span class="sxs-lookup"><span data-stu-id="14649-150">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="14649-151">**FetchAttributes** 方法會要求佇列服務擷取佇列屬性，其中包含訊息計數。</span><span class="sxs-lookup"><span data-stu-id="14649-151">The **FetchAttributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="14649-152">**ApproximateMethodCount** 屬性會傳回 **FetchAttributes** 方法所擷取的最後一個值，而無需呼叫佇列服務。</span><span class="sxs-lookup"><span data-stu-id="14649-152">The **ApproximateMethodCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the Queue service.</span></span>

    // Fetch the queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve the cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-the-async-await-pattern-with-common-azure-queue-apis"></a><span data-ttu-id="14649-153">搭配使用 Async-Await 模式和通用 Azure 佇列 API</span><span class="sxs-lookup"><span data-stu-id="14649-153">Use the Async-Await Pattern with common Azure Queue APIs</span></span>
<span data-ttu-id="14649-154">這個範例示範如何搭配使用 Async-Await 模式和通用 Azure 佇列 API。</span><span class="sxs-lookup"><span data-stu-id="14649-154">This example shows how to use the Async-Await pattern with common Azure Queue APIs.</span></span> <span data-ttu-id="14649-155">此範例會呼叫每個指定方法的非同步版本，這可從每個方法的 **Async** 字尾看出。</span><span class="sxs-lookup"><span data-stu-id="14649-155">The sample calls the async version of each of the given methods, this can be seen by the **Async** post-fix of each method.</span></span> <span data-ttu-id="14649-156">使用非同步方法時，async-await 模式會暫停本機執行，直到呼叫完成為止。</span><span class="sxs-lookup"><span data-stu-id="14649-156">When an async method is used the async-await pattern suspends local execution until the call completes.</span></span> <span data-ttu-id="14649-157">這種行為可讓目前的執行緒執行其他工作，有助於避免發生效能瓶頸並提升應用程式的整體回應。</span><span class="sxs-lookup"><span data-stu-id="14649-157">This behavior allows the current thread to do other work which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="14649-158">如需在 .NET 中使用 Async-Await 模式的詳細資訊，請參閱 [Async 和 Await (C# 和 Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="14649-158">For more details on using the Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message to put in the queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add the message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue the message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete the message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a><span data-ttu-id="14649-159">刪除佇列</span><span class="sxs-lookup"><span data-stu-id="14649-159">Delete a queue</span></span>
<span data-ttu-id="14649-160">若要刪除佇列及其內含的所有訊息，請在佇列物件上呼叫 **Delete** 方法。</span><span class="sxs-lookup"><span data-stu-id="14649-160">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

    // Delete the queue.
    messageQueue.Delete();

## <a name="next-steps"></a><span data-ttu-id="14649-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="14649-161">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

