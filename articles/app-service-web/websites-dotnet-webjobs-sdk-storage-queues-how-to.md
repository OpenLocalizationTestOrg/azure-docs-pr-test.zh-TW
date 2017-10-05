---
title: "如何透過 WebJobs SDK 使用 Azure 佇列儲存體"
description: "了解如何透過 WebJobs SDK 使用 Azure 佇列儲存體。 建立和刪除查詢、插入、查看、取得和刪除佇列訊息等。"
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
ms.openlocfilehash: 63b987a2c9471f2929b8d2dd605323910d2ad43b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-queue-storage-with-the-webjobs-sdk"></a><span data-ttu-id="1833c-104">如何透過 WebJobs SDK 使用 Azure 佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="1833c-104">How to use Azure queue storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="1833c-105">概觀</span><span class="sxs-lookup"><span data-stu-id="1833c-105">Overview</span></span>
<span data-ttu-id="1833c-106">本指南提供了 C# 程式碼範例，示範如何透過 Azure 佇列儲存體服務使用 Azure WebJobs SDK 1.x 版。</span><span class="sxs-lookup"><span data-stu-id="1833c-106">This guide provides C# code samples that show how to use the Azure WebJobs SDK version 1.x with the Azure queue storage service.</span></span>

<span data-ttu-id="1833c-107">本指南假設您知道[如何使用指向您儲存體帳戶的連接字串，在 Visual Studio 中建立 WebJob 專案](websites-dotnet-webjobs-sdk-get-started.md)，或是使用指向[多個儲存體帳戶](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs)的連接字串來建立該專案。</span><span class="sxs-lookup"><span data-stu-id="1833c-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="1833c-108">大部分的程式碼片段只會顯示函數，不會顯示建立 `JobHost` 物件的程式碼，如此範例所示：</span><span class="sxs-lookup"><span data-stu-id="1833c-108">Most of the code snippets only show functions, not the code that creates the `JobHost` object as in this example:</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

<span data-ttu-id="1833c-109">本指南包含下列主題：</span><span class="sxs-lookup"><span data-stu-id="1833c-109">The guide includes the following topics:</span></span>

