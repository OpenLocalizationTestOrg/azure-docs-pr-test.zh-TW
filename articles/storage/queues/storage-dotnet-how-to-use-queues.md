---
title: "開始使用適用於.NET 的 Azure 佇列儲存體 aaaGet |Microsoft 文件"
description: "Azure 佇列可在應用程式元件之間提供可靠的非同步傳訊。 獨立雲端訊息可讓您的應用程式元件 tooscale。"
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
ms.openlocfilehash: 0cf6a71392b2fe859c7c9a9898c1ec84bcab4b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a><span data-ttu-id="3aa19-104">以 .NET 開始使用 Azure 佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="3aa19-104">Get started with Azure Queue storage using .NET</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a><span data-ttu-id="3aa19-105">Overview</span><span class="sxs-lookup"><span data-stu-id="3aa19-105">Overview</span></span>
<span data-ttu-id="3aa19-106">Azure 佇列儲存體可提供應用程式元件之間的雲端傳訊。</span><span class="sxs-lookup"><span data-stu-id="3aa19-106">Azure Queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="3aa19-107">設計擴充性的應用程式時，會經常分離應用程式元件，以便進行個別擴充。</span><span class="sxs-lookup"><span data-stu-id="3aa19-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="3aa19-108">佇列儲存體提供非同步傳訊應用程式元件之間的通訊是否在 hello 雲端中，在 hello 桌面上、 在內部部署伺服器上，或行動裝置上執行。</span><span class="sxs-lookup"><span data-stu-id="3aa19-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="3aa19-109">佇列儲存體也支援管理非同步工作並建置處理工作流程。</span><span class="sxs-lookup"><span data-stu-id="3aa19-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="3aa19-110">關於本教學課程</span><span class="sxs-lookup"><span data-stu-id="3aa19-110">About this tutorial</span></span>
<span data-ttu-id="3aa19-111">本教學課程會示範如何 toowrite.NET 程式碼為使用 Azure 佇列儲存體的一些常見案例。</span><span class="sxs-lookup"><span data-stu-id="3aa19-111">This tutorial shows how toowrite .NET code for some common scenarios using Azure Queue storage.</span></span> <span data-ttu-id="3aa19-112">本文說明的案例包括建立和刪除佇列，以及新增、讀取和刪除佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="3aa19-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span></span>

<span data-ttu-id="3aa19-113">**估計時間 toocomplete:** 45 分鐘的時間</span><span class="sxs-lookup"><span data-stu-id="3aa19-113">**Estimated time toocomplete:** 45 minutes</span></span>

<span data-ttu-id="3aa19-114">**先決條件：**</span><span class="sxs-lookup"><span data-stu-id="3aa19-114">**Prerequisities:**</span></span>

