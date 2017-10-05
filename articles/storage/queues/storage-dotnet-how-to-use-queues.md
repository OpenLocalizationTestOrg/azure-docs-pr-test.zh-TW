---
title: "以 .NET 開始使用 Azure 佇列儲存體 | Microsoft Docs"
description: "Azure 佇列可在應用程式元件之間提供可靠的非同步傳訊。 雲端傳訊可讓您的應用程式元件獨立擴充。"
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: c0f82537-a613-4f01-b2ed-fc82e5eea2a7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: robinsh
ms.openlocfilehash: aa292c1eb048444f988a641df44183312cf39d28
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a><span data-ttu-id="27368-104">以 .NET 開始使用 Azure 佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="27368-104">Get started with Azure Queue storage using .NET</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a><span data-ttu-id="27368-105">Overview</span><span class="sxs-lookup"><span data-stu-id="27368-105">Overview</span></span>
<span data-ttu-id="27368-106">Azure 佇列儲存體可提供應用程式元件之間的雲端傳訊。</span><span class="sxs-lookup"><span data-stu-id="27368-106">Azure Queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="27368-107">設計擴充性的應用程式時，會經常分離應用程式元件，以便進行個別擴充。</span><span class="sxs-lookup"><span data-stu-id="27368-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="27368-108">佇列儲存體可針對應用程式元件間的通訊，提供非同步傳訊，無論應用程式元件是在雲端、桌面、內部部署伺服器或行動裝置上執行。</span><span class="sxs-lookup"><span data-stu-id="27368-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="27368-109">佇列儲存體也支援管理非同步工作並建置處理工作流程。</span><span class="sxs-lookup"><span data-stu-id="27368-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="27368-110">關於本教學課程</span><span class="sxs-lookup"><span data-stu-id="27368-110">About this tutorial</span></span>
<span data-ttu-id="27368-111">本教學課程說明如何使用 Azure 佇列儲存體撰寫一些常見案例的 .NET 程式碼。</span><span class="sxs-lookup"><span data-stu-id="27368-111">This tutorial shows how to write .NET code for some common scenarios using Azure Queue storage.</span></span> <span data-ttu-id="27368-112">本文說明的案例包括建立和刪除佇列，以及新增、讀取和刪除佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="27368-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span></span>

<span data-ttu-id="27368-113">**預估完成時間：** 45 分鐘</span><span class="sxs-lookup"><span data-stu-id="27368-113">**Estimated time to complete:** 45 minutes</span></span>

<span data-ttu-id="27368-114">**先決條件：**</span><span class="sxs-lookup"><span data-stu-id="27368-114">**Prerequisities:**</span></span>

