---
title: "aaaHow toouse hello WebJobs SDK 使用 Azure 佇列儲存體"
description: "了解如何 toouse Azure 佇列儲存體與 hello WebJobs SDK。 建立和刪除查詢、插入、查看、取得和刪除佇列訊息等。"
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: dbfac5d9-f4a0-4e3e-9ecc-af3d7bf80463
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 49f844436b0453489800b2762a5c7dc30b9db805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-queue-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="ecdc1-104">如何 toouse Azure 佇列儲存體與 hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="ecdc1-104">How toouse Azure queue storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="ecdc1-105">概觀</span><span class="sxs-lookup"><span data-stu-id="ecdc1-105">Overview</span></span>
<span data-ttu-id="ecdc1-106">本指南提供 C# 程式碼範例，示範如何 toouse hello Azure WebJobs SDK 版本 1.x 以 hello Azure 佇列儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-106">This guide provides C# code samples that show how toouse hello Azure WebJobs SDK version 1.x with hello Azure queue storage service.</span></span>

<span data-ttu-id="ecdc1-107">hello 指南假設您知道[toocreate WebJob 專案在 Visual Studio 中使用連接字串該點 tooyour 儲存體帳戶的方式](websites-dotnet-webjobs-sdk-get-started.md)或太[多個儲存體帳戶](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="ecdc1-108">大部分的 hello 程式碼片段只會顯示函式，不 hello 程式碼會建立 hello`JobHost`物件，如此範例所示：</span><span class="sxs-lookup"><span data-stu-id="ecdc1-108">Most of hello code snippets only show functions, not hello code that creates hello `JobHost` object as in this example:</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

<span data-ttu-id="ecdc1-109">hello 指南包含下列主題中的 hello:</span><span class="sxs-lookup"><span data-stu-id="ecdc1-109">hello guide includes hello following topics:</span></span>

* [<span data-ttu-id="ecdc1-110">如何 tootrigger 接收佇列訊息時的函式</span><span class="sxs-lookup"><span data-stu-id="ecdc1-110">How tootrigger a function when a queue message is received</span></span>](#trigger)
  * <span data-ttu-id="ecdc1-111">字串佇列訊息</span><span class="sxs-lookup"><span data-stu-id="ecdc1-111">String queue messages</span></span>
  * <span data-ttu-id="ecdc1-112">POCO 佇列訊息</span><span class="sxs-lookup"><span data-stu-id="ecdc1-112">POCO queue messages</span></span>
  * <span data-ttu-id="ecdc1-113">Async 函數</span><span class="sxs-lookup"><span data-stu-id="ecdc1-113">Async functions</span></span>
  * <span data-ttu-id="ecdc1-114">適用於類型 hello QueueTrigger 屬性</span><span class="sxs-lookup"><span data-stu-id="ecdc1-114">Types hello QueueTrigger attribute works with</span></span>
  * <span data-ttu-id="ecdc1-115">輪詢演算法</span><span class="sxs-lookup"><span data-stu-id="ecdc1-115">Polling algorithm</span></span>
  * <span data-ttu-id="ecdc1-116">多個執行個體</span><span class="sxs-lookup"><span data-stu-id="ecdc1-116">Multiple instances</span></span>
  * <span data-ttu-id="ecdc1-117">平行執行</span><span class="sxs-lookup"><span data-stu-id="ecdc1-117">Parallel execution</span></span>
  * <span data-ttu-id="ecdc1-118">取得佇列或佇列訊息中繼資料</span><span class="sxs-lookup"><span data-stu-id="ecdc1-118">Get queue or queue message metadata</span></span>
  * <span data-ttu-id="ecdc1-119">正常關機</span><span class="sxs-lookup"><span data-stu-id="ecdc1-119">Graceful shutdown</span></span>
* [<span data-ttu-id="ecdc1-120">Toocreate 佇列處理的佇列訊息時訊息的方式</span><span class="sxs-lookup"><span data-stu-id="ecdc1-120">How toocreate a queue message while processing a queue message</span></span>](#createqueue)
  * <span data-ttu-id="ecdc1-121">字串佇列訊息</span><span class="sxs-lookup"><span data-stu-id="ecdc1-121">String queue messages</span></span>
  * <span data-ttu-id="ecdc1-122">POCO 佇列訊息</span><span class="sxs-lookup"><span data-stu-id="ecdc1-122">POCO queue messages</span></span>
  * <span data-ttu-id="ecdc1-123">建立多個訊息或使用非同步函式</span><span class="sxs-lookup"><span data-stu-id="ecdc1-123">Create multiple messages or in async functions</span></span>
  * <span data-ttu-id="ecdc1-124">適用於類型 hello 佇列屬性</span><span class="sxs-lookup"><span data-stu-id="ecdc1-124">Types hello Queue attribute works with</span></span>
  * <span data-ttu-id="ecdc1-125">使用 WebJobs SDK hello 函式主體中的屬性</span><span class="sxs-lookup"><span data-stu-id="ecdc1-125">Use WebJobs SDK attributes in hello body of a function</span></span>
* [<span data-ttu-id="ecdc1-126">Tooread 和寫入 blob 處理的佇列訊息時的方式</span><span class="sxs-lookup"><span data-stu-id="ecdc1-126">How tooread and write blobs while processing a queue message</span></span>](#blobs)
  * <span data-ttu-id="ecdc1-127">字串佇列訊息</span><span class="sxs-lookup"><span data-stu-id="ecdc1-127">String queue messages</span></span>
  * <span data-ttu-id="ecdc1-128">POCO 佇列訊息</span><span class="sxs-lookup"><span data-stu-id="ecdc1-128">POCO queue messages</span></span>
  * <span data-ttu-id="ecdc1-129">適用於類型 hello Blob 屬性</span><span class="sxs-lookup"><span data-stu-id="ecdc1-129">Types hello Blob attribute works with</span></span>
* [<span data-ttu-id="ecdc1-130">如何 toohandle 有害訊息</span><span class="sxs-lookup"><span data-stu-id="ecdc1-130">How toohandle poison messages</span></span>](#poison)
  * <span data-ttu-id="ecdc1-131">自動處理有害訊息</span><span class="sxs-lookup"><span data-stu-id="ecdc1-131">Automatic poison message handling</span></span>
  * <span data-ttu-id="ecdc1-132">手動處理有害訊息</span><span class="sxs-lookup"><span data-stu-id="ecdc1-132">Manual poison message handling</span></span>
* [<span data-ttu-id="ecdc1-133">如何 tooset 組態選項</span><span class="sxs-lookup"><span data-stu-id="ecdc1-133">How tooset configuration options</span></span>](#config)
  * <span data-ttu-id="ecdc1-134">在程式碼中設定 SDK 連接字串</span><span class="sxs-lookup"><span data-stu-id="ecdc1-134">Set SDK connection strings in code</span></span>
  * <span data-ttu-id="ecdc1-135">設定 QueueTrigger 設定</span><span class="sxs-lookup"><span data-stu-id="ecdc1-135">Configure QueueTrigger settings</span></span>
  * <span data-ttu-id="ecdc1-136">在程式碼中設定 WebJobs SDK 建構函式參數的值</span><span class="sxs-lookup"><span data-stu-id="ecdc1-136">Set values for WebJobs SDK constructor parameters in code</span></span>
* [<span data-ttu-id="ecdc1-137">如何 tootrigger 函式以手動方式</span><span class="sxs-lookup"><span data-stu-id="ecdc1-137">How tootrigger a function manually</span></span>](#manual)
* [<span data-ttu-id="ecdc1-138">Toowrite 的記錄檔</span><span class="sxs-lookup"><span data-stu-id="ecdc1-138">How toowrite logs</span></span>](#logs)
* [<span data-ttu-id="ecdc1-139">如何 toohandle 錯誤和設定的逾時</span><span class="sxs-lookup"><span data-stu-id="ecdc1-139">How toohandle errors and configure timeouts</span></span>](#errors)
* [<span data-ttu-id="ecdc1-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ecdc1-140">Next steps</span></span>](#nextsteps)

## <span data-ttu-id="ecdc1-141"><a id="trigger"></a>如何 tootrigger 接收佇列訊息時的函式</span><span class="sxs-lookup"><span data-stu-id="ecdc1-141"><a id="trigger"></a> How tootrigger a function when a queue message is received</span></span>
<span data-ttu-id="ecdc1-142">toowrite hello WebJobs SDK 的函式呼叫接收佇列訊息時，請使用 hello`QueueTrigger`屬性。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-142">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello `QueueTrigger` attribute.</span></span> <span data-ttu-id="ecdc1-143">hello 屬性建構函式接受字串參數，指定 hello 佇列 toopoll hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-143">hello attribute constructor takes a string parameter that specifies hello name of hello queue toopoll.</span></span> <span data-ttu-id="ecdc1-144">您也可以[動態設定 hello 佇列名稱](#config)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-144">You can also [set hello queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="ecdc1-145">字串佇列訊息</span><span class="sxs-lookup"><span data-stu-id="ecdc1-145">String queue messages</span></span>
<span data-ttu-id="ecdc1-146">在下列範例的 hello，hello 佇列包含字串訊息，因此`QueueTrigger`是套用的 tooa 字串參數名稱為`logMessage`包含 hello hello 佇列訊息內容。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-146">In hello following example, hello queue contains a string message, so `QueueTrigger` is applied tooa string parameter named `logMessage` which contains hello content of hello queue message.</span></span> <span data-ttu-id="ecdc1-147">hello 函式[寫入記錄檔訊息 toohello 儀表板](#logs)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-147">hello function [writes a log message toohello Dashboard](#logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="ecdc1-148">除了`string`，hello 參數可以是位元組陣列，`CloudQueueMessage`物件或您定義 POCO。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-148">Besides `string`, hello parameter may be a byte array, a `CloudQueueMessage` object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="ecdc1-149">POCO ( [純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 佇列訊息</span><span class="sxs-lookup"><span data-stu-id="ecdc1-149">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="ecdc1-150">在下列範例的 hello，hello 佇列訊息包含的 JSON`BlobInformation`物件，其中包括`BlobName`屬性。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-150">In hello following example, hello queue message contains JSON for a `BlobInformation` object which includes a `BlobName` property.</span></span> <span data-ttu-id="ecdc1-151">hello SDK 會自動將 hello 物件還原序列化。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-151">hello SDK automatically deserializes hello object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="ecdc1-152">hello SDK 會使用 hello [Newtonsoft.Json NuGet 套件](http://www.nuget.org/packages/Newtonsoft.Json)tooserialize 和還原序列化訊息。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-152">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="ecdc1-153">如果您未使用 hello WebJobs SDK 的程式中建立訊息排入佇列，您可以撰寫程式碼，如下列範例 toocreate POCO 佇列訊息的 hello SDK 可以剖析該 hello。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-153">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="ecdc1-154">Async 函數</span><span class="sxs-lookup"><span data-stu-id="ecdc1-154">Async functions</span></span>
<span data-ttu-id="ecdc1-155">遵循 async 函式的 hello[寫入記錄檔 toohello 儀表板](#logs)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-155">hello following async function [writes a log toohello Dashboard](#logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="ecdc1-156">非同步函式可能需要[取消語彙基元](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken)，如下列範例複製 blob 的 hello 所示。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-156">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in hello following example which copies a blob.</span></span> <span data-ttu-id="ecdc1-157">(如需說明的 hello`queueTrigger`預留位置，請參閱 hello [Blob](#blobs) > 一節。)</span><span class="sxs-lookup"><span data-stu-id="ecdc1-157">(For an explanation of hello `queueTrigger` placeholder, see hello [Blobs](#blobs) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <span data-ttu-id="ecdc1-158"><a id="qtattributetypes"></a>適用於類型 hello QueueTrigger 屬性</span><span class="sxs-lookup"><span data-stu-id="ecdc1-158"><a id="qtattributetypes"></a> Types hello QueueTrigger attribute works with</span></span>
<span data-ttu-id="ecdc1-159">您可以使用`QueueTrigger`以 hello 下列類型：</span><span class="sxs-lookup"><span data-stu-id="ecdc1-159">You can use `QueueTrigger` with hello following types:</span></span>

* `string`
* <span data-ttu-id="ecdc1-160">序列化為 JSON 的 POCO 型別</span><span class="sxs-lookup"><span data-stu-id="ecdc1-160">A POCO type serialized as JSON</span></span>
* `byte[]`
* `CloudQueueMessage`

### <span data-ttu-id="ecdc1-161"><a id="polling"></a> 輪詢演算法</span><span class="sxs-lookup"><span data-stu-id="ecdc1-161"><a id="polling"></a> Polling algorithm</span></span>
<span data-ttu-id="ecdc1-162">hello SDK 實作閒置佇列輪詢對於儲存體交易成本的隨機指數型撤退演算法 tooreduce hello 的效果。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-162">hello SDK implements a random exponential back-off algorithm tooreduce hello effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="ecdc1-163">Hello SDK 找到訊息時，會等待兩秒，並且接著會檢查其他訊息;找到沒有訊息時它會等候大約四個秒後再試一次。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-163">When a message is found, hello SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="ecdc1-164">後續的嘗試失敗的 tooget 佇列訊息之後, hello 等候時間持續 tooincrease 直到達到 hello 最長等待時間的預設值 tooone 分鐘。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-164">After subsequent failed attempts tooget a queue message, hello wait time continues tooincrease until it reaches hello maximum wait time, which defaults tooone minute.</span></span> <span data-ttu-id="ecdc1-165">[hello 最長等待時間是可設定](#config)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-165">[hello maximum wait time is configurable](#config).</span></span>

### <span data-ttu-id="ecdc1-166"><a id="instances"></a> 多個執行個體</span><span class="sxs-lookup"><span data-stu-id="ecdc1-166"><a id="instances"></a> Multiple instances</span></span>
<span data-ttu-id="ecdc1-167">如果您的 web 應用程式在多個執行個體上執行，在每部電腦上，執行連續的 WebJob 和每一部機器將會等候觸發程序，並嘗試 toorun 函式。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-167">If your web app runs on multiple instances, a continuous WebJob runs on each machine, and each machine will wait for triggers and attempt toorun functions.</span></span> <span data-ttu-id="ecdc1-168">hello WebJobs SDK 佇列觸發程序會自動防止函式處理佇列訊息多次;函式沒有 toobe 寫入 toobe 具有等冪性。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-168">hello WebJobs SDK queue trigger automatically prevents a function from processing a queue message multiple times; functions do not have toobe written toobe idempotent.</span></span> <span data-ttu-id="ecdc1-169">不過，如果您想 tooensure 函式只能有一個執行個體執行，即使有多個執行個體的 hello 主機 web 應用程式，您可以使用 hello`Singleton`屬性。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-169">However, if you want tooensure that only one instance of a function runs even when there are multiple instances of hello host web app, you can use hello `Singleton` attribute.</span></span>

### <span data-ttu-id="ecdc1-170"><a id="parallel"></a> 平行執行</span><span class="sxs-lookup"><span data-stu-id="ecdc1-170"><a id="parallel"></a> Parallel execution</span></span>
<span data-ttu-id="ecdc1-171">如果您有多個函式在不同的佇列上接聽，hello SDK 會呼叫它們以平行方式同時接收訊息時。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-171">If you have multiple functions listening on different queues, hello SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="ecdc1-172">hello 也是如此單一佇列接收多個訊息時。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-172">hello same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="ecdc1-173">根據預設，hello SDK 取得 16 的佇列訊息的批次，一次，並執行以平行方式處理它們的 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-173">By default, hello SDK gets a batch of 16 queue messages at a time and executes hello function that processes them in parallel.</span></span> <span data-ttu-id="ecdc1-174">[hello 批次大小是可設定](#config)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-174">[hello batch size is configurable](#config).</span></span> <span data-ttu-id="ecdc1-175">當正在處理的 hello 數目取得 toohalf hello 批次大小的清單時，hello SDK 取得另一個批次，並開始處理這些訊息。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-175">When hello number being processed gets down toohalf of hello batch size, hello SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="ecdc1-176">因此 hello 的並行處理每個函式的訊息數目上限是一倍半 hello 批次大小。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-176">Therefore hello maximum number of concurrent messages being processed per function is one and a half times hello batch size.</span></span> <span data-ttu-id="ecdc1-177">這項限制會分別套用 tooeach 函式具有`QueueTrigger`屬性。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-177">This limit applies separately tooeach function that has a `QueueTrigger` attribute.</span></span>

<span data-ttu-id="ecdc1-178">如果您不想為上一個佇列接收訊息的平行執行，您可以設定 hello 批次大小 too1。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-178">If you don't want parallel execution for messages received on one queue, you can set hello batch size too1.</span></span> <span data-ttu-id="ecdc1-179">另請參閱 **Azure WebJobs SDK 1.1.0 RTM** 中的 [更充分掌控佇列處理](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-179">See also **More control over Queue processing** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span></span>

### <span data-ttu-id="ecdc1-180"><a id="queuemetadata"></a>取得佇列或佇列訊息中繼資料</span><span class="sxs-lookup"><span data-stu-id="ecdc1-180"><a id="queuemetadata"></a>Get queue or queue message metadata</span></span>
<span data-ttu-id="ecdc1-181">您可以取得下列訊息屬性加入參數 toohello 方法簽章的 hello:</span><span class="sxs-lookup"><span data-stu-id="ecdc1-181">You can get hello following message properties by adding parameters toohello method signature:</span></span>

* <span data-ttu-id="ecdc1-182">`DateTimeOffset` expirationTime</span><span class="sxs-lookup"><span data-stu-id="ecdc1-182">`DateTimeOffset` expirationTime</span></span>
* <span data-ttu-id="ecdc1-183">`DateTimeOffset` insertionTime</span><span class="sxs-lookup"><span data-stu-id="ecdc1-183">`DateTimeOffset` insertionTime</span></span>
* <span data-ttu-id="ecdc1-184">`DateTimeOffset` nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="ecdc1-184">`DateTimeOffset` nextVisibleTime</span></span>
* <span data-ttu-id="ecdc1-185">`string` queueTrigger (包含訊息文字)</span><span class="sxs-lookup"><span data-stu-id="ecdc1-185">`string` queueTrigger (contains message text)</span></span>
* <span data-ttu-id="ecdc1-186">`string` id</span><span class="sxs-lookup"><span data-stu-id="ecdc1-186">`string` id</span></span>
* <span data-ttu-id="ecdc1-187">`string` popReceipt</span><span class="sxs-lookup"><span data-stu-id="ecdc1-187">`string` popReceipt</span></span>
* <span data-ttu-id="ecdc1-188">`int` dequeueCount</span><span class="sxs-lookup"><span data-stu-id="ecdc1-188">`int` dequeueCount</span></span>

<span data-ttu-id="ecdc1-189">如果您想 toowork 直接與 hello Azure 儲存體 API，您也可以加入`CloudStorageAccount`參數。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-189">If you want toowork directly with hello Azure storage API, you can also add a `CloudStorageAccount` parameter.</span></span>

<span data-ttu-id="ecdc1-190">hello 下列範例會將所有寫入此中繼資料 tooan 資訊應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-190">hello following example writes all of this metadata tooan INFO application log.</span></span> <span data-ttu-id="ecdc1-191">在 hello 範例中，則為 logMessage 和 queueTrigger 包含 hello hello 佇列訊息內容。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-191">In hello example, both logMessage and queueTrigger contain hello content of hello queue message.</span></span>

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

<span data-ttu-id="ecdc1-192">以下是範例記錄檔寫入 hello 範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="ecdc1-192">Here is a sample log written by hello sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <span data-ttu-id="ecdc1-193"><a id="graceful"></a>順利關機</span><span class="sxs-lookup"><span data-stu-id="ecdc1-193"><a id="graceful"></a>Graceful shutdown</span></span>
<span data-ttu-id="ecdc1-194">在連續 web 工作執行的函式可以接受`CancellationToken`參數可讓 hello 作業系統 toonotify hello 函式時 hello WebJob 即將 toobe 終止。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-194">A function that runs in a continuous WebJob can accept a `CancellationToken` parameter which enables hello operating system toonotify hello function when hello WebJob is about toobe terminated.</span></span> <span data-ttu-id="ecdc1-195">您可以使用此通知 toomake 確定 hello 函式不會意外終止，使資料處於不一致狀態的方式。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-195">You can use this notification toomake sure hello function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="ecdc1-196">下列範例會示範如何 hello toocheck 即將發生的 WebJob 終止函式中。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-196">hello following example shows how toocheck for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="ecdc1-197">**注意：** hello 儀表板，可能無法正確顯示 hello 狀態和已關閉的函式的輸出。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-197">**Note:** hello Dashboard might not correctly show hello status and output of functions that have been shut down.</span></span>

<span data-ttu-id="ecdc1-198">如需詳細資訊，請參閱 [WebJobs 正常關機](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-198">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <span data-ttu-id="ecdc1-199"><a id="createqueue"></a>Toocreate 佇列處理的佇列訊息時訊息的方式</span><span class="sxs-lookup"><span data-stu-id="ecdc1-199"><a id="createqueue"></a> How toocreate a queue message while processing a queue message</span></span>
<span data-ttu-id="ecdc1-200">toowrite 函式會建立新的佇列訊息，使用 hello`Queue`屬性。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-200">toowrite a function that creates a new queue message, use hello `Queue` attribute.</span></span> <span data-ttu-id="ecdc1-201">像`QueueTrigger`、 您要傳入 hello 佇列名稱做為字串，或您可以[動態設定 hello 佇列名稱](#config)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-201">Like `QueueTrigger`, you pass in hello queue name as a string or you can [set hello queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="ecdc1-202">字串佇列訊息</span><span class="sxs-lookup"><span data-stu-id="ecdc1-202">String queue messages</span></span>
<span data-ttu-id="ecdc1-203">hello 下列非非同步程式碼範例會建立新的佇列訊息，名為"outputqueue"hello 佇列中以內容為 hello 佇列訊息相同收到 hello 佇列名為"inputqueue 」 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-203">hello following non-async code sample creates a new queue message in hello queue named "outputqueue" with hello same content as hello queue message received in hello queue named "inputqueue".</span></span> <span data-ttu-id="ecdc1-204">(如需非同步函式，請使用 `IAsyncCollector<T>`，如本節後續內容所示。)</span><span class="sxs-lookup"><span data-stu-id="ecdc1-204">(For async functions use `IAsyncCollector<T>` as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="ecdc1-205">POCO ( [純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 佇列訊息</span><span class="sxs-lookup"><span data-stu-id="ecdc1-205">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="ecdc1-206">toocreate 包含 POCO，而不是字串時，傳遞 hello POCO 的佇列訊息型別作為輸出參數 toohello`Queue`屬性建構函式。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-206">toocreate a queue message that contains a POCO rather than a string, pass hello POCO type as an output parameter toohello `Queue` attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="ecdc1-207">hello SDK 自動序列化 hello 物件 tooJSON。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-207">hello SDK automatically serializes hello object tooJSON.</span></span> <span data-ttu-id="ecdc1-208">一律建立佇列訊息，即使 hello 物件為 null。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-208">A queue message is always created, even if hello object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="ecdc1-209">建立多個訊息或使用非同步函式</span><span class="sxs-lookup"><span data-stu-id="ecdc1-209">Create multiple messages or in async functions</span></span>
<span data-ttu-id="ecdc1-210">toocreate 多則訊息，請 hello 輸出佇列的 hello 參數類型`ICollector<T>`或`IAsyncCollector<T>`hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-210">toocreate multiple messages, make hello parameter type for hello output queue `ICollector<T>` or `IAsyncCollector<T>`, as shown in hello following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="ecdc1-211">每個佇列的訊息建立時立即 hello`Add`方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-211">Each queue message is created immediately when hello `Add` method is called.</span></span>

### <a name="types-that-hello-queue-attribute-works-with"></a><span data-ttu-id="ecdc1-212">型別適用於該 hello 佇列屬性</span><span class="sxs-lookup"><span data-stu-id="ecdc1-212">Types that hello Queue attribute works with</span></span>
<span data-ttu-id="ecdc1-213">您可以使用 hello `Queue` hello 下列參數類型的屬性：</span><span class="sxs-lookup"><span data-stu-id="ecdc1-213">You can use hello `Queue` attribute on hello following parameter types:</span></span>

* <span data-ttu-id="ecdc1-214">`out string`（如果參數值為非 null，hello 函式結束時，會建立佇列訊息）</span><span class="sxs-lookup"><span data-stu-id="ecdc1-214">`out string` (creates queue message if parameter value is non-null when hello function ends)</span></span>
* <span data-ttu-id="ecdc1-215">`out byte[]` (作用就像是 `string`)</span><span class="sxs-lookup"><span data-stu-id="ecdc1-215">`out byte[]` (works like `string`)</span></span>
* <span data-ttu-id="ecdc1-216">`out CloudQueueMessage` (作用就像是 `string`)</span><span class="sxs-lookup"><span data-stu-id="ecdc1-216">`out CloudQueueMessage` (works like `string`)</span></span>
* <span data-ttu-id="ecdc1-217">`out POCO`（可序列化的型別，如果會建立訊息的 null 物件 hello 參數為 null，hello 函式結束時）</span><span class="sxs-lookup"><span data-stu-id="ecdc1-217">`out POCO` (a serializable type, creates a message with a null object if hello paramter is null when hello function ends)</span></span>
* `ICollector`
* `IAsyncCollector`
* <span data-ttu-id="ecdc1-218">`CloudQueue`（適用於建立使用手動 hello Azure 儲存體 API 直接的訊息）</span><span class="sxs-lookup"><span data-stu-id="ecdc1-218">`CloudQueue` (for creating messages manually using hello Azure Storage API directly)</span></span>

### <span data-ttu-id="ecdc1-219"><a id="ibinder"></a>使用 WebJobs SDK hello 函式主體中的屬性</span><span class="sxs-lookup"><span data-stu-id="ecdc1-219"><a id="ibinder"></a>Use WebJobs SDK attributes in hello body of a function</span></span>
<span data-ttu-id="ecdc1-220">如果您需要 toodo 一些適用於您的函式之前使用 WebJobs SDK 屬性，例如`Queue`， `Blob`，或`Table`，您可以使用 hello`IBinder`介面。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-220">If you need toodo some work in your function before using a WebJobs SDK attribute such as `Queue`, `Blob`, or `Table`, you can use hello `IBinder` interface.</span></span>

<span data-ttu-id="ecdc1-221">hello 下列範例會採用輸入的佇列訊息，並以相同的內容中輸出佇列的 hello 建立新的訊息。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-221">hello following example takes an input queue message and creates a new message with hello same content in an output queue.</span></span> <span data-ttu-id="ecdc1-222">hello 輸出佇列名稱是由 hello hello 函式主體中的程式碼設定。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-222">hello output queue name is set by code in hello body of hello function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="ecdc1-223">hello`IBinder`介面也可以搭配 hello`Table`和`Blob`屬性。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-223">hello `IBinder` interface can also be used with hello `Table` and `Blob` attributes.</span></span>

## <span data-ttu-id="ecdc1-224"><a id="blobs"></a>Tooread 和寫入的 blob 和資料表處理佇列訊息時</span><span class="sxs-lookup"><span data-stu-id="ecdc1-224"><a id="blobs"></a> How tooread and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="ecdc1-225">hello`Blob`和`Table`屬性 tooread 可讓您和寫入 blob 和資料表。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-225">hello `Blob` and `Table` attributes enable you tooread and write blobs and tables.</span></span> <span data-ttu-id="ecdc1-226">本節中的 hello 範例套用 tooblobs。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-226">hello samples in this section apply tooblobs.</span></span> <span data-ttu-id="ecdc1-227">程式碼範例，示範如何 tootrigger 處理當建立或更新的 blob 時，請參閱[toouse Azure blob 儲存體與 hello WebJobs SDK 的方式](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)，以及讀取和寫入資料表的程式碼範例，請參閱[如何 toouse Azure 資料表儲存體與 hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-227">For code samples that show how tootrigger processes when blobs are created or updated, see [How toouse Azure blob storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How toouse Azure table storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="ecdc1-228">觸發 Blob 作業的字串佇列訊息</span><span class="sxs-lookup"><span data-stu-id="ecdc1-228">String queue messages triggering blob operations</span></span>
<span data-ttu-id="ecdc1-229">包含字串，佇列訊息`queueTrigger`是的預留位置，您可以使用在 hello`Blob`屬性的`blobPath`包含 hello hello 訊息內容的參數。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-229">For a queue message that contains a string, `queueTrigger` is a placeholder you can use in hello `Blob` attribute's `blobPath` parameter that contains hello contents of hello message.</span></span>

<span data-ttu-id="ecdc1-230">hello 下列範例會使用`Stream`物件 tooread 和寫入 blob。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-230">hello following example uses `Stream` objects tooread and write blobs.</span></span> <span data-ttu-id="ecdc1-231">hello 佇列訊息是 blob 的 hello 位於 hello textblobs 容器中名稱。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-231">hello queue message is hello name of a blob located in hello textblobs container.</span></span> <span data-ttu-id="ecdc1-232">一份 hello blob"-新 「 附加的 toohello 名稱中建立 hello 相同容器。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-232">A copy of hello blob with "-new" appended toohello name is created in hello same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="ecdc1-233">hello`Blob`屬性建構函式會採用`blobPath`指定 hello 容器和 blob 名稱的參數。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-233">hello `Blob` attribute constructor takes a `blobPath` parameter that specifies hello container and blob name.</span></span> <span data-ttu-id="ecdc1-234">如需這個預留位置的詳細資訊，請參閱[如何 toouse Azure blob 儲存體與 hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)，</span><span class="sxs-lookup"><span data-stu-id="ecdc1-234">For more information about this placeholder, see [How toouse Azure blob storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span></span>

<span data-ttu-id="ecdc1-235">當 hello 屬性裝飾`Stream`物件，另一個建構函式參數指定 hello`FileAccess`為讀取、 寫入或讀取/寫入模式。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-235">When hello attribute decorates a `Stream` object, another constructor parameter specifies hello `FileAccess` mode as read, write, or read/write.</span></span>

<span data-ttu-id="ecdc1-236">hello 下列範例會使用`CloudBlockBlob`物件 toodelete blob。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-236">hello following example uses a `CloudBlockBlob` object toodelete a blob.</span></span> <span data-ttu-id="ecdc1-237">hello 佇列訊息是 hello hello blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-237">hello queue message is hello name of hello blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <span data-ttu-id="ecdc1-238"><a id="pocoblobs"></a> POCO ( [純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 佇列訊息</span><span class="sxs-lookup"><span data-stu-id="ecdc1-238"><a id="pocoblobs"></a> POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="ecdc1-239">POCO，以 JSON 格式儲存在 hello 佇列訊息，您可以使用該名稱在 hello 的 hello 物件內容的預留位置`Queue`屬性的`blobPath`參數。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-239">For a POCO stored as JSON in hello queue message, you can use placeholders that name properties of hello object in hello `Queue` attribute's `blobPath` parameter.</span></span> <span data-ttu-id="ecdc1-240">您也可以使用 [佇列中繼資料屬性名稱](#queuemetadata) 做為預留位置。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-240">You can also use [queue metadata property names](#queuemetadata) as placeholders.</span></span>

<span data-ttu-id="ecdc1-241">hello 下列範例會複製不同的擴充功能的 blob tooa 新 blob。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-241">hello following example copies a blob tooa new blob with a different extension.</span></span> <span data-ttu-id="ecdc1-242">hello 佇列訊息是`BlobInformation`物件，其中包含`BlobName`和`BlobNameWithoutExtension`屬性。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-242">hello queue message is a `BlobInformation` object that includes `BlobName` and `BlobNameWithoutExtension` properties.</span></span> <span data-ttu-id="ecdc1-243">hello 屬性名稱作為 hello blob 路徑中的預留位置 hello`Blob`屬性。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-243">hello property names are used as placeholders in hello blob path for hello `Blob` attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="ecdc1-244">hello SDK 會使用 hello [Newtonsoft.Json NuGet 套件](http://www.nuget.org/packages/Newtonsoft.Json)tooserialize 和還原序列化訊息。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-244">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="ecdc1-245">如果您未使用 hello WebJobs SDK 的程式中建立訊息排入佇列，您可以撰寫程式碼，如下列範例 toocreate POCO 佇列訊息的 hello SDK 可以剖析該 hello。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-245">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="ecdc1-246">如果您需要函式中的某些工作的 toodo 繫結 blob tooan 物件之前，您可以使用 hello hello 函式，主體中的 hello 屬性[如上所示為 hello 佇列屬性](#ibinder)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-246">If you need toodo some work in your function before binding a blob tooan object, you can use hello attribute in hello body of hello function, [as shown earlier for hello Queue attribute](#ibinder).</span></span>

### <span data-ttu-id="ecdc1-247"><a id="blobattributetypes"></a>您可以使用 hello 類型 Blob 屬性</span><span class="sxs-lookup"><span data-stu-id="ecdc1-247"><a id="blobattributetypes"></a> Types you can use hello Blob attribute with</span></span>
<span data-ttu-id="ecdc1-248">hello`Blob`屬性可用以 hello 下列類型：</span><span class="sxs-lookup"><span data-stu-id="ecdc1-248">hello `Blob` attribute can be used with hello following types:</span></span>

* <span data-ttu-id="ecdc1-249">`Stream`（讀取或寫入使用 hello FileAccess 建構函式參數所指定）</span><span class="sxs-lookup"><span data-stu-id="ecdc1-249">`Stream` (read or write, specified by using hello FileAccess constructor parameter)</span></span>
* `TextReader`
* `TextWriter`
* <span data-ttu-id="ecdc1-250">`string` (讀取)</span><span class="sxs-lookup"><span data-stu-id="ecdc1-250">`string` (read)</span></span>
* <span data-ttu-id="ecdc1-251">`out string`（撰寫; hello 字串參數為非 null，當 hello 函式傳回時，才會建立 blob）</span><span class="sxs-lookup"><span data-stu-id="ecdc1-251">`out string` (write; creates a blob only if hello string parameter is non-null when hello function returns)</span></span>
* <span data-ttu-id="ecdc1-252">POCO (讀取)</span><span class="sxs-lookup"><span data-stu-id="ecdc1-252">POCO (read)</span></span>
* <span data-ttu-id="ecdc1-253">POCO 出撰寫; 一律建立的 blob (如果 POCO 參數為 null，hello 函式傳回時，會建立為 null 的物件）</span><span class="sxs-lookup"><span data-stu-id="ecdc1-253">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when hello function returns)</span></span>
* <span data-ttu-id="ecdc1-254">`CloudBlobStream` (寫入)</span><span class="sxs-lookup"><span data-stu-id="ecdc1-254">`CloudBlobStream` (write)</span></span>
* <span data-ttu-id="ecdc1-255">`ICloudBlob` (讀取或寫入)</span><span class="sxs-lookup"><span data-stu-id="ecdc1-255">`ICloudBlob` (read or write)</span></span>
* <span data-ttu-id="ecdc1-256">`CloudBlockBlob` (讀取或寫入)</span><span class="sxs-lookup"><span data-stu-id="ecdc1-256">`CloudBlockBlob` (read or write)</span></span>
* <span data-ttu-id="ecdc1-257">`CloudPageBlob` (讀取或寫入)</span><span class="sxs-lookup"><span data-stu-id="ecdc1-257">`CloudPageBlob` (read or write)</span></span>

## <span data-ttu-id="ecdc1-258"><a id="poison"></a>如何 toohandle 有害訊息</span><span class="sxs-lookup"><span data-stu-id="ecdc1-258"><a id="poison"></a> How toohandle poison messages</span></span>
<span data-ttu-id="ecdc1-259">訊息內容會導致函式 toofail 稱為*有害訊息*。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-259">Messages whose content causes a function toofail are called *poison messages*.</span></span> <span data-ttu-id="ecdc1-260">Hello 函式失敗時，不會刪除 hello 佇列訊息，且最終會收取一次，導致 hello 循環 toobe 重複。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-260">When hello function fails, hello queue message is not deleted and eventually is picked up again, causing hello cycle toobe repeated.</span></span> <span data-ttu-id="ecdc1-261">hello SDK 可以自動中斷 hello 循環之後有限數目的反覆項目，或手動進行。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-261">hello SDK can automatically interrupt hello cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="ecdc1-262">自動處理有害訊息</span><span class="sxs-lookup"><span data-stu-id="ecdc1-262">Automatic poison message handling</span></span>
<span data-ttu-id="ecdc1-263">hello SDK 會呼叫向上 too5 時間 tooprocess 佇列訊息的函式。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-263">hello SDK will call a function up too5 times tooprocess a queue message.</span></span> <span data-ttu-id="ecdc1-264">如果 hello 第五個再試一次失敗，hello 訊息是移動的 tooa 有害佇列。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-264">If hello fifth try fails, hello message is moved tooa poison queue.</span></span> <span data-ttu-id="ecdc1-265">[hello 重試次數上限是可設定](#config)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-265">[hello maximum number of retries is configurable](#config).</span></span>

<span data-ttu-id="ecdc1-266">hello 有害佇列名為*{originalqueuename}*-有害。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-266">hello poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="ecdc1-267">您可以撰寫函式 tooprocess 訊息從 hello 有害佇列記錄或傳送通知，需要進行手動處理。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-267">You can write a function tooprocess messages from hello poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="ecdc1-268">在下列範例 hello hello`CopyBlob`佇列訊息包含 hello 名稱不存在的 blob 時，函式將會失敗。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-268">In hello following example hello `CopyBlob` function will fail when a queue message contains hello name of a blob that doesn't exist.</span></span> <span data-ttu-id="ecdc1-269">當發生這種情況時，hello 訊息移動 hello copyblobqueue 佇列 toohello copyblobqueue 有害佇列中。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-269">When that happens, hello message is moved from hello copyblobqueue queue toohello copyblobqueue-poison queue.</span></span> <span data-ttu-id="ecdc1-270">hello`ProcessPoisonMessage`則記錄檔 hello 有害訊息。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-270">hello `ProcessPoisonMessage` then logs hello poison message.</span></span>

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

<span data-ttu-id="ecdc1-271">hello 如下圖所示這些函式的主控台的輸出處理有害訊息時。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-271">hello following illustration shows console output from these functions when a poison message is processed.</span></span>

![主控台輸出中的有害訊息處理](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="ecdc1-273">手動處理有害訊息</span><span class="sxs-lookup"><span data-stu-id="ecdc1-273">Manual poison message handling</span></span>
<span data-ttu-id="ecdc1-274">您可以新增取得 hello 取用訊息的次數處理`int`參數名為`dequeueCount`tooyour 函式。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-274">You can get hello number of times a message has been picked up for processing by adding an `int` parameter named `dequeueCount` tooyour function.</span></span> <span data-ttu-id="ecdc1-275">接著，您可以核取 hello 清除佇列計數在函式程式碼和執行您自己有害訊息處理時所 hello 超過臨界值，如 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-275">You can then check hello dequeue count in function code and perform your own poison message handling when hello number exceeds a threshold, as shown in hello following example.</span></span>

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

## <span data-ttu-id="ecdc1-276"><a id="config"></a>如何 tooset 組態選項</span><span class="sxs-lookup"><span data-stu-id="ecdc1-276"><a id="config"></a> How tooset configuration options</span></span>
<span data-ttu-id="ecdc1-277">您可以使用 hello`JobHostConfiguration`類型 tooset hello 下列組態選項：</span><span class="sxs-lookup"><span data-stu-id="ecdc1-277">You can use hello `JobHostConfiguration` type tooset hello following configuration options:</span></span>

* <span data-ttu-id="ecdc1-278">程式碼中設定 hello SDK 連接字串。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-278">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="ecdc1-279">設定 `QueueTrigger` 設定，例如清除佇列計數上限。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-279">Configure `QueueTrigger` settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="ecdc1-280">從組態取得佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-280">Get queue names from configuration.</span></span>

### <span data-ttu-id="ecdc1-281"><a id="setconnstr"></a>在程式碼中設定 SDK 連接字串</span><span class="sxs-lookup"><span data-stu-id="ecdc1-281"><a id="setconnstr"></a>Set SDK connection strings in code</span></span>
<span data-ttu-id="ecdc1-282">程式碼中設定 hello SDK 連接字串可讓您 toouse 自己組態檔或環境變數中的連接字串名稱 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-282">Setting hello SDK connection strings in code enables you toouse your own connection string names in configuration files or environment variables, as shown in hello following example.</span></span>

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

### <span data-ttu-id="ecdc1-283"><a id="configqueue"></a>設定 QueueTrigger 設定</span><span class="sxs-lookup"><span data-stu-id="ecdc1-283"><a id="configqueue"></a>Configure QueueTrigger  settings</span></span>
<span data-ttu-id="ecdc1-284">您可以設定下列設定適用於 toohello 佇列的訊息處理 hello:</span><span class="sxs-lookup"><span data-stu-id="ecdc1-284">You can configure hello following settings that apply toohello queue message processing:</span></span>

* <span data-ttu-id="ecdc1-285">hello 同時平行執行的 toobe 會收取的佇列訊息的最大數目 （預設值為 16）。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-285">hello maximum number of queue messages that are picked up simultaneously toobe executed in parallel (default is 16).</span></span>
* <span data-ttu-id="ecdc1-286">hello 佇列訊息傳送 tooa 有害佇列之前的重試次數上限 （預設值為 5）。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-286">hello maximum number of retries before a queue message is sent tooa poison queue (default is 5).</span></span>
* <span data-ttu-id="ecdc1-287">hello 最長等待時間之前再次輪詢佇列空的時 （預設值為 1 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-287">hello maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="ecdc1-288">下列範例會示範如何 hello tooconfigure 這些設定：</span><span class="sxs-lookup"><span data-stu-id="ecdc1-288">hello following example shows how tooconfigure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <span data-ttu-id="ecdc1-289"><a id="setnamesincode"></a>在程式碼中設定 WebJobs SDK 建構函式參數的值</span><span class="sxs-lookup"><span data-stu-id="ecdc1-289"><a id="setnamesincode"></a>Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="ecdc1-290">有時候您會想 toospecify 佇列名稱、 blob 名稱或容器，或資料表名稱在程式碼，而不是硬式編碼它。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-290">Sometimes you want toospecify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="ecdc1-291">例如，您可能會想 toospecify hello 佇列名稱`QueueTrigger`組態檔或環境變數中。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-291">For example, you might want toospecify hello queue name for `QueueTrigger` in a configuration file or environment variable.</span></span>

<span data-ttu-id="ecdc1-292">您可以執行此動作，傳遞`NameResolver`物件 toohello`JobHostConfiguration`型別。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-292">You can do that by passing in a `NameResolver` object toohello `JobHostConfiguration` type.</span></span> <span data-ttu-id="ecdc1-293">您加入特殊的預留位置包圍百分比 （%） 符號 WebJobs SDK 屬性建構函式參數，而您`NameResolver`程式碼會指定用來取代這些預留位置 hello 實際值 toobe。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-293">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your `NameResolver` code specifies hello actual values toobe used in place of those placeholders.</span></span>

<span data-ttu-id="ecdc1-294">例如，假設您想要 toouse 佇列名為 logqueuetest hello 測試環境和生產環境中的一個具名的 logqueueprod。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-294">For example, suppose you want toouse a queue named logqueuetest in hello test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="ecdc1-295">而不是硬式編碼的佇列名稱，您會想 toospecify hello hello 中的項目名稱`appSettings`必須 hello 實際的佇列名稱的集合。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-295">Instead of a hard-coded queue name, you want toospecify hello name of an entry in hello `appSettings` collection that would have hello actual queue name.</span></span> <span data-ttu-id="ecdc1-296">如果 hello`appSettings`索引鍵是 logqueue、 您的函式可能看起來像下列範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-296">If hello `appSettings` key is logqueue, your function could look like hello following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="ecdc1-297">您`NameResolver`類別無法再取得 hello 佇列名稱，從`appSettings`hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="ecdc1-297">Your `NameResolver` class could then get hello queue name from `appSettings` as shown in hello following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="ecdc1-298">您傳遞 hello`NameResolver`類別中 toohello`JobHost`物件 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-298">You pass hello `NameResolver` class in toohello `JobHost` object as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="ecdc1-299">**注意：**佇列、 資料表和 blob 名稱，會解析每次呼叫函式，但 hello 應用程式啟動時，才解析 blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-299">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when hello application starts.</span></span> <span data-ttu-id="ecdc1-300">Hello 作業執行時，您無法變更 blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-300">You can't change blob container name while hello job is running.</span></span>

## <span data-ttu-id="ecdc1-301"><a id="manual"></a>如何 tootrigger 函式以手動方式</span><span class="sxs-lookup"><span data-stu-id="ecdc1-301"><a id="manual"></a>How tootrigger a function manually</span></span>
<span data-ttu-id="ecdc1-302">tootrigger 函式以手動方式，使用 hello`Call`或`CallAsync`方法上 hello`JobHost`物件和 hello `NoAutomaticTrigger` hello 下列範例所示，在 hello 函式，屬性。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-302">tootrigger a function manually, use hello `Call` or `CallAsync` method on hello `JobHost` object and hello `NoAutomaticTrigger` attribute on hello function, as shown in hello following example.</span></span>

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

## <span data-ttu-id="ecdc1-303"><a id="logs"></a>Toowrite 的記錄檔</span><span class="sxs-lookup"><span data-stu-id="ecdc1-303"><a id="logs"></a>How toowrite logs</span></span>
<span data-ttu-id="ecdc1-304">hello 儀表板會顯示記錄檔中兩個地方： hello 分頁的 hello WebJob 及在特定的 WebJob 呼叫 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-304">hello Dashboard shows logs in two places: hello page for hello WebJob, and hello page for a particular WebJob invocation.</span></span>

![WebJob 頁面中的記錄檔](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![函式引動過程頁面中的記錄檔](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="ecdc1-307">從主控台的方法，讓您呼叫的函式中或在 hello 輸出`Main()`方法會出現，而非在特定的方法引動過程的 hello 頁面中的 hello WebJob hello 儀表板頁面。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-307">Output from Console methods that you call in a function or in hello `Main()` method appears in hello Dashboard page for hello WebJob, not in hello page for a particular method invocation.</span></span> <span data-ttu-id="ecdc1-308">從您自參數取得您的方法簽章中的 hello TextWriter 物件的輸出會出現在方法引動過程的 hello 儀表板頁面。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-308">Output from hello TextWriter object that you get from a parameter in your method signature appears in hello Dashboard page for a method invocation.</span></span>

<span data-ttu-id="ecdc1-309">主控台輸出無法連結的 tooa 特定的方法引動過程，因為 hello 主控台時，單一執行緒，可能會在 hello 執行許多工作函式相同的時間。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-309">Console output can't be linked tooa particular method invocation because hello Console is single-threaded, while many job functions may be running at hello same time.</span></span> <span data-ttu-id="ecdc1-310">這就是為什麼 hello SDK 提供與它自己唯一的記錄寫入器物件的每個函式引動過程。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-310">That's why hello  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="ecdc1-311">toowrite[應用程式的追蹤記錄檔](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview)，使用`Console.Out`（建立標示為資訊的記錄檔） 和`Console.Error`（建立標示為錯誤記錄檔）。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-311">toowrite [application tracing logs](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (creates logs marked as INFO) and `Console.Error` (creates logs marked as ERROR).</span></span> <span data-ttu-id="ecdc1-312">替代方式是 toouse[追蹤或 TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)、 提供詳細資訊，警告和嚴重層級中加入 tooInfo 和錯誤。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-312">An alternative is toouse [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition tooInfo and Error.</span></span> <span data-ttu-id="ecdc1-313">應用程式的追蹤記錄檔會出現在 hello web 應用程式記錄檔，Azure 資料表，或 Azure blob，根據您設定您的 Azure web 應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-313">Application tracing logs appear in hello web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="ecdc1-314">如為 true 的所有主控台輸出，hello 最近 100 應用程式記錄檔也會出現在 hello WebJob，不 hello 頁面函式的引動過程的 hello 儀表板頁面。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-314">As is true of all Console output, hello most recent 100 application logs also appear in hello Dashboard page for hello WebJob, not hello page for a function invocation.</span></span>

<span data-ttu-id="ecdc1-315">主控台輸出會出現在 hello 儀表板才 hello 程式執行 Azure WebJob，除非 hello 程式在本機執行或某些其他環境中。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-315">Console output appears in hello Dashboard only if hello program is running in an Azure WebJob, not if hello program is running locally or in some other environment.</span></span>

<span data-ttu-id="ecdc1-316">停用針對高輸送量的儀表板記錄。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-316">Disable dashboard logging for high throughput scenarios.</span></span> <span data-ttu-id="ecdc1-317">根據預設，hello SDK 寫入記錄檔 toostorage，而且這項活動可能會降低效能，當您要處理許多訊息。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-317">By default, hello SDK writes logs toostorage, and this activity could degrade performance when you are processing many messages.</span></span> <span data-ttu-id="ecdc1-318">記錄、 toodisable 設定 hello 儀表板連線字串 toonull hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-318">toodisable logging, set hello dashboard connection string toonull as shown in hello following example.</span></span>

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

<span data-ttu-id="ecdc1-319">hello 下列範例顯示數種方式 toowrite 記錄檔：</span><span class="sxs-lookup"><span data-stu-id="ecdc1-319">hello following example shows several ways toowrite logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="ecdc1-320">Hello WebJobs SDK 儀表板，在 hello 輸出 hello`TextWriter`物件顯示當您移至特定的 toohello 頁面函式引動過程，並按一下**切換輸出**:</span><span class="sxs-lookup"><span data-stu-id="ecdc1-320">In hello WebJobs SDK Dashboard, hello output from hello `TextWriter` object shows up when you go toohello page for a particular function invocation and click **Toggle Output**:</span></span>

![按一下函式引動過程連結](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![函式引動過程頁面中的記錄檔](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="ecdc1-323">Hello WebJobs SDK 儀表板，hello 最近 100 行主控台的輸出顯示出當您移至 toohello 頁面 hello WebJob （不適用於 hello 函式引動過程），然後按一下**切換輸出**。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-323">In hello WebJobs SDK Dashboard, hello most recent 100 lines of Console output show up when you go toohello page for hello WebJob (not for hello function invocation) and click **Toggle Output**.</span></span>

![按一下切換輸出](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

<span data-ttu-id="ecdc1-325">在連續的 WebJob，應用程式記錄檔中顯示/資料/工作/連續/*{webjobname}*/job_log.txt hello web 應用程式檔案系統中的。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-325">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in hello web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="ecdc1-326">在 Azure blob hello 應用程式記錄檔，看起來像這樣： 2014年-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write-Hello world ！、 2014年-09-26T21:01:13，錯誤，contosoadsnew，491e54，635473620738373502,0,17404,19,Console.Error-Hello world ！、 2014年-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out-Hello world ！，</span><span class="sxs-lookup"><span data-stu-id="ecdc1-326">In an Azure blob hello application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="ecdc1-327">在 Azure 資料表 hello`Console.Out`和`Console.Error`記錄看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="ecdc1-327">And in an Azure table hello `Console.Out` and `Console.Error` logs look like this:</span></span>

![在資料表中的資訊記錄檔](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![在資料表中的錯誤記錄檔](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

<span data-ttu-id="ecdc1-330">如果您希望 tooplug 自己記錄器，請參閱[本例](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-330">If you want tooplug in your own logger, see [this example](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span></span>

## <span data-ttu-id="ecdc1-331"><a id="errors"></a>如何 toohandle 錯誤和設定的逾時</span><span class="sxs-lookup"><span data-stu-id="ecdc1-331"><a id="errors"></a>How toohandle errors and configure timeouts</span></span>
<span data-ttu-id="ecdc1-332">hello WebJobs SDK 也包含[逾時](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs)屬性，您可以使用的 toocause 函式 toobe 取消，如果沒有指定的一段時間內完成。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-332">hello WebJobs SDK also includes a [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) attribute that you can use toocause a function toobe canceled if doesn't complete within a specified amount of time.</span></span> <span data-ttu-id="ecdc1-333">如果您想要 tooraise 警示會在一段指定時間內進行太多錯誤，您可以使用 hello`ErrorTrigger`屬性。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-333">And if you want tooraise an alert when too many errors happen within a specified period of time, you can use hello `ErrorTrigger` attribute.</span></span> <span data-ttu-id="ecdc1-334">以下是一個 [ErrorTrigger 範例](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-334">Here is an [ErrorTrigger example](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span></span>

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    too= "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors toohello Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

<span data-ttu-id="ecdc1-335">您也會動態地可停用並啟用函式 toocontrol 是否它們可以觸發，藉由使用應用程式設定或環境變數名稱可能是組態參數。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-335">You can also dynamically disable and enable functions toocontrol whether they can be triggered, by using a configuration switch that could be an app setting or environment variable name.</span></span> <span data-ttu-id="ecdc1-336">範例程式碼，請參閱 hello`Disable`屬性[hello WebJobs SDK 範例儲存機制](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-336">For sample code, see hello `Disable` attribute in [hello WebJobs SDK samples repository](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span></span>

## <span data-ttu-id="ecdc1-337"><a id="nextsteps"></a> 後續步驟</span><span class="sxs-lookup"><span data-stu-id="ecdc1-337"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="ecdc1-338">本指南提供的程式碼範例會顯示如何以使用 Azure 佇列 toohandle 常見案例。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-338">This guide has provided code samples that show how toohandle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="ecdc1-339">如需有關如何 toouse Azure WebJobs 和 hello WebJobs SDK，請參閱[Azure WebJobs 建議資源](http://go.microsoft.com/fwlink/?linkid=390226)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-339">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>