* [<span data-ttu-id="3aa19-115">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3aa19-115">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="3aa19-116">適用於 .NET 的 Azure 儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="3aa19-116">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="3aa19-117">適用於.NET 的 Azure 設定管理員</span><span class="sxs-lookup"><span data-stu-id="3aa19-117">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="3aa19-118">[Azure 儲存體帳戶](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="3aa19-118">An [Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="3aa19-119">新增 using 指示詞</span><span class="sxs-lookup"><span data-stu-id="3aa19-119">Add using directives</span></span>
<span data-ttu-id="3aa19-120">新增下列 hello`using`指示詞 toohello 頂端 hello`Program.cs`檔案：</span><span class="sxs-lookup"><span data-stu-id="3aa19-120">Add hello following `using` directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="3aa19-121">剖析 hello 連接字串</span><span class="sxs-lookup"><span data-stu-id="3aa19-121">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a><span data-ttu-id="3aa19-122">建立 hello 佇列服務用戶端</span><span class="sxs-lookup"><span data-stu-id="3aa19-122">Create hello Queue service client</span></span>
<span data-ttu-id="3aa19-123">hello **CloudQueueClient**類別可讓您 tooretrieve 佇列佇列儲存體中。</span><span class="sxs-lookup"><span data-stu-id="3aa19-123">hello **CloudQueueClient** class enables you tooretrieve queues stored in Queue storage.</span></span> <span data-ttu-id="3aa19-124">以下是其中一種方式 toocreate hello 服務用戶端：</span><span class="sxs-lookup"><span data-stu-id="3aa19-124">Here's one way toocreate hello service client:</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
<span data-ttu-id="3aa19-125">現在您已準備好 toowrite 讀取和寫入資料 tooQueue 儲存的程式碼。</span><span class="sxs-lookup"><span data-stu-id="3aa19-125">Now you are ready toowrite code that reads data from and writes data tooQueue storage.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="3aa19-126">建立佇列</span><span class="sxs-lookup"><span data-stu-id="3aa19-126">Create a queue</span></span>
<span data-ttu-id="3aa19-127">這個範例會示範如何 toocreate 佇列，如果不存在：</span><span class="sxs-lookup"><span data-stu-id="3aa19-127">This example shows how toocreate a queue if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a><span data-ttu-id="3aa19-128">將訊息插入佇列</span><span class="sxs-lookup"><span data-stu-id="3aa19-128">Insert a message into a queue</span></span>
<span data-ttu-id="3aa19-129">tooinsert 將訊息插入現有佇列，先建立新**CloudQueueMessage**。</span><span class="sxs-lookup"><span data-stu-id="3aa19-129">tooinsert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="3aa19-130">接下來，呼叫 hello **AddMessage**方法。</span><span class="sxs-lookup"><span data-stu-id="3aa19-130">Next, call hello **AddMessage** method.</span></span> <span data-ttu-id="3aa19-131">您可以從字串 (採用 UTF-8 格式) 或**位元組**陣列建立 **CloudQueueMessage**。</span><span class="sxs-lookup"><span data-stu-id="3aa19-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span></span> <span data-ttu-id="3aa19-132">以下是它會建立佇列 （如果存在） 並插入 hello 訊息 'Hello World' 的程式碼：</span><span class="sxs-lookup"><span data-stu-id="3aa19-132">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it toohello queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="3aa19-133">查看 hello 下一個訊息</span><span class="sxs-lookup"><span data-stu-id="3aa19-133">Peek at hello next message</span></span>
<span data-ttu-id="3aa19-134">您可以查看 hello 前方的佇列中的 hello 訊息而不需移除 hello 佇列中所呼叫的 hello **PeekMessage**方法。</span><span class="sxs-lookup"><span data-stu-id="3aa19-134">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessage** method.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at hello next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="3aa19-135">變更佇列的訊息 hello 內容</span><span class="sxs-lookup"><span data-stu-id="3aa19-135">Change hello contents of a queued message</span></span>
<span data-ttu-id="3aa19-136">您可以變更訊息就地 hello 佇列中的 hello 的內容。</span><span class="sxs-lookup"><span data-stu-id="3aa19-136">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="3aa19-137">如果訊息代表的工作，您可以使用此功能 tooupdate hello 工作工作的狀態。</span><span class="sxs-lookup"><span data-stu-id="3aa19-137">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="3aa19-138">下列程式碼的 hello 更新 hello 佇列訊息與新的內容，並設定 hello 的可見性逾時 tooextend 另一個 60 秒。</span><span class="sxs-lookup"><span data-stu-id="3aa19-138">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="3aa19-139">這樣會節省 hello 與 hello 訊息相關聯的工作狀態，並提供 hello 用戶端 hello 訊息處理的另一個分鐘 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="3aa19-139">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="3aa19-140">您無法使用此技巧 tootrack 多步驟工作流程佇列的訊息，而不需 toostart 透過從 hello 開頭，如果因為 toohardware 或軟體失敗的處理步驟失敗。</span><span class="sxs-lookup"><span data-stu-id="3aa19-140">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="3aa19-141">一般而言，您會保留重試計數，而且如果 hello 訊息重試一次以上 *n* 時間，您會將它刪除。</span><span class="sxs-lookup"><span data-stu-id="3aa19-141">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="3aa19-142">這麼做可防止每次處理時便觸發應用程式錯誤的訊息。</span><span class="sxs-lookup"><span data-stu-id="3aa19-142">This protects against a message that triggers an application error each time it is processed.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello message from hello queue and update hello message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="3aa19-143">清除佇列 hello 下一個訊息</span><span class="sxs-lookup"><span data-stu-id="3aa19-143">De-queue hello next message</span></span>
<span data-ttu-id="3aa19-144">您的程式碼可以使用兩個步驟將訊息自佇列中清除佇列。</span><span class="sxs-lookup"><span data-stu-id="3aa19-144">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="3aa19-145">當您呼叫**GetMessage**，您會收到 hello 下一個訊息，佇列中。</span><span class="sxs-lookup"><span data-stu-id="3aa19-145">When you call **GetMessage**, you get hello next message in a queue.</span></span> <span data-ttu-id="3aa19-146">傳回訊息**GetMessage**變成不可見的 tooany 從此佇列讀取訊息的其他程式碼。</span><span class="sxs-lookup"><span data-stu-id="3aa19-146">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="3aa19-147">依預設，此訊息會維持 30 秒的不可見狀態。</span><span class="sxs-lookup"><span data-stu-id="3aa19-147">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="3aa19-148">toofinish 移除 hello 訊息從 hello 佇列，您必須也呼叫**DeleteMessage**。</span><span class="sxs-lookup"><span data-stu-id="3aa19-148">toofinish removing hello message from hello queue, you must also call **DeleteMessage**.</span></span> <span data-ttu-id="3aa19-149">這兩個步驟的程序中移除訊息可確保，如果您的程式碼失敗的 tooprocess 到期 toohardware 或軟體失敗，您的程式碼的另一個執行個體訊息可以取得 hello 相同的訊息並再試一次。</span><span class="sxs-lookup"><span data-stu-id="3aa19-149">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="3aa19-150">您的程式碼呼叫**DeleteMessage**處理 hello 訊息之後，以滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="3aa19-150">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process hello message in less than 30 seconds, and then delete hello message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a><span data-ttu-id="3aa19-151">搭配通用佇列儲存體 API 使用 Async-Await 模式</span><span class="sxs-lookup"><span data-stu-id="3aa19-151">Use Async-Await pattern with common Queue storage APIs</span></span>
<span data-ttu-id="3aa19-152">這個範例會示範如何 toouse hello 非同步等候模式與一般佇列儲存體 Api。</span><span class="sxs-lookup"><span data-stu-id="3aa19-152">This example shows how toouse hello Async-Await pattern with common Queue storage APIs.</span></span> <span data-ttu-id="3aa19-153">hello 範例 hello 所示，呼叫 hello 非同步版本的每個指定方法的 hello*非同步*每一種方法的後置詞。</span><span class="sxs-lookup"><span data-stu-id="3aa19-153">hello sample calls hello asynchronous version of each of hello given methods, as indicated by hello *Async* suffix of each method.</span></span> <span data-ttu-id="3aa19-154">使用非同步方法時，hello 非同步-await 模式會暫停本機執行，直到 hello 呼叫完成。</span><span class="sxs-lookup"><span data-stu-id="3aa19-154">When an async method is used, hello async-await pattern suspends local execution until hello call completes.</span></span> <span data-ttu-id="3aa19-155">此行為可讓目前的執行緒 toodo hello 其他工作，可以協助避免效能瓶頸並提高 hello 應用程式的整體回應性。</span><span class="sxs-lookup"><span data-stu-id="3aa19-155">This behavior allows hello current thread toodo other work, which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="3aa19-156">如需有關使用 hello.NET 中的非同步 Await 模式請參閱 < [Async 和 Await （C# 和 Visual Basic）](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="3aa19-156">For more details on using hello Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

```csharp
// Create hello queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message tooput in hello queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue hello message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue hello message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete hello message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="3aa19-157">運用清除佇列訊息的其他選項</span><span class="sxs-lookup"><span data-stu-id="3aa19-157">Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="3aa19-158">自訂從佇列中擷取訊息的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="3aa19-158">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="3aa19-159">首先，您可以取得一批訊息 （向上 too32)。</span><span class="sxs-lookup"><span data-stu-id="3aa19-159">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="3aa19-160">第二，您可以設定長或短過了隱藏逾時，可讓您的程式碼更多或較少時間 toofully 處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="3aa19-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="3aa19-161">hello 下列程式碼範例使用**GetMessages**方法 tooget 20 訊息在單一呼叫中的。</span><span class="sxs-lookup"><span data-stu-id="3aa19-161">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="3aa19-162">接著它會使用 **foreach** 迴圈處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="3aa19-162">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="3aa19-163">它也會設定 hello 過了隱藏逾時 toofive 分鐘數的每個訊息。</span><span class="sxs-lookup"><span data-stu-id="3aa19-163">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="3aa19-164">請注意該 hello 5 分鐘所有 hello 訊息啟動相同的時間，因此後 5 分鐘自以來已經過 hello 呼叫太**GetMessages**，任何已被刪除的訊息一次將變成可見。</span><span class="sxs-lookup"><span data-stu-id="3aa19-164">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**GetMessages**, any messages which have not been deleted will become visible again.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-hello-queue-length"></a><span data-ttu-id="3aa19-165">取得 hello 佇列長度</span><span class="sxs-lookup"><span data-stu-id="3aa19-165">Get hello queue length</span></span>
<span data-ttu-id="3aa19-166">您可以在佇列中取得估計的 hello 訊息數目。</span><span class="sxs-lookup"><span data-stu-id="3aa19-166">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="3aa19-167">**FetchAttributes**方法會要求 hello 佇列服務，以擷取 hello 佇列屬性，包括 hello 訊息計數。</span><span class="sxs-lookup"><span data-stu-id="3aa19-167">The **FetchAttributes** method asks hello Queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="3aa19-168">hello **ApproximateMessageCount**屬性會傳回 hello 所擷取的最後一個值**FetchAttributes**方法，而不需要呼叫 hello 佇列服務。</span><span class="sxs-lookup"><span data-stu-id="3aa19-168">hello **ApproximateMessageCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello Queue service.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch hello queue attributes.
queue.FetchAttributes();

// Retrieve hello cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a><span data-ttu-id="3aa19-169">刪除佇列</span><span class="sxs-lookup"><span data-stu-id="3aa19-169">Delete a queue</span></span>
<span data-ttu-id="3aa19-170">toodelete 佇列和所有 hello 訊息包含在它，請呼叫**刪除**hello 佇列物件上的方法。</span><span class="sxs-lookup"><span data-stu-id="3aa19-170">toodelete a queue and all hello messages contained in it, call the **Delete** method on hello queue object.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete hello queue.
queue.Delete();
```
    

## <a name="next-steps"></a><span data-ttu-id="3aa19-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3aa19-171">Next steps</span></span>
<span data-ttu-id="3aa19-172">現在，您學到的佇列儲存體的 hello 基本概念，請遵循這些有關更複雜的儲存體工作的連結 toolearn。</span><span class="sxs-lookup"><span data-stu-id="3aa19-172">Now that you've learned hello basics of Queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="3aa19-173">檢視 hello 佇列服務參考文件，如需可用的應用程式開發介面的完整詳細資料：</span><span class="sxs-lookup"><span data-stu-id="3aa19-173">View hello Queue service reference documentation for complete details about available APIs:</span></span>
  * [<span data-ttu-id="3aa19-174">Storage Client Library for .NET 參考資料</span><span class="sxs-lookup"><span data-stu-id="3aa19-174">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [<span data-ttu-id="3aa19-175">REST API 參考資料</span><span class="sxs-lookup"><span data-stu-id="3aa19-175">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="3aa19-176">了解您所撰寫 toosimplify hello 程式碼如何使用 hello 與 Azure 儲存體 toowork [Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="3aa19-176">Learn how toosimplify hello code you write toowork with Azure Storage by using hello [Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span>
* <span data-ttu-id="3aa19-177">檢視有關將資料儲存在 Azure 中的其他選項的詳細功能指南 toolearn。</span><span class="sxs-lookup"><span data-stu-id="3aa19-177">View more feature guides toolearn about additional options for storing data in Azure.</span></span>
  * <span data-ttu-id="3aa19-178">[開始使用適用於.NET 的 Azure 資料表儲存體使用](../../cosmos-db/table-storage-how-to-use-dotnet.md)toostore 結構化資料。</span><span class="sxs-lookup"><span data-stu-id="3aa19-178">[Get started with Azure Table storage using .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) toostore structured data.</span></span>
  * <span data-ttu-id="3aa19-179">[開始使用適用於.NET 的 Azure Blob 儲存體使用](../blobs/storage-dotnet-how-to-use-blobs.md)toostore 非結構化的資料。</span><span class="sxs-lookup"><span data-stu-id="3aa19-179">[Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) toostore unstructured data.</span></span>
  * <span data-ttu-id="3aa19-180">[使用.NET (C#) 連線 tooSQL 資料庫](../../sql-database/sql-database-connect-query-dotnet-core.md)toostore 關聯式資料。</span><span class="sxs-lookup"><span data-stu-id="3aa19-180">[Connect tooSQL Database by using .NET (C#)](../../sql-database/sql-database-connect-query-dotnet-core.md) toostore relational data.</span></span>

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