* [<span data-ttu-id="27368-115">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="27368-115">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="27368-116">適用於 .NET 的 Azure 儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="27368-116">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="27368-117">適用於.NET 的 Azure 設定管理員</span><span class="sxs-lookup"><span data-stu-id="27368-117">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="27368-118">[Azure 儲存體帳戶](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="27368-118">An [Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="27368-119">新增 using 指示詞</span><span class="sxs-lookup"><span data-stu-id="27368-119">Add using directives</span></span>
<span data-ttu-id="27368-120">將下列 `using` 指示詞新增至 `Program.cs` 檔案的開頭處：</span><span class="sxs-lookup"><span data-stu-id="27368-120">Add the following `using` directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="27368-121">解析連接字串</span><span class="sxs-lookup"><span data-stu-id="27368-121">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-queue-service-client"></a><span data-ttu-id="27368-122">建立佇列服務用戶端</span><span class="sxs-lookup"><span data-stu-id="27368-122">Create the Queue service client</span></span>
<span data-ttu-id="27368-123">**CloudQueueClient** 類別可讓您擷取佇列儲存體中儲存的佇列。</span><span class="sxs-lookup"><span data-stu-id="27368-123">The **CloudQueueClient** class enables you to retrieve queues stored in Queue storage.</span></span> <span data-ttu-id="27368-124">以下是建立服務用戶端的其中一種方式：</span><span class="sxs-lookup"><span data-stu-id="27368-124">Here's one way to create the service client:</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
<span data-ttu-id="27368-125">您現在可以開始撰寫程式碼，以讀取佇列儲存體的資料並將資料寫入其中。</span><span class="sxs-lookup"><span data-stu-id="27368-125">Now you are ready to write code that reads data from and writes data to Queue storage.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="27368-126">建立佇列</span><span class="sxs-lookup"><span data-stu-id="27368-126">Create a queue</span></span>
<span data-ttu-id="27368-127">此範例說明如何建立尚不存在的佇列：</span><span class="sxs-lookup"><span data-stu-id="27368-127">This example shows how to create a queue if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a><span data-ttu-id="27368-128">將訊息插入佇列</span><span class="sxs-lookup"><span data-stu-id="27368-128">Insert a message into a queue</span></span>
<span data-ttu-id="27368-129">若要將訊息插入現有佇列，請先建立新的 **CloudQueueMessage**。</span><span class="sxs-lookup"><span data-stu-id="27368-129">To insert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="27368-130">接著，呼叫 **AddMessage** 方法。</span><span class="sxs-lookup"><span data-stu-id="27368-130">Next, call the **AddMessage** method.</span></span> <span data-ttu-id="27368-131">您可以從字串 (採用 UTF-8 格式) 或**位元組**陣列建立 **CloudQueueMessage**。</span><span class="sxs-lookup"><span data-stu-id="27368-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span></span> <span data-ttu-id="27368-132">以下是建立佇列 (如果佇列不存在) 並插入訊息 'Hello, World' 的程式碼：</span><span class="sxs-lookup"><span data-stu-id="27368-132">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it to the queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-the-next-message"></a><span data-ttu-id="27368-133">查看下一個訊息</span><span class="sxs-lookup"><span data-stu-id="27368-133">Peek at the next message</span></span>
<span data-ttu-id="27368-134">透過呼叫 **PeekMessage** 方法，您可以在佇列前面查看訊息，而無需將它從佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="27368-134">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessage** method.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at the next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="27368-135">變更佇列訊息的內容</span><span class="sxs-lookup"><span data-stu-id="27368-135">Change the contents of a queued message</span></span>
<span data-ttu-id="27368-136">您可以在佇列中就地變更訊息內容。</span><span class="sxs-lookup"><span data-stu-id="27368-136">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="27368-137">如果訊息代表工作作業，則您可以使用此功能來更新工作作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="27368-137">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="27368-138">下列程式碼將使用新的內容更新佇列訊息，並將可見度逾時設定延長 60 秒。</span><span class="sxs-lookup"><span data-stu-id="27368-138">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="27368-139">這可儲存與訊息相關的工作狀態，並提供用戶端多一分鐘的時間繼續處理訊息。</span><span class="sxs-lookup"><span data-stu-id="27368-139">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="27368-140">您可以使用此技巧來追蹤佇列訊息上的多步驟工作流程，如果因為硬體或軟體故障而導致某個處理步驟失敗，將無需從頭開始。</span><span class="sxs-lookup"><span data-stu-id="27368-140">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="27368-141">通常，您也會保留重試計數，如果訊息重試超過 *n* 次，您會將它刪除。</span><span class="sxs-lookup"><span data-stu-id="27368-141">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="27368-142">這麼做可防止每次處理時便觸發應用程式錯誤的訊息。</span><span class="sxs-lookup"><span data-stu-id="27368-142">This protects against a message that triggers an application error each time it is processed.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the message from the queue and update the message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-the-next-message"></a><span data-ttu-id="27368-143">將下一個訊息清除佇列</span><span class="sxs-lookup"><span data-stu-id="27368-143">De-queue the next message</span></span>
<span data-ttu-id="27368-144">您的程式碼可以使用兩個步驟將訊息自佇列中清除佇列。</span><span class="sxs-lookup"><span data-stu-id="27368-144">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="27368-145">呼叫 **GetMessage**時，您會取得佇列中的下一個訊息。</span><span class="sxs-lookup"><span data-stu-id="27368-145">When you call **GetMessage**, you get the next message in a queue.</span></span> <span data-ttu-id="27368-146">從 **GetMessage** 傳回的訊息，對於從此佇列讀取訊息的任何其他程式碼而言將會是不可見的。</span><span class="sxs-lookup"><span data-stu-id="27368-146">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="27368-147">依預設，此訊息會維持 30 秒的不可見狀態。</span><span class="sxs-lookup"><span data-stu-id="27368-147">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="27368-148">若要完成從佇列中移除訊息，您還必須呼叫 **DeleteMessage**。</span><span class="sxs-lookup"><span data-stu-id="27368-148">To finish removing the message from the queue, you must also call **DeleteMessage**.</span></span> <span data-ttu-id="27368-149">這個移除訊息的兩步驟程序可確保您的程式碼因為硬體或軟體故障而無法處理訊息時，另一個程式碼的執行個體可以取得相同訊息並再試一次。</span><span class="sxs-lookup"><span data-stu-id="27368-149">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="27368-150">您的程式碼會在處理完訊息之後立即呼叫 **DeleteMessage** 。</span><span class="sxs-lookup"><span data-stu-id="27368-150">Your code calls **DeleteMessage** right after the message has been processed.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process the message in less than 30 seconds, and then delete the message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a><span data-ttu-id="27368-151">搭配通用佇列儲存體 API 使用 Async-Await 模式</span><span class="sxs-lookup"><span data-stu-id="27368-151">Use Async-Await pattern with common Queue storage APIs</span></span>
<span data-ttu-id="27368-152">這個範例示範如何搭配通用佇列儲存體 API 使用 Async-Await 模式。</span><span class="sxs-lookup"><span data-stu-id="27368-152">This example shows how to use the Async-Await pattern with common Queue storage APIs.</span></span> <span data-ttu-id="27368-153">此範例會呼叫每個指定方法的非同步版本，就像每個方法的非同步 *Async* 尾碼所指示的一樣。</span><span class="sxs-lookup"><span data-stu-id="27368-153">The sample calls the asynchronous version of each of the given methods, as indicated by the *Async* suffix of each method.</span></span> <span data-ttu-id="27368-154">使用非同步方法時，async-await 模式會暫停本機執行，直到呼叫完成為止。</span><span class="sxs-lookup"><span data-stu-id="27368-154">When an async method is used, the async-await pattern suspends local execution until the call completes.</span></span> <span data-ttu-id="27368-155">這種行為可讓目前的執行緒執行其他工作，有助於避免發生效能瓶頸並提升應用程式的整體回應。</span><span class="sxs-lookup"><span data-stu-id="27368-155">This behavior allows the current thread to do other work, which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="27368-156">如需在 .NET 中使用 Async-Await 模式的詳細資訊，請參閱 [Async 和 Await (C# 和 Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="27368-156">For more details on using the Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

```csharp
// Create the queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message to put in the queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue the message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue the message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete the message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="27368-157">運用清除佇列訊息的其他選項</span><span class="sxs-lookup"><span data-stu-id="27368-157">Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="27368-158">自訂從佇列中擷取訊息的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="27368-158">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="27368-159">首先，您可以取得一批訊息 (最多 32 個)。</span><span class="sxs-lookup"><span data-stu-id="27368-159">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="27368-160">其次，您可以設定較長或較短的可見度逾時，讓您的程式碼有較長或較短的時間可以完全處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="27368-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="27368-161">下列程式碼範例將使用 **GetMessages** 方法，在一次呼叫中取得 20 個訊息。</span><span class="sxs-lookup"><span data-stu-id="27368-161">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="27368-162">接著它會使用 **foreach** 迴圈處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="27368-162">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="27368-163">它也會將可見度逾時設定為每個訊息五分鐘。</span><span class="sxs-lookup"><span data-stu-id="27368-163">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="27368-164">請注意，系統會針對所有訊息同時開始計時 5 分鐘，所以從呼叫 **GetMessages**開始的 5 分鐘後，任何尚未刪除的訊息都會重新出現。</span><span class="sxs-lookup"><span data-stu-id="27368-164">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **GetMessages**, any messages which have not been deleted will become visible again.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-the-queue-length"></a><span data-ttu-id="27368-165">取得佇列長度</span><span class="sxs-lookup"><span data-stu-id="27368-165">Get the queue length</span></span>
<span data-ttu-id="27368-166">您可以取得佇列中的估計訊息數目。</span><span class="sxs-lookup"><span data-stu-id="27368-166">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="27368-167">**FetchAttributes** 方法會要求佇列服務擷取佇列屬性，其中包含訊息計數。</span><span class="sxs-lookup"><span data-stu-id="27368-167">The **FetchAttributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="27368-168">**ApproximateMessageCount** 屬性會傳回 **FetchAttributes** 方法所擷取的最後一個值，而無需呼叫佇列服務。</span><span class="sxs-lookup"><span data-stu-id="27368-168">The **ApproximateMessageCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the Queue service.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch the queue attributes.
queue.FetchAttributes();

// Retrieve the cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a><span data-ttu-id="27368-169">刪除佇列</span><span class="sxs-lookup"><span data-stu-id="27368-169">Delete a queue</span></span>
<span data-ttu-id="27368-170">若要刪除佇列及其內含的所有訊息，請在佇列物件上呼叫 **Delete** 方法。</span><span class="sxs-lookup"><span data-stu-id="27368-170">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete the queue.
queue.Delete();
```
    

## <a name="next-steps"></a><span data-ttu-id="27368-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="27368-171">Next steps</span></span>
<span data-ttu-id="27368-172">了解佇列儲存體的基礎概念之後，請參考下列連結以了解有關更複雜的儲存工作。</span><span class="sxs-lookup"><span data-stu-id="27368-172">Now that you've learned the basics of Queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="27368-173">如需可用 API 的完整詳細資訊，請檢視佇列服務參考文件：</span><span class="sxs-lookup"><span data-stu-id="27368-173">View the Queue service reference documentation for complete details about available APIs:</span></span>
  * [<span data-ttu-id="27368-174">Storage Client Library for .NET 參考資料</span><span class="sxs-lookup"><span data-stu-id="27368-174">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [<span data-ttu-id="27368-175">REST API 參考資料</span><span class="sxs-lookup"><span data-stu-id="27368-175">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="27368-176">了解如何使用 [Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md)，來簡化您撰寫以使用 Azure 儲存體的程式碼。</span><span class="sxs-lookup"><span data-stu-id="27368-176">Learn how to simplify the code you write to work with Azure Storage by using the [Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span>
* <span data-ttu-id="27368-177">如需了解 Azure 中的其他資料儲存選項，請檢視更多功能指南。</span><span class="sxs-lookup"><span data-stu-id="27368-177">View more feature guides to learn about additional options for storing data in Azure.</span></span>
  * <span data-ttu-id="27368-178">[以 .NET 開始使用 Azure 表格儲存體](../../cosmos-db/table-storage-how-to-use-dotnet.md) 以儲存結構化資料。</span><span class="sxs-lookup"><span data-stu-id="27368-178">[Get started with Azure Table storage using .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) to store structured data.</span></span>
  * <span data-ttu-id="27368-179">[以 .NET 開始使用 Azure Blob 儲存體](../blobs/storage-dotnet-how-to-use-blobs.md) 以儲存非結構化資料。</span><span class="sxs-lookup"><span data-stu-id="27368-179">[Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) to store unstructured data.</span></span>
  * <span data-ttu-id="27368-180">[使用 .NET (C#) 連接到 SQL Database ](../../sql-database/sql-database-connect-query-dotnet-core.md) 以儲存關聯式資料。</span><span class="sxs-lookup"><span data-stu-id="27368-180">[Connect to SQL Database by using .NET (C#)](../../sql-database/sql-database-connect-query-dotnet-core.md) to store relational data.</span></span>

[Download and install the Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
