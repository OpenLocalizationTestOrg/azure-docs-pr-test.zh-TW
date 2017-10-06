---
title: "開始使用佇列儲存體和 Visual Studio 已連線的服務 （WebJob 專案） 的 aaaGetting |Microsoft 文件"
description: "如何 tooget 啟動 WebJob 專案中使用 Azure 佇列儲存體之後連接 tooa 儲存體帳戶，使用 Visual Studio 已連接服務。"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 720e96fda734c31e1b1d68d4f95aa9531a20a3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="d33db-103">開始使用 Azure 佇列儲存體和 Visual Studio 已連接服務 (WebJob 專案)</span><span class="sxs-lookup"><span data-stu-id="d33db-103">Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="d33db-104">概觀</span><span class="sxs-lookup"><span data-stu-id="d33db-104">Overview</span></span>
<span data-ttu-id="d33db-105">本文說明如何開始使用 Azure 佇列中的 Visual Studio Azure WebJob 專案之後，您建立或使用參考 Azure 儲存體帳戶的儲存體 hello Visual Studio**加入已連接服務** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d33db-105">This article describes how get started using Azure Queue storage in a Visual Studio Azure WebJob project after you have created or referenced an Azure storage account by using hello Visual Studio  **Add Connected Services** dialog box.</span></span> <span data-ttu-id="d33db-106">當您使用 Visual Studio hello 新增儲存體帳戶 tooa WebJob 專案**加入已連接服務** 對話方塊中，hello 適當的 Azure 儲存體 NuGet 封裝已安裝，不會加入的 toohello hello 適當的.NET 參考專案和 hello 儲存體帳戶的連接字串會更新在 hello App.config 檔案中。</span><span class="sxs-lookup"><span data-stu-id="d33db-106">When you add a storage account tooa WebJob project by using hello Visual Studio **Add Connected Services** dialog, hello appropriate Azure Storage NuGet packages are installed, hello appropriate .NET references are added toohello project, and connection strings for hello storage account are updated in hello App.config file.</span></span>  

<span data-ttu-id="d33db-107">本文章提供 C# 程式碼範例，示範如何 toouse hello Azure WebJobs SDK 版本 1.x 以 hello Azure 佇列儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="d33db-107">This article provides C# code samples that show how toouse hello Azure WebJobs SDK version 1.x with hello Azure Queue storage service.</span></span>

