---
title: "開始使用佇列儲存體和 Visual Studio 已連接服務 (WebJob 專案) | Microsoft Docs"
description: "在使用 Visual Studio 已連接服務連接至儲存體帳戶之後，如何於 WebJob 專案中開始使用 Azure 佇列儲存體。"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: ef40db782114bfdaa02dafeabcfc6da6c41423e1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="05db8-103">開始使用 Azure 佇列儲存體和 Visual Studio 已連接服務 (WebJob 專案)</span><span class="sxs-lookup"><span data-stu-id="05db8-103">Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="05db8-104">Overview</span><span class="sxs-lookup"><span data-stu-id="05db8-104">Overview</span></span>
<span data-ttu-id="05db8-105">本文描述如何在您使用 Visual Studio 的 [新增連接的服務] 對話方塊，建立或參考了 Azure 儲存體帳戶之後，開始在 Visual Studio Azure WebJob 專案中使用 Azure 佇列儲存體。</span><span class="sxs-lookup"><span data-stu-id="05db8-105">This article describes how get started using Azure Queue storage in a Visual Studio Azure WebJob project after you have created or referenced an Azure storage account by using the Visual Studio  **Add Connected Services** dialog box.</span></span> <span data-ttu-id="05db8-106">當您使用 Visual Studio [新增連接的服務]  對話方塊將儲存體帳戶加入 WebJob 專案時，適當的 Azure 儲存體 NuGet 封裝便已安裝、適當的 .NET 參考會加入至專案，以及儲存體帳戶的連接字串會在 App.config 檔案中更新。</span><span class="sxs-lookup"><span data-stu-id="05db8-106">When you add a storage account to a WebJob project by using the Visual Studio **Add Connected Services** dialog, the appropriate Azure Storage NuGet packages are installed, the appropriate .NET references are added to the project, and connection strings for the storage account are updated in the App.config file.</span></span>  

<span data-ttu-id="05db8-107">本文提供了 C# 程式碼範例，示範如何透過 Azure 佇列儲存體服務使用 Azure WebJobs SDK 1.x 版。</span><span class="sxs-lookup"><span data-stu-id="05db8-107">This article provides C# code samples that show how to use the Azure WebJobs SDK version 1.x with the Azure Queue storage service.</span></span>