* [<span data-ttu-id="1833c-110">如何在接收到佇列訊息時觸發函數</span><span class="sxs-lookup"><span data-stu-id="1833c-110">How to trigger a function when a queue message is received</span></span>](#trigger)
  * <span data-ttu-id="1833c-111">字串佇列訊息</span><span class="sxs-lookup"><span data-stu-id="1833c-111">String queue messages</span></span>
  * <span data-ttu-id="1833c-112">POCO 佇列訊息</span><span class="sxs-lookup"><span data-stu-id="1833c-112">POCO queue messages</span></span>
  * <span data-ttu-id="1833c-113">Async 函數</span><span class="sxs-lookup"><span data-stu-id="1833c-113">Async functions</span></span>
  * <span data-ttu-id="1833c-114">適用於 QueueTrigger 屬性的型別</span><span class="sxs-lookup"><span data-stu-id="1833c-114">Types the QueueTrigger attribute works with</span></span>
  * <span data-ttu-id="1833c-115">輪詢演算法</span><span class="sxs-lookup"><span data-stu-id="1833c-115">Polling algorithm</span></span>
  * <span data-ttu-id="1833c-116">多個執行個體</span><span class="sxs-lookup"><span data-stu-id="1833c-116">Multiple instances</span></span>
  * <span data-ttu-id="1833c-117">平行執行</span><span class="sxs-lookup"><span data-stu-id="1833c-117">Parallel execution</span></span>
  * <span data-ttu-id="1833c-118">取得佇列或佇列訊息中繼資料</span><span class="sxs-lookup"><span data-stu-id="1833c-118">Get queue or queue message metadata</span></span>
  * <span data-ttu-id="1833c-119">正常關機</span><span class="sxs-lookup"><span data-stu-id="1833c-119">Graceful shutdown</span></span>
* [<span data-ttu-id="1833c-120">如何在處理佇列訊息時建立佇列訊息</span><span class="sxs-lookup"><span data-stu-id="1833c-120">How to create a queue message while processing a queue message</span></span>](#createqueue)
  * <span data-ttu-id="1833c-121">字串佇列訊息</span><span class="sxs-lookup"><span data-stu-id="1833c-121">String queue messages</span></span>
  * <span data-ttu-id="1833c-122">POCO 佇列訊息</span><span class="sxs-lookup"><span data-stu-id="1833c-122">POCO queue messages</span></span>
  * <span data-ttu-id="1833c-123">建立多個訊息或使用非同步函式</span><span class="sxs-lookup"><span data-stu-id="1833c-123">Create multiple messages or in async functions</span></span>
  * <span data-ttu-id="1833c-124">適用於 Queue 屬性的型別</span><span class="sxs-lookup"><span data-stu-id="1833c-124">Types the Queue attribute works with</span></span>
  * <span data-ttu-id="1833c-125">在函式主體中使用 WebJobs SDK 屬性</span><span class="sxs-lookup"><span data-stu-id="1833c-125">Use WebJobs SDK attributes in the body of a function</span></span>
* [<span data-ttu-id="1833c-126">如何在處理佇列訊息時讀取及寫入 Blob</span><span class="sxs-lookup"><span data-stu-id="1833c-126">How to read and write blobs while processing a queue message</span></span>](#blobs)
  * <span data-ttu-id="1833c-127">字串佇列訊息</span><span class="sxs-lookup"><span data-stu-id="1833c-127">String queue messages</span></span>
  * <span data-ttu-id="1833c-128">POCO 佇列訊息</span><span class="sxs-lookup"><span data-stu-id="1833c-128">POCO queue messages</span></span>
  * <span data-ttu-id="1833c-129">適用於 Blob 屬性的型別</span><span class="sxs-lookup"><span data-stu-id="1833c-129">Types the Blob attribute works with</span></span>
* [<span data-ttu-id="1833c-130">如何處理有害訊息</span><span class="sxs-lookup"><span data-stu-id="1833c-130">How to handle poison messages</span></span>](#poison)
  * <span data-ttu-id="1833c-131">自動處理有害訊息</span><span class="sxs-lookup"><span data-stu-id="1833c-131">Automatic poison message handling</span></span>
  * <span data-ttu-id="1833c-132">手動處理有害訊息</span><span class="sxs-lookup"><span data-stu-id="1833c-132">Manual poison message handling</span></span>
* [<span data-ttu-id="1833c-133">如何設定組態選項</span><span class="sxs-lookup"><span data-stu-id="1833c-133">How to set configuration options</span></span>](#config)
  * <span data-ttu-id="1833c-134">在程式碼中設定 SDK 連接字串</span><span class="sxs-lookup"><span data-stu-id="1833c-134">Set SDK connection strings in code</span></span>
  * <span data-ttu-id="1833c-135">設定 QueueTrigger 設定</span><span class="sxs-lookup"><span data-stu-id="1833c-135">Configure QueueTrigger settings</span></span>
  * <span data-ttu-id="1833c-136">在程式碼中設定 WebJobs SDK 建構函式參數的值</span><span class="sxs-lookup"><span data-stu-id="1833c-136">Set values for WebJobs SDK constructor parameters in code</span></span>
* [<span data-ttu-id="1833c-137">如何手動觸發函數</span><span class="sxs-lookup"><span data-stu-id="1833c-137">How to trigger a function manually</span></span>](#manual)
* [<span data-ttu-id="1833c-138">如何寫入記錄檔</span><span class="sxs-lookup"><span data-stu-id="1833c-138">How to write logs</span></span>](#logs)
* [<span data-ttu-id="1833c-139">如何處理錯誤及設定逾時</span><span class="sxs-lookup"><span data-stu-id="1833c-139">How to handle errors and configure timeouts</span></span>](#errors)
* [<span data-ttu-id="1833c-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1833c-140">Next steps</span></span>](#nextsteps)

## <span data-ttu-id="1833c-141"><a id="trigger"></a> 如何在接收到佇列訊息時觸發函數</span><span class="sxs-lookup"><span data-stu-id="1833c-141"><a id="trigger"></a> How to trigger a function when a queue message is received</span></span>
<span data-ttu-id="1833c-142">若要撰寫 WebJobs SDK 在收到佇列訊息時所呼叫的函數，請使用 `QueueTrigger` 屬性。</span><span class="sxs-lookup"><span data-stu-id="1833c-142">To write a function that the WebJobs SDK calls when a queue message is received, use the `QueueTrigger` attribute.</span></span> <span data-ttu-id="1833c-143">屬性建構函式採用字串參數，來指定要輪詢的佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="1833c-143">The attribute constructor takes a string parameter that specifies the name of the queue to poll.</span></span> <span data-ttu-id="1833c-144">您也可以 [動態設定佇列名稱](#config)。</span><span class="sxs-lookup"><span data-stu-id="1833c-144">You can also [set the queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="1833c-145">字串佇列訊息</span><span class="sxs-lookup"><span data-stu-id="1833c-145">String queue messages</span></span>
<span data-ttu-id="1833c-146">在下列範例中，佇列包含字串訊息，以便 套用 `QueueTrigger` 至名為 `logMessage` 的字串參數，其中包含佇列訊息的內容。</span><span class="sxs-lookup"><span data-stu-id="1833c-146">In the following example, the queue contains a string message, so `QueueTrigger` is applied to a string parameter named `logMessage` which contains the content of the queue message.</span></span> <span data-ttu-id="1833c-147">函數會 [將記錄訊息寫入儀表板](#logs)。</span><span class="sxs-lookup"><span data-stu-id="1833c-147">The function [writes a log message to the Dashboard](#logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="1833c-148">除了 `string` 之外，參數也可以是一個位元組陣列、一個 `CloudQueueMessage` 物件，或一個您定義的 POCO。</span><span class="sxs-lookup"><span data-stu-id="1833c-148">Besides `string`, the parameter may be a byte array, a `CloudQueueMessage` object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="1833c-149">POCO ( [純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 佇列訊息</span><span class="sxs-lookup"><span data-stu-id="1833c-149">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="1833c-150">在下列範例中，佇列訊息會包含 `BlobInformation` 物件的 JSON，其中包含 `BlobName` 屬性。</span><span class="sxs-lookup"><span data-stu-id="1833c-150">In the following example, the queue message contains JSON for a `BlobInformation` object which includes a `BlobName` property.</span></span> <span data-ttu-id="1833c-151">SDK 會自動將物件還原序列化。</span><span class="sxs-lookup"><span data-stu-id="1833c-151">The SDK automatically deserializes the object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="1833c-152">SDK 會使用 [Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) 封裝來序列化和還原序列化訊息。</span><span class="sxs-lookup"><span data-stu-id="1833c-152">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="1833c-153">如果您在不使用 WebJobs SDK 的程式中建立佇列訊息，您可以撰寫和下面範例類似的程式碼來建立 SDK 能夠剖析的 POCO 佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="1833c-153">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="1833c-154">Async 函數</span><span class="sxs-lookup"><span data-stu-id="1833c-154">Async functions</span></span>
<span data-ttu-id="1833c-155">下面的非同步函式會 [將記錄檔寫入儀表板](#logs)。</span><span class="sxs-lookup"><span data-stu-id="1833c-155">The following async function [writes a log to the Dashboard](#logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="1833c-156">Async 函數可能需要取 [消語彙基元](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken)，如下列範例所示 (會複製 Blob)。</span><span class="sxs-lookup"><span data-stu-id="1833c-156">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in the following example which copies a blob.</span></span> <span data-ttu-id="1833c-157">(如需 `queueTrigger` 預留位置的說明，請參閱 [Blobs](#blobs) 一節。)</span><span class="sxs-lookup"><span data-stu-id="1833c-157">(For an explanation of the `queueTrigger` placeholder, see the [Blobs](#blobs) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <span data-ttu-id="1833c-158"><a id="qtattributetypes"></a> 適用於 QueueTrigger 屬性的型別</span><span class="sxs-lookup"><span data-stu-id="1833c-158"><a id="qtattributetypes"></a> Types the QueueTrigger attribute works with</span></span>
<span data-ttu-id="1833c-159">您可以將 `QueueTrigger` 與下列型別搭配使用：</span><span class="sxs-lookup"><span data-stu-id="1833c-159">You can use `QueueTrigger` with the following types:</span></span>

* `string`
* <span data-ttu-id="1833c-160">序列化為 JSON 的 POCO 型別</span><span class="sxs-lookup"><span data-stu-id="1833c-160">A POCO type serialized as JSON</span></span>
* `byte[]`
* `CloudQueueMessage`

### <span data-ttu-id="1833c-161"><a id="polling"></a> 輪詢演算法</span><span class="sxs-lookup"><span data-stu-id="1833c-161"><a id="polling"></a> Polling algorithm</span></span>
<span data-ttu-id="1833c-162">SDK 會實作隨機指數型倒退演算法，以降低閒置佇列輪詢對儲存體交易成本的影響。</span><span class="sxs-lookup"><span data-stu-id="1833c-162">The SDK implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="1833c-163">找到訊息時，SDK 會等待兩秒，然後檢查的另一個訊息；當找不到任何訊息時，它會等候大約四秒，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="1833c-163">When a message is found, the SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="1833c-164">連續嘗試取得佇列訊息失敗後，等候時間會持續增加，直到它到達等待時間上限 (預設值為一分鐘)。</span><span class="sxs-lookup"><span data-stu-id="1833c-164">After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.</span></span> <span data-ttu-id="1833c-165">[您可以設定等待時間上限](#config)。</span><span class="sxs-lookup"><span data-stu-id="1833c-165">[The maximum wait time is configurable](#config).</span></span>

### <span data-ttu-id="1833c-166"><a id="instances"></a> 多個執行個體</span><span class="sxs-lookup"><span data-stu-id="1833c-166"><a id="instances"></a> Multiple instances</span></span>
<span data-ttu-id="1833c-167">如果您的 Web 應用程式是在多個執行個體上執行，則會有一個連續的 WebJob 在每部機器上執行，而每部機器將會等待觸發程序，才嘗試執行函式。</span><span class="sxs-lookup"><span data-stu-id="1833c-167">If your web app runs on multiple instances, a continuous WebJob runs on each machine, and each machine will wait for triggers and attempt to run functions.</span></span> <span data-ttu-id="1833c-168">WebJobs SDK 佇列觸發程序會自動防止函式處理佇列訊息多次；不需將函式撰寫成等冪函式。</span><span class="sxs-lookup"><span data-stu-id="1833c-168">The WebJobs SDK queue trigger automatically prevents a function from processing a queue message multiple times; functions do not have to be written to be idempotent.</span></span> <span data-ttu-id="1833c-169">不過，如果您想要確保在即使有多個主 Web 應用程式執行個體的情況下，仍然只有一個函式執行個體會執行，則您可以使用 `Singleton` 屬性。</span><span class="sxs-lookup"><span data-stu-id="1833c-169">However, if you want to ensure that only one instance of a function runs even when there are multiple instances of the host web app, you can use the `Singleton` attribute.</span></span>

### <span data-ttu-id="1833c-170"><a id="parallel"></a> 平行執行</span><span class="sxs-lookup"><span data-stu-id="1833c-170"><a id="parallel"></a> Parallel execution</span></span>
<span data-ttu-id="1833c-171">如果您有多個函數在不同的佇列上接聽，則同時接收到訊息時，SDK 會以平行方式呼叫它們。</span><span class="sxs-lookup"><span data-stu-id="1833c-171">If you have multiple functions listening on different queues, the SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="1833c-172">收到單一佇列的多個訊息時也是如此。</span><span class="sxs-lookup"><span data-stu-id="1833c-172">The same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="1833c-173">根據預設，SDK 會一次取得一批 (16 個) 佇列訊息，並執行以平行方式處理它們的函數。</span><span class="sxs-lookup"><span data-stu-id="1833c-173">By default, the SDK gets a batch of 16 queue messages at a time and executes the function that processes them in parallel.</span></span> <span data-ttu-id="1833c-174">[您可以設定批次大小](#config)。</span><span class="sxs-lookup"><span data-stu-id="1833c-174">[The batch size is configurable](#config).</span></span> <span data-ttu-id="1833c-175">當要處理的訊息數目減少到批次大小 (該批訊息數目) 的一半時，SDK 就會取得另一批訊息並開始處理那些訊息。</span><span class="sxs-lookup"><span data-stu-id="1833c-175">When the number being processed gets down to half of the batch size, the SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="1833c-176">因此，每個函數並行處理之訊息的上限數目為批次大小 (該批訊息數目) 的 1.5 倍。</span><span class="sxs-lookup"><span data-stu-id="1833c-176">Therefore the maximum number of concurrent messages being processed per function is one and a half times the batch size.</span></span> <span data-ttu-id="1833c-177">這項限制個別套用至具有 `QueueTrigger` 屬性的每個函式。</span><span class="sxs-lookup"><span data-stu-id="1833c-177">This limit applies separately to each function that has a `QueueTrigger` attribute.</span></span>

<span data-ttu-id="1833c-178">如果您不想要平行執行在單一佇列上收到的訊息，您可以將批次大小設定為 1。</span><span class="sxs-lookup"><span data-stu-id="1833c-178">If you don't want parallel execution for messages received on one queue, you can set the batch size to 1.</span></span> <span data-ttu-id="1833c-179">另請參閱 **Azure WebJobs SDK 1.1.0 RTM** 中的 [更充分掌控佇列處理](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/)。</span><span class="sxs-lookup"><span data-stu-id="1833c-179">See also **More control over Queue processing** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span></span>

### <span data-ttu-id="1833c-180"><a id="queuemetadata"></a>取得佇列或佇列訊息中繼資料</span><span class="sxs-lookup"><span data-stu-id="1833c-180"><a id="queuemetadata"></a>Get queue or queue message metadata</span></span>
<span data-ttu-id="1833c-181">您可以透過新增參數至方法簽章來取得下列訊息屬性：</span><span class="sxs-lookup"><span data-stu-id="1833c-181">You can get the following message properties by adding parameters to the method signature:</span></span>

* <span data-ttu-id="1833c-182">`DateTimeOffset` expirationTime</span><span class="sxs-lookup"><span data-stu-id="1833c-182">`DateTimeOffset` expirationTime</span></span>
* <span data-ttu-id="1833c-183">`DateTimeOffset` insertionTime</span><span class="sxs-lookup"><span data-stu-id="1833c-183">`DateTimeOffset` insertionTime</span></span>
* <span data-ttu-id="1833c-184">`DateTimeOffset` nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="1833c-184">`DateTimeOffset` nextVisibleTime</span></span>
* <span data-ttu-id="1833c-185">`string` queueTrigger (包含訊息文字)</span><span class="sxs-lookup"><span data-stu-id="1833c-185">`string` queueTrigger (contains message text)</span></span>
* <span data-ttu-id="1833c-186">`string` id</span><span class="sxs-lookup"><span data-stu-id="1833c-186">`string` id</span></span>
* <span data-ttu-id="1833c-187">`string` popReceipt</span><span class="sxs-lookup"><span data-stu-id="1833c-187">`string` popReceipt</span></span>
* <span data-ttu-id="1833c-188">`int` dequeueCount</span><span class="sxs-lookup"><span data-stu-id="1833c-188">`int` dequeueCount</span></span>

<span data-ttu-id="1833c-189">如果您想要直接使用 Azure 儲存體 API，您也可以加入 `CloudStorageAccount` 參數。</span><span class="sxs-lookup"><span data-stu-id="1833c-189">If you want to work directly with the Azure storage API, you can also add a `CloudStorageAccount` parameter.</span></span>

<span data-ttu-id="1833c-190">下列範例會將此中繼資料全部寫入至 INFO 應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1833c-190">The following example writes all of this metadata to an INFO application log.</span></span> <span data-ttu-id="1833c-191">在範例中，logMessage 和 queueTrigger 包含佇列訊息的內容。</span><span class="sxs-lookup"><span data-stu-id="1833c-191">In the example, both logMessage and queueTrigger contain the content of the queue message.</span></span>

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

<span data-ttu-id="1833c-192">以下是範例程式碼所寫入的範例記錄：</span><span class="sxs-lookup"><span data-stu-id="1833c-192">Here is a sample log written by the sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <span data-ttu-id="1833c-193"><a id="graceful"></a>順利關機</span><span class="sxs-lookup"><span data-stu-id="1833c-193"><a id="graceful"></a>Graceful shutdown</span></span>
<span data-ttu-id="1833c-194">在連續 WebJob 中執行的函數可以接受 `CancellationToken` 參數，該參數可讓作業系統在 WebJob 即將終止時通知函數。</span><span class="sxs-lookup"><span data-stu-id="1833c-194">A function that runs in a continuous WebJob can accept a `CancellationToken` parameter which enables the operating system to notify the function when the WebJob is about to be terminated.</span></span> <span data-ttu-id="1833c-195">您可以使用此通知來確保函數不會在讓資料維持不一致狀態的情況下意外終止。</span><span class="sxs-lookup"><span data-stu-id="1833c-195">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="1833c-196">下列範例示範如何透過函數檢查即將終止的 WebJob。</span><span class="sxs-lookup"><span data-stu-id="1833c-196">The following example shows how to check for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="1833c-197">**注意：** 儀表板可能不會正確顯示已關閉之函數的狀態與輸出。</span><span class="sxs-lookup"><span data-stu-id="1833c-197">**Note:** The Dashboard might not correctly show the status and output of functions that have been shut down.</span></span>

<span data-ttu-id="1833c-198">如需詳細資訊，請參閱 [WebJobs 正常關機](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR)。</span><span class="sxs-lookup"><span data-stu-id="1833c-198">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <span data-ttu-id="1833c-199"><a id="createqueue"></a> 如何在處理佇列訊息時建立佇列訊息</span><span class="sxs-lookup"><span data-stu-id="1833c-199"><a id="createqueue"></a> How to create a queue message while processing a queue message</span></span>
<span data-ttu-id="1833c-200">若要編寫會建立新佇列訊息的函數，請使用 `Queue` 屬性。</span><span class="sxs-lookup"><span data-stu-id="1833c-200">To write a function that creates a new queue message, use the `Queue` attribute.</span></span> <span data-ttu-id="1833c-201">就像 `QueueTrigger`一樣，您可以用字串的方式傳入佇列名稱，或者您可以 [動態設定佇列名稱](#config)。</span><span class="sxs-lookup"><span data-stu-id="1833c-201">Like `QueueTrigger`, you pass in the queue name as a string or you can [set the queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="1833c-202">字串佇列訊息</span><span class="sxs-lookup"><span data-stu-id="1833c-202">String queue messages</span></span>
<span data-ttu-id="1833c-203">下面的非同步程式碼範例會在名稱為 "outputqueue" 的佇列中建立一個新的佇列訊息，其內容與名為 "inputqueue" 的佇列中收到的佇列訊息相同。</span><span class="sxs-lookup"><span data-stu-id="1833c-203">The following non-async code sample creates a new queue message in the queue named "outputqueue" with the same content as the queue message received in the queue named "inputqueue".</span></span> <span data-ttu-id="1833c-204">(如需非同步函式，請使用 `IAsyncCollector<T>`，如本節後續內容所示。)</span><span class="sxs-lookup"><span data-stu-id="1833c-204">(For async functions use `IAsyncCollector<T>` as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="1833c-205">POCO ( [純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 佇列訊息</span><span class="sxs-lookup"><span data-stu-id="1833c-205">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="1833c-206">若要建立包含 POCO 物件 (而非字串) 的佇列訊息，請將 POCO 做為輸出參數傳送至 `Queue` 屬性建構函式。</span><span class="sxs-lookup"><span data-stu-id="1833c-206">To create a queue message that contains a POCO rather than a string, pass the POCO type as an output parameter to the `Queue` attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="1833c-207">SDK 會自動將物件序列化為 JSON。</span><span class="sxs-lookup"><span data-stu-id="1833c-207">The SDK automatically serializes the object to JSON.</span></span> <span data-ttu-id="1833c-208">即使物件是空值，也一律會建立佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="1833c-208">A queue message is always created, even if the object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="1833c-209">建立多個訊息或使用非同步函式</span><span class="sxs-lookup"><span data-stu-id="1833c-209">Create multiple messages or in async functions</span></span>
<span data-ttu-id="1833c-210">若要建立多個訊息，請將輸出佇列的參數型別設為 `ICollector<T>` 或 `IAsyncCollector<T>`，如下面範例所示。</span><span class="sxs-lookup"><span data-stu-id="1833c-210">To create multiple messages, make the parameter type for the output queue `ICollector<T>` or `IAsyncCollector<T>`, as shown in the following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="1833c-211">呼叫 `Add` 方法時，就會立即建立每個佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="1833c-211">Each queue message is created immediately when the `Add` method is called.</span></span>

### <a name="types-that-the-queue-attribute-works-with"></a><span data-ttu-id="1833c-212">適用於 Queue 屬性的型別</span><span class="sxs-lookup"><span data-stu-id="1833c-212">Types that the Queue attribute works with</span></span>
<span data-ttu-id="1833c-213">您可以在下列參數型別使用 `Queue` 屬性：</span><span class="sxs-lookup"><span data-stu-id="1833c-213">You can use the `Queue` attribute on the following parameter types:</span></span>

* <span data-ttu-id="1833c-214">`out string` (函式結束時，如果參數值非 Null，就會建立佇列訊息)</span><span class="sxs-lookup"><span data-stu-id="1833c-214">`out string` (creates queue message if parameter value is non-null when the function ends)</span></span>
* <span data-ttu-id="1833c-215">`out byte[]` (作用就像是 `string`)</span><span class="sxs-lookup"><span data-stu-id="1833c-215">`out byte[]` (works like `string`)</span></span>
* <span data-ttu-id="1833c-216">`out CloudQueueMessage` (作用就像是 `string`)</span><span class="sxs-lookup"><span data-stu-id="1833c-216">`out CloudQueueMessage` (works like `string`)</span></span>
* <span data-ttu-id="1833c-217">`out POCO` (可序列化型別，當函式結束時，如果參數為 Null，就會使用 Null 物件建立訊息)</span><span class="sxs-lookup"><span data-stu-id="1833c-217">`out POCO` (a serializable type, creates a message with a null object if the paramter is null when the function ends)</span></span>
* `ICollector`
* `IAsyncCollector`
* <span data-ttu-id="1833c-218">`CloudQueue` (用於直接使用 Azure 儲存體 API 手動建立訊息)</span><span class="sxs-lookup"><span data-stu-id="1833c-218">`CloudQueue` (for creating messages manually using the Azure Storage API directly)</span></span>

### <span data-ttu-id="1833c-219"><a id="ibinder"></a>在函式主體中使用 WebJobs SDK 屬性</span><span class="sxs-lookup"><span data-stu-id="1833c-219"><a id="ibinder"></a>Use WebJobs SDK attributes in the body of a function</span></span>
<span data-ttu-id="1833c-220">如果您需要先在函式中執行部分工作，然後再使用 WebJobs SDK 屬性，例如 `Queue`、`Blob`  或 `Table`，您可以使用 `IBinder` 介面。</span><span class="sxs-lookup"><span data-stu-id="1833c-220">If you need to do some work in your function before using a WebJobs SDK attribute such as `Queue`, `Blob`, or `Table`, you can use the `IBinder` interface.</span></span>

<span data-ttu-id="1833c-221">下列範例會使用輸入佇列訊息，並在輸出佇列中建立含有相同內容的新訊息。</span><span class="sxs-lookup"><span data-stu-id="1833c-221">The following example takes an input queue message and creates a new message with the same content in an output queue.</span></span> <span data-ttu-id="1833c-222">輸出佇列名稱會由函數主體中的程式碼設定。</span><span class="sxs-lookup"><span data-stu-id="1833c-222">The output queue name is set by code in the body of the function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="1833c-223">`IBinder` 介面也能與 `Table` 和 `Blob` 屬性搭配使用。</span><span class="sxs-lookup"><span data-stu-id="1833c-223">The `IBinder` interface can also be used with the `Table` and `Blob` attributes.</span></span>

## <span data-ttu-id="1833c-224"><a id="blobs"></a> 如何在處理佇列訊息時讀取及寫入 Blob 與表格</span><span class="sxs-lookup"><span data-stu-id="1833c-224"><a id="blobs"></a> How to read and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="1833c-225">`Blob` 與 `Table` 屬性可讓您讀取和寫入 Blob 與資料表。</span><span class="sxs-lookup"><span data-stu-id="1833c-225">The `Blob` and `Table` attributes enable you to read and write blobs and tables.</span></span> <span data-ttu-id="1833c-226">本節中的範例適用於 Blob。</span><span class="sxs-lookup"><span data-stu-id="1833c-226">The samples in this section apply to blobs.</span></span> <span data-ttu-id="1833c-227">如需示範如何在建立或更新 Blob 時觸發程序的程式碼範例，請參閱[如何透過 WebJobs SDK 使用 Azure Blob 儲存體](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)，若需讀取和撰寫資料表的程式碼範例，請參閱[如何透過 WebJobs SDK 使用 Azure 資料表儲存體](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="1833c-227">For code samples that show how to trigger processes when blobs are created or updated, see [How to use Azure blob storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How to use Azure table storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="1833c-228">觸發 Blob 作業的字串佇列訊息</span><span class="sxs-lookup"><span data-stu-id="1833c-228">String queue messages triggering blob operations</span></span>
<span data-ttu-id="1833c-229">對於包含字串的佇列訊息，您可以在 `Blob` 屬性的 `blobPath` 參數中使用 `queueTrigger` 預留位置，它包含了訊息的內容。</span><span class="sxs-lookup"><span data-stu-id="1833c-229">For a queue message that contains a string, `queueTrigger` is a placeholder you can use in the `Blob` attribute's `blobPath` parameter that contains the contents of the message.</span></span>

<span data-ttu-id="1833c-230">下列範例使用 `Stream` 物件來讀取及寫入 Blob。</span><span class="sxs-lookup"><span data-stu-id="1833c-230">The following example uses `Stream` objects to read and write blobs.</span></span> <span data-ttu-id="1833c-231">佇列訊息提供位於 textblobs 容器中 Blob 的名稱。</span><span class="sxs-lookup"><span data-stu-id="1833c-231">The queue message is the name of a blob located in the textblobs container.</span></span> <span data-ttu-id="1833c-232">會在相同的容器中建立 Blob 的複本，並在其名稱中附加 "-new"。</span><span class="sxs-lookup"><span data-stu-id="1833c-232">A copy of the blob with "-new" appended to the name is created in the same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="1833c-233">`Blob` 屬性建構函式採用 `blobPath` 參數來指定容器與 Blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="1833c-233">The `Blob` attribute constructor takes a `blobPath` parameter that specifies the container and blob name.</span></span> <span data-ttu-id="1833c-234">如需此預留位置的詳細資訊，請參閱 [如何透過 WebJobs SDK 使用 Azure Blob 儲存體](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="1833c-234">For more information about this placeholder, see [How to use Azure blob storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span></span>

<span data-ttu-id="1833c-235">當這個屬性裝飾 `Stream` 物件，另一個建構函式參數會將 `FileAccess` 模式指定為讀取、 寫入或讀取/寫入。</span><span class="sxs-lookup"><span data-stu-id="1833c-235">When the attribute decorates a `Stream` object, another constructor parameter specifies the `FileAccess` mode as read, write, or read/write.</span></span>

<span data-ttu-id="1833c-236">下列範例使用 `CloudBlockBlob` 物件來刪除 Blob。</span><span class="sxs-lookup"><span data-stu-id="1833c-236">The following example uses a `CloudBlockBlob` object to delete a blob.</span></span> <span data-ttu-id="1833c-237">佇列訊息就是 Blob 的名稱。</span><span class="sxs-lookup"><span data-stu-id="1833c-237">The queue message is the name of the blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <span data-ttu-id="1833c-238"><a id="pocoblobs"></a> POCO ( [純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 佇列訊息</span><span class="sxs-lookup"><span data-stu-id="1833c-238"><a id="pocoblobs"></a> POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="1833c-239">對於在佇列訊息中儲存為 JSON 的 POCO 物件，您可以在 `Queue` 屬性的 `blobPath` 參數中使用指定物件屬性的預留位置。</span><span class="sxs-lookup"><span data-stu-id="1833c-239">For a POCO stored as JSON in the queue message, you can use placeholders that name properties of the object in the `Queue` attribute's `blobPath` parameter.</span></span> <span data-ttu-id="1833c-240">您也可以使用 [佇列中繼資料屬性名稱](#queuemetadata) 做為預留位置。</span><span class="sxs-lookup"><span data-stu-id="1833c-240">You can also use [queue metadata property names](#queuemetadata) as placeholders.</span></span>

<span data-ttu-id="1833c-241">下列範例會將 Blob 複製到具有不同副檔名的新 Blob。</span><span class="sxs-lookup"><span data-stu-id="1833c-241">The following example copies a blob to a new blob with a different extension.</span></span> <span data-ttu-id="1833c-242">佇列訊息就是包含 `BlobName` 與 `BlobNameWithoutExtension` 屬性的 `BlobInformation` 物件。</span><span class="sxs-lookup"><span data-stu-id="1833c-242">The queue message is a `BlobInformation` object that includes `BlobName` and `BlobNameWithoutExtension` properties.</span></span> <span data-ttu-id="1833c-243">在 `Blob` 屬性的 Blob 路徑中使用屬性名稱做為預留位置。</span><span class="sxs-lookup"><span data-stu-id="1833c-243">The property names are used as placeholders in the blob path for the `Blob` attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="1833c-244">SDK 會使用 [Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) 封裝來序列化和還原序列化訊息。</span><span class="sxs-lookup"><span data-stu-id="1833c-244">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="1833c-245">如果您在不使用 WebJobs SDK 的程式中建立佇列訊息，您可以撰寫和下面範例類似的程式碼來建立 SDK 能夠剖析的 POCO 佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="1833c-245">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="1833c-246">如果您需要先在函數中執行部分工作，然後再將 Blob 繫結至物件，您可以在函數主體中使用屬性， [如之前所示的佇列屬性](#ibinder)。</span><span class="sxs-lookup"><span data-stu-id="1833c-246">If you need to do some work in your function before binding a blob to an object, you can use the attribute in the body of the function, [as shown earlier for the Queue attribute](#ibinder).</span></span>

### <span data-ttu-id="1833c-247"><a id="blobattributetypes"></a> 可以與 Blob 屬性搭配使用的型別</span><span class="sxs-lookup"><span data-stu-id="1833c-247"><a id="blobattributetypes"></a> Types you can use the Blob attribute with</span></span>
<span data-ttu-id="1833c-248">`Blob` 屬性能與下列型別搭配使用：</span><span class="sxs-lookup"><span data-stu-id="1833c-248">The `Blob` attribute can be used with the following types:</span></span>

* <span data-ttu-id="1833c-249">`Stream` (讀取或寫入，可使用 FileAccess 建構函式參數指定)</span><span class="sxs-lookup"><span data-stu-id="1833c-249">`Stream` (read or write, specified by using the FileAccess constructor parameter)</span></span>
* `TextReader`
* `TextWriter`
* <span data-ttu-id="1833c-250">`string` (讀取)</span><span class="sxs-lookup"><span data-stu-id="1833c-250">`string` (read)</span></span>
* <span data-ttu-id="1833c-251">`out string` (寫入；當函式傳回時，如果字串參數非 Null，就只會建立 Blob)</span><span class="sxs-lookup"><span data-stu-id="1833c-251">`out string` (write; creates a blob only if the string parameter is non-null when the function returns)</span></span>
* <span data-ttu-id="1833c-252">POCO (讀取)</span><span class="sxs-lookup"><span data-stu-id="1833c-252">POCO (read)</span></span>
* <span data-ttu-id="1833c-253">out POCO (寫入；一律會建立 Blob，當函式傳回時，如果 POCO 參數為 Null，就建立為 Null 物件)</span><span class="sxs-lookup"><span data-stu-id="1833c-253">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when the function returns)</span></span>
* <span data-ttu-id="1833c-254">`CloudBlobStream` (寫入)</span><span class="sxs-lookup"><span data-stu-id="1833c-254">`CloudBlobStream` (write)</span></span>
* <span data-ttu-id="1833c-255">`ICloudBlob` (讀取或寫入)</span><span class="sxs-lookup"><span data-stu-id="1833c-255">`ICloudBlob` (read or write)</span></span>
* <span data-ttu-id="1833c-256">`CloudBlockBlob` (讀取或寫入)</span><span class="sxs-lookup"><span data-stu-id="1833c-256">`CloudBlockBlob` (read or write)</span></span>
* <span data-ttu-id="1833c-257">`CloudPageBlob` (讀取或寫入)</span><span class="sxs-lookup"><span data-stu-id="1833c-257">`CloudPageBlob` (read or write)</span></span>

## <span data-ttu-id="1833c-258"><a id="poison"></a> 如何處理有害訊息</span><span class="sxs-lookup"><span data-stu-id="1833c-258"><a id="poison"></a> How to handle poison messages</span></span>
<span data-ttu-id="1833c-259">內容會導致函數失敗的訊息稱為「有害訊息」 。</span><span class="sxs-lookup"><span data-stu-id="1833c-259">Messages whose content causes a function to fail are called *poison messages*.</span></span> <span data-ttu-id="1833c-260">當函數失敗時不會刪除佇列訊息，最後會再度挑選到該訊息，造成重複循環。</span><span class="sxs-lookup"><span data-stu-id="1833c-260">When the function fails, the queue message is not deleted and eventually is picked up again, causing the cycle to be repeated.</span></span> <span data-ttu-id="1833c-261">SDK 可在有限的反覆次數之後自動中斷循環，或者您可以手動中斷循環。</span><span class="sxs-lookup"><span data-stu-id="1833c-261">The SDK can automatically interrupt the cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="1833c-262">自動處理有害訊息</span><span class="sxs-lookup"><span data-stu-id="1833c-262">Automatic poison message handling</span></span>
<span data-ttu-id="1833c-263">SDK 將會呼叫函數最多 5 次以處理佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="1833c-263">The SDK will call a function up to 5 times to process a queue message.</span></span> <span data-ttu-id="1833c-264">如果第五次嘗試失敗，訊息便會移到有害佇列中。</span><span class="sxs-lookup"><span data-stu-id="1833c-264">If the fifth try fails, the message is moved to a poison queue.</span></span> <span data-ttu-id="1833c-265">[您可以設定重試次數上限](#config)。</span><span class="sxs-lookup"><span data-stu-id="1833c-265">[The maximum number of retries is configurable](#config).</span></span>

<span data-ttu-id="1833c-266">有害佇列名為 *{originalqueuename}*-poison。</span><span class="sxs-lookup"><span data-stu-id="1833c-266">The poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="1833c-267">您可以撰寫函數，透過記錄或傳送通知表示需要手動處理，來處理有害佇列中的訊息。</span><span class="sxs-lookup"><span data-stu-id="1833c-267">You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="1833c-268">在下列範例中，當佇列訊息包含不存在的 Blob 名稱時， `CopyBlob` 函式將會失敗。</span><span class="sxs-lookup"><span data-stu-id="1833c-268">In the following example the `CopyBlob` function will fail when a queue message contains the name of a blob that doesn't exist.</span></span> <span data-ttu-id="1833c-269">發生時，就會從 copyblobqueue 佇列將訊息移至 copyblobqueue-poison 佇列。</span><span class="sxs-lookup"><span data-stu-id="1833c-269">When that happens, the message is moved from the copyblobqueue queue to the copyblobqueue-poison queue.</span></span> <span data-ttu-id="1833c-270">`ProcessPoisonMessage` 接著會記錄有害訊息。</span><span class="sxs-lookup"><span data-stu-id="1833c-270">The `ProcessPoisonMessage` then logs the poison message.</span></span>

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

<span data-ttu-id="1833c-271">下圖顯示這些函數處理有害訊息之後的主控台輸出。</span><span class="sxs-lookup"><span data-stu-id="1833c-271">The following illustration shows console output from these functions when a poison message is processed.</span></span>

![主控台輸出中的有害訊息處理](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="1833c-273">手動處理有害訊息</span><span class="sxs-lookup"><span data-stu-id="1833c-273">Manual poison message handling</span></span>
<span data-ttu-id="1833c-274">您可以將名為 `dequeueCount` 的 `int` 參數加入到函式中，來取得訊息已被挑選來處理的次數。</span><span class="sxs-lookup"><span data-stu-id="1833c-274">You can get the number of times a message has been picked up for processing by adding an `int` parameter named `dequeueCount` to your function.</span></span> <span data-ttu-id="1833c-275">然後您可以檢查函數程式碼中的清除佇列計數，並在數目超出臨界值時自行執行有害訊息處理，如下面的範例所示。</span><span class="sxs-lookup"><span data-stu-id="1833c-275">You can then check the dequeue count in function code and perform your own poison message handling when the number exceeds a threshold, as shown in the following example.</span></span>

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

## <span data-ttu-id="1833c-276"><a id="config"></a> 如何設定組態選項</span><span class="sxs-lookup"><span data-stu-id="1833c-276"><a id="config"></a> How to set configuration options</span></span>
<span data-ttu-id="1833c-277">您可以使用 `JobHostConfiguration` 型別來設定下列組態選項：</span><span class="sxs-lookup"><span data-stu-id="1833c-277">You can use the `JobHostConfiguration` type to set the following configuration options:</span></span>

* <span data-ttu-id="1833c-278">在程式碼中設定 SDK 連接字串。</span><span class="sxs-lookup"><span data-stu-id="1833c-278">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="1833c-279">設定 `QueueTrigger` 設定，例如清除佇列計數上限。</span><span class="sxs-lookup"><span data-stu-id="1833c-279">Configure `QueueTrigger` settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="1833c-280">從組態取得佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="1833c-280">Get queue names from configuration.</span></span>

### <span data-ttu-id="1833c-281"><a id="setconnstr"></a>在程式碼中設定 SDK 連接字串</span><span class="sxs-lookup"><span data-stu-id="1833c-281"><a id="setconnstr"></a>Set SDK connection strings in code</span></span>
<span data-ttu-id="1833c-282">在程式碼中設定 SDK 連接字串可讓您在組態檔或環境變數中使用您自己的連接字串名稱，如下面範例所示。</span><span class="sxs-lookup"><span data-stu-id="1833c-282">Setting the SDK connection strings in code enables you to use your own connection string names in configuration files or environment variables, as shown in the following example.</span></span>

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

### <span data-ttu-id="1833c-283"><a id="configqueue"></a>設定 QueueTrigger 設定</span><span class="sxs-lookup"><span data-stu-id="1833c-283"><a id="configqueue"></a>Configure QueueTrigger  settings</span></span>
<span data-ttu-id="1833c-284">您可以配置會套用至佇列訊息處理的下列設定：</span><span class="sxs-lookup"><span data-stu-id="1833c-284">You can configure the following settings that apply to the queue message processing:</span></span>

* <span data-ttu-id="1833c-285">挑選以同時平行執行的佇列訊息數目上限 (預設值為 16)。</span><span class="sxs-lookup"><span data-stu-id="1833c-285">The maximum number of queue messages that are picked up simultaneously to be executed in parallel (default is 16).</span></span>
* <span data-ttu-id="1833c-286">將佇列訊息傳送到有害佇列之前的重試次數上限 (預設值為 5)。</span><span class="sxs-lookup"><span data-stu-id="1833c-286">The maximum number of retries before a queue message is sent to a poison queue (default is 5).</span></span>
* <span data-ttu-id="1833c-287">佇列為空的時，要再次輪詢前的等待時間上限 (預設值為 1 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="1833c-287">The maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="1833c-288">下列範例示範如何配置這些設定：</span><span class="sxs-lookup"><span data-stu-id="1833c-288">The following example shows how to configure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <span data-ttu-id="1833c-289"><a id="setnamesincode"></a>在程式碼中設定 WebJobs SDK 建構函式參數的值</span><span class="sxs-lookup"><span data-stu-id="1833c-289"><a id="setnamesincode"></a>Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="1833c-290">有時候您不想要採取硬式編碼的方式，而是在程式碼中指定佇列名稱、Blob 名稱或容器或資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="1833c-290">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="1833c-291">例如，您可能想要在組態檔或環境變數中指定 `QueueTrigger` 的佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="1833c-291">For example, you might want to specify the queue name for `QueueTrigger` in a configuration file or environment variable.</span></span>

<span data-ttu-id="1833c-292">方法是將 `NameResolver` 物件傳入 `JobHostConfiguration` 型別。</span><span class="sxs-lookup"><span data-stu-id="1833c-292">You can do that by passing in a `NameResolver` object to the `JobHostConfiguration` type.</span></span> <span data-ttu-id="1833c-293">在 WebJobs SDK 屬性建構函式參數中包含以百分比 (%) 符號括住的特殊預留位置，然後 `NameResolver` 程式碼會指定實際要用以取代那些預留位置的值。</span><span class="sxs-lookup"><span data-stu-id="1833c-293">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your `NameResolver` code specifies the actual values to be used in place of those placeholders.</span></span>

<span data-ttu-id="1833c-294">例如，假設您想要在測試環境中使用名為 logqueuetest 的佇列，和在生產環境中使用名為 logqueueprod 的佇列。</span><span class="sxs-lookup"><span data-stu-id="1833c-294">For example, suppose you want to use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="1833c-295">您不想使用硬式編碼的佇列名稱，而想要在會有實際佇列名稱的 `appSettings` 集合中指定項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="1833c-295">Instead of a hard-coded queue name, you want to specify the name of an entry in the `appSettings` collection that would have the actual queue name.</span></span> <span data-ttu-id="1833c-296">如果 `appSettings` 索引鍵為 logqueue，您的函式看起來可能像下面的範例。</span><span class="sxs-lookup"><span data-stu-id="1833c-296">If the `appSettings` key is logqueue, your function could look like the following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="1833c-297">`NameResolver` 類別接著可以從 `appSettings` 取得佇列名稱，如下面範例所示：</span><span class="sxs-lookup"><span data-stu-id="1833c-297">Your `NameResolver` class could then get the queue name from `appSettings` as shown in the following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="1833c-298">您將 `NameResolver` 類別傳入 `JobHost` 物件，如下面範例所示。</span><span class="sxs-lookup"><span data-stu-id="1833c-298">You pass the `NameResolver` class in to the `JobHost` object as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="1833c-299">**注意：** 每次呼叫函式時，都會解析佇列、資料表及 Blob 名稱，但只有在應用程式啟動時才會解析 Blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="1833c-299">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when the application starts.</span></span> <span data-ttu-id="1833c-300">您無法在執行工作時，變更 Blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="1833c-300">You can't change blob container name while the job is running.</span></span>

## <span data-ttu-id="1833c-301"><a id="manual"></a>如何手動觸發函數</span><span class="sxs-lookup"><span data-stu-id="1833c-301"><a id="manual"></a>How to trigger a function manually</span></span>
<span data-ttu-id="1833c-302">若要手動觸發函式，請在函式的 `JobHost` 物件與 `NoAutomaticTrigger` 屬性上使用 `Call` 或 `CallAsync` 方法，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="1833c-302">To trigger a function manually, use the `Call` or `CallAsync` method on the `JobHost` object and the `NoAutomaticTrigger` attribute on the function, as shown in the following example.</span></span>

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

## <span data-ttu-id="1833c-303"><a id="logs"></a>如何寫入記錄檔</span><span class="sxs-lookup"><span data-stu-id="1833c-303"><a id="logs"></a>How to write logs</span></span>
<span data-ttu-id="1833c-304">儀表板會在兩個地方顯示記錄檔：WebJob 的頁面與特定 WebJob 引動過程的頁面。</span><span class="sxs-lookup"><span data-stu-id="1833c-304">The Dashboard shows logs in two places: the page for the WebJob, and the page for a particular WebJob invocation.</span></span>

![WebJob 頁面中的記錄檔](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![函式引動過程頁面中的記錄檔](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="1833c-307">您在函式或在 `Main()` 方法中所呼叫主控台方法的輸出會顯示在 WebJob 的 [儀表板] 頁面，而不是特定方法引動過程的頁面。</span><span class="sxs-lookup"><span data-stu-id="1833c-307">Output from Console methods that you call in a function or in the `Main()` method appears in the Dashboard page for the WebJob, not in the page for a particular method invocation.</span></span> <span data-ttu-id="1833c-308">您從方法簽章的參數所取得 TextWriter 物件的輸出會顯示在方法引動過程的 [儀表板] 頁面。</span><span class="sxs-lookup"><span data-stu-id="1833c-308">Output from the TextWriter object that you get from a parameter in your method signature appears in the Dashboard page for a method invocation.</span></span>

<span data-ttu-id="1833c-309">因為主控台屬於單一執行緒，無法同時執行許多工作函式，所以主控台輸出無法連結到特定的方法引動過程。</span><span class="sxs-lookup"><span data-stu-id="1833c-309">Console output can't be linked to a particular method invocation because the Console is single-threaded, while many job functions may be running at the same time.</span></span> <span data-ttu-id="1833c-310">這就是 SDK 提供的每個函式引動過程都使用自己專屬的記錄寫入器物件的原因。</span><span class="sxs-lookup"><span data-stu-id="1833c-310">That's why the  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="1833c-311">若要寫入[應用程式追蹤記錄](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview)，請使用 `Console.Out` (建立標示為 INFO 的記錄檔) 與 `Console.Error` (建立標示為 ERROR 的記錄檔)。</span><span class="sxs-lookup"><span data-stu-id="1833c-311">To write [application tracing logs](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (creates logs marked as INFO) and `Console.Error` (creates logs marked as ERROR).</span></span> <span data-ttu-id="1833c-312">替代方法是使用 [Trace 或 TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)，除了資訊與錯誤之外，還能提供詳細資訊、警告及嚴重層級。</span><span class="sxs-lookup"><span data-stu-id="1833c-312">An alternative is to use [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition to Info and Error.</span></span> <span data-ttu-id="1833c-313">視您設定 Azure 網頁應用程式的方式而定，應用程式追蹤記錄檔會出現在網頁應用程式記錄檔、Azure 資料表或 Azure Blob 中。</span><span class="sxs-lookup"><span data-stu-id="1833c-313">Application tracing logs appear in the web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="1833c-314">所有主控台輸出的應用程式記錄檔裡最近的 100 筆記錄也同樣會顯示在 WebJob 的 [儀表板] 頁面，而不是函式引動過程的頁面。</span><span class="sxs-lookup"><span data-stu-id="1833c-314">As is true of all Console output, the most recent 100 application logs also appear in the Dashboard page for the WebJob, not the page for a function invocation.</span></span>

<span data-ttu-id="1833c-315">只有當程式是以 Azure WebJob 執行時，主控台輸出才會顯示在儀表板，而不是在本機或在某些其他環境中執行時。</span><span class="sxs-lookup"><span data-stu-id="1833c-315">Console output appears in the Dashboard only if the program is running in an Azure WebJob, not if the program is running locally or in some other environment.</span></span>

<span data-ttu-id="1833c-316">停用針對高輸送量的儀表板記錄。</span><span class="sxs-lookup"><span data-stu-id="1833c-316">Disable dashboard logging for high throughput scenarios.</span></span> <span data-ttu-id="1833c-317">根據預設，SDK 會將記錄寫入儲存體，而且在處理許多訊息時，這項活動可能會降低效能。</span><span class="sxs-lookup"><span data-stu-id="1833c-317">By default, the SDK writes logs to storage, and this activity could degrade performance when you are processing many messages.</span></span> <span data-ttu-id="1833c-318">若要停用記錄，請將儀表板連接字串設定為 null，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="1833c-318">To disable logging, set the dashboard connection string to null as shown in the following example.</span></span>

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

<span data-ttu-id="1833c-319">下列範例示範寫入記錄檔的數種方式：</span><span class="sxs-lookup"><span data-stu-id="1833c-319">The following example shows several ways to write logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="1833c-320">在 WebJobs SDK 儀表板中，當您移到某個特定函式引動過程的頁面並按一下 [切換輸出] 時，就會顯示來自 `TextWriter` 物件的輸出：</span><span class="sxs-lookup"><span data-stu-id="1833c-320">In the WebJobs SDK Dashboard, the output from the `TextWriter` object shows up when you go to the page for a particular function invocation and click **Toggle Output**:</span></span>

![按一下函式引動過程連結](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![函式引動過程頁面中的記錄檔](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="1833c-323">在 WebJobs SDK 儀表板中，當您移到 WebJob (而非函式引動過程) 的頁面並按一下 [切換輸出] 時，則會顯示主控台輸出最近的 100 行。</span><span class="sxs-lookup"><span data-stu-id="1833c-323">In the WebJobs SDK Dashboard, the most recent 100 lines of Console output show up when you go to the page for the WebJob (not for the function invocation) and click **Toggle Output**.</span></span>

![按一下切換輸出](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

<span data-ttu-id="1833c-325">在連續的 WebJob 中，應用程式記錄檔顯示在 Web 應用程式檔案系統中的 /data/jobs/continuous/*{webjobname}*/job_log.txt。</span><span class="sxs-lookup"><span data-stu-id="1833c-325">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in the web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="1833c-326">在 Azure Blob 中，應用程式記錄檔看起來如下所示：2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span><span class="sxs-lookup"><span data-stu-id="1833c-326">In an Azure blob the application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="1833c-327">而在 Azure 資料表中，`Console.Out` 和 `Console.Error` 記錄檔看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="1833c-327">And in an Azure table the `Console.Out` and `Console.Error` logs look like this:</span></span>

![在資料表中的資訊記錄檔](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![在資料表中的錯誤記錄檔](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

<span data-ttu-id="1833c-330">如果您想要插入自己的記錄器，請參閱 [這個範例](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs)。</span><span class="sxs-lookup"><span data-stu-id="1833c-330">If you want to plug in your own logger, see [this example](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span></span>

## <span data-ttu-id="1833c-331"><a id="errors"></a>如何處理錯誤及設定逾時</span><span class="sxs-lookup"><span data-stu-id="1833c-331"><a id="errors"></a>How to handle errors and configure timeouts</span></span>
<span data-ttu-id="1833c-332">WebJobs SDK 也包含 [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) 屬性，您可以使用此屬性讓函式在未於指定的時間長度內完成時取消執行。</span><span class="sxs-lookup"><span data-stu-id="1833c-332">The WebJobs SDK also includes a [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) attribute that you can use to cause a function to be canceled if doesn't complete within a specified amount of time.</span></span> <span data-ttu-id="1833c-333">而如果您想要在於一段指定的時間內有太多錯誤發生時引發警示，則可以使用 `ErrorTrigger` 屬性。</span><span class="sxs-lookup"><span data-stu-id="1833c-333">And if you want to raise an alert when too many errors happen within a specified period of time, you can use the `ErrorTrigger` attribute.</span></span> <span data-ttu-id="1833c-334">以下是一個 [ErrorTrigger 範例](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring)。</span><span class="sxs-lookup"><span data-stu-id="1833c-334">Here is an [ErrorTrigger example](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span></span>

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    To = "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors to the Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

<span data-ttu-id="1833c-335">您也可以藉由使用組態參數 (可以是應用程式設定或環境變數名稱)，動態停用和啟用函式來控制是否可以觸發這些函式。</span><span class="sxs-lookup"><span data-stu-id="1833c-335">You can also dynamically disable and enable functions to control whether they can be triggered, by using a configuration switch that could be an app setting or environment variable name.</span></span> <span data-ttu-id="1833c-336">如需範例程式碼，請參閱 [WebJobs SDK 範例儲存機制](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs)中的 `Disable` 屬性。</span><span class="sxs-lookup"><span data-stu-id="1833c-336">For sample code, see the `Disable` attribute in [the WebJobs SDK samples repository](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span></span>

## <span data-ttu-id="1833c-337"><a id="nextsteps"></a> 後續步驟</span><span class="sxs-lookup"><span data-stu-id="1833c-337"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="1833c-338">本指南提供的程式碼範例示範如何處理使用 Azure 佇列的常見案例。</span><span class="sxs-lookup"><span data-stu-id="1833c-338">This guide has provided code samples that show how to handle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="1833c-339">如需 Azure WebJobs 和 WebJobs SDK 的詳細資訊，請參閱 [Azure WebJobs 建議使用的資源](http://go.microsoft.com/fwlink/?linkid=390226)。</span><span class="sxs-lookup"><span data-stu-id="1833c-339">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>
