---
title: "開始使用 Blob 儲存體和 Visual Studio 已連接服務 (WebJob 專案) | Microsoft Docs"
description: "在使用 Visual Studio 已連接服務連接至 Azure 儲存體之後，如何於 WebJob 專案中開始使用 Blob 儲存體。"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 324c9376-0225-4092-9825-5d1bd5550058
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: a50a265feff8c0aec28825eb0bc4e33585ea5a02
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="68da7-103">開始使用 Azure Blob 儲存體和 Visual Studio 已連接服務 (WebJob 專案)</span><span class="sxs-lookup"><span data-stu-id="68da7-103">Get started with Azure Blob storage and Visual Studio connected services (WebJob projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="68da7-104">概觀</span><span class="sxs-lookup"><span data-stu-id="68da7-104">Overview</span></span>
<span data-ttu-id="68da7-105">本文提供 C# 程式碼範例，示範如何在建立或更新 Azure Blob 時觸發程序。</span><span class="sxs-lookup"><span data-stu-id="68da7-105">This article provides C# code samples that show how to trigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="68da7-106">此程式碼範例會使用 [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) 1.x 版。</span><span class="sxs-lookup"><span data-stu-id="68da7-106">The code samples use the [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span> <span data-ttu-id="68da7-107">當您使用 Visual Studio [加入連接的服務]  對話方塊將儲存體帳戶加入 WebJob 專案時，適當的 Azure 儲存體 NuGet 套件會隨即安裝、適當的 .NET 參考會隨即加入專案中，而儲存體帳戶的連接字串也會隨即在 App.config 檔案中更新。</span><span class="sxs-lookup"><span data-stu-id="68da7-107">When you add a storage account to a WebJob project by using the Visual Studio **Add Connected Services** dialog, the appropriate Azure Storage NuGet package is installed, the appropriate .NET references are added to the project, and connection strings for the storage account are updated in the App.config file.</span></span>

## <a name="how-to-trigger-a-function-when-a-blob-is-created-or-updated"></a><span data-ttu-id="68da7-108">如何在建立或更新 Blob 時觸發函數</span><span class="sxs-lookup"><span data-stu-id="68da7-108">How to trigger a function when a blob is created or updated</span></span>
<span data-ttu-id="68da7-109">本節示範如何使用 **BlobTrigger** 屬性。</span><span class="sxs-lookup"><span data-stu-id="68da7-109">This section shows how to use the **BlobTrigger** attribute.</span></span>

 <span data-ttu-id="68da7-110">**附註：** WebJobs SDK 會掃描要監看的的記錄檔，找出新的或變更的 Blob。</span><span class="sxs-lookup"><span data-stu-id="68da7-110">**Note:** The WebJobs SDK scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="68da7-111">此程序的速度原本就很慢；可能直到建立 Blob 之後數分鐘或更久，才會觸發函數。</span><span class="sxs-lookup"><span data-stu-id="68da7-111">This process is inherently slow; a function might not get triggered until several minutes or longer after the blob is created.</span></span>  <span data-ttu-id="68da7-112">如果您的應用程式需要立即處理 Blob，建議的方法是在您建立 Blob 時建立佇列訊息，並在處理 Blob 的函數上使用 [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) 屬性，而不是 **BlobTrigger** 屬性。</span><span class="sxs-lookup"><span data-stu-id="68da7-112">If your application needs to process blobs immediately, the recommended method is to create a queue message when you create the blob, and use the [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of the **BlobTrigger** attribute on the function that processes the blob.</span></span>

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="68da7-113">適用於含有副檔名之 Blob 名稱的單一預留位置</span><span class="sxs-lookup"><span data-stu-id="68da7-113">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="68da7-114">下列程式碼範例會將出現在 *input* 容器中的文字 Blob 複製到 *output* 容器：</span><span class="sxs-lookup"><span data-stu-id="68da7-114">The following code sample copies text blobs that appear in the *input* container to the *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="68da7-115">屬性建構函式會接受字串參數，以指定容器名稱和 Blob 名稱的預留位置。</span><span class="sxs-lookup"><span data-stu-id="68da7-115">The attribute constructor takes a string parameter that specifies the container name and a placeholder for the blob name.</span></span> <span data-ttu-id="68da7-116">在此範例中，如果已在 *input* 容器中建立名為 *Blob1.txt* 的 Blob，此函數便會在 *output* 容器中建立名為 *Blob1.txt* 的 Blob。</span><span class="sxs-lookup"><span data-stu-id="68da7-116">In this example, if a blob named *Blob1.txt* is created in the *input* container, the function creates a blob named *Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="68da7-117">您可以使用 Blob 名稱預留位置來指定名稱模式，如下列程式碼範例所示：</span><span class="sxs-lookup"><span data-stu-id="68da7-117">You can specify a name pattern with the blob name placeholder, as shown in the following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="68da7-118">此程式碼只會複製以 "original-" 做為名稱開頭的 Blob。</span><span class="sxs-lookup"><span data-stu-id="68da7-118">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="68da7-119">例如，*input* 容器中的*original-Blob1.txt* 會複製到 *output* 容器中的 *copy-Blob1.txt*。</span><span class="sxs-lookup"><span data-stu-id="68da7-119">For example, *original-Blob1.txt* in the *input* container is copied to *copy-Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="68da7-120">如果您需要針對名稱中包含大括號的 Blob 名稱指定名稱模式，請按兩下大括號。</span><span class="sxs-lookup"><span data-stu-id="68da7-120">If you need to specify a name pattern for blob names that have curly braces in the name, double the curly braces.</span></span> <span data-ttu-id="68da7-121">例如，如果您想要在 *images* 容器中尋找具備如下名稱的 Blob：</span><span class="sxs-lookup"><span data-stu-id="68da7-121">For example, if you want to find blobs in the *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="68da7-122">針對您的模式使用下一行程式碼：</span><span class="sxs-lookup"><span data-stu-id="68da7-122">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="68da7-123">在此範例中，*name* 預留位置的值會是 *soundfile.mp3*。</span><span class="sxs-lookup"><span data-stu-id="68da7-123">In the example, the *name* placeholder value would be *soundfile.mp3*.</span></span>

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="68da7-124">個別的 Blob 名稱和副檔名預留位置</span><span class="sxs-lookup"><span data-stu-id="68da7-124">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="68da7-125">下列程式碼範例會在將出現於 *input* 容器中的 Blob 複製到 *output* 容器時變更副檔名。</span><span class="sxs-lookup"><span data-stu-id="68da7-125">The following code sample changes the file extension as it copies blobs that appear in the *input* container to the *output* container.</span></span> <span data-ttu-id="68da7-126">此程式碼會記錄 *input* Blob 的副檔名，並將 *output* Blob 的副檔名設為 *.txt*。</span><span class="sxs-lookup"><span data-stu-id="68da7-126">The code logs the extension of the *input* blob and sets the extension of the *output* blob to *.txt*.</span></span>

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

## <a name="types-that-you-can-bind-to-blobs"></a><span data-ttu-id="68da7-127">您可以繫結至 Blob 的類型</span><span class="sxs-lookup"><span data-stu-id="68da7-127">Types that you can bind to blobs</span></span>
<span data-ttu-id="68da7-128">您可將 **BlobTrigger** 屬性用於下列類型：</span><span class="sxs-lookup"><span data-stu-id="68da7-128">You can use the **BlobTrigger** attribute on the following types:</span></span>

* <span data-ttu-id="68da7-129">**字串**</span><span class="sxs-lookup"><span data-stu-id="68da7-129">**string**</span></span>
* <span data-ttu-id="68da7-130">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="68da7-130">**TextReader**</span></span>
* <span data-ttu-id="68da7-131">**Stream**</span><span class="sxs-lookup"><span data-stu-id="68da7-131">**Stream**</span></span>
* <span data-ttu-id="68da7-132">**ICloudBlob**</span><span class="sxs-lookup"><span data-stu-id="68da7-132">**ICloudBlob**</span></span>
* <span data-ttu-id="68da7-133">**CloudBlockBlob**</span><span class="sxs-lookup"><span data-stu-id="68da7-133">**CloudBlockBlob**</span></span>
* <span data-ttu-id="68da7-134">**CloudPageBlob**</span><span class="sxs-lookup"><span data-stu-id="68da7-134">**CloudPageBlob**</span></span>
* <span data-ttu-id="68da7-135">透過 [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span><span class="sxs-lookup"><span data-stu-id="68da7-135">Other types deserialized by [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span></span>

<span data-ttu-id="68da7-136">如果您想要直接使用 Azure 儲存體帳戶，也可以將 **CloudStorageAccount** 參數新增至方法簽章。</span><span class="sxs-lookup"><span data-stu-id="68da7-136">If you want to work directly with the Azure storage account, you can also add a **CloudStorageAccount** parameter to the method signature.</span></span>

## <a name="getting-text-blob-content-by-binding-to-string"></a><span data-ttu-id="68da7-137">繫結至字串來取得文字 Blob 內容</span><span class="sxs-lookup"><span data-stu-id="68da7-137">Getting text blob content by binding to string</span></span>
<span data-ttu-id="68da7-138">如果預期會取得文字 Blob，就可以將 **BlobTrigger** 套用至 **string** 參數。</span><span class="sxs-lookup"><span data-stu-id="68da7-138">If text blobs are expected, **BlobTrigger** can be applied to a **string** parameter.</span></span> <span data-ttu-id="68da7-139">下列程式碼範例會將文字 Blob 繫結至名為 **logMessage** 的 **string** 參數。</span><span class="sxs-lookup"><span data-stu-id="68da7-139">The following code sample binds a text blob to a **string** parameter named **logMessage**.</span></span> <span data-ttu-id="68da7-140">此函數會使用該參數，將 Blob 的內容寫入 WebJobs SDK 儀表板。</span><span class="sxs-lookup"><span data-stu-id="68da7-140">The function uses that parameter to write the contents of the blob to the WebJobs SDK dashboard.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a><span data-ttu-id="68da7-141">使用 ICloudBlobStreamBinder 來取得序列化的 Blob 內容</span><span class="sxs-lookup"><span data-stu-id="68da7-141">Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="68da7-142">下列程式碼範例會使用實作 **ICloudBlobStreamBinder** 以啟用 **BlobTrigger** 屬性的類別，將 Blob 繫結至 **WebImage** 類型。</span><span class="sxs-lookup"><span data-stu-id="68da7-142">The following code sample uses a class that implements **ICloudBlobStreamBinder** to enable the **BlobTrigger** attribute to bind a blob to the **WebImage** type.</span></span>

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

<span data-ttu-id="68da7-143">衍生自 **ICloudBlobStreamBinder** 的 **WebImageBinder** 類別會提供 **WebImage** 繫結程式碼。</span><span class="sxs-lookup"><span data-stu-id="68da7-143">The **WebImage** binding code is provided in a **WebImageBinder** class that derives from **ICloudBlobStreamBinder**.</span></span>

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

## <a name="how-to-handle-poison-blobs"></a><span data-ttu-id="68da7-144">如何處理有害的 Blob</span><span class="sxs-lookup"><span data-stu-id="68da7-144">How to handle poison blobs</span></span>
<span data-ttu-id="68da7-145">當 **BlobTrigger** 函數失敗時，SDK 會再次加以呼叫，以防失敗是因暫時性錯誤而造成。</span><span class="sxs-lookup"><span data-stu-id="68da7-145">When a **BlobTrigger** function fails, the SDK calls it again, in case the failure was caused by a transient error.</span></span> <span data-ttu-id="68da7-146">如果失敗是因為 Blob 的內容所造成，則此函數會在其每次嘗試處理該 Blob 時失敗。</span><span class="sxs-lookup"><span data-stu-id="68da7-146">If the failure is caused by the content of the blob, the function fails every time it tries to process the blob.</span></span> <span data-ttu-id="68da7-147">根據預設，SDK 最多會針對指定的 Blob 呼叫函數 5 次。</span><span class="sxs-lookup"><span data-stu-id="68da7-147">By default, the SDK calls a function up to 5 times for a given blob.</span></span> <span data-ttu-id="68da7-148">如果第五次嘗試失敗，則 SDK 會在名為 *webjobs-blobtrigger-poison*的佇列中新增一則訊息。</span><span class="sxs-lookup"><span data-stu-id="68da7-148">If the fifth try fails, the SDK adds a message to a queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="68da7-149">您可以設定重試次數上限。</span><span class="sxs-lookup"><span data-stu-id="68da7-149">The maximum number of retries is configurable.</span></span> <span data-ttu-id="68da7-150">相同的 [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) 設定可用於處理有害的 Blob 和處理有害的佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="68da7-150">The same [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span>

<span data-ttu-id="68da7-151">適用於有害 Blob 的佇列訊息是一個 JSON 物件，其中包含下列屬性：</span><span class="sxs-lookup"><span data-stu-id="68da7-151">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="68da7-152">FunctionId (格式為 *{WebJob name}*.Functions.*{Function name}*，例如：WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="68da7-152">FunctionId (in the format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="68da7-153">BlobType ("BlockBlob" 或 "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="68da7-153">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="68da7-154">ContainerName</span><span class="sxs-lookup"><span data-stu-id="68da7-154">ContainerName</span></span>
* <span data-ttu-id="68da7-155">BlobName</span><span class="sxs-lookup"><span data-stu-id="68da7-155">BlobName</span></span>
* <span data-ttu-id="68da7-156">ETag (Blob 版本識別碼，例如："0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="68da7-156">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="68da7-157">在下列程式碼範例中， **CopyBlob** 函數內含會導致每次受呼叫時都失敗的程式碼。</span><span class="sxs-lookup"><span data-stu-id="68da7-157">In the following code sample, the **CopyBlob** function has code that causes it to fail every time it's called.</span></span> <span data-ttu-id="68da7-158">在 SDK 加以呼叫的重試次數達到上限之後，就會在有害的 Blob 佇列中建立訊息，而該訊息會由 **LogPoisonBlob** 函數處理。</span><span class="sxs-lookup"><span data-stu-id="68da7-158">After the SDK calls it for the maximum number of retries, a message is created on the poison blob queue, and that message is processed by the **LogPoisonBlob** function.</span></span>

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

<span data-ttu-id="68da7-159">SDK 會自動將該 JSON 訊息還原序列化。</span><span class="sxs-lookup"><span data-stu-id="68da7-159">The SDK automatically deserializes the JSON message.</span></span> <span data-ttu-id="68da7-160">以下是 **PoisonBlobMessage** 類別：</span><span class="sxs-lookup"><span data-stu-id="68da7-160">Here is the **PoisonBlobMessage** class:</span></span>

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a><span data-ttu-id="68da7-161">Blob 輪詢演算法</span><span class="sxs-lookup"><span data-stu-id="68da7-161">Blob polling algorithm</span></span>
<span data-ttu-id="68da7-162">WebJobs SDK 會在應用程式啟動時，掃描 **BlobTrigger** 屬性所指定的所有容器。</span><span class="sxs-lookup"><span data-stu-id="68da7-162">The WebJobs SDK scans all containers specified by **BlobTrigger** attributes at application start.</span></span> <span data-ttu-id="68da7-163">在大型儲存體帳戶中，這項掃描需要花費一些時間，因此，可能需要一些時間才能找到新的 Blob 以及執行 **BlobTrigger** 函數。</span><span class="sxs-lookup"><span data-stu-id="68da7-163">In a large storage account this scan can take some time, so it might be a while before new blobs are found and **BlobTrigger** functions are executed.</span></span>

<span data-ttu-id="68da7-164">為了在應用程式啟動之後偵測新的或已變更的 Blob，SDK 會定期讀取 Blob 儲存體記錄檔。</span><span class="sxs-lookup"><span data-stu-id="68da7-164">To detect new or changed blobs after application start, the SDK periodically reads from the blob storage logs.</span></span> <span data-ttu-id="68da7-165">Blob 記錄檔會進行緩衝處理，大約每隔 10 分鐘才有實際寫入，因此在建立或更新 Blob 之後可能會有明顯的延遲，然後才執行相對應的 **BlobTrigger** 函數。</span><span class="sxs-lookup"><span data-stu-id="68da7-165">The blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before the corresponding **BlobTrigger** function executes.</span></span>

<span data-ttu-id="68da7-166">您使用 **Blob** 屬性建立的 Blob 有例外狀況。</span><span class="sxs-lookup"><span data-stu-id="68da7-166">There is an exception for blobs that you create by using the **Blob** attribute.</span></span> <span data-ttu-id="68da7-167">當 WebJobs SDK 建立新的 Blob 時，會立即將新的 Blob 傳遞到任何相符的 **BlobTrigger** 函數。</span><span class="sxs-lookup"><span data-stu-id="68da7-167">When the WebJobs SDK creates a new blob, it passes the new blob immediately to any matching **BlobTrigger** functions.</span></span> <span data-ttu-id="68da7-168">因此，如果您具有 Blob 輸入和輸出的鏈結，就能有效率地處理它們。</span><span class="sxs-lookup"><span data-stu-id="68da7-168">Therefore if you have a chain of blob inputs and outputs, the SDK can process them efficiently.</span></span> <span data-ttu-id="68da7-169">但是，如果您想要降低透過其他方法建立或更新的 Blob 執行 Blob 處理函數時的延遲，建議使用 **QueueTrigger** 而非 **BlobTrigger**。</span><span class="sxs-lookup"><span data-stu-id="68da7-169">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using **QueueTrigger** rather than **BlobTrigger**.</span></span>

### <a name="blob-receipts"></a><span data-ttu-id="68da7-170">Blob 回條</span><span class="sxs-lookup"><span data-stu-id="68da7-170">Blob receipts</span></span>
<span data-ttu-id="68da7-171">WebJobs SDK 可確保不會針對相同的新 Blob 或更新的 Blob，多次呼叫 **BlobTrigger** 函數。</span><span class="sxs-lookup"><span data-stu-id="68da7-171">The WebJobs SDK makes sure that no **BlobTrigger** function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="68da7-172">它的運作方式是藉由維護 *Blob 回條* 來判斷指定的 Blob 版本是否已處理過。</span><span class="sxs-lookup"><span data-stu-id="68da7-172">It does this by maintaining *blob receipts* in order to determine if a given blob version has been processed.</span></span>

<span data-ttu-id="68da7-173">Blob 回條儲存於 AzureWebJobsStorage 連接字串所指定之 Azure 儲存體帳戶中名為 *azure-webjobs-hosts* 的容器中。</span><span class="sxs-lookup"><span data-stu-id="68da7-173">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account specified by the AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="68da7-174">Blob 回條具有下列資訊：</span><span class="sxs-lookup"><span data-stu-id="68da7-174">A blob receipt has the following  information:</span></span>

* <span data-ttu-id="68da7-175">已為 Blob 呼叫的函數 ("*{WebJob name}*.Functions.*{Function name}*"，例如："WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="68da7-175">The function that was called for the blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="68da7-176">容器名稱</span><span class="sxs-lookup"><span data-stu-id="68da7-176">The container name</span></span>
* <span data-ttu-id="68da7-177">Blob 類型 ("BlockBlob" 或 "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="68da7-177">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="68da7-178">Blob 名稱</span><span class="sxs-lookup"><span data-stu-id="68da7-178">The blob name</span></span>
* <span data-ttu-id="68da7-179">ETag (Blob 版本識別碼，例如："0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="68da7-179">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="68da7-180">如果您想要強制重新處理某個 Blob，可以從 *azure-webjobs-hosts* 容器中手動刪除該 Blob 的 Blob 回條。</span><span class="sxs-lookup"><span data-stu-id="68da7-180">If you want to force reprocessing of a blob, you can manually delete the blob receipt for that blob from the *azure-webjobs-hosts* container.</span></span>

## <a name="related-topics-covered-by-the-queues-article"></a><span data-ttu-id="68da7-181">佇列文章所涵蓋的相關主題</span><span class="sxs-lookup"><span data-stu-id="68da7-181">Related topics covered by the queues article</span></span>
<span data-ttu-id="68da7-182">如需如何處理佇列訊息所觸發的 Blob 處理的相關資訊，或是非 Blob 處理特有的 WebJobs SDK 案例，請參閱 [如何透過 WebJobs SDK 使用 Azure 佇列儲存體](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="68da7-182">For information about how to handle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific to blob processing, see [How to use Azure queue storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span>

<span data-ttu-id="68da7-183">該文章中涵蓋的相關主題如下：</span><span class="sxs-lookup"><span data-stu-id="68da7-183">Related topics covered in that article include the following:</span></span>

* <span data-ttu-id="68da7-184">Async 函數</span><span class="sxs-lookup"><span data-stu-id="68da7-184">Async functions</span></span>
* <span data-ttu-id="68da7-185">多個執行個體</span><span class="sxs-lookup"><span data-stu-id="68da7-185">Multiple instances</span></span>
* <span data-ttu-id="68da7-186">正常關機</span><span class="sxs-lookup"><span data-stu-id="68da7-186">Graceful shutdown</span></span>
* <span data-ttu-id="68da7-187">在函式主體中使用 WebJobs SDK 屬性</span><span class="sxs-lookup"><span data-stu-id="68da7-187">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="68da7-188">在程式碼中設定 SDK 連接字串。</span><span class="sxs-lookup"><span data-stu-id="68da7-188">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="68da7-189">在程式碼中設定 WebJobs SDK 建構函式參數的值</span><span class="sxs-lookup"><span data-stu-id="68da7-189">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="68da7-190">設定 **MaxDequeueCount** 以處理有害的 Blob。</span><span class="sxs-lookup"><span data-stu-id="68da7-190">Configure **MaxDequeueCount** for poison blob handling.</span></span>
* <span data-ttu-id="68da7-191">手動觸發函式</span><span class="sxs-lookup"><span data-stu-id="68da7-191">Trigger a function manually</span></span>
* <span data-ttu-id="68da7-192">寫入記錄檔</span><span class="sxs-lookup"><span data-stu-id="68da7-192">Write logs</span></span>

## <a name="next-steps"></a><span data-ttu-id="68da7-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="68da7-193">Next steps</span></span>
<span data-ttu-id="68da7-194">本文提供的程式碼範例示範如何處理使用 Azure Blob 的常見案例。</span><span class="sxs-lookup"><span data-stu-id="68da7-194">This article has provided code samples that show how to handle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="68da7-195">如需如何使用 Azure WebJobs 和 WebJobs SDK 的詳細資訊，請參閱 [Azure WebJobs 文件資源](http://go.microsoft.com/fwlink/?linkid=390226)。</span><span class="sxs-lookup"><span data-stu-id="68da7-195">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