<span data-ttu-id="05db8-108">Azure 佇列儲存體是一項儲存大量訊息的服務，全球任何地方都可利用 HTTP 或 HTTPS 並透過驗證的呼叫來存取這些訊息。</span><span class="sxs-lookup"><span data-stu-id="05db8-108">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="05db8-109">單一佇列訊息的大小上限為 64 KB，而一個佇列可以包含數百萬個訊息，以儲存體帳戶的總容量為限。</span><span class="sxs-lookup"><span data-stu-id="05db8-109">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span> <span data-ttu-id="05db8-110">如需詳細資訊，請參閱 [以 .NET 開始使用 Azure 佇列儲存體](../storage/queues/storage-dotnet-how-to-use-queues.md) 。</span><span class="sxs-lookup"><span data-stu-id="05db8-110">See [Get started with Azure Queue Storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information.</span></span> <span data-ttu-id="05db8-111">如需 ASP.NET 的詳細資訊，請參閱 [ASP.NET](http://www.asp.net)。</span><span class="sxs-lookup"><span data-stu-id="05db8-111">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="how-to-trigger-a-function-when-a-queue-message-is-received"></a><span data-ttu-id="05db8-112">如何在接收到佇列訊息時觸發函數</span><span class="sxs-lookup"><span data-stu-id="05db8-112">How to trigger a function when a queue message is received</span></span>
<span data-ttu-id="05db8-113">若要撰寫 WebJobs SDK 在收到佇列訊息時所呼叫的函數，請使用 **QueueTrigger** 屬性。</span><span class="sxs-lookup"><span data-stu-id="05db8-113">To write a function that the WebJobs SDK calls when a queue message is received, use the **QueueTrigger** attribute.</span></span> <span data-ttu-id="05db8-114">屬性建構函式採用字串參數，來指定要輪詢的佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="05db8-114">The attribute constructor takes a string parameter that specifies the name of the queue to poll.</span></span> <span data-ttu-id="05db8-115">若要了解如何動態設定佇列名稱，請參閱 [如何設定組態選項](#how-to-set-configuration-options)。</span><span class="sxs-lookup"><span data-stu-id="05db8-115">To see how to set the queue name dynamically, check out [How to set Configuration Options](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="05db8-116">字串佇列訊息</span><span class="sxs-lookup"><span data-stu-id="05db8-116">String queue messages</span></span>
<span data-ttu-id="05db8-117">在下列範例中，佇列包含字串訊息，以便 **QueueTrigger** 套用至名為 **logMessage** 的字串參數，其中包含佇列訊息的內容。</span><span class="sxs-lookup"><span data-stu-id="05db8-117">In the following example, the queue contains a string message, so **QueueTrigger** is applied to a string parameter named **logMessage** which contains the content of the queue message.</span></span> <span data-ttu-id="05db8-118">函數會 [將記錄訊息寫入儀表板](#how-to-write-logs)。</span><span class="sxs-lookup"><span data-stu-id="05db8-118">The function [writes a log message to the Dashboard](#how-to-write-logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="05db8-119">除了 **string** 以外，參數可能是位元組陣列、**CloudQueueMessage** 物件或您定義的 POCO。</span><span class="sxs-lookup"><span data-stu-id="05db8-119">Besides **string**, the parameter may be a byte array, a **CloudQueueMessage** object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="05db8-120">POCO ( [純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 佇列訊息</span><span class="sxs-lookup"><span data-stu-id="05db8-120">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="05db8-121">在下列範例中，佇列訊息會包含 **BlobInformation** 物件的 JSON，其中包含 **BlobName** 屬性。</span><span class="sxs-lookup"><span data-stu-id="05db8-121">In the following example, the queue message contains JSON for a **BlobInformation** object which includes a **BlobName** property.</span></span> <span data-ttu-id="05db8-122">SDK 會自動將物件還原序列化。</span><span class="sxs-lookup"><span data-stu-id="05db8-122">The SDK automatically deserializes the object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="05db8-123">SDK 會使用 [Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) 封裝來序列化和還原序列化訊息。</span><span class="sxs-lookup"><span data-stu-id="05db8-123">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="05db8-124">如果您在不使用 WebJobs SDK 的程式中建立佇列訊息，您可以撰寫和下面範例類似的程式碼來建立 SDK 能夠剖析的 POCO 佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="05db8-124">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="05db8-125">Async 函數</span><span class="sxs-lookup"><span data-stu-id="05db8-125">Async functions</span></span>
<span data-ttu-id="05db8-126">下面的非同步函式會 [將記錄檔寫入儀表板](#how-to-write-logs)。</span><span class="sxs-lookup"><span data-stu-id="05db8-126">The following async function [writes a log to the Dashboard](#how-to-write-logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="05db8-127">Async 函數可能需要取 [消語彙基元](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken)，如下列範例所示 (會複製 Blob)。</span><span class="sxs-lookup"><span data-stu-id="05db8-127">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in the following example which copies a blob.</span></span> <span data-ttu-id="05db8-128">(如需 **queueTrigger** 預留位置的說明，請參閱 [Blob](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) 區段)。</span><span class="sxs-lookup"><span data-stu-id="05db8-128">(For an explanation of the **queueTrigger** placeholder, see the [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-the-queuetrigger-attribute-works-with"></a><span data-ttu-id="05db8-129">適用於 QueueTrigger 屬性的型別</span><span class="sxs-lookup"><span data-stu-id="05db8-129">Types the QueueTrigger attribute works with</span></span>
<span data-ttu-id="05db8-130">您可以將 **QueueTrigger** 與下列類型搭配使用：</span><span class="sxs-lookup"><span data-stu-id="05db8-130">You can use **QueueTrigger** with the following types:</span></span>

* <span data-ttu-id="05db8-131">**字串**</span><span class="sxs-lookup"><span data-stu-id="05db8-131">**string**</span></span>
* <span data-ttu-id="05db8-132">序列化為 JSON 的 POCO 型別</span><span class="sxs-lookup"><span data-stu-id="05db8-132">A POCO type serialized as JSON</span></span>
* <span data-ttu-id="05db8-133">**byte[]**</span><span class="sxs-lookup"><span data-stu-id="05db8-133">**byte[]**</span></span>
* <span data-ttu-id="05db8-134">**CloudQueueMessage**</span><span class="sxs-lookup"><span data-stu-id="05db8-134">**CloudQueueMessage**</span></span>

## <a name="polling-algorithm"></a><span data-ttu-id="05db8-135">輪詢演算法</span><span class="sxs-lookup"><span data-stu-id="05db8-135">Polling algorithm</span></span>
<span data-ttu-id="05db8-136">SDK 會實作隨機指數型倒退演算法，以降低閒置佇列輪詢對儲存體交易成本的影響。</span><span class="sxs-lookup"><span data-stu-id="05db8-136">The SDK implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="05db8-137">找到訊息時，SDK 會等待兩秒，然後檢查的另一個訊息；當找不到任何訊息時，它會等候大約四秒，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="05db8-137">When a message is found, the SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="05db8-138">連續嘗試取得佇列訊息失敗後，等候時間會持續增加，直到它到達等待時間上限 (預設值為一分鐘)。</span><span class="sxs-lookup"><span data-stu-id="05db8-138">After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.</span></span> <span data-ttu-id="05db8-139">[您可以設定等待時間上限](#how-to-set-configuration-options)。</span><span class="sxs-lookup"><span data-stu-id="05db8-139">[The maximum wait time is configurable](#how-to-set-configuration-options).</span></span>

## <a name="multiple-instances"></a><span data-ttu-id="05db8-140">多個執行個體</span><span class="sxs-lookup"><span data-stu-id="05db8-140">Multiple instances</span></span>
<span data-ttu-id="05db8-141">如果您的 Web 應用程式在多個執行個體上執行，則連續 WebJob 將在每部機器上執行，而且每部機器將會等待觸發程序並嘗試執行函數。</span><span class="sxs-lookup"><span data-stu-id="05db8-141">If your web app runs on multiple instances, a continuous WebJobs runs on each machine, and each machine will wait for triggers and attempt to run functions.</span></span> <span data-ttu-id="05db8-142">在某些案例中，這會導致部分函數處理相同的資料兩次，因此函數應是以等冪的方式 (寫入，因此使用相同輸入資料重複呼叫函數才不會產生重複的結果)。</span><span class="sxs-lookup"><span data-stu-id="05db8-142">In some scenarios this can lead to some functions processing the same data twice, so functions should be idempotent (written so that calling them repeatedly with the same input data doesn't produce duplicate results).</span></span>  

## <a name="parallel-execution"></a><span data-ttu-id="05db8-143">平行執行</span><span class="sxs-lookup"><span data-stu-id="05db8-143">Parallel execution</span></span>
<span data-ttu-id="05db8-144">如果您有多個函數在不同的佇列上接聽，則同時接收到訊息時，SDK 會以平行方式呼叫它們。</span><span class="sxs-lookup"><span data-stu-id="05db8-144">If you have multiple functions listening on different queues, the SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="05db8-145">收到單一佇列的多個訊息時也是如此。</span><span class="sxs-lookup"><span data-stu-id="05db8-145">The same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="05db8-146">根據預設，SDK 會一次取得一批 (16 個) 佇列訊息，並執行以平行方式處理它們的函數。</span><span class="sxs-lookup"><span data-stu-id="05db8-146">By default, the SDK gets a batch of 16 queue messages at a time and executes the function that processes them in parallel.</span></span> <span data-ttu-id="05db8-147">[您可以設定批次大小](#how-to-set-configuration-options)。</span><span class="sxs-lookup"><span data-stu-id="05db8-147">[The batch size is configurable](#how-to-set-configuration-options).</span></span> <span data-ttu-id="05db8-148">當要處理的訊息數目減少到批次大小 (該批訊息數目) 的一半時，SDK 就會取得另一批訊息並開始處理那些訊息。</span><span class="sxs-lookup"><span data-stu-id="05db8-148">When the number being processed gets down to half of the batch size, the SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="05db8-149">因此，每個函數並行處理之訊息的上限數目為批次大小 (該批訊息數目) 的 1.5 倍。</span><span class="sxs-lookup"><span data-stu-id="05db8-149">Therefore the maximum number of concurrent messages being processed per function is one and a half times the batch size.</span></span> <span data-ttu-id="05db8-150">這項限制個別套用至具有 **QueueTrigger** 屬性的每個函數。</span><span class="sxs-lookup"><span data-stu-id="05db8-150">This limit applies separately to each function that has a **QueueTrigger** attribute.</span></span> <span data-ttu-id="05db8-151">如果您不想平行執行在單一佇列中收到的訊息，請將批次大小設定為 1。</span><span class="sxs-lookup"><span data-stu-id="05db8-151">If you don't want parallel execution for messages received on one queue, set the batch size to 1.</span></span>

## <a name="get-queue-or-queue-message-metadata"></a><span data-ttu-id="05db8-152">取得佇列或佇列訊息中繼資料</span><span class="sxs-lookup"><span data-stu-id="05db8-152">Get queue or queue message metadata</span></span>
<span data-ttu-id="05db8-153">您可以透過新增參數至方法簽章來取得下列訊息屬性：</span><span class="sxs-lookup"><span data-stu-id="05db8-153">You can get the following message properties by adding parameters to the method signature:</span></span>

* <span data-ttu-id="05db8-154">**DateTimeOffset** expirationTime</span><span class="sxs-lookup"><span data-stu-id="05db8-154">**DateTimeOffset** expirationTime</span></span>
* <span data-ttu-id="05db8-155">**DateTimeOffset** insertionTime</span><span class="sxs-lookup"><span data-stu-id="05db8-155">**DateTimeOffset** insertionTime</span></span>
* <span data-ttu-id="05db8-156">**DateTimeOffset** nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="05db8-156">**DateTimeOffset** nextVisibleTime</span></span>
* <span data-ttu-id="05db8-157">**string** queueTrigger (包含訊息文字)</span><span class="sxs-lookup"><span data-stu-id="05db8-157">**string** queueTrigger (contains message text)</span></span>
* <span data-ttu-id="05db8-158">**string** id</span><span class="sxs-lookup"><span data-stu-id="05db8-158">**string** id</span></span>
* <span data-ttu-id="05db8-159">**string** popReceipt</span><span class="sxs-lookup"><span data-stu-id="05db8-159">**string** popReceipt</span></span>
* <span data-ttu-id="05db8-160">**int** dequeueCount</span><span class="sxs-lookup"><span data-stu-id="05db8-160">**int** dequeueCount</span></span>

<span data-ttu-id="05db8-161">如果您想要直接使用 Azure 儲存體 API，您也可以加入 **CloudStorageAccount** 參數。</span><span class="sxs-lookup"><span data-stu-id="05db8-161">If you want to work directly with the Azure storage API, you can also add a **CloudStorageAccount** parameter.</span></span>

<span data-ttu-id="05db8-162">下列範例會將此中繼資料全部寫入至 INFO 應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="05db8-162">The following example writes all of this metadata to an INFO application log.</span></span> <span data-ttu-id="05db8-163">在範例中，logMessage 和 queueTrigger 包含佇列訊息的內容。</span><span class="sxs-lookup"><span data-stu-id="05db8-163">In the example, both logMessage and queueTrigger contain the content of the queue message.</span></span>

        public static void WriteLog([QueueTrigger("logqueue")] string logMessage,
            DateTimeOffset expirationTime,
            DateTimeOffset insertionTime,
            DateTimeOffset nextVisibleTime,
            string id,
            string popReceipt,
            int dequeueCount,
            string queueTrigger,
            CloudStorageAccount cloudStorageAccount,
            TextWriter logger)
        {
            logger.WriteLine(
                "logMessage={0}\n" +
            "expirationTime={1}\ninsertionTime={2}\n" +
                "nextVisibleTime={3}\n" +
                "id={4}\npopReceipt={5}\ndequeueCount={6}\n" +
                "queue endpoint={7} queueTrigger={8}",
                logMessage, expirationTime,
                insertionTime,
                nextVisibleTime, id,
                popReceipt, dequeueCount,
                cloudStorageAccount.QueueEndpoint,
                queueTrigger);
        }

<span data-ttu-id="05db8-164">以下是範例程式碼所寫入的範例記錄：</span><span class="sxs-lookup"><span data-stu-id="05db8-164">Here is a sample log written by the sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a><span data-ttu-id="05db8-165">正常關機</span><span class="sxs-lookup"><span data-stu-id="05db8-165">Graceful shutdown</span></span>
<span data-ttu-id="05db8-166">連續 WebJob 中執行的函數可以接受 **CancellationToken** 參數，來讓作業系統能夠在 WebJob 即將終止時通知函數。</span><span class="sxs-lookup"><span data-stu-id="05db8-166">A function that runs in a continuous WebJob can accept a **CancellationToken** parameter which enables the operating system to notify the function when the WebJob is about to be terminated.</span></span> <span data-ttu-id="05db8-167">您可以使用此通知來確保函數不會在讓資料維持不一致狀態的情況下意外終止。</span><span class="sxs-lookup"><span data-stu-id="05db8-167">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="05db8-168">下列範例示範如何透過函數檢查即將終止的 WebJob。</span><span class="sxs-lookup"><span data-stu-id="05db8-168">The following example shows how to check for impending WebJob termination in a function.</span></span>

    public static void GracefulShutdownDemo(
                [QueueTrigger("inputqueue")] string inputText,
                TextWriter logger,
                CancellationToken token)
    {
        for (int i = 0; i < 100; i++)
        {
            if (token.IsCancellationRequested)
            {
                logger.WriteLine("Function was cancelled at iteration {0}", i);
                break;
            }
            Thread.Sleep(1000);
            logger.WriteLine("Normal processing for queue message={0}", inputText);
        }
    }

<span data-ttu-id="05db8-169">**注意：** 儀表板可能不會正確顯示已關閉之函數的狀態與輸出。</span><span class="sxs-lookup"><span data-stu-id="05db8-169">**Note:** The Dashboard might not correctly show the status and output of functions that have been shut down.</span></span>

<span data-ttu-id="05db8-170">如需詳細資訊，請參閱 [WebJobs 正常關機](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR)。</span><span class="sxs-lookup"><span data-stu-id="05db8-170">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <a name="how-to-create-a-queue-message-while-processing-a-queue-message"></a><span data-ttu-id="05db8-171">如何在處理佇列訊息時建立佇列訊息</span><span class="sxs-lookup"><span data-stu-id="05db8-171">How to create a queue message while processing a queue message</span></span>
<span data-ttu-id="05db8-172">若要編寫會建立新佇列訊息的函數，請使用 **Queue** 屬性。</span><span class="sxs-lookup"><span data-stu-id="05db8-172">To write a function that creates a new queue message, use the **Queue** attribute.</span></span> <span data-ttu-id="05db8-173">如同 **QueueTrigger**，您可透過字串傳入佇列名稱，或可以 [動態設定的佇列名稱](#how-to-set-configuration-options)。</span><span class="sxs-lookup"><span data-stu-id="05db8-173">Like **QueueTrigger**, you pass in the queue name as a string or you can [set the queue name dynamically](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="05db8-174">字串佇列訊息</span><span class="sxs-lookup"><span data-stu-id="05db8-174">String queue messages</span></span>
<span data-ttu-id="05db8-175">下面的非同步程式碼範例會在名稱為 "outputqueue" 的佇列中建立一個新的佇列訊息，其內容與名為 "inputqueue" 的佇列中收到的佇列訊息相同。</span><span class="sxs-lookup"><span data-stu-id="05db8-175">The following non-async code sample creates a new queue message in the queue named "outputqueue" with the same content as the queue message received in the queue named "inputqueue".</span></span> <span data-ttu-id="05db8-176">(如需非同步函式，請使用 **IAsyncCollector<T>**，如本節後續內容所示。)</span><span class="sxs-lookup"><span data-stu-id="05db8-176">(For async functions use **IAsyncCollector<T>** as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="05db8-177">POCO ( [純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 佇列訊息</span><span class="sxs-lookup"><span data-stu-id="05db8-177">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="05db8-178">若要建立包含 POCO 物件 (而非字串) 的佇列訊息，請將 POCO 做為輸出參數傳送至 **Queue** 屬性建構函式。</span><span class="sxs-lookup"><span data-stu-id="05db8-178">To create a queue message that contains a POCO rather than a string, pass the POCO type as an output parameter to the **Queue** attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="05db8-179">SDK 會自動將物件序列化為 JSON。</span><span class="sxs-lookup"><span data-stu-id="05db8-179">The SDK automatically serializes the object to JSON.</span></span> <span data-ttu-id="05db8-180">即使物件是空值，也一律會建立佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="05db8-180">A queue message is always created, even if the object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="05db8-181">建立多個訊息或使用非同步函式</span><span class="sxs-lookup"><span data-stu-id="05db8-181">Create multiple messages or in async functions</span></span>
<span data-ttu-id="05db8-182">若要建立多個訊息，將 **ICollector<T>** 或 **IAsyncCollector<T>** 設為輸出佇列的參數類型，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="05db8-182">To create multiple messages, make the parameter type for the output queue **ICollector<T>** or **IAsyncCollector<T>**, as shown in the following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="05db8-183">呼叫 **Add** 方法時，即會立即建立每個佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="05db8-183">Each queue message is created immediately when the **Add** method is called.</span></span>

### <a name="types-that-the-queue-attribute-works-with"></a><span data-ttu-id="05db8-184">適用於 Queue 屬性的型別</span><span class="sxs-lookup"><span data-stu-id="05db8-184">Types that the Queue attribute works with</span></span>
<span data-ttu-id="05db8-185">您可以在下列參數型別使用 **Queue** 屬性：</span><span class="sxs-lookup"><span data-stu-id="05db8-185">You can use the **Queue** attribute on the following parameter types:</span></span>

* <span data-ttu-id="05db8-186">**out string** (函式結束時，如果參數值非 Null，就會建立佇列訊息)</span><span class="sxs-lookup"><span data-stu-id="05db8-186">**out string** (creates queue message if parameter value is non-null when the function ends)</span></span>
* <span data-ttu-id="05db8-187">**out byte[]** (運作方式類似 **字串**)</span><span class="sxs-lookup"><span data-stu-id="05db8-187">**out byte[]** (works like **string**)</span></span>
* <span data-ttu-id="05db8-188">**out CloudQueueMessage** (運作方式類似 **字串**)</span><span class="sxs-lookup"><span data-stu-id="05db8-188">**out CloudQueueMessage** (works like **string**)</span></span>
* <span data-ttu-id="05db8-189">**out POCO** (可序列化型別，當函式結束時，如果參數為 Null，就會使用 Null 物件建立訊息)</span><span class="sxs-lookup"><span data-stu-id="05db8-189">**out POCO** (a serializable type, creates a message with a null object if the paramter is null when the function ends)</span></span>
* <span data-ttu-id="05db8-190">**ICollector**</span><span class="sxs-lookup"><span data-stu-id="05db8-190">**ICollector**</span></span>
* <span data-ttu-id="05db8-191">**IAsyncCollector**</span><span class="sxs-lookup"><span data-stu-id="05db8-191">**IAsyncCollector**</span></span>
* <span data-ttu-id="05db8-192">**CloudQueue** (用於直接使用 Azure 儲存體 API 手動建立訊息)</span><span class="sxs-lookup"><span data-stu-id="05db8-192">**CloudQueue** (for creating messages manually using the Azure Storage API directly)</span></span>

### <a name="use-webjobs-sdk-attributes-in-the-body-of-a-function"></a><span data-ttu-id="05db8-193">在函式主體中使用 WebJobs SDK 屬性</span><span class="sxs-lookup"><span data-stu-id="05db8-193">Use WebJobs SDK attributes in the body of a function</span></span>
<span data-ttu-id="05db8-194">如果您需要先在函式中執行部分工作，然後再使用 WebJobs SDK 屬性，例如 **Queue****Blob** 或 **Table**，您可以使用 **IBinder** 介面。</span><span class="sxs-lookup"><span data-stu-id="05db8-194">If you need to do some work in your function before using a WebJobs SDK attribute such as **Queue**, **Blob**, or **Table**, you can use the **IBinder** interface.</span></span>

<span data-ttu-id="05db8-195">下列範例會使用輸入佇列訊息，並在輸出佇列中建立含有相同內容的新訊息。</span><span class="sxs-lookup"><span data-stu-id="05db8-195">The following example takes an input queue message and creates a new message with the same content in an output queue.</span></span> <span data-ttu-id="05db8-196">輸出佇列名稱會由函數主體中的程式碼設定。</span><span class="sxs-lookup"><span data-stu-id="05db8-196">The output queue name is set by code in the body of the function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="05db8-197">**IBinder** 介面也可以搭配 **Table** 和 **Blob** 屬性使用。</span><span class="sxs-lookup"><span data-stu-id="05db8-197">The **IBinder** interface can also be used with the **Table** and **Blob** attributes.</span></span>

## <a name="how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message"></a><span data-ttu-id="05db8-198">如何在處理佇列訊息時讀取和寫入 Blob 和資料表</span><span class="sxs-lookup"><span data-stu-id="05db8-198">How to read and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="05db8-199">**Blob** 和 **Table** 屬性可讓您讀取和寫入 Blob 和資料表。</span><span class="sxs-lookup"><span data-stu-id="05db8-199">The **Blob** and **Table** attributes enable you to read and write blobs and tables.</span></span> <span data-ttu-id="05db8-200">本節中的範例適用於 Blob。</span><span class="sxs-lookup"><span data-stu-id="05db8-200">The samples in this section apply to blobs.</span></span> <span data-ttu-id="05db8-201">如需示範如何在建立或更新 Blob 時觸發程序的程式碼範例，請參閱[如何透過 WebJobs SDK 使用 Azure Blob 儲存體](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)，若需讀取和撰寫資料表的程式碼範例，請參閱[如何透過 WebJobs SDK 使用 Azure 資料表儲存體](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="05db8-201">For code samples that show how to trigger processes when blobs are created or updated, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How to use Azure table storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="05db8-202">觸發 Blob 作業的字串佇列訊息</span><span class="sxs-lookup"><span data-stu-id="05db8-202">String queue messages triggering blob operations</span></span>
<span data-ttu-id="05db8-203">對於包含字串的佇列訊息，**queueTrigger** 預留位置可在 **Blob** 屬性的 **blobPath** 參數中使用，其中包含訊息的內容。</span><span class="sxs-lookup"><span data-stu-id="05db8-203">For a queue message that contains a string, **queueTrigger** is a placeholder you can use in the **Blob** attribute's **blobPath** parameter that contains the contents of the message.</span></span>

<span data-ttu-id="05db8-204">下列範例會使用 **Stream** 物件來讀取和寫入 Blob。</span><span class="sxs-lookup"><span data-stu-id="05db8-204">The following example uses **Stream** objects to read and write blobs.</span></span> <span data-ttu-id="05db8-205">佇列訊息提供位於 textblobs 容器中 Blob 的名稱。</span><span class="sxs-lookup"><span data-stu-id="05db8-205">The queue message is the name of a blob located in the textblobs container.</span></span> <span data-ttu-id="05db8-206">會在相同的容器中建立 Blob 的複本，並在其名稱中附加 "-new"。</span><span class="sxs-lookup"><span data-stu-id="05db8-206">A copy of the blob with "-new" appended to the name is created in the same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="05db8-207">**Blob** 屬性建構函式採用 **blobPath** 參數來指定容器與 Blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="05db8-207">The **Blob** attribute constructor takes a **blobPath** parameter that specifies the container and blob name.</span></span> <span data-ttu-id="05db8-208">如需此預留位置的詳細資訊，請參閱 [如何透過 WebJobs SDK 使用 Azure Blob 儲存體](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="05db8-208">For more information about this placeholder, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span></span>

<span data-ttu-id="05db8-209">當這個屬性裝飾 **Stream** 物件，另一個建構函式參數會將 **FileAccess** 模式指定為讀取、寫入或讀取/寫入。</span><span class="sxs-lookup"><span data-stu-id="05db8-209">When the attribute decorates a **Stream** object, another constructor parameter specifies the **FileAccess** mode as read, write, or read/write.</span></span>

<span data-ttu-id="05db8-210">下列範例會使用 **CloudBlockBlob** 物件刪除 Blob。</span><span class="sxs-lookup"><span data-stu-id="05db8-210">The following example uses a **CloudBlockBlob** object to delete a blob.</span></span> <span data-ttu-id="05db8-211">佇列訊息就是 Blob 的名稱。</span><span class="sxs-lookup"><span data-stu-id="05db8-211">The queue message is the name of the blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="05db8-212">POCO ( [純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 佇列訊息</span><span class="sxs-lookup"><span data-stu-id="05db8-212">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="05db8-213">針對以 JSON 格式儲存在佇列訊息中的 POCO，您可以使用 **Queue** 屬性之 **blobPath** 參數中物件的屬性名稱來做為預留位置。</span><span class="sxs-lookup"><span data-stu-id="05db8-213">For a POCO stored as JSON in the queue message, you can use placeholders that name properties of the object in the **Queue** attribute's **blobPath** parameter.</span></span> <span data-ttu-id="05db8-214">您也可以使用佇列中繼資料屬性名稱做為預留位置。</span><span class="sxs-lookup"><span data-stu-id="05db8-214">You can also use queue metadata property names as placeholders.</span></span> <span data-ttu-id="05db8-215">請參閱 [取得佇列或佇列訊息中繼資料](#get-queue-or-queue-message-metadata)。</span><span class="sxs-lookup"><span data-stu-id="05db8-215">See [Get queue or queue message metadata](#get-queue-or-queue-message-metadata).</span></span>

<span data-ttu-id="05db8-216">下列範例會將 Blob 複製到具有不同副檔名的新 Blob。</span><span class="sxs-lookup"><span data-stu-id="05db8-216">The following example copies a blob to a new blob with a different extension.</span></span> <span data-ttu-id="05db8-217">佇列訊息是包含 **BlobName** 和 **BlobNameWithoutExtension** 屬性的 **BlobInformation** 物件。</span><span class="sxs-lookup"><span data-stu-id="05db8-217">The queue message is a **BlobInformation** object that includes **BlobName** and **BlobNameWithoutExtension** properties.</span></span> <span data-ttu-id="05db8-218">在 **Blob** 屬性的 Blob 路徑中使用屬性名稱做為預留位置。</span><span class="sxs-lookup"><span data-stu-id="05db8-218">The property names are used as placeholders in the blob path for the **Blob** attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="05db8-219">SDK 會使用 [Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) 封裝來序列化和還原序列化訊息。</span><span class="sxs-lookup"><span data-stu-id="05db8-219">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="05db8-220">如果您在不使用 WebJobs SDK 的程式中建立佇列訊息，您可以撰寫和下面範例類似的程式碼來建立 SDK 能夠剖析的 POCO 佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="05db8-220">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="05db8-221">如果您需要先在函式中執行部分工作，然後再將 Blob 繫結至物件，您可以在函式主體中使用屬性，如 [在函式主體中使用 WebJobs SDK 屬性](#use-webjobs-sdk-attributes-in-the-body-of-a-function)中所示。</span><span class="sxs-lookup"><span data-stu-id="05db8-221">If you need to do some work in your function before binding a blob to an object, you can use the attribute in the body of the function, as shown in [Use WebJobs SDK attributes in the body of a function](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span></span>

### <a name="types-you-can-use-the-blob-attribute-with"></a><span data-ttu-id="05db8-222">可以與 Blob 屬性搭配使用的型別</span><span class="sxs-lookup"><span data-stu-id="05db8-222">Types you can use the Blob attribute with</span></span>
<span data-ttu-id="05db8-223">**Blob** 屬性能與下列型別搭配使用：</span><span class="sxs-lookup"><span data-stu-id="05db8-223">The **Blob** attribute can be used with the following types:</span></span>

* <span data-ttu-id="05db8-224">**Stream** (讀取或寫入，可使用 FileAccess 建構函式參數指定)</span><span class="sxs-lookup"><span data-stu-id="05db8-224">**Stream** (read or write, specified by using the FileAccess constructor parameter)</span></span>
* <span data-ttu-id="05db8-225">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="05db8-225">**TextReader**</span></span>
* <span data-ttu-id="05db8-226">**TextWriter**</span><span class="sxs-lookup"><span data-stu-id="05db8-226">**TextWriter**</span></span>
* <span data-ttu-id="05db8-227">**string** (讀取)</span><span class="sxs-lookup"><span data-stu-id="05db8-227">**string** (read)</span></span>
* <span data-ttu-id="05db8-228">**out string** (寫入；當函式傳回時，如果字串參數非 Null，就只會建立 Blob)</span><span class="sxs-lookup"><span data-stu-id="05db8-228">**out string** (write; creates a blob only if the string parameter is non-null when the function returns)</span></span>
* <span data-ttu-id="05db8-229">POCO (讀取)</span><span class="sxs-lookup"><span data-stu-id="05db8-229">POCO (read)</span></span>
* <span data-ttu-id="05db8-230">out POCO (寫入；一律會建立 Blob，當函式傳回時，如果 POCO 參數為 Null，就建立為 Null 物件)</span><span class="sxs-lookup"><span data-stu-id="05db8-230">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when the function returns)</span></span>
* <span data-ttu-id="05db8-231">**CloudBlobStream** (寫入)</span><span class="sxs-lookup"><span data-stu-id="05db8-231">**CloudBlobStream** (write)</span></span>
* <span data-ttu-id="05db8-232">**ICloudBlob** (讀取或寫入)</span><span class="sxs-lookup"><span data-stu-id="05db8-232">**ICloudBlob** (read or write)</span></span>
* <span data-ttu-id="05db8-233">**CloudBlockBlob** (讀取或寫入)</span><span class="sxs-lookup"><span data-stu-id="05db8-233">**CloudBlockBlob** (read or write)</span></span>
* <span data-ttu-id="05db8-234">**CloudPageBlob** (讀取或寫入)</span><span class="sxs-lookup"><span data-stu-id="05db8-234">**CloudPageBlob** (read or write)</span></span>

## <a name="how-to-handle-poison-messages"></a><span data-ttu-id="05db8-235">如何處理有害訊息</span><span class="sxs-lookup"><span data-stu-id="05db8-235">How to handle poison messages</span></span>
<span data-ttu-id="05db8-236">內容會導致函數失敗的訊息稱為「有害訊息」 。</span><span class="sxs-lookup"><span data-stu-id="05db8-236">Messages whose content causes a function to fail are called *poison messages*.</span></span> <span data-ttu-id="05db8-237">當函數失敗時不會刪除佇列訊息，最後會再度挑選到該訊息，造成重複循環。</span><span class="sxs-lookup"><span data-stu-id="05db8-237">When the function fails, the queue message is not deleted and eventually is picked up again, causing the cycle to be repeated.</span></span> <span data-ttu-id="05db8-238">SDK 可在有限的反覆次數之後自動中斷循環，或者您可以手動中斷循環。</span><span class="sxs-lookup"><span data-stu-id="05db8-238">The SDK can automatically interrupt the cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="05db8-239">自動處理有害訊息</span><span class="sxs-lookup"><span data-stu-id="05db8-239">Automatic poison message handling</span></span>
<span data-ttu-id="05db8-240">SDK 將會呼叫函數最多 5 次以處理佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="05db8-240">The SDK will call a function up to 5 times to process a queue message.</span></span> <span data-ttu-id="05db8-241">如果第五次嘗試失敗，訊息便會移到有害佇列中。</span><span class="sxs-lookup"><span data-stu-id="05db8-241">If the fifth try fails, the message is moved to a poison queue.</span></span> <span data-ttu-id="05db8-242">您可以在 [如何設定組態選項](#how-to-set-configuration-options)中了解如何設定重試次數上限。</span><span class="sxs-lookup"><span data-stu-id="05db8-242">You can see how to configure the maximum number of retries in [How to set configuration options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="05db8-243">有害佇列名為 *{originalqueuename}*-poison。</span><span class="sxs-lookup"><span data-stu-id="05db8-243">The poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="05db8-244">您可以撰寫函數，透過記錄或傳送通知表示需要手動處理，來處理有害佇列中的訊息。</span><span class="sxs-lookup"><span data-stu-id="05db8-244">You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="05db8-245">在下列範例中，當佇列訊息包含不存在的 Blob 名稱， **CopyBlob** 函數將會失敗。</span><span class="sxs-lookup"><span data-stu-id="05db8-245">In the following example the **CopyBlob** function will fail when a queue message contains the name of a blob that doesn't exist.</span></span> <span data-ttu-id="05db8-246">發生時，就會從 copyblobqueue 佇列將訊息移至 copyblobqueue-poison 佇列。</span><span class="sxs-lookup"><span data-stu-id="05db8-246">When that happens, the message is moved from the copyblobqueue queue to the copyblobqueue-poison queue.</span></span> <span data-ttu-id="05db8-247">接著， **ProcessPoisonMessage** 會記錄有害訊息。</span><span class="sxs-lookup"><span data-stu-id="05db8-247">The **ProcessPoisonMessage** then logs the poison message.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

        public static void ProcessPoisonMessage(
            [QueueTrigger("copyblobqueue-poison")] string blobName, TextWriter logger)
        {
            logger.WriteLine("Failed to copy blob, name=" + blobName);
        }

<span data-ttu-id="05db8-248">下圖顯示這些函數處理有害訊息之後的主控台輸出。</span><span class="sxs-lookup"><span data-stu-id="05db8-248">The following illustration shows console output from these functions when a poison message is processed.</span></span>

![主控台輸出中的有害訊息處理](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="05db8-250">手動處理有害訊息</span><span class="sxs-lookup"><span data-stu-id="05db8-250">Manual poison message handling</span></span>
<span data-ttu-id="05db8-251">您可以將名為 **dequeueCount** 的 **int** 參數加入到函數中，來取得訊息已被挑選來處理的次數。</span><span class="sxs-lookup"><span data-stu-id="05db8-251">You can get the number of times a message has been picked up for processing by adding an **int** parameter named **dequeueCount** to your function.</span></span> <span data-ttu-id="05db8-252">然後您可以檢查函數程式碼中的清除佇列計數，並在數目超出臨界值時自行執行有害訊息處理，如下面的範例所示。</span><span class="sxs-lookup"><span data-stu-id="05db8-252">You can then check the dequeue count in function code and perform your own poison message handling when the number exceeds a threshold, as shown in the following example.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed to copy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a name="how-to-set-configuration-options"></a><span data-ttu-id="05db8-253">如何設定組態選項</span><span class="sxs-lookup"><span data-stu-id="05db8-253">How to set configuration options</span></span>
<span data-ttu-id="05db8-254">您可以使用 **JobHostConfiguration** 類型來設定下列組態選項：</span><span class="sxs-lookup"><span data-stu-id="05db8-254">You can use the **JobHostConfiguration** type to set the following configuration options:</span></span>

* <span data-ttu-id="05db8-255">在程式碼中設定 SDK 連接字串。</span><span class="sxs-lookup"><span data-stu-id="05db8-255">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="05db8-256">配置 **QueueTrigger** 設定，例如清除佇列計數上限。</span><span class="sxs-lookup"><span data-stu-id="05db8-256">Configure **QueueTrigger** settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="05db8-257">從組態取得佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="05db8-257">Get queue names from configuration.</span></span>

### <a name="set-sdk-connection-strings-in-code"></a><span data-ttu-id="05db8-258">在程式碼中設定 SDK 連接字串</span><span class="sxs-lookup"><span data-stu-id="05db8-258">Set SDK connection strings in code</span></span>
<span data-ttu-id="05db8-259">在程式碼中設定 SDK 連接字串可讓您在組態檔或環境變數中使用您自己的連接字串名稱，如下面範例所示。</span><span class="sxs-lookup"><span data-stu-id="05db8-259">Setting the SDK connection strings in code enables you to use your own connection string names in configuration files or environment variables, as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            var _storageConn = ConfigurationManager
                .ConnectionStrings["MyStorageConnection"].ConnectionString;

            var _dashboardConn = ConfigurationManager
                .ConnectionStrings["MyDashboardConnection"].ConnectionString;

            var _serviceBusConn = ConfigurationManager
                .ConnectionStrings["MyServiceBusConnection"].ConnectionString;

            JobHostConfiguration config = new JobHostConfiguration();
            config.StorageConnectionString = _storageConn;
            config.DashboardConnectionString = _dashboardConn;
            config.ServiceBusConnectionString = _serviceBusConn;
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="configure-queuetrigger--settings"></a><span data-ttu-id="05db8-260">設定 QueueTrigger 設定</span><span class="sxs-lookup"><span data-stu-id="05db8-260">Configure QueueTrigger  settings</span></span>
<span data-ttu-id="05db8-261">您可以配置會套用至佇列訊息處理的下列設定：</span><span class="sxs-lookup"><span data-stu-id="05db8-261">You can configure the following settings that apply to the queue message processing:</span></span>

* <span data-ttu-id="05db8-262">挑選以同時平行執行的佇列訊息數目上限 (預設值為 16)。</span><span class="sxs-lookup"><span data-stu-id="05db8-262">The maximum number of queue messages that are picked up simultaneously to be executed in parallel (default is 16).</span></span>
* <span data-ttu-id="05db8-263">將佇列訊息傳送到有害佇列之前的重試次數上限 (預設值為 5)。</span><span class="sxs-lookup"><span data-stu-id="05db8-263">The maximum number of retries before a queue message is sent to a poison queue (default is 5).</span></span>
* <span data-ttu-id="05db8-264">佇列為空的時，要再次輪詢前的等待時間上限 (預設值為 1 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="05db8-264">The maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="05db8-265">下列範例示範如何配置這些設定：</span><span class="sxs-lookup"><span data-stu-id="05db8-265">The following example shows how to configure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a><span data-ttu-id="05db8-266">在程式碼中設定 WebJobs SDK 建構函式參數的值</span><span class="sxs-lookup"><span data-stu-id="05db8-266">Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="05db8-267">有時候您不想要採取硬式編碼的方式，而是在程式碼中指定佇列名稱、Blob 名稱或容器或資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="05db8-267">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="05db8-268">例如，您可能想要在組態檔或環境變數中指定 **QueueTrigger** 的佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="05db8-268">For example, you might want to specify the queue name for **QueueTrigger** in a configuration file or environment variable.</span></span>

<span data-ttu-id="05db8-269">您可以藉由將 **NameResolver** 物件傳入至 **JobHostConfiguration** 類型來執行此作業。</span><span class="sxs-lookup"><span data-stu-id="05db8-269">You can do that by passing in a **NameResolver** object to the **JobHostConfiguration** type.</span></span> <span data-ttu-id="05db8-270">在 WebJobs SDK 屬性建構函式參數中包含以百分比 (%) 符號括住的特殊預留位置，然後 **NameResolver** 程式碼會指定實際要用以取代那些預留位置的值。</span><span class="sxs-lookup"><span data-stu-id="05db8-270">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your **NameResolver** code specifies the actual values to be used in place of those placeholders.</span></span>

<span data-ttu-id="05db8-271">例如，假設您想要在測試環境中使用名為 logqueuetest 的佇列，和在生產環境中使用名為 logqueueprod 的佇列。</span><span class="sxs-lookup"><span data-stu-id="05db8-271">For example, suppose you want to use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="05db8-272">不用將佇列名稱寫入程式碼，您要在 **appSettings** 集合 (會有實際佇列名稱) 中指定項目名稱。</span><span class="sxs-lookup"><span data-stu-id="05db8-272">Instead of a hard-coded queue name, you want to specify the name of an entry in the **appSettings** collection that would have the actual queue name.</span></span> <span data-ttu-id="05db8-273">如果 **appSettings** 索引鍵是 logqueue，您的函數看起來可能如下所示。</span><span class="sxs-lookup"><span data-stu-id="05db8-273">If the **appSettings** key is logqueue, your function could look like the following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="05db8-274">**NameResolver** 類別接著可以從 **appSettings** 取得佇列名稱，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="05db8-274">Your **NameResolver** class could then get the queue name from **appSettings** as shown in the following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="05db8-275">您可以將 **NameResolver** 類別傳遞至 **JobHost** 物件中，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="05db8-275">You pass the **NameResolver** class in to the **JobHost** object as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="05db8-276">**注意：** 每次呼叫函式時，都會解析佇列、資料表及 Blob 名稱，但只有在應用程式啟動時才會解析 Blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="05db8-276">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when the application starts.</span></span> <span data-ttu-id="05db8-277">您無法在執行工作時，變更 Blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="05db8-277">You can't change blob container name while the job is running.</span></span>

## <a name="how-to-trigger-a-function-manually"></a><span data-ttu-id="05db8-278">如何手動觸發函數</span><span class="sxs-lookup"><span data-stu-id="05db8-278">How to trigger a function manually</span></span>
<span data-ttu-id="05db8-279">若要手動觸發函數，請在 **JobHost** 物件上使用 **Call** 或 **CallAsync** 方法，和在函數上使用 **NoAutomaticTrigger** 屬性，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="05db8-279">To trigger a function manually, use the **Call** or **CallAsync** method on the **JobHost** object and the **NoAutomaticTrigger** attribute on the function, as shown in the following example.</span></span>

        public class Program
        {
            static void Main(string[] args)
            {
                JobHost host = new JobHost();
                host.Call(typeof(Program).GetMethod("CreateQueueMessage"), new { value = "Hello world!" });
            }

            [NoAutomaticTrigger]
            public static void CreateQueueMessage(
                TextWriter logger,
                string value,
                [Queue("outputqueue")] out string message)
            {
                message = value;
                logger.WriteLine("Creating queue message: ", message);
            }
        }

## <a name="how-to-write-logs"></a><span data-ttu-id="05db8-280">如何寫入記錄檔</span><span class="sxs-lookup"><span data-stu-id="05db8-280">How to write logs</span></span>
<span data-ttu-id="05db8-281">儀表板會在兩個地方顯示記錄檔：WebJob 的頁面與特定 WebJob 引動過程的頁面。</span><span class="sxs-lookup"><span data-stu-id="05db8-281">The Dashboard shows logs in two places: the page for the WebJob, and the page for a particular WebJob invocation.</span></span>

![WebJob 頁面中的記錄檔](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![函式引動過程頁面中的記錄檔](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="05db8-284">您在函式或在 **Main()** 方法中所呼叫主控台方法的輸出會顯示在 WebJob 的 [儀表板] 頁面，而不是特定方法引動過程的頁面。</span><span class="sxs-lookup"><span data-stu-id="05db8-284">Output from Console methods that you call in a function or in the **Main()** method appears in the Dashboard page for the WebJob, not in the page for a particular method invocation.</span></span> <span data-ttu-id="05db8-285">您從方法簽章的參數所取得 TextWriter 物件的輸出會顯示在方法引動過程的 [儀表板] 頁面。</span><span class="sxs-lookup"><span data-stu-id="05db8-285">Output from the TextWriter object that you get from a parameter in your method signature appears in the Dashboard page for a method invocation.</span></span>

<span data-ttu-id="05db8-286">因為主控台屬於單一執行緒，無法同時執行許多工作函式，所以主控台輸出無法連結到特定的方法引動過程。</span><span class="sxs-lookup"><span data-stu-id="05db8-286">Console output can't be linked to a particular method invocation because the Console is single-threaded, while many job functions may be running at the same time.</span></span> <span data-ttu-id="05db8-287">這就是 SDK 提供的每個函式引動過程都使用自己專屬的記錄寫入器物件的原因。</span><span class="sxs-lookup"><span data-stu-id="05db8-287">That's why the  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="05db8-288">若要寫入[應用程式追蹤記錄](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview)，使用 **Console.Out** (建立標示為 INFO 的記錄檔) 和 **Console.Error** (建立標示為 ERROR 的記錄檔)。</span><span class="sxs-lookup"><span data-stu-id="05db8-288">To write [application tracing logs](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (creates logs marked as INFO) and **Console.Error** (creates logs marked as ERROR).</span></span> <span data-ttu-id="05db8-289">替代方法是使用 [Trace 或 TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)，除了資訊與錯誤之外，還能提供詳細資訊、警告及嚴重層級。</span><span class="sxs-lookup"><span data-stu-id="05db8-289">An alternative is to use [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition to Info and Error.</span></span> <span data-ttu-id="05db8-290">視您設定 Azure 網頁應用程式的方式而定，應用程式追蹤記錄檔會出現在網頁應用程式記錄檔、Azure 資料表或 Azure Blob 中。</span><span class="sxs-lookup"><span data-stu-id="05db8-290">Application tracing logs appear in the web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="05db8-291">所有主控台輸出的應用程式記錄檔裡最近的 100 筆記錄也同樣會顯示在 WebJob 的 [儀表板] 頁面，而不是函式引動過程的頁面。</span><span class="sxs-lookup"><span data-stu-id="05db8-291">As is true of all Console output, the most recent 100 application logs also appear in the Dashboard page for the WebJob, not the page for a function invocation.</span></span>

<span data-ttu-id="05db8-292">只有當程式是以 Azure WebJob 執行時，主控台輸出才會顯示在儀表板，而不是在本機或在某些其他環境中執行時。</span><span class="sxs-lookup"><span data-stu-id="05db8-292">Console output appears in the Dashboard only if the program is running in an Azure WebJob, not if the program is running locally or in some other environment.</span></span>

<span data-ttu-id="05db8-293">您可以將儀表板連接字串設定為 null 來停用記錄。</span><span class="sxs-lookup"><span data-stu-id="05db8-293">You can disable logging by setting the Dashboard connection string to null.</span></span> <span data-ttu-id="05db8-294">如需詳細資訊，請參閱 [如何設定組態選項](#how-to-set-configuration-options)。</span><span class="sxs-lookup"><span data-stu-id="05db8-294">For more information, see [How to set Configuration Options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="05db8-295">下列範例示範寫入記錄檔的數種方式：</span><span class="sxs-lookup"><span data-stu-id="05db8-295">The following example shows several ways to write logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="05db8-296">在「WebJobs SDK 儀表板」中，當您移至頁面以進行特定函數叫用並選取 [切換輸出] 時，會顯示來自 **TextWriter** 物件的輸出：</span><span class="sxs-lookup"><span data-stu-id="05db8-296">In the WebJobs SDK Dashboard, the output from the **TextWriter** object shows up when you go to the page for a particular function invocation and select **Toggle Output**:</span></span>

![叫用連結](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![函式引動過程頁面中的記錄檔](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="05db8-299">在「WebJobs SDK 儀表板」中，當您移至 WebJob (而非函數叫用) 的頁面並選取 [切換輸出] 時，會顯示最近 100 行的「主控台」輸出。</span><span class="sxs-lookup"><span data-stu-id="05db8-299">In the WebJobs SDK Dashboard, the most recent 100 lines of Console output show up when you go to the page for the WebJob (not for the function invocation) and select **Toggle Output**.</span></span>

![TextWriter](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

<span data-ttu-id="05db8-301">在連續的 WebJob 中，應用程式記錄檔顯示在 Web 應用程式檔案系統中的 /data/jobs/continuous/*{webjobname}*/job_log.txt。</span><span class="sxs-lookup"><span data-stu-id="05db8-301">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in the web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="05db8-302">在 Azure Blob 中，應用程式記錄檔看起來如下所示：2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span><span class="sxs-lookup"><span data-stu-id="05db8-302">In an Azure blob the application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="05db8-303">而在 Azure 資料表中，**Console.Out** 和 **Console.Error** 記錄檔看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="05db8-303">And in an Azure table the **Console.Out** and **Console.Error** logs look like this:</span></span>

![在資料表中的資訊記錄檔](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![在資料表中的錯誤記錄檔](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a><span data-ttu-id="05db8-306">後續步驟</span><span class="sxs-lookup"><span data-stu-id="05db8-306">Next steps</span></span>
<span data-ttu-id="05db8-307">本文提供的程式碼範例示範如何處理使用 Azure 佇列的常見案例。</span><span class="sxs-lookup"><span data-stu-id="05db8-307">This article has provided code samples that show how to handle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="05db8-308">如需如何使用 Azure WebJobs 和 WebJobs SDK 的詳細資訊，請參閱 [Azure WebJobs 文件資源](http://go.microsoft.com/fwlink/?linkid=390226)。</span><span class="sxs-lookup"><span data-stu-id="05db8-308">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

