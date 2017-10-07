---
title: "aaaHow toouse 以 hello WebJobs SDK 的 Azure blob 儲存體"
description: "了解如何 toouse Azure blob 儲存體與 hello WebJobs SDK。 在容器中出現新的 Blob 時觸發程序並處理「有害 Blob」 。"
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.assetid: bf32f919-f7bc-4aaa-916e-461c02f2e26c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: b34ea8cffee7c0475641886150dee521130a3132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="45298-104">如何 toouse Azure blob 儲存體與 hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="45298-104">How toouse Azure blob storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="45298-105">概觀</span><span class="sxs-lookup"><span data-stu-id="45298-105">Overview</span></span>
<span data-ttu-id="45298-106">本指南提供 C# 程式碼範例會顯示如何 tootrigger 處理程序時建立或更新 Azure blob。</span><span class="sxs-lookup"><span data-stu-id="45298-106">This guide provides C# code samples that show how tootrigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="45298-107">hello 程式碼範例使用[WebJobs SDK](websites-dotnet-webjobs-sdk.md)版本 1.x。</span><span class="sxs-lookup"><span data-stu-id="45298-107">hello code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="45298-108">如需顯示 toocreate 的 blob 的程式碼範例，請參閱[如何 toouse Azure 佇列儲存體與 hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="45298-108">For code samples that show how toocreate blobs, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="45298-109">hello 指南假設您知道[toocreate WebJob 專案在 Visual Studio 中使用連接字串該點 tooyour 儲存體帳戶的方式](websites-dotnet-webjobs-sdk-get-started.md)或太[多個儲存體帳戶](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs)。</span><span class="sxs-lookup"><span data-stu-id="45298-109">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

## <span data-ttu-id="45298-110"><a id="trigger"></a>如何 tootrigger 時建立或更新 blob 的函式</span><span class="sxs-lookup"><span data-stu-id="45298-110"><a id="trigger"></a> How tootrigger a function when a blob is created or updated</span></span>
<span data-ttu-id="45298-111">此區段會顯示如何 toouse hello`BlobTrigger`屬性。</span><span class="sxs-lookup"><span data-stu-id="45298-111">This section shows how toouse hello `BlobTrigger` attribute.</span></span> 