<span data-ttu-id="d33db-108">Azure 佇列儲存體是用於儲存大量訊息，可透過使用 HTTP 或 HTTPS 驗證呼叫的 hello world 中從任何地方存取服務。</span><span class="sxs-lookup"><span data-stu-id="d33db-108">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="d33db-109">單一佇列訊息可以是總 too64 KB 的大小，並佇列可以包含數百萬個訊息，向上 toohello 總容量限制的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d33db-109">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span> <span data-ttu-id="d33db-110">如需詳細資訊，請參閱 [以 .NET 開始使用 Azure 佇列儲存體](storage-dotnet-how-to-use-queues.md) 。</span><span class="sxs-lookup"><span data-stu-id="d33db-110">See [Get started with Azure Queue Storage using .NET](storage-dotnet-how-to-use-queues.md) for more information.</span></span> <span data-ttu-id="d33db-111">如需 ASP.NET 的詳細資訊，請參閱 [ASP.NET](http://www.asp.net)。</span><span class="sxs-lookup"><span data-stu-id="d33db-111">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="how-tootrigger-a-function-when-a-queue-message-is-received"></a><span data-ttu-id="d33db-112">如何 tootrigger 接收佇列訊息時的函式</span><span class="sxs-lookup"><span data-stu-id="d33db-112">How tootrigger a function when a queue message is received</span></span>
<span data-ttu-id="d33db-113">toowrite hello WebJobs SDK 的函式呼叫接收佇列訊息時，請使用 hello **QueueTrigger**屬性。</span><span class="sxs-lookup"><span data-stu-id="d33db-113">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello **QueueTrigger** attribute.</span></span> <span data-ttu-id="d33db-114">hello 屬性建構函式接受字串參數，指定 hello 佇列 toopoll hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="d33db-114">hello attribute constructor takes a string parameter that specifies hello name of hello queue toopoll.</span></span> <span data-ttu-id="d33db-115">toosee 如何 tooset hello 佇列名稱，以動態方式簽出[如何 tooset 組態選項](#how-to-set-configuration-options)。</span><span class="sxs-lookup"><span data-stu-id="d33db-115">toosee how tooset hello queue name dynamically, check out [How tooset Configuration Options](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="d33db-116">字串佇列訊息</span><span class="sxs-lookup"><span data-stu-id="d33db-116">String queue messages</span></span>
<span data-ttu-id="d33db-117">在下列範例的 hello，hello 佇列包含字串訊息，因此**QueueTrigger**是套用的 tooa 字串參數名稱為**logMessage**包含 hello hello 佇列訊息內容。</span><span class="sxs-lookup"><span data-stu-id="d33db-117">In hello following example, hello queue contains a string message, so **QueueTrigger** is applied tooa string parameter named **logMessage** which contains hello content of hello queue message.</span></span> <span data-ttu-id="d33db-118">hello 函式[寫入記錄檔訊息 toohello 儀表板](#how-to-write-logs)。</span><span class="sxs-lookup"><span data-stu-id="d33db-118">hello function [writes a log message toohello Dashboard](#how-to-write-logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="d33db-119">除了**字串**，hello 參數可以是位元組陣列， **CloudQueueMessage**物件或您定義 POCO。</span><span class="sxs-lookup"><span data-stu-id="d33db-119">Besides **string**, hello parameter may be a byte array, a **CloudQueueMessage** object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="d33db-120">POCO ( [純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 佇列訊息</span><span class="sxs-lookup"><span data-stu-id="d33db-120">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="d33db-121">在下列範例的 hello，hello 佇列訊息包含的 JSON **BlobInformation**物件，其中包括**BlobName**屬性。</span><span class="sxs-lookup"><span data-stu-id="d33db-121">In hello following example, hello queue message contains JSON for a **BlobInformation** object which includes a **BlobName** property.</span></span> <span data-ttu-id="d33db-122">hello SDK 會自動將 hello 物件還原序列化。</span><span class="sxs-lookup"><span data-stu-id="d33db-122">hello SDK automatically deserializes hello object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="d33db-123">hello SDK 會使用 hello [Newtonsoft.Json NuGet 套件](http://www.nuget.org/packages/Newtonsoft.Json)tooserialize 和還原序列化訊息。</span><span class="sxs-lookup"><span data-stu-id="d33db-123">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="d33db-124">如果您未使用 hello WebJobs SDK 的程式中建立訊息排入佇列，您可以撰寫程式碼，如下列範例 toocreate POCO 佇列訊息的 hello SDK 可以剖析該 hello。</span><span class="sxs-lookup"><span data-stu-id="d33db-124">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="d33db-125">Async 函數</span><span class="sxs-lookup"><span data-stu-id="d33db-125">Async functions</span></span>
<span data-ttu-id="d33db-126">遵循 async 函式的 hello[寫入記錄檔 toohello 儀表板](#how-to-write-logs)。</span><span class="sxs-lookup"><span data-stu-id="d33db-126">hello following async function [writes a log toohello Dashboard](#how-to-write-logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="d33db-127">非同步函式可能需要[取消語彙基元](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken)，如下列範例複製 blob 的 hello 所示。</span><span class="sxs-lookup"><span data-stu-id="d33db-127">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in hello following example which copies a blob.</span></span> <span data-ttu-id="d33db-128">(如需說明的 hello **queueTrigger**預留位置，請參閱 hello [Blob](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) > 一節。)</span><span class="sxs-lookup"><span data-stu-id="d33db-128">(For an explanation of hello **queueTrigger** placeholder, see hello [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-hello-queuetrigger-attribute-works-with"></a><span data-ttu-id="d33db-129">適用於類型 hello QueueTrigger 屬性</span><span class="sxs-lookup"><span data-stu-id="d33db-129">Types hello QueueTrigger attribute works with</span></span>
<span data-ttu-id="d33db-130">您可以使用**QueueTrigger**以 hello 下列類型：</span><span class="sxs-lookup"><span data-stu-id="d33db-130">You can use **QueueTrigger** with hello following types:</span></span>

* <span data-ttu-id="d33db-131">**字串**</span><span class="sxs-lookup"><span data-stu-id="d33db-131">**string**</span></span>
* <span data-ttu-id="d33db-132">序列化為 JSON 的 POCO 型別</span><span class="sxs-lookup"><span data-stu-id="d33db-132">A POCO type serialized as JSON</span></span>
* <span data-ttu-id="d33db-133">**byte[]**</span><span class="sxs-lookup"><span data-stu-id="d33db-133">**byte[]**</span></span>
* <span data-ttu-id="d33db-134">**CloudQueueMessage**</span><span class="sxs-lookup"><span data-stu-id="d33db-134">**CloudQueueMessage**</span></span>

## <a name="polling-algorithm"></a><span data-ttu-id="d33db-135">輪詢演算法</span><span class="sxs-lookup"><span data-stu-id="d33db-135">Polling algorithm</span></span>
<span data-ttu-id="d33db-136">hello SDK 實作閒置佇列輪詢對於儲存體交易成本的隨機指數型撤退演算法 tooreduce hello 的效果。</span><span class="sxs-lookup"><span data-stu-id="d33db-136">hello SDK implements a random exponential back-off algorithm tooreduce hello effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="d33db-137">Hello SDK 找到訊息時，會等待兩秒，並且接著會檢查其他訊息;找到沒有訊息時它會等候大約四個秒後再試一次。</span><span class="sxs-lookup"><span data-stu-id="d33db-137">When a message is found, hello SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="d33db-138">後續的嘗試失敗的 tooget 佇列訊息之後, hello 等候時間持續 tooincrease 直到達到 hello 最長等待時間的預設值 tooone 分鐘。</span><span class="sxs-lookup"><span data-stu-id="d33db-138">After subsequent failed attempts tooget a queue message, hello wait time continues tooincrease until it reaches hello maximum wait time, which defaults tooone minute.</span></span> <span data-ttu-id="d33db-139">[hello 最長等待時間是可設定](#how-to-set-configuration-options)。</span><span class="sxs-lookup"><span data-stu-id="d33db-139">[hello maximum wait time is configurable](#how-to-set-configuration-options).</span></span>

## <a name="multiple-instances"></a><span data-ttu-id="d33db-140">多個執行個體</span><span class="sxs-lookup"><span data-stu-id="d33db-140">Multiple instances</span></span>
<span data-ttu-id="d33db-141">如果您的 web 應用程式在多個執行個體上執行，每個電腦上執行的連續 web 工作和每一部機器將會等候觸發程序，並嘗試 toorun 函式。</span><span class="sxs-lookup"><span data-stu-id="d33db-141">If your web app runs on multiple instances, a continuous WebJobs runs on each machine, and each machine will wait for triggers and attempt toorun functions.</span></span> <span data-ttu-id="d33db-142">在某些情況下，這可能會導致 toosome 函式處理 hello 相同的資料兩次，因此函式應該具有等冪性 （寫入因此重複呼叫以 hello 不會產生相同的輸入的資料重複的結果）。</span><span class="sxs-lookup"><span data-stu-id="d33db-142">In some scenarios this can lead toosome functions processing hello same data twice, so functions should be idempotent (written so that calling them repeatedly with hello same input data doesn't produce duplicate results).</span></span>  

## <a name="parallel-execution"></a><span data-ttu-id="d33db-143">平行執行</span><span class="sxs-lookup"><span data-stu-id="d33db-143">Parallel execution</span></span>
<span data-ttu-id="d33db-144">如果您有多個函式在不同的佇列上接聽，hello SDK 會呼叫它們以平行方式同時接收訊息時。</span><span class="sxs-lookup"><span data-stu-id="d33db-144">If you have multiple functions listening on different queues, hello SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="d33db-145">hello 也是如此單一佇列接收多個訊息時。</span><span class="sxs-lookup"><span data-stu-id="d33db-145">hello same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="d33db-146">根據預設，hello SDK 取得 16 的佇列訊息的批次，一次，並執行以平行方式處理它們的 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="d33db-146">By default, hello SDK gets a batch of 16 queue messages at a time and executes hello function that processes them in parallel.</span></span> <span data-ttu-id="d33db-147">[hello 批次大小是可設定](#how-to-set-configuration-options)。</span><span class="sxs-lookup"><span data-stu-id="d33db-147">[hello batch size is configurable](#how-to-set-configuration-options).</span></span> <span data-ttu-id="d33db-148">當正在處理的 hello 數目取得 toohalf hello 批次大小的清單時，hello SDK 取得另一個批次，並開始處理這些訊息。</span><span class="sxs-lookup"><span data-stu-id="d33db-148">When hello number being processed gets down toohalf of hello batch size, hello SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="d33db-149">因此 hello 的並行處理每個函式的訊息數目上限是一倍半 hello 批次大小。</span><span class="sxs-lookup"><span data-stu-id="d33db-149">Therefore hello maximum number of concurrent messages being processed per function is one and a half times hello batch size.</span></span> <span data-ttu-id="d33db-150">這項限制會分別套用 tooeach 函式具有**QueueTrigger**屬性。</span><span class="sxs-lookup"><span data-stu-id="d33db-150">This limit applies separately tooeach function that has a **QueueTrigger** attribute.</span></span> <span data-ttu-id="d33db-151">如果您不想平行執行的上一個佇列接收訊息，設定 hello 批次大小 too1。</span><span class="sxs-lookup"><span data-stu-id="d33db-151">If you don't want parallel execution for messages received on one queue, set hello batch size too1.</span></span>

## <a name="get-queue-or-queue-message-metadata"></a><span data-ttu-id="d33db-152">取得佇列或佇列訊息中繼資料</span><span class="sxs-lookup"><span data-stu-id="d33db-152">Get queue or queue message metadata</span></span>
<span data-ttu-id="d33db-153">您可以取得下列訊息屬性加入參數 toohello 方法簽章的 hello:</span><span class="sxs-lookup"><span data-stu-id="d33db-153">You can get hello following message properties by adding parameters toohello method signature:</span></span>

* <span data-ttu-id="d33db-154">**DateTimeOffset** expirationTime</span><span class="sxs-lookup"><span data-stu-id="d33db-154">**DateTimeOffset** expirationTime</span></span>
* <span data-ttu-id="d33db-155">**DateTimeOffset** insertionTime</span><span class="sxs-lookup"><span data-stu-id="d33db-155">**DateTimeOffset** insertionTime</span></span>
* <span data-ttu-id="d33db-156">**DateTimeOffset** nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="d33db-156">**DateTimeOffset** nextVisibleTime</span></span>
* <span data-ttu-id="d33db-157">**string** queueTrigger (包含訊息文字)</span><span class="sxs-lookup"><span data-stu-id="d33db-157">**string** queueTrigger (contains message text)</span></span>
* <span data-ttu-id="d33db-158">**string** id</span><span class="sxs-lookup"><span data-stu-id="d33db-158">**string** id</span></span>
* <span data-ttu-id="d33db-159">**string** popReceipt</span><span class="sxs-lookup"><span data-stu-id="d33db-159">**string** popReceipt</span></span>
* <span data-ttu-id="d33db-160">**int** dequeueCount</span><span class="sxs-lookup"><span data-stu-id="d33db-160">**int** dequeueCount</span></span>

<span data-ttu-id="d33db-161">如果您想 toowork 直接與 hello Azure 儲存體 API，您也可以加入**CloudStorageAccount**參數。</span><span class="sxs-lookup"><span data-stu-id="d33db-161">If you want toowork directly with hello Azure storage API, you can also add a **CloudStorageAccount** parameter.</span></span>

<span data-ttu-id="d33db-162">hello 下列範例會將所有寫入此中繼資料 tooan 資訊應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="d33db-162">hello following example writes all of this metadata tooan INFO application log.</span></span> <span data-ttu-id="d33db-163">在 hello 範例中，則為 logMessage 和 queueTrigger 包含 hello hello 佇列訊息內容。</span><span class="sxs-lookup"><span data-stu-id="d33db-163">In hello example, both logMessage and queueTrigger contain hello content of hello queue message.</span></span>

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

<span data-ttu-id="d33db-164">以下是範例記錄檔寫入 hello 範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="d33db-164">Here is a sample log written by hello sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a><span data-ttu-id="d33db-165">正常關機</span><span class="sxs-lookup"><span data-stu-id="d33db-165">Graceful shutdown</span></span>
<span data-ttu-id="d33db-166">在連續 web 工作執行的函式可以接受**CancellationToken**參數可讓 hello 作業系統 toonotify hello 函式時 hello WebJob 即將 toobe 終止。</span><span class="sxs-lookup"><span data-stu-id="d33db-166">A function that runs in a continuous WebJob can accept a **CancellationToken** parameter which enables hello operating system toonotify hello function when hello WebJob is about toobe terminated.</span></span> <span data-ttu-id="d33db-167">您可以使用此通知 toomake 確定 hello 函式不會意外終止，使資料處於不一致狀態的方式。</span><span class="sxs-lookup"><span data-stu-id="d33db-167">You can use this notification toomake sure hello function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="d33db-168">下列範例會示範如何 hello toocheck 即將發生的 WebJob 終止函式中。</span><span class="sxs-lookup"><span data-stu-id="d33db-168">hello following example shows how toocheck for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="d33db-169">**注意：** hello 儀表板，可能無法正確顯示 hello 狀態和已關閉的函式的輸出。</span><span class="sxs-lookup"><span data-stu-id="d33db-169">**Note:** hello Dashboard might not correctly show hello status and output of functions that have been shut down.</span></span>

<span data-ttu-id="d33db-170">如需詳細資訊，請參閱 [WebJobs 正常關機](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR)。</span><span class="sxs-lookup"><span data-stu-id="d33db-170">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <a name="how-toocreate-a-queue-message-while-processing-a-queue-message"></a><span data-ttu-id="d33db-171">Toocreate 佇列處理的佇列訊息時訊息的方式</span><span class="sxs-lookup"><span data-stu-id="d33db-171">How toocreate a queue message while processing a queue message</span></span>
<span data-ttu-id="d33db-172">toowrite 函式會建立新的佇列訊息，使用 hello**佇列**屬性。</span><span class="sxs-lookup"><span data-stu-id="d33db-172">toowrite a function that creates a new queue message, use hello **Queue** attribute.</span></span> <span data-ttu-id="d33db-173">像**QueueTrigger**、 您要傳入 hello 佇列名稱做為字串，或您可以[動態設定 hello 佇列名稱](#how-to-set-configuration-options)。</span><span class="sxs-lookup"><span data-stu-id="d33db-173">Like **QueueTrigger**, you pass in hello queue name as a string or you can [set hello queue name dynamically](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="d33db-174">字串佇列訊息</span><span class="sxs-lookup"><span data-stu-id="d33db-174">String queue messages</span></span>
<span data-ttu-id="d33db-175">hello 下列非非同步程式碼範例會建立新的佇列訊息，名為"outputqueue"hello 佇列中以內容為 hello 佇列訊息相同收到 hello 佇列名為"inputqueue 」 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="d33db-175">hello following non-async code sample creates a new queue message in hello queue named "outputqueue" with hello same content as hello queue message received in hello queue named "inputqueue".</span></span> <span data-ttu-id="d33db-176">(如需非同步函式，請使用 **IAsyncCollector<T>**，如本節後續內容所示。)</span><span class="sxs-lookup"><span data-stu-id="d33db-176">(For async functions use **IAsyncCollector<T>** as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="d33db-177">POCO ( [純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 佇列訊息</span><span class="sxs-lookup"><span data-stu-id="d33db-177">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="d33db-178">toocreate 包含 POCO，而不是字串時，傳遞 hello POCO 的佇列訊息型別作為輸出參數 toohello**佇列**屬性建構函式。</span><span class="sxs-lookup"><span data-stu-id="d33db-178">toocreate a queue message that contains a POCO rather than a string, pass hello POCO type as an output parameter toohello **Queue** attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="d33db-179">hello SDK 自動序列化 hello 物件 tooJSON。</span><span class="sxs-lookup"><span data-stu-id="d33db-179">hello SDK automatically serializes hello object tooJSON.</span></span> <span data-ttu-id="d33db-180">一律建立佇列訊息，即使 hello 物件為 null。</span><span class="sxs-lookup"><span data-stu-id="d33db-180">A queue message is always created, even if hello object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="d33db-181">建立多個訊息或使用非同步函式</span><span class="sxs-lookup"><span data-stu-id="d33db-181">Create multiple messages or in async functions</span></span>
<span data-ttu-id="d33db-182">toocreate 多則訊息，請 hello 輸出佇列的 hello 參數類型**ICollector<T>** 或**IAsyncCollector<T>**hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="d33db-182">toocreate multiple messages, make hello parameter type for hello output queue **ICollector<T>** or **IAsyncCollector<T>**, as shown in hello following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="d33db-183">每個佇列的訊息建立時立即 hello**新增**方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="d33db-183">Each queue message is created immediately when hello **Add** method is called.</span></span>

### <a name="types-that-hello-queue-attribute-works-with"></a><span data-ttu-id="d33db-184">型別適用於該 hello 佇列屬性</span><span class="sxs-lookup"><span data-stu-id="d33db-184">Types that hello Queue attribute works with</span></span>
<span data-ttu-id="d33db-185">您可以使用 hello**佇列**hello 下列參數類型的屬性：</span><span class="sxs-lookup"><span data-stu-id="d33db-185">You can use hello **Queue** attribute on hello following parameter types:</span></span>

* <span data-ttu-id="d33db-186">**字串**（如果參數值為非 null，hello 函式結束時，會建立佇列訊息）</span><span class="sxs-lookup"><span data-stu-id="d33db-186">**out string** (creates queue message if parameter value is non-null when hello function ends)</span></span>
* <span data-ttu-id="d33db-187">**out byte[]** (運作方式類似 **字串**)</span><span class="sxs-lookup"><span data-stu-id="d33db-187">**out byte[]** (works like **string**)</span></span>
* <span data-ttu-id="d33db-188">**out CloudQueueMessage** (運作方式類似 **字串**)</span><span class="sxs-lookup"><span data-stu-id="d33db-188">**out CloudQueueMessage** (works like **string**)</span></span>
* <span data-ttu-id="d33db-189">**POCO 出**（可序列化的型別，如果會建立訊息的 null 物件 hello 參數為 null，hello 函式結束時）</span><span class="sxs-lookup"><span data-stu-id="d33db-189">**out POCO** (a serializable type, creates a message with a null object if hello paramter is null when hello function ends)</span></span>
* <span data-ttu-id="d33db-190">**ICollector**</span><span class="sxs-lookup"><span data-stu-id="d33db-190">**ICollector**</span></span>
* <span data-ttu-id="d33db-191">**IAsyncCollector**</span><span class="sxs-lookup"><span data-stu-id="d33db-191">**IAsyncCollector**</span></span>
* <span data-ttu-id="d33db-192">**CloudQueue** (手動建立訊息使用 hello Azure 儲存體 API 直接)</span><span class="sxs-lookup"><span data-stu-id="d33db-192">**CloudQueue** (for creating messages manually using hello Azure Storage API directly)</span></span>

### <a name="use-webjobs-sdk-attributes-in-hello-body-of-a-function"></a><span data-ttu-id="d33db-193">使用 WebJobs SDK hello 函式主體中的屬性</span><span class="sxs-lookup"><span data-stu-id="d33db-193">Use WebJobs SDK attributes in hello body of a function</span></span>
<span data-ttu-id="d33db-194">如果您需要 toodo 一些適用於您的函式之前使用 WebJobs SDK 屬性，例如**佇列**， **Blob**，或**資料表**，您可以使用 hello **IBinder**介面。</span><span class="sxs-lookup"><span data-stu-id="d33db-194">If you need toodo some work in your function before using a WebJobs SDK attribute such as **Queue**, **Blob**, or **Table**, you can use hello **IBinder** interface.</span></span>

<span data-ttu-id="d33db-195">hello 下列範例會採用輸入的佇列訊息，並以相同的內容中輸出佇列的 hello 建立新的訊息。</span><span class="sxs-lookup"><span data-stu-id="d33db-195">hello following example takes an input queue message and creates a new message with hello same content in an output queue.</span></span> <span data-ttu-id="d33db-196">hello 輸出佇列名稱是由 hello hello 函式主體中的程式碼設定。</span><span class="sxs-lookup"><span data-stu-id="d33db-196">hello output queue name is set by code in hello body of hello function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="d33db-197">hello **IBinder**介面也可以搭配 hello**資料表**和**Blob**屬性。</span><span class="sxs-lookup"><span data-stu-id="d33db-197">hello **IBinder** interface can also be used with hello **Table** and **Blob** attributes.</span></span>

## <a name="how-tooread-and-write-blobs-and-tables-while-processing-a-queue-message"></a><span data-ttu-id="d33db-198">Tooread 和寫入的 blob 和資料表處理佇列訊息時</span><span class="sxs-lookup"><span data-stu-id="d33db-198">How tooread and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="d33db-199">hello **Blob**和**資料表**屬性 tooread 可讓您和寫入 blob 和資料表。</span><span class="sxs-lookup"><span data-stu-id="d33db-199">hello **Blob** and **Table** attributes enable you tooread and write blobs and tables.</span></span> <span data-ttu-id="d33db-200">本節中的 hello 範例套用 tooblobs。</span><span class="sxs-lookup"><span data-stu-id="d33db-200">hello samples in this section apply tooblobs.</span></span> <span data-ttu-id="d33db-201">程式碼範例，示範如何 tootrigger 處理當建立或更新的 blob 時，請參閱[toouse Azure blob 儲存體與 hello WebJobs SDK 的方式](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)，以及讀取和寫入資料表的程式碼範例，請參閱[如何 toouse Azure 資料表儲存體與 hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="d33db-201">For code samples that show how tootrigger processes when blobs are created or updated, see [How toouse Azure blob storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How toouse Azure table storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="d33db-202">觸發 Blob 作業的字串佇列訊息</span><span class="sxs-lookup"><span data-stu-id="d33db-202">String queue messages triggering blob operations</span></span>
<span data-ttu-id="d33db-203">包含字串，佇列訊息**queueTrigger**是的預留位置，您可以使用在 hello **Blob**屬性的**blobPath**包含 hello 內容參數hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="d33db-203">For a queue message that contains a string, **queueTrigger** is a placeholder you can use in hello **Blob** attribute's **blobPath** parameter that contains hello contents of hello message.</span></span>

<span data-ttu-id="d33db-204">hello 下列範例會使用**資料流**物件 tooread 和寫入 blob。</span><span class="sxs-lookup"><span data-stu-id="d33db-204">hello following example uses **Stream** objects tooread and write blobs.</span></span> <span data-ttu-id="d33db-205">hello 佇列訊息是 blob 的 hello 位於 hello textblobs 容器中名稱。</span><span class="sxs-lookup"><span data-stu-id="d33db-205">hello queue message is hello name of a blob located in hello textblobs container.</span></span> <span data-ttu-id="d33db-206">一份 hello blob"-新 「 附加的 toohello 名稱中建立 hello 相同容器。</span><span class="sxs-lookup"><span data-stu-id="d33db-206">A copy of hello blob with "-new" appended toohello name is created in hello same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="d33db-207">hello **Blob**屬性建構函式會採用**blobPath**指定 hello 容器和 blob 名稱的參數。</span><span class="sxs-lookup"><span data-stu-id="d33db-207">hello **Blob** attribute constructor takes a **blobPath** parameter that specifies hello container and blob name.</span></span> <span data-ttu-id="d33db-208">如需這個預留位置的詳細資訊，請參閱[如何 toouse Azure blob 儲存體與 hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="d33db-208">For more information about this placeholder, see [How toouse Azure blob storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span></span>

<span data-ttu-id="d33db-209">當 hello 屬性裝飾**資料流**物件，另一個建構函式參數指定 hello **FileAccess**為讀取、 寫入或讀取/寫入模式。</span><span class="sxs-lookup"><span data-stu-id="d33db-209">When hello attribute decorates a **Stream** object, another constructor parameter specifies hello **FileAccess** mode as read, write, or read/write.</span></span>

<span data-ttu-id="d33db-210">hello 下列範例會使用**CloudBlockBlob**物件 toodelete blob。</span><span class="sxs-lookup"><span data-stu-id="d33db-210">hello following example uses a **CloudBlockBlob** object toodelete a blob.</span></span> <span data-ttu-id="d33db-211">hello 佇列訊息是 hello hello blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="d33db-211">hello queue message is hello name of hello blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="d33db-212">POCO ( [純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 佇列訊息</span><span class="sxs-lookup"><span data-stu-id="d33db-212">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="d33db-213">POCO，以 JSON 格式儲存在 hello 佇列訊息，您可以使用該名稱在 hello 的 hello 物件內容的預留位置**佇列**屬性的**blobPath**參數。</span><span class="sxs-lookup"><span data-stu-id="d33db-213">For a POCO stored as JSON in hello queue message, you can use placeholders that name properties of hello object in hello **Queue** attribute's **blobPath** parameter.</span></span> <span data-ttu-id="d33db-214">您也可以使用佇列中繼資料屬性名稱做為預留位置。</span><span class="sxs-lookup"><span data-stu-id="d33db-214">You can also use queue metadata property names as placeholders.</span></span> <span data-ttu-id="d33db-215">請參閱 [取得佇列或佇列訊息中繼資料](#get-queue-or-queue-message-metadata)。</span><span class="sxs-lookup"><span data-stu-id="d33db-215">See [Get queue or queue message metadata](#get-queue-or-queue-message-metadata).</span></span>

<span data-ttu-id="d33db-216">hello 下列範例會複製不同的擴充功能的 blob tooa 新 blob。</span><span class="sxs-lookup"><span data-stu-id="d33db-216">hello following example copies a blob tooa new blob with a different extension.</span></span> <span data-ttu-id="d33db-217">hello 佇列訊息是**BlobInformation**物件，其中包含**BlobName**和**BlobNameWithoutExtension**屬性。</span><span class="sxs-lookup"><span data-stu-id="d33db-217">hello queue message is a **BlobInformation** object that includes **BlobName** and **BlobNameWithoutExtension** properties.</span></span> <span data-ttu-id="d33db-218">hello 屬性名稱作為 hello blob 路徑中的預留位置 hello **Blob**屬性。</span><span class="sxs-lookup"><span data-stu-id="d33db-218">hello property names are used as placeholders in hello blob path for hello **Blob** attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="d33db-219">hello SDK 會使用 hello [Newtonsoft.Json NuGet 套件](http://www.nuget.org/packages/Newtonsoft.Json)tooserialize 和還原序列化訊息。</span><span class="sxs-lookup"><span data-stu-id="d33db-219">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="d33db-220">如果您未使用 hello WebJobs SDK 的程式中建立訊息排入佇列，您可以撰寫程式碼，如下列範例 toocreate POCO 佇列訊息的 hello SDK 可以剖析該 hello。</span><span class="sxs-lookup"><span data-stu-id="d33db-220">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="d33db-221">如果您需要函式中的某些工作的 toodo 繫結 blob tooan 物件之前，您可以使用 hello hello 函式，主體中的 hello 屬性中所示[hello 函式主體中的使用 WebJobs SDK 屬性](#use-webjobs-sdk-attributes-in-the-body-of-a-function)。</span><span class="sxs-lookup"><span data-stu-id="d33db-221">If you need toodo some work in your function before binding a blob tooan object, you can use hello attribute in hello body of hello function, as shown in [Use WebJobs SDK attributes in hello body of a function](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span></span>

### <a name="types-you-can-use-hello-blob-attribute-with"></a><span data-ttu-id="d33db-222">您可以使用 hello 類型 Blob 屬性</span><span class="sxs-lookup"><span data-stu-id="d33db-222">Types you can use hello Blob attribute with</span></span>
<span data-ttu-id="d33db-223">hello **Blob**屬性可用以 hello 下列類型：</span><span class="sxs-lookup"><span data-stu-id="d33db-223">hello **Blob** attribute can be used with hello following types:</span></span>

* <span data-ttu-id="d33db-224">**資料流**（讀取或寫入使用 hello FileAccess 建構函式參數所指定）</span><span class="sxs-lookup"><span data-stu-id="d33db-224">**Stream** (read or write, specified by using hello FileAccess constructor parameter)</span></span>
* <span data-ttu-id="d33db-225">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="d33db-225">**TextReader**</span></span>
* <span data-ttu-id="d33db-226">**TextWriter**</span><span class="sxs-lookup"><span data-stu-id="d33db-226">**TextWriter**</span></span>
* <span data-ttu-id="d33db-227">**string** (讀取)</span><span class="sxs-lookup"><span data-stu-id="d33db-227">**string** (read)</span></span>
* <span data-ttu-id="d33db-228">**字串**（寫入; hello 字串參數為非 null，當 hello 函式傳回時，才會建立 blob）</span><span class="sxs-lookup"><span data-stu-id="d33db-228">**out string** (write; creates a blob only if hello string parameter is non-null when hello function returns)</span></span>
* <span data-ttu-id="d33db-229">POCO (讀取)</span><span class="sxs-lookup"><span data-stu-id="d33db-229">POCO (read)</span></span>
* <span data-ttu-id="d33db-230">POCO 出撰寫; 一律建立的 blob (如果 POCO 參數為 null，hello 函式傳回時，會建立為 null 的物件）</span><span class="sxs-lookup"><span data-stu-id="d33db-230">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when hello function returns)</span></span>
* <span data-ttu-id="d33db-231">**CloudBlobStream** (寫入)</span><span class="sxs-lookup"><span data-stu-id="d33db-231">**CloudBlobStream** (write)</span></span>
* <span data-ttu-id="d33db-232">**ICloudBlob** (讀取或寫入)</span><span class="sxs-lookup"><span data-stu-id="d33db-232">**ICloudBlob** (read or write)</span></span>
* <span data-ttu-id="d33db-233">**CloudBlockBlob** (讀取或寫入)</span><span class="sxs-lookup"><span data-stu-id="d33db-233">**CloudBlockBlob** (read or write)</span></span>
* <span data-ttu-id="d33db-234">**CloudPageBlob** (讀取或寫入)</span><span class="sxs-lookup"><span data-stu-id="d33db-234">**CloudPageBlob** (read or write)</span></span>

## <a name="how-toohandle-poison-messages"></a><span data-ttu-id="d33db-235">如何 toohandle 有害訊息</span><span class="sxs-lookup"><span data-stu-id="d33db-235">How toohandle poison messages</span></span>
<span data-ttu-id="d33db-236">訊息內容會導致函式 toofail 稱為*有害訊息*。</span><span class="sxs-lookup"><span data-stu-id="d33db-236">Messages whose content causes a function toofail are called *poison messages*.</span></span> <span data-ttu-id="d33db-237">Hello 函式失敗時，不會刪除 hello 佇列訊息，且最終會收取一次，導致 hello 循環 toobe 重複。</span><span class="sxs-lookup"><span data-stu-id="d33db-237">When hello function fails, hello queue message is not deleted and eventually is picked up again, causing hello cycle toobe repeated.</span></span> <span data-ttu-id="d33db-238">hello SDK 可以自動中斷 hello 循環之後有限數目的反覆項目，或手動進行。</span><span class="sxs-lookup"><span data-stu-id="d33db-238">hello SDK can automatically interrupt hello cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="d33db-239">自動處理有害訊息</span><span class="sxs-lookup"><span data-stu-id="d33db-239">Automatic poison message handling</span></span>
<span data-ttu-id="d33db-240">hello SDK 會呼叫向上 too5 時間 tooprocess 佇列訊息的函式。</span><span class="sxs-lookup"><span data-stu-id="d33db-240">hello SDK will call a function up too5 times tooprocess a queue message.</span></span> <span data-ttu-id="d33db-241">如果 hello 第五個再試一次失敗，hello 訊息是移動的 tooa 有害佇列。</span><span class="sxs-lookup"><span data-stu-id="d33db-241">If hello fifth try fails, hello message is moved tooa poison queue.</span></span> <span data-ttu-id="d33db-242">您可以查看如何 tooconfigure hello 中重試次數上限[如何 tooset 組態選項](#how-to-set-configuration-options)。</span><span class="sxs-lookup"><span data-stu-id="d33db-242">You can see how tooconfigure hello maximum number of retries in [How tooset configuration options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="d33db-243">hello 有害佇列名為*{originalqueuename}*-有害。</span><span class="sxs-lookup"><span data-stu-id="d33db-243">hello poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="d33db-244">您可以撰寫函式 tooprocess 訊息從 hello 有害佇列記錄或傳送通知，需要進行手動處理。</span><span class="sxs-lookup"><span data-stu-id="d33db-244">You can write a function tooprocess messages from hello poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="d33db-245">在下列範例 hello hello **copyblob 應用程式開發**佇列訊息包含 hello 名稱不存在的 blob 時，函式將會失敗。</span><span class="sxs-lookup"><span data-stu-id="d33db-245">In hello following example hello **CopyBlob** function will fail when a queue message contains hello name of a blob that doesn't exist.</span></span> <span data-ttu-id="d33db-246">當發生這種情況時，hello 訊息移動 hello copyblobqueue 佇列 toohello copyblobqueue 有害佇列中。</span><span class="sxs-lookup"><span data-stu-id="d33db-246">When that happens, hello message is moved from hello copyblobqueue queue toohello copyblobqueue-poison queue.</span></span> <span data-ttu-id="d33db-247">hello **ProcessPoisonMessage**則記錄檔 hello 有害訊息。</span><span class="sxs-lookup"><span data-stu-id="d33db-247">hello **ProcessPoisonMessage** then logs hello poison message.</span></span>

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
            logger.WriteLine("Failed toocopy blob, name=" + blobName);
        }

<span data-ttu-id="d33db-248">hello 如下圖所示這些函式的主控台的輸出處理有害訊息時。</span><span class="sxs-lookup"><span data-stu-id="d33db-248">hello following illustration shows console output from these functions when a poison message is processed.</span></span>

![主控台輸出中的有害訊息處理](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="d33db-250">手動處理有害訊息</span><span class="sxs-lookup"><span data-stu-id="d33db-250">Manual poison message handling</span></span>
<span data-ttu-id="d33db-251">您可以新增取得 hello 取用訊息的次數處理**int**參數名為**dequeueCount** tooyour 函式。</span><span class="sxs-lookup"><span data-stu-id="d33db-251">You can get hello number of times a message has been picked up for processing by adding an **int** parameter named **dequeueCount** tooyour function.</span></span> <span data-ttu-id="d33db-252">接著，您可以核取 hello 清除佇列計數在函式程式碼和執行您自己有害訊息處理時所 hello 超過臨界值，如 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="d33db-252">You can then check hello dequeue count in function code and perform your own poison message handling when hello number exceeds a threshold, as shown in hello following example.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed toocopy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a name="how-tooset-configuration-options"></a><span data-ttu-id="d33db-253">如何 tooset 組態選項</span><span class="sxs-lookup"><span data-stu-id="d33db-253">How tooset configuration options</span></span>
<span data-ttu-id="d33db-254">您可以使用 hello **JobHostConfiguration**類型 tooset hello 下列組態選項：</span><span class="sxs-lookup"><span data-stu-id="d33db-254">You can use hello **JobHostConfiguration** type tooset hello following configuration options:</span></span>

* <span data-ttu-id="d33db-255">程式碼中設定 hello SDK 連接字串。</span><span class="sxs-lookup"><span data-stu-id="d33db-255">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="d33db-256">配置 **QueueTrigger** 設定，例如清除佇列計數上限。</span><span class="sxs-lookup"><span data-stu-id="d33db-256">Configure **QueueTrigger** settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="d33db-257">從組態取得佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="d33db-257">Get queue names from configuration.</span></span>

### <a name="set-sdk-connection-strings-in-code"></a><span data-ttu-id="d33db-258">在程式碼中設定 SDK 連接字串</span><span class="sxs-lookup"><span data-stu-id="d33db-258">Set SDK connection strings in code</span></span>
<span data-ttu-id="d33db-259">程式碼中設定 hello SDK 連接字串可讓您 toouse 自己組態檔或環境變數中的連接字串名稱 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="d33db-259">Setting hello SDK connection strings in code enables you toouse your own connection string names in configuration files or environment variables, as shown in hello following example.</span></span>

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

### <a name="configure-queuetrigger--settings"></a><span data-ttu-id="d33db-260">設定 QueueTrigger 設定</span><span class="sxs-lookup"><span data-stu-id="d33db-260">Configure QueueTrigger  settings</span></span>
<span data-ttu-id="d33db-261">您可以設定下列設定適用於 toohello 佇列的訊息處理 hello:</span><span class="sxs-lookup"><span data-stu-id="d33db-261">You can configure hello following settings that apply toohello queue message processing:</span></span>

* <span data-ttu-id="d33db-262">hello 同時平行執行的 toobe 會收取的佇列訊息的最大數目 （預設值為 16）。</span><span class="sxs-lookup"><span data-stu-id="d33db-262">hello maximum number of queue messages that are picked up simultaneously toobe executed in parallel (default is 16).</span></span>
* <span data-ttu-id="d33db-263">hello 佇列訊息傳送 tooa 有害佇列之前的重試次數上限 （預設值為 5）。</span><span class="sxs-lookup"><span data-stu-id="d33db-263">hello maximum number of retries before a queue message is sent tooa poison queue (default is 5).</span></span>
* <span data-ttu-id="d33db-264">hello 最長等待時間之前再次輪詢佇列空的時 （預設值為 1 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="d33db-264">hello maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="d33db-265">下列範例會示範如何 hello tooconfigure 這些設定：</span><span class="sxs-lookup"><span data-stu-id="d33db-265">hello following example shows how tooconfigure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a><span data-ttu-id="d33db-266">在程式碼中設定 WebJobs SDK 建構函式參數的值</span><span class="sxs-lookup"><span data-stu-id="d33db-266">Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="d33db-267">有時候您會想 toospecify 佇列名稱、 blob 名稱或容器，或資料表名稱在程式碼，而不是硬式編碼它。</span><span class="sxs-lookup"><span data-stu-id="d33db-267">Sometimes you want toospecify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="d33db-268">例如，您可能會想 toospecify hello 佇列名稱**QueueTrigger**組態檔或環境變數中。</span><span class="sxs-lookup"><span data-stu-id="d33db-268">For example, you might want toospecify hello queue name for **QueueTrigger** in a configuration file or environment variable.</span></span>

<span data-ttu-id="d33db-269">您可以執行此動作，傳遞**NameResolver**物件 toohello **JobHostConfiguration**型別。</span><span class="sxs-lookup"><span data-stu-id="d33db-269">You can do that by passing in a **NameResolver** object toohello **JobHostConfiguration** type.</span></span> <span data-ttu-id="d33db-270">您加入特殊的預留位置包圍百分比 （%） 符號 WebJobs SDK 屬性建構函式參數，而您**NameResolver**程式碼會指定用來取代這些預留位置 hello 實際值 toobe。</span><span class="sxs-lookup"><span data-stu-id="d33db-270">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your **NameResolver** code specifies hello actual values toobe used in place of those placeholders.</span></span>

<span data-ttu-id="d33db-271">例如，假設您想要 toouse 佇列名為 logqueuetest hello 測試環境和生產環境中的一個具名的 logqueueprod。</span><span class="sxs-lookup"><span data-stu-id="d33db-271">For example, suppose you want toouse a queue named logqueuetest in hello test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="d33db-272">而不是硬式編碼的佇列名稱，您會想 toospecify hello hello 中的項目名稱**appSettings**必須 hello 實際的佇列名稱的集合。</span><span class="sxs-lookup"><span data-stu-id="d33db-272">Instead of a hard-coded queue name, you want toospecify hello name of an entry in hello **appSettings** collection that would have hello actual queue name.</span></span> <span data-ttu-id="d33db-273">如果 hello **appSettings**索引鍵是 logqueue、 您的函式可能看起來像下列範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="d33db-273">If hello **appSettings** key is logqueue, your function could look like hello following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="d33db-274">您**NameResolver**類別無法再取得 hello 佇列名稱，從**appSettings** hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="d33db-274">Your **NameResolver** class could then get hello queue name from **appSettings** as shown in hello following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="d33db-275">您傳遞 hello **NameResolver**類別中 toohello **JobHost**物件 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="d33db-275">You pass hello **NameResolver** class in toohello **JobHost** object as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="d33db-276">**注意：**佇列、 資料表和 blob 名稱，會解析每次呼叫函式，但 hello 應用程式啟動時，才解析 blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="d33db-276">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when hello application starts.</span></span> <span data-ttu-id="d33db-277">Hello 作業執行時，您無法變更 blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="d33db-277">You can't change blob container name while hello job is running.</span></span>

## <a name="how-tootrigger-a-function-manually"></a><span data-ttu-id="d33db-278">如何 tootrigger 函式以手動方式</span><span class="sxs-lookup"><span data-stu-id="d33db-278">How tootrigger a function manually</span></span>
<span data-ttu-id="d33db-279">tootrigger 函式以手動方式，使用 hello**呼叫**或**CallAsync**方法上 hello **JobHost**物件和 hello **NoAutomaticTrigger**在 hello 函式，如下列範例中的 hello 中所示的屬性。</span><span class="sxs-lookup"><span data-stu-id="d33db-279">tootrigger a function manually, use hello **Call** or **CallAsync** method on hello **JobHost** object and hello **NoAutomaticTrigger** attribute on hello function, as shown in hello following example.</span></span>

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

## <a name="how-toowrite-logs"></a><span data-ttu-id="d33db-280">Toowrite 的記錄檔</span><span class="sxs-lookup"><span data-stu-id="d33db-280">How toowrite logs</span></span>
<span data-ttu-id="d33db-281">hello 儀表板會顯示記錄檔中兩個地方： hello 分頁的 hello WebJob 及在特定的 WebJob 呼叫 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="d33db-281">hello Dashboard shows logs in two places: hello page for hello WebJob, and hello page for a particular WebJob invocation.</span></span>

![WebJob 頁面中的記錄檔](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![函式引動過程頁面中的記錄檔](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="d33db-284">從主控台的方法，讓您呼叫的函式中或在 hello 輸出**main （)**方法會出現，而非在特定的方法引動過程的 hello 頁面中的 hello WebJob hello 儀表板頁面。</span><span class="sxs-lookup"><span data-stu-id="d33db-284">Output from Console methods that you call in a function or in hello **Main()** method appears in hello Dashboard page for hello WebJob, not in hello page for a particular method invocation.</span></span> <span data-ttu-id="d33db-285">從您自參數取得您的方法簽章中的 hello TextWriter 物件的輸出會出現在方法引動過程的 hello 儀表板頁面。</span><span class="sxs-lookup"><span data-stu-id="d33db-285">Output from hello TextWriter object that you get from a parameter in your method signature appears in hello Dashboard page for a method invocation.</span></span>

<span data-ttu-id="d33db-286">主控台輸出無法連結的 tooa 特定的方法引動過程，因為 hello 主控台時，單一執行緒，可能會在 hello 執行許多工作函式相同的時間。</span><span class="sxs-lookup"><span data-stu-id="d33db-286">Console output can't be linked tooa particular method invocation because hello Console is single-threaded, while many job functions may be running at hello same time.</span></span> <span data-ttu-id="d33db-287">這就是為什麼 hello SDK 提供與它自己唯一的記錄寫入器物件的每個函式引動過程。</span><span class="sxs-lookup"><span data-stu-id="d33db-287">That's why hello  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="d33db-288">toowrite[應用程式的追蹤記錄檔](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview)，使用**Console.Out** （建立標示為資訊的記錄檔） 和**Console.Error** （建立標示為錯誤記錄檔）。</span><span class="sxs-lookup"><span data-stu-id="d33db-288">toowrite [application tracing logs](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (creates logs marked as INFO) and **Console.Error** (creates logs marked as ERROR).</span></span> <span data-ttu-id="d33db-289">替代方式是 toouse[追蹤或 TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)、 提供詳細資訊，警告和嚴重層級中加入 tooInfo 和錯誤。</span><span class="sxs-lookup"><span data-stu-id="d33db-289">An alternative is toouse [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition tooInfo and Error.</span></span> <span data-ttu-id="d33db-290">應用程式的追蹤記錄檔會出現在 hello web 應用程式記錄檔，Azure 資料表，或 Azure blob，根據您設定您的 Azure web 應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="d33db-290">Application tracing logs appear in hello web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="d33db-291">如為 true 的所有主控台輸出，hello 最近 100 應用程式記錄檔也會出現在 hello WebJob，不 hello 頁面函式的引動過程的 hello 儀表板頁面。</span><span class="sxs-lookup"><span data-stu-id="d33db-291">As is true of all Console output, hello most recent 100 application logs also appear in hello Dashboard page for hello WebJob, not hello page for a function invocation.</span></span>

<span data-ttu-id="d33db-292">主控台輸出會出現在 hello 儀表板才 hello 程式執行 Azure WebJob，除非 hello 程式在本機執行或某些其他環境中。</span><span class="sxs-lookup"><span data-stu-id="d33db-292">Console output appears in hello Dashboard only if hello program is running in an Azure WebJob, not if hello program is running locally or in some other environment.</span></span>

<span data-ttu-id="d33db-293">您可以藉由設定 hello 儀表板連線字串 toonull 停用記錄。</span><span class="sxs-lookup"><span data-stu-id="d33db-293">You can disable logging by setting hello Dashboard connection string toonull.</span></span> <span data-ttu-id="d33db-294">如需詳細資訊，請參閱[如何 tooset 組態選項](#how-to-set-configuration-options)。</span><span class="sxs-lookup"><span data-stu-id="d33db-294">For more information, see [How tooset Configuration Options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="d33db-295">hello 下列範例顯示數種方式 toowrite 記錄檔：</span><span class="sxs-lookup"><span data-stu-id="d33db-295">hello following example shows several ways toowrite logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="d33db-296">Hello WebJobs SDK 儀表板，在 hello 輸出 hello **TextWriter**物件顯示當您移至特定的 toohello 頁面函式引動過程，並選取**切換輸出**:</span><span class="sxs-lookup"><span data-stu-id="d33db-296">In hello WebJobs SDK Dashboard, hello output from hello **TextWriter** object shows up when you go toohello page for a particular function invocation and select **Toggle Output**:</span></span>

![叫用連結](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![函式引動過程頁面中的記錄檔](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="d33db-299">Hello WebJobs SDK 儀表板，在主控台的最新的 100 hello 行時，將輸出顯示向上移至 toohello 頁面 hello WebJob （不適用於 hello 函式引動過程），然後選取**切換輸出**。</span><span class="sxs-lookup"><span data-stu-id="d33db-299">In hello WebJobs SDK Dashboard, hello most recent 100 lines of Console output show up when you go toohello page for hello WebJob (not for hello function invocation) and select **Toggle Output**.</span></span>

![TextWriter](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

<span data-ttu-id="d33db-301">在連續的 WebJob，應用程式記錄檔中顯示/資料/工作/連續/*{webjobname}*/job_log.txt hello web 應用程式檔案系統中的。</span><span class="sxs-lookup"><span data-stu-id="d33db-301">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in hello web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="d33db-302">在 Azure blob hello 應用程式記錄檔，看起來像這樣： 2014年-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write-Hello world ！、 2014年-09-26T21:01:13，錯誤，contosoadsnew，491e54，635473620738373502,0,17404,19,Console.Error-Hello world ！、 2014年-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out-Hello world ！，</span><span class="sxs-lookup"><span data-stu-id="d33db-302">In an Azure blob hello application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="d33db-303">在 Azure 資料表 hello **Console.Out**和**Console.Error**記錄看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="d33db-303">And in an Azure table hello **Console.Out** and **Console.Error** logs look like this:</span></span>

![在資料表中的資訊記錄檔](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![在資料表中的錯誤記錄檔](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a><span data-ttu-id="d33db-306">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d33db-306">Next steps</span></span>
<span data-ttu-id="d33db-307">本文提供的程式碼範例會顯示如何以使用 Azure 佇列 toohandle 常見案例。</span><span class="sxs-lookup"><span data-stu-id="d33db-307">This article has provided code samples that show how toohandle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="d33db-308">如需有關如何 toouse Azure WebJobs 和 hello WebJobs SDK，請參閱[Azure WebJobs 文件資源](http://go.microsoft.com/fwlink/?linkid=390226)。</span><span class="sxs-lookup"><span data-stu-id="d33db-308">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