> [!NOTE]
> <span data-ttu-id="45298-112">hello WebJobs SDK 掃描記錄檔 toowatch 的新增或變更的 blob。</span><span class="sxs-lookup"><span data-stu-id="45298-112">hello WebJobs SDK scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="45298-113">此程序不是即時;函式可能不會觸發直到幾分鐘的時間或更久之後建立 hello 的 blob。</span><span class="sxs-lookup"><span data-stu-id="45298-113">This process is not real-time; a function might not get triggered until several minutes or longer after hello blob is created.</span></span> <span data-ttu-id="45298-114">此外， [儲存體記錄檔建立在「竭盡所能」](https://msdn.microsoft.com/library/azure/hh343262.aspx) 的基礎上；並不保證會擷取所有事件。</span><span class="sxs-lookup"><span data-stu-id="45298-114">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; there is no guarantee that all events will be captured.</span></span> <span data-ttu-id="45298-115">在某些情況下可能會遺失記錄檔。</span><span class="sxs-lookup"><span data-stu-id="45298-115">Under some conditions, logs might be missed.</span></span> <span data-ttu-id="45298-116">如果 hello blob 觸發程序的速度和可靠性限制不適用於您的應用程式，hello 建議的方法是 toocreate 佇列訊息，當您建立 hello blob，並使用 hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger)屬性，而非hello`BlobTrigger`處理 hello blob 的 hello 函式上的屬性。</span><span class="sxs-lookup"><span data-stu-id="45298-116">If hello speed and reliability limitations of blob triggers are not acceptable for your application, hello recommended method is toocreate a queue message when you create hello blob, and use hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of hello `BlobTrigger` attribute on hello function that processes hello blob.</span></span>
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="45298-117">適用於含有副檔名之 Blob 名稱的單一預留位置</span><span class="sxs-lookup"><span data-stu-id="45298-117">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="45298-118">hello 下列程式碼範例顯示的文字 blob 中複製 hello*輸入*容器 toohello*輸出*容器：</span><span class="sxs-lookup"><span data-stu-id="45298-118">hello following code sample copies text blobs that appear in hello *input* container toohello *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="45298-119">hello 屬性建構函式接受字串參數，指定 hello 容器名稱和 hello blob 名稱的預留位置。</span><span class="sxs-lookup"><span data-stu-id="45298-119">hello attribute constructor takes a string parameter that specifies hello container name and a placeholder for hello blob name.</span></span> <span data-ttu-id="45298-120">在此範例中，如果 blob 名稱*Blob1.txt*會建立在 hello*輸入*容器，hello 函式會建立名為 blob *Blob1.txt*在 hello*輸出*容器。</span><span class="sxs-lookup"><span data-stu-id="45298-120">In this example, if a blob named *Blob1.txt* is created in hello *input* container, hello function creates a blob named *Blob1.txt* in hello *output* container.</span></span> 

<span data-ttu-id="45298-121">Hello，下列程式碼範例所示，您可以指定 hello blob 名稱的預留位置，以名稱模式：</span><span class="sxs-lookup"><span data-stu-id="45298-121">You can specify a name pattern with hello blob name placeholder, as shown in hello following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="45298-122">此程式碼只會複製以 "original-" 做為名稱開頭的 Blob。</span><span class="sxs-lookup"><span data-stu-id="45298-122">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="45298-123">例如，*原始 Blob1.txt*在 hello*輸入*太複製容器*複製 Blob1.txt*在 hello*輸出*容器。</span><span class="sxs-lookup"><span data-stu-id="45298-123">For example, *original-Blob1.txt* in hello *input* container is copied too*copy-Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="45298-124">如果您需要 toospecify 名稱模式的 blob 名稱 hello 名稱中有大括號時，請按兩下 hello 大括號。</span><span class="sxs-lookup"><span data-stu-id="45298-124">If you need toospecify a name pattern for blob names that have curly braces in hello name, double hello curly braces.</span></span> <span data-ttu-id="45298-125">例如，如果您想要在 hello toofind blob*映像*容器名稱如下：</span><span class="sxs-lookup"><span data-stu-id="45298-125">For example, if you want toofind blobs in hello *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="45298-126">針對您的模式使用下一行程式碼：</span><span class="sxs-lookup"><span data-stu-id="45298-126">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="45298-127">在 hello 範例 hello*名稱*預留位置的值會是*soundfile.mp3*。</span><span class="sxs-lookup"><span data-stu-id="45298-127">In hello example, hello *name* placeholder value would be *soundfile.mp3*.</span></span> 

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="45298-128">個別的 Blob 名稱和副檔名預留位置</span><span class="sxs-lookup"><span data-stu-id="45298-128">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="45298-129">hello 下列程式碼範例會變更 hello 副檔名為複製 blob 出現在 hello*輸入*容器 toohello*輸出*容器。</span><span class="sxs-lookup"><span data-stu-id="45298-129">hello following code sample changes hello file extension as it copies blobs that appear in hello *input* container toohello *output* container.</span></span> <span data-ttu-id="45298-130">hello 程式碼會記錄 hello 延伸模組的 hello*輸入*blob 和設定 hello 延伸模組的 hello*輸出*太 blob*.txt*。</span><span class="sxs-lookup"><span data-stu-id="45298-130">hello code logs hello extension of hello *input* blob and sets hello extension of hello *output* blob too*.txt*.</span></span>

        public static void CopyBlobToTxtFile([BlobTrigger("input/{name}.{ext}")] TextReader input,
            [Blob("output/{name}.txt")] out string output,
            string name,
            string ext,
            TextWriter logger)
        {
            logger.WriteLine("Blob name:" + name);
            logger.WriteLine("Blob extension:" + ext);
            output = input.ReadToEnd();
        }

## <span data-ttu-id="45298-131"><a id="types"></a>您可以繫結 tooblobs 類型</span><span class="sxs-lookup"><span data-stu-id="45298-131"><a id="types"></a> Types that you can bind tooblobs</span></span>
<span data-ttu-id="45298-132">您可以使用 hello `BlobTrigger` hello 下列類型的屬性：</span><span class="sxs-lookup"><span data-stu-id="45298-132">You can use hello `BlobTrigger` attribute on hello following types:</span></span>

* `string`
* `TextReader`
* `Stream`
* `ICloudBlob`
* `CloudBlockBlob`
* `CloudPageBlob`
* `CloudBlobContainer`
* `CloudBlobDirectory`
* `IEnumerable<CloudBlockBlob>`
* `IEnumerable<CloudPageBlob>`
* <span data-ttu-id="45298-133">透過 [ICloudBlobStreamBinder](#icbsb)</span><span class="sxs-lookup"><span data-stu-id="45298-133">Other types deserialized by [ICloudBlobStreamBinder](#icbsb)</span></span> 

<span data-ttu-id="45298-134">如果您想 toowork 直接與 hello Azure 儲存體帳戶，您也可以加入`CloudStorageAccount`參數 toohello 方法簽章。</span><span class="sxs-lookup"><span data-stu-id="45298-134">If you want toowork directly with hello Azure storage account, you can also add a `CloudStorageAccount` parameter toohello method signature.</span></span>

<span data-ttu-id="45298-135">如需範例，請參閱 hello [blob 上 GitHub.com hello azure-webjobs-sdk 儲存機制中的繫結程式碼](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs)。</span><span class="sxs-lookup"><span data-stu-id="45298-135">For examples, see hello [blob binding code in hello azure-webjobs-sdk repository on GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span></span>

## <span data-ttu-id="45298-136"><a id="string"></a>取得繫結 toostring 文字 blob 內容</span><span class="sxs-lookup"><span data-stu-id="45298-136"><a id="string"></a> Getting text blob content by binding toostring</span></span>
<span data-ttu-id="45298-137">如果預期文字 blob，`BlobTrigger`可以套用的 tooa`string`參數。</span><span class="sxs-lookup"><span data-stu-id="45298-137">If text blobs are expected, `BlobTrigger` can be applied tooa `string` parameter.</span></span> <span data-ttu-id="45298-138">hello 下列程式碼範例會將繫結文字 blob tooa`string`參數名為`logMessage`。</span><span class="sxs-lookup"><span data-stu-id="45298-138">hello following code sample binds a text blob tooa `string` parameter named `logMessage`.</span></span> <span data-ttu-id="45298-139">hello 函式會使用該參數 toowrite hello 的內容 hello blob toohello WebJobs SDK 儀表板。</span><span class="sxs-lookup"><span data-stu-id="45298-139">hello function uses that parameter toowrite hello contents of hello blob toohello WebJobs SDK dashboard.</span></span> 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <span data-ttu-id="45298-140"><a id="icbsb"></a> 使用 ICloudBlobStreamBinder 來取得序列化的 Blob 內容</span><span class="sxs-lookup"><span data-stu-id="45298-140"><a id="icbsb"></a> Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="45298-141">hello 下列程式碼範例會使用類別可實作`ICloudBlobStreamBinder`tooenable hello`BlobTrigger`屬性 toobind blob toohello`WebImage`型別。</span><span class="sxs-lookup"><span data-stu-id="45298-141">hello following code sample uses a class that implements `ICloudBlobStreamBinder` tooenable hello `BlobTrigger` attribute toobind a blob toohello `WebImage` type.</span></span>

        public static void WaterMark(
            [BlobTrigger("images3/{name}")] WebImage input,
            [Blob("images3-watermarked/{name}")] out WebImage output)
        {
            output = input.AddTextWatermark("WebJobs SDK", 
                horizontalAlign: "Center", verticalAlign: "Middle",
                fontSize: 48, opacity: 50);
        }
        public static void Resize(
            [BlobTrigger("images3-watermarked/{name}")] WebImage input,
            [Blob("images3-resized/{name}")] out WebImage output)
        {
            var width = 180;
            var height = Convert.ToInt32(input.Height * 180 / input.Width);
            output = input.Resize(width, height);
        }

<span data-ttu-id="45298-142">hello`WebImage`繫結程式碼中提供`WebImageBinder`類別衍生自`ICloudBlobStreamBinder`。</span><span class="sxs-lookup"><span data-stu-id="45298-142">hello `WebImage` binding code is provided in a `WebImageBinder` class that derives from `ICloudBlobStreamBinder`.</span></span>

        public class WebImageBinder : ICloudBlobStreamBinder<WebImage>
        {
            public Task<WebImage> ReadFromStreamAsync(Stream input, 
                System.Threading.CancellationToken cancellationToken)
            {
                return Task.FromResult<WebImage>(new WebImage(input));
            }
            public Task WriteToStreamAsync(WebImage value, Stream output,
                System.Threading.CancellationToken cancellationToken)
            {
                var bytes = value.GetBytes();
                return output.WriteAsync(bytes, 0, bytes.Length, cancellationToken);
            }
        }

## <a name="getting-hello-blob-path-for-hello-triggering-blob"></a><span data-ttu-id="45298-143">取得觸發 blob hello hello blob 路徑</span><span class="sxs-lookup"><span data-stu-id="45298-143">Getting hello blob path for hello triggering blob</span></span>
<span data-ttu-id="45298-144">tooget hello 容器名稱和 blob 名稱的 hello blob 的已觸發 hello 函式，包括`blobTrigger`字串 hello 函式簽章中的參數。</span><span class="sxs-lookup"><span data-stu-id="45298-144">tooget hello container name and blob name of hello blob that has triggered hello function, include a `blobTrigger` string parameter in hello function signature.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <span data-ttu-id="45298-145"><a id="poison"></a>Toohandle 有害的 blob</span><span class="sxs-lookup"><span data-stu-id="45298-145"><a id="poison"></a> How toohandle poison blobs</span></span>
<span data-ttu-id="45298-146">當`BlobTrigger`函式失敗，hello SDK 呼叫它一次，以防 hello 失敗由暫時性錯誤所造成。</span><span class="sxs-lookup"><span data-stu-id="45298-146">When a `BlobTrigger` function fails, hello SDK calls it again, in case hello failure was caused by a transient error.</span></span> <span data-ttu-id="45298-147">如果 hello 失敗因為 hello 的 hello blob 的內容，hello 函式會失敗，每次嘗試 tooprocess hello blob。</span><span class="sxs-lookup"><span data-stu-id="45298-147">If hello failure is caused by hello content of hello blob, hello function fails every time it tries tooprocess hello blob.</span></span> <span data-ttu-id="45298-148">根據預設，hello SDK 會呼叫 too5 時間的函式，針對指定的 blob。</span><span class="sxs-lookup"><span data-stu-id="45298-148">By default, hello SDK calls a function up too5 times for a given blob.</span></span> <span data-ttu-id="45298-149">Hello SDK 如果 hello 第五個再試一次失敗時，加入名為訊息 tooa 佇列*webjobs-blobtrigger-有害*。</span><span class="sxs-lookup"><span data-stu-id="45298-149">If hello fifth try fails, hello SDK adds a message tooa queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="45298-150">hello 重試次數上限是可設定的。</span><span class="sxs-lookup"><span data-stu-id="45298-150">hello maximum number of retries is configurable.</span></span> <span data-ttu-id="45298-151">hello 相同[MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue)設定用於有害的 blob 處理和有害佇列訊息處理。</span><span class="sxs-lookup"><span data-stu-id="45298-151">hello same [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span> 

<span data-ttu-id="45298-152">hello 佇列訊息的有害的 blob 是 JSON 物件，包含下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="45298-152">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="45298-153">FunctionId (hello 格式*{web 工作名稱}*。函式。*{函式名稱}*，例如： WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="45298-153">FunctionId (in hello format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="45298-154">BlobType ("BlockBlob" 或 "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="45298-154">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="45298-155">ContainerName</span><span class="sxs-lookup"><span data-stu-id="45298-155">ContainerName</span></span>
* <span data-ttu-id="45298-156">BlobName</span><span class="sxs-lookup"><span data-stu-id="45298-156">BlobName</span></span>
* <span data-ttu-id="45298-157">ETag (Blob 版本識別碼，例如："0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="45298-157">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="45298-158">在 hello 下列程式碼範例，hello`CopyBlob`函式有造成 toofail 每次呼叫時的程式碼。</span><span class="sxs-lookup"><span data-stu-id="45298-158">In hello following code sample, hello `CopyBlob` function has code that causes it toofail every time it's called.</span></span> <span data-ttu-id="45298-159">Hello SDK 呼叫它的 hello 重試次數上限，訊息會建立 hello blob 有害佇列，而且 hello 處理該訊息之後`LogPoisonBlob`函式。</span><span class="sxs-lookup"><span data-stu-id="45298-159">After hello SDK calls it for hello maximum number of retries, a message is created on hello poison blob queue, and that message is processed by hello `LogPoisonBlob` function.</span></span> 

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("textblobs/output-{name}")] out string output)
        {
            throw new Exception("Exception for testing poison blob handling");
            output = input.ReadToEnd();
        }

        public static void LogPoisonBlob(
        [QueueTrigger("webjobs-blobtrigger-poison")] PoisonBlobMessage message,
            TextWriter logger)
        {
            logger.WriteLine("FunctionId: {0}", message.FunctionId);
            logger.WriteLine("BlobType: {0}", message.BlobType);
            logger.WriteLine("ContainerName: {0}", message.ContainerName);
            logger.WriteLine("BlobName: {0}", message.BlobName);
            logger.WriteLine("ETag: {0}", message.ETag);
        }

<span data-ttu-id="45298-160">hello SDK 自動還原序列化 hello JSON 訊息。</span><span class="sxs-lookup"><span data-stu-id="45298-160">hello SDK automatically deserializes hello JSON message.</span></span> <span data-ttu-id="45298-161">以下是 hello`PoisonBlobMessage`類別：</span><span class="sxs-lookup"><span data-stu-id="45298-161">Here is hello `PoisonBlobMessage` class:</span></span> 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <span data-ttu-id="45298-162"><a id="polling"></a> Blob 輪詢演算法</span><span class="sxs-lookup"><span data-stu-id="45298-162"><a id="polling"></a> Blob polling algorithm</span></span>
<span data-ttu-id="45298-163">hello WebJobs SDK 會掃描所指定的所有容器`BlobTrigger`於應用程式啟動的屬性。</span><span class="sxs-lookup"><span data-stu-id="45298-163">hello WebJobs SDK scans all containers specified by `BlobTrigger` attributes at application start.</span></span> <span data-ttu-id="45298-164">在大型儲存體帳戶中，這個掃描需要花費一些時間，因此，可能需要一段時間才能找到新的 Blob 以及執行 `BlobTrigger` 函數。</span><span class="sxs-lookup"><span data-stu-id="45298-164">In a large storage account this scan can take some time, so it might be a while before new blobs are found and `BlobTrigger` functions are executed.</span></span>

<span data-ttu-id="45298-165">toodetect 新增或變更 blob 應用程式啟動之後，hello SDK 定期從 hello blob 儲存體讀取記錄。</span><span class="sxs-lookup"><span data-stu-id="45298-165">toodetect new or changed blobs after application start, hello SDK periodically reads from hello blob storage logs.</span></span> <span data-ttu-id="45298-166">或 hello blob 記錄檔會進行緩衝處理，只取得實際寫入每隔 10 分鐘，因此可能有明顯的延遲後建立或更新之前 hello 對應 blob`BlobTrigger`函式會執行。</span><span class="sxs-lookup"><span data-stu-id="45298-166">hello blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before hello corresponding `BlobTrigger` function executes.</span></span> 

<span data-ttu-id="45298-167">發生例外狀況的 blob，您使用建立的 hello`Blob`屬性。</span><span class="sxs-lookup"><span data-stu-id="45298-167">There is an exception for blobs that you create by using hello `Blob` attribute.</span></span> <span data-ttu-id="45298-168">當 hello WebJobs SDK 建立新的 blob 時，它會立即傳 hello 新 blob tooany 比對`BlobTrigger`函式。</span><span class="sxs-lookup"><span data-stu-id="45298-168">When hello WebJobs SDK creates a new blob, it passes hello new blob immediately tooany matching `BlobTrigger` functions.</span></span> <span data-ttu-id="45298-169">因此如果您有 blob 輸入和輸出的鏈結，hello SDK 可以處理這些有效率。</span><span class="sxs-lookup"><span data-stu-id="45298-169">Therefore if you have a chain of blob inputs and outputs, hello SDK can process them efficiently.</span></span> <span data-ttu-id="45298-170">但是，如果您想要降低在針對透過其他方法建立或更新的 Blob 執行 Blob 處理函數時的延遲，建議使用 `QueueTrigger` 而非 `BlobTrigger`。</span><span class="sxs-lookup"><span data-stu-id="45298-170">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using `QueueTrigger` rather than `BlobTrigger`.</span></span>

### <span data-ttu-id="45298-171"><a id="receipts"></a> Blob 回條</span><span class="sxs-lookup"><span data-stu-id="45298-171"><a id="receipts"></a> Blob receipts</span></span>
<span data-ttu-id="45298-172">hello WebJobs SDK 可確保沒有`BlobTrigger`函式會呼叫一次以上 hello 相同新增或更新 blob。</span><span class="sxs-lookup"><span data-stu-id="45298-172">hello WebJobs SDK makes sure that no `BlobTrigger` function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="45298-173">其做法是維護*blob 回條*順序 toodetermine 如果已處理指定的 blob 版本中。</span><span class="sxs-lookup"><span data-stu-id="45298-173">It does this by maintaining *blob receipts* in order toodetermine if a given blob version has been processed.</span></span>

<span data-ttu-id="45298-174">Blob 的回條會儲存在名為容器*azure webjobs 託管*hello hello AzureWebJobsStorage 連接字串所指定的 Azure 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="45298-174">Blob receipts are stored in a container named *azure-webjobs-hosts* in hello Azure storage account specified by hello AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="45298-175">Blob 的回條具有 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="45298-175">A blob receipt has hello following  information:</span></span>

* <span data-ttu-id="45298-176">hello hello blob 所呼叫函式 (「*{web 工作名稱}*。函式。*{函式名稱}*"，例如:"WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="45298-176">hello function that was called for hello blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="45298-177">hello 容器名稱</span><span class="sxs-lookup"><span data-stu-id="45298-177">hello container name</span></span>
* <span data-ttu-id="45298-178">hello blob 類型 （"BlockBlob"或"PageBlob"）</span><span class="sxs-lookup"><span data-stu-id="45298-178">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="45298-179">hello blob 名稱</span><span class="sxs-lookup"><span data-stu-id="45298-179">hello blob name</span></span>
* <span data-ttu-id="45298-180">hello ETag (例如 blob 版本識別碼:"0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="45298-180">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="45298-181">如果您想 tooforce 重新處理的 blob，您可以手動刪除該 blob 的 hello blob 回條 hello *azure webjobs 託管*容器。</span><span class="sxs-lookup"><span data-stu-id="45298-181">If you want tooforce reprocessing of a blob, you can manually delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container.</span></span>

## <span data-ttu-id="45298-182"><a id="queues"></a>Hello 佇列文章所涵蓋的相關的主題</span><span class="sxs-lookup"><span data-stu-id="45298-182"><a id="queues"></a>Related topics covered by hello queues article</span></span>
<span data-ttu-id="45298-183">如需如何 toohandle blob 處理觸發佇列訊息，或 WebJobs SDK 案例不特定 tooblob 處理，請參閱[如何 toouse Azure 佇列儲存體與 hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="45298-183">For information about how toohandle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific tooblob processing, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="45298-184">在該文件中涵蓋的相關的主題 hello 如下：</span><span class="sxs-lookup"><span data-stu-id="45298-184">Related topics covered in that article include hello following:</span></span>

* <span data-ttu-id="45298-185">Async 函數</span><span class="sxs-lookup"><span data-stu-id="45298-185">Async functions</span></span>
* <span data-ttu-id="45298-186">多個執行個體</span><span class="sxs-lookup"><span data-stu-id="45298-186">Multiple instances</span></span>
* <span data-ttu-id="45298-187">正常關機</span><span class="sxs-lookup"><span data-stu-id="45298-187">Graceful shutdown</span></span>
* <span data-ttu-id="45298-188">使用 WebJobs SDK hello 函式主體中的屬性</span><span class="sxs-lookup"><span data-stu-id="45298-188">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="45298-189">程式碼中設定 hello SDK 連接字串。</span><span class="sxs-lookup"><span data-stu-id="45298-189">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="45298-190">在程式碼中設定 WebJobs SDK 建構函式參數的值</span><span class="sxs-lookup"><span data-stu-id="45298-190">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="45298-191">設定 `MaxDequeueCount` 來處理有害的 Blob。</span><span class="sxs-lookup"><span data-stu-id="45298-191">Configure `MaxDequeueCount` for poison blob handling.</span></span>
* <span data-ttu-id="45298-192">手動觸發函式</span><span class="sxs-lookup"><span data-stu-id="45298-192">Trigger a function manually</span></span>
* <span data-ttu-id="45298-193">寫入記錄檔</span><span class="sxs-lookup"><span data-stu-id="45298-193">Write logs</span></span>

## <span data-ttu-id="45298-194"><a id="nextsteps"></a> 後續步驟</span><span class="sxs-lookup"><span data-stu-id="45298-194"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="45298-195">本指南提供的程式碼範例，顯示 toohandle 常見的案例來處理 Azure 的 blob。</span><span class="sxs-lookup"><span data-stu-id="45298-195">This guide has provided code samples that show how toohandle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="45298-196">如需有關如何 toouse Azure WebJobs 和 hello WebJobs SDK，請參閱[Azure WebJobs 建議資源](http://go.microsoft.com/fwlink/?linkid=390226)。</span><span class="sxs-lookup"><span data-stu-id="45298-196">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

