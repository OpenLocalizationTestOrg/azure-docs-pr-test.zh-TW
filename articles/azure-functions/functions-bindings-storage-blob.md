---
title: "aaaAzure 函式的 Blob 儲存體繫結 |Microsoft 文件"
description: "了解觸發 toouse Azure 儲存體的方式，在 Azure 函式中的繫結。"
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函數, 事件處理, 動態運算, 無伺服器架構"
ms.assetid: aba8976c-6568-4ec7-86f5-410efd6b0fb9
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: cef44bd2154d0b97cca9220b6c5024a5b620c80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-blob-storage-bindings"></a><span data-ttu-id="58e00-104">Azure Functions Blob 儲存體繫結</span><span class="sxs-lookup"><span data-stu-id="58e00-104">Azure Functions Blob storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="58e00-105">這篇文章說明如何 tooconfigure 地使用 Azure 功能中的 Azure Blob 儲存體繫結。</span><span class="sxs-lookup"><span data-stu-id="58e00-105">This article explains how tooconfigure and work with Azure Blob storage bindings in Azure Functions.</span></span> <span data-ttu-id="58e00-106">Azure Functions 支援適用於 Azure Blob 儲存體的觸發程序、輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="58e00-106">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="58e00-107">如需所有繫結中可用的功能，請參閱 [Azure Functions 觸發程序和繫結概念](functions-triggers-bindings.md)。</span><span class="sxs-lookup"><span data-stu-id="58e00-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> <span data-ttu-id="58e00-108">不支援[僅限 blob 儲存體帳戶](../storage/common/storage-create-storage-account.md#blob-storage-accounts)。</span><span class="sxs-lookup"><span data-stu-id="58e00-108">A [blob only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts) is not supported.</span></span> <span data-ttu-id="58e00-109">Blob 儲存體觸發程序和繫結需要一般用途的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="58e00-109">Blob storage triggers and bindings require a general-purpose storage account.</span></span> 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a><span data-ttu-id="58e00-110">Blob 儲存體觸發程序和繫結</span><span class="sxs-lookup"><span data-stu-id="58e00-110">Blob storage triggers and bindings</span></span>

<span data-ttu-id="58e00-111">使用 hello Azure Blob 儲存體觸發程序，便會在偵測到新的或更新的 blob 時，呼叫您的函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="58e00-111">Using hello Azure Blob storage trigger, your function code is called when a new or updated blob is detected.</span></span> <span data-ttu-id="58e00-112">輸入的 toohello 函式，提供 hello blob 內容。</span><span class="sxs-lookup"><span data-stu-id="58e00-112">hello blob contents are provided as input toohello function.</span></span>

<span data-ttu-id="58e00-113">定義使用 hello blob 儲存體觸發程序**整合**hello 函式的入口網站中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="58e00-113">Define a blob storage trigger using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="58e00-114">hello 入口網站會建立下列 hello 中的定義的 hello**繫結**區段*function.json*:</span><span class="sxs-lookup"><span data-stu-id="58e00-114">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container toomonitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

<span data-ttu-id="58e00-115">Blob 輸入和輸出繫結透過定義`blob`hello 繫結類型為：</span><span class="sxs-lookup"><span data-stu-id="58e00-115">Blob input and output bindings are defined using `blob` as hello binding type:</span></span>

```json
{
  "name": "<hello name used tooidentify hello blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* <span data-ttu-id="58e00-116">hello`path`屬性支援繫結運算式和篩選參數。</span><span class="sxs-lookup"><span data-stu-id="58e00-116">hello `path` property supports binding expressions and filter parameters.</span></span> <span data-ttu-id="58e00-117">請參閱[名稱模式](#pattern)。</span><span class="sxs-lookup"><span data-stu-id="58e00-117">See [Name patterns](#pattern).</span></span>
* <span data-ttu-id="58e00-118">hello`connection`屬性必須包含 hello 包含儲存體連接字串的應用程式設定名稱。</span><span class="sxs-lookup"><span data-stu-id="58e00-118">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="58e00-119">Hello Azure 入口網站，在 hello 標準編輯器中 hello**整合** 索引標籤會將此應用程式設定，當您選取的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="58e00-119">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="58e00-120">當您使用的 blob 觸發程序消耗計劃時，可以有向上 tooa 10 分鐘的延遲之後函式應用程式已進入閒置處理新的 blob。</span><span class="sxs-lookup"><span data-stu-id="58e00-120">When you're using a blob trigger on a Consumption plan, there can be up tooa 10-minute delay in processing new blobs after a function app has gone idle.</span></span> <span data-ttu-id="58e00-121">Hello 函式應用程式執行之後，blob 會立即處理。</span><span class="sxs-lookup"><span data-stu-id="58e00-121">After hello function app is running, blobs are processed immediately.</span></span> <span data-ttu-id="58e00-122">此初始 tooavoid 延遲，請考慮下列選項的 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="58e00-122">tooavoid this initial delay, consider one of hello following options:</span></span>
> - <span data-ttu-id="58e00-123">使用 App Service 方案並啟用「永遠開啟」。</span><span class="sxs-lookup"><span data-stu-id="58e00-123">Use an App Service plan with Always On enabled.</span></span>
> - <span data-ttu-id="58e00-124">使用處理，例如包含 hello blob 名稱的佇列訊息另一個的機制 tootrigger hello blob。</span><span class="sxs-lookup"><span data-stu-id="58e00-124">Use another mechanism tootrigger hello blob processing, such as a queue message that contains hello blob name.</span></span> <span data-ttu-id="58e00-125">如需範例，請參閱[具有 blob 輸入繫結的佇列觸發程序](#input-sample)。</span><span class="sxs-lookup"><span data-stu-id="58e00-125">For an example, see [Queue trigger with blob input binding](#input-sample).</span></span>

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="58e00-126">名稱模式</span><span class="sxs-lookup"><span data-stu-id="58e00-126">Name patterns</span></span>
<span data-ttu-id="58e00-127">您可以指定 blob 名稱模式中 hello`path`屬性，可以篩選或繫結運算式。</span><span class="sxs-lookup"><span data-stu-id="58e00-127">You can specify a blob name pattern in hello `path` property, which can be a filter or binding expression.</span></span> <span data-ttu-id="58e00-128">請參閱[繫結運算式和模式](functions-triggers-bindings.md#binding-expressions-and-patterns)。</span><span class="sxs-lookup"><span data-stu-id="58e00-128">See [Binding expressions and patterns](functions-triggers-bindings.md#binding-expressions-and-patterns).</span></span>

<span data-ttu-id="58e00-129">比方說，toofilter tooblobs 開頭為 「 原始 」 hello 字串使用下列定義 hello。</span><span class="sxs-lookup"><span data-stu-id="58e00-129">For example, toofilter tooblobs that start with hello string "original," use hello following definition.</span></span> <span data-ttu-id="58e00-130">這個路徑尋找名為 blob*原始 Blob1.txt*在 hello*輸入*容器和 hello hello 值`name`函式程式碼中的變數是`Blob1`。</span><span class="sxs-lookup"><span data-stu-id="58e00-130">This path finds a blob named *original-Blob1.txt* in hello *input* container, and hello value of hello `name` variable in function code is `Blob1`.</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="58e00-131">toobind toohello blob 檔案名稱和副檔名分別使用兩種模式。</span><span class="sxs-lookup"><span data-stu-id="58e00-131">toobind toohello blob file name and extension separately, use two patterns.</span></span> <span data-ttu-id="58e00-132">此路徑也會尋找名為 blob*原始 Blob1.txt*，和 hello hello 值`blobname`和`blobextension`函式程式碼中的變數*原始 Blob1*和*txt*.</span><span class="sxs-lookup"><span data-stu-id="58e00-132">This path also finds a blob named *original-Blob1.txt*, and hello value of hello `blobname` and `blobextension` variables in function code are *original-Blob1* and *txt*.</span></span>

```json
"path": "input/{blobname}.{blobextension}",
```

<span data-ttu-id="58e00-133">您可以使用固定的值 hello 副檔名限制 hello 檔案類型的 blob。</span><span class="sxs-lookup"><span data-stu-id="58e00-133">You can restrict hello file type of blobs by using a fixed value for hello file extension.</span></span> <span data-ttu-id="58e00-134">比方說，tootrigger 只能在.png 檔案上使用 hello 下列模式：</span><span class="sxs-lookup"><span data-stu-id="58e00-134">For instance, tootrigger only on .png files, use hello following pattern:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="58e00-135">大括號是名稱模式中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="58e00-135">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="58e00-136">toospecify blob 名稱 hello 名稱中有大括號，您可以逸出 hello 使用兩個大括號的大括號。</span><span class="sxs-lookup"><span data-stu-id="58e00-136">toospecify blob names that have curly braces in hello name, you can escape hello braces using two braces.</span></span> <span data-ttu-id="58e00-137">hello 下列範例會尋找名為 blob *{20140101}-soundfile.mp3*在 hello*映像*容器和 hello `name` hello 函式程式碼中變數的值是*soundfile.mp3*。</span><span class="sxs-lookup"><span data-stu-id="58e00-137">hello following example finds a blob named *{20140101}-soundfile.mp3* in hello *images* container, and hello `name` variable value in hello function code is *soundfile.mp3*.</span></span> 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a><span data-ttu-id="58e00-138">觸發程序中繼資料</span><span class="sxs-lookup"><span data-stu-id="58e00-138">Trigger metadata</span></span>

<span data-ttu-id="58e00-139">hello blob 觸發程序會提供數個中繼資料屬性。</span><span class="sxs-lookup"><span data-stu-id="58e00-139">hello blob trigger provides several metadata properties.</span></span> <span data-ttu-id="58e00-140">這些屬性可作為其他繫結中繫結運算式的一部分或程式碼中的參數使用。</span><span class="sxs-lookup"><span data-stu-id="58e00-140">These properties can be used as part of bindings expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="58e00-141">這些值有 hello 相同的語意[CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="58e00-141">These values have hello same semantics as [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span></span>

- <span data-ttu-id="58e00-142">**BlobTrigger**：</span><span class="sxs-lookup"><span data-stu-id="58e00-142">**BlobTrigger**.</span></span> <span data-ttu-id="58e00-143">輸入 `string`。</span><span class="sxs-lookup"><span data-stu-id="58e00-143">Type `string`.</span></span> <span data-ttu-id="58e00-144">hello 觸發 blob 路徑</span><span class="sxs-lookup"><span data-stu-id="58e00-144">hello triggering blob path</span></span>
- <span data-ttu-id="58e00-145">**URI**：</span><span class="sxs-lookup"><span data-stu-id="58e00-145">**Uri**.</span></span> <span data-ttu-id="58e00-146">輸入 `System.Uri`。</span><span class="sxs-lookup"><span data-stu-id="58e00-146">Type `System.Uri`.</span></span> <span data-ttu-id="58e00-147">hello 主要位置的 hello blob 的 URI。</span><span class="sxs-lookup"><span data-stu-id="58e00-147">hello blob's URI for hello primary location.</span></span>
- <span data-ttu-id="58e00-148">**屬性**：</span><span class="sxs-lookup"><span data-stu-id="58e00-148">**Properties**.</span></span> <span data-ttu-id="58e00-149">輸入 `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`。</span><span class="sxs-lookup"><span data-stu-id="58e00-149">Type `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span></span> <span data-ttu-id="58e00-150">hello blob 的系統屬性。</span><span class="sxs-lookup"><span data-stu-id="58e00-150">hello blob's system properties.</span></span>
- <span data-ttu-id="58e00-151">**中繼資料**：</span><span class="sxs-lookup"><span data-stu-id="58e00-151">**Metadata**.</span></span> <span data-ttu-id="58e00-152">輸入 `IDictionary<string,string>`。</span><span class="sxs-lookup"><span data-stu-id="58e00-152">Type `IDictionary<string,string>`.</span></span> <span data-ttu-id="58e00-153">hello hello blob 的使用者定義中繼資料。</span><span class="sxs-lookup"><span data-stu-id="58e00-153">hello user-defined metadata for hello blob.</span></span>

<a name="receipts"></a>

### <a name="blob-receipts"></a><span data-ttu-id="58e00-154">Blob 回條</span><span class="sxs-lookup"><span data-stu-id="58e00-154">Blob receipts</span></span>
<span data-ttu-id="58e00-155">hello Azure 函式執行階段會確保沒有任何 blob 觸發程序函式取得呼叫一次以上的 hello 相同的新功能或更新 blob。</span><span class="sxs-lookup"><span data-stu-id="58e00-155">hello Azure Functions runtime ensures that no blob trigger function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="58e00-156">如果已處理指定的 blob 版本 toodetermine，它會維護*blob 回條*。</span><span class="sxs-lookup"><span data-stu-id="58e00-156">toodetermine if a given blob version has been processed, it maintains *blob receipts*.</span></span>

<span data-ttu-id="58e00-157">Azure 的函式存放區 blob 容器中的回條*azure webjobs 託管*hello 函式應用程式的 Azure 儲存體帳戶中 (hello 應用程式設定所定義`AzureWebJobsStorage`)。</span><span class="sxs-lookup"><span data-stu-id="58e00-157">Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in hello Azure storage account for your function app (defined by hello app setting `AzureWebJobsStorage`).</span></span> <span data-ttu-id="58e00-158">Blob 的回條具有 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="58e00-158">A blob receipt has hello following information:</span></span>

* <span data-ttu-id="58e00-159">hello 觸發函式 (「*&lt;函式應用程式名稱 >*。函式。*&lt;函式名稱 >*"，例如:"MyFunctionApp.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="58e00-159">hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "MyFunctionApp.Functions.CopyBlob")</span></span>
* <span data-ttu-id="58e00-160">hello 容器名稱</span><span class="sxs-lookup"><span data-stu-id="58e00-160">hello container name</span></span>
* <span data-ttu-id="58e00-161">hello blob 類型 （"BlockBlob"或"PageBlob"）</span><span class="sxs-lookup"><span data-stu-id="58e00-161">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="58e00-162">hello blob 名稱</span><span class="sxs-lookup"><span data-stu-id="58e00-162">hello blob name</span></span>
* <span data-ttu-id="58e00-163">hello ETag (例如 blob 版本識別碼:"0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="58e00-163">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="58e00-164">tooforce 重新處理的 blob，blob 的 hello blob 回條刪除 hello *azure webjobs 託管*容器以手動方式。</span><span class="sxs-lookup"><span data-stu-id="58e00-164">tooforce reprocessing of a blob, delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container manually.</span></span>

<a name="poison"></a>

### <a name="handling-poison-blobs"></a><span data-ttu-id="58e00-165">處理有害的 blob</span><span class="sxs-lookup"><span data-stu-id="58e00-165">Handling poison blobs</span></span>
<span data-ttu-id="58e00-166">當指定 blob 的 blob 觸發程序函式失敗時，Azure Functions 預設一共會重試該函式 5 次。</span><span class="sxs-lookup"><span data-stu-id="58e00-166">When a blob trigger function fails for a given blob, Azure Functions retries that function a total of 5 times by default.</span></span> 

<span data-ttu-id="58e00-167">如果所有 5 次嘗試失敗，Azure 函式會將名為訊息 tooa 儲存體佇列*webjobs-blobtrigger-有害*。</span><span class="sxs-lookup"><span data-stu-id="58e00-167">If all 5 tries fail, Azure Functions adds a message tooa Storage queue named *webjobs-blobtrigger-poison*.</span></span> <span data-ttu-id="58e00-168">hello 佇列訊息的有害的 blob 是 JSON 物件，包含下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="58e00-168">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="58e00-169">FunctionId (hello 格式*&lt;函式應用程式名稱 >*。函式。*&lt;函式名稱 >*)</span><span class="sxs-lookup"><span data-stu-id="58e00-169">FunctionId (in hello format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="58e00-170">BlobType ("BlockBlob" 或 "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="58e00-170">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="58e00-171">ContainerName</span><span class="sxs-lookup"><span data-stu-id="58e00-171">ContainerName</span></span>
* <span data-ttu-id="58e00-172">BlobName</span><span class="sxs-lookup"><span data-stu-id="58e00-172">BlobName</span></span>
* <span data-ttu-id="58e00-173">ETag (Blob 版本識別碼，例如："0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="58e00-173">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

### <a name="blob-polling-for-large-containers"></a><span data-ttu-id="58e00-174">大型容器的 Blob 輪詢</span><span class="sxs-lookup"><span data-stu-id="58e00-174">Blob polling for large containers</span></span>
<span data-ttu-id="58e00-175">如果受監視的 hello blob 容器包含超過 10,000 個 blob，hello 函式執行階段掃描記錄檔 toowatch 的新增或變更的 blob。</span><span class="sxs-lookup"><span data-stu-id="58e00-175">If hello blob container being monitored contains more than 10,000 blobs, hello Functions runtime scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="58e00-176">此程序不是即時。</span><span class="sxs-lookup"><span data-stu-id="58e00-176">This process is not real time.</span></span> <span data-ttu-id="58e00-177">函式可能不會觸發直到幾分鐘的時間或更久之後建立 hello 的 blob。</span><span class="sxs-lookup"><span data-stu-id="58e00-177">A function might not get triggered until several minutes or longer after hello blob is created.</span></span> <span data-ttu-id="58e00-178">此外，[會以「最大努力」建立儲存體記錄](/rest/api/storageservices/About-Storage-Analytics-Logging)。</span><span class="sxs-lookup"><span data-stu-id="58e00-178">In addition, [storage logs are created on a "best effort"](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span></span> <span data-ttu-id="58e00-179">並不保證會擷取所有的事件。</span><span class="sxs-lookup"><span data-stu-id="58e00-179">There is no guarantee that all events are captured.</span></span> <span data-ttu-id="58e00-180">在某些情況下可能會遺失記錄檔。</span><span class="sxs-lookup"><span data-stu-id="58e00-180">Under some conditions, logs may be missed.</span></span> <span data-ttu-id="58e00-181">如果您需要更快或更可靠的 blob 處理，請考慮建立[佇列訊息](../storage/queues/storage-dotnet-how-to-use-queues.md)當您建立 hello blob。</span><span class="sxs-lookup"><span data-stu-id="58e00-181">If you require faster or more reliable blob processing, consider creating a [queue message](../storage/queues/storage-dotnet-how-to-use-queues.md) when you create hello blob.</span></span> <span data-ttu-id="58e00-182">然後，使用[佇列觸發程序](functions-bindings-storage-queue.md)而不是 blob 觸發程序 tooprocess hello blob。</span><span class="sxs-lookup"><span data-stu-id="58e00-182">Then, use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger tooprocess hello blob.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a><span data-ttu-id="58e00-183">使用 blob 觸發程序和輸入繫結</span><span class="sxs-lookup"><span data-stu-id="58e00-183">Using a blob trigger and input binding</span></span>
<span data-ttu-id="58e00-184">在.NET 函式，存取 hello blob 資料使用的方法參數，例如`Stream paramName`。</span><span class="sxs-lookup"><span data-stu-id="58e00-184">In .NET functions, access hello blob data using a method parameter such as `Stream paramName`.</span></span> <span data-ttu-id="58e00-185">在這裡，`paramName`是您在 hello 中指定的 hello 值[觸發程序組態](#trigger)。</span><span class="sxs-lookup"><span data-stu-id="58e00-185">Here, `paramName` is hello value you specified in hello [trigger configuration](#trigger).</span></span> <span data-ttu-id="58e00-186">在 Node.js 函數中，輸入使用的 blob 資料存取 hello `context.bindings.<name>`。</span><span class="sxs-lookup"><span data-stu-id="58e00-186">In Node.js functions, access hello input blob data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="58e00-187">在.NET 中，您可以結合 hello 型別的 tooany hello 下面的清單中。</span><span class="sxs-lookup"><span data-stu-id="58e00-187">In .NET, you can bind tooany of hello types in hello list below.</span></span> <span data-ttu-id="58e00-188">如果用作輸入繫結，其中一些類型需要 *function.json* 中的 `inout` 繫結方向。</span><span class="sxs-lookup"><span data-stu-id="58e00-188">If used as an input binding, some of these types require an `inout` binding direction in *function.json*.</span></span> <span data-ttu-id="58e00-189">因此您必須使用進階編輯器 hello hello 標準編輯器中，不被支援這個方向。</span><span class="sxs-lookup"><span data-stu-id="58e00-189">This direction is not supported by hello standard editor, so you must use hello advanced editor.</span></span>

* `TextReader`
* `Stream`
* <span data-ttu-id="58e00-190">`ICloudBlob` (需要 "inout" 繫結方向)</span><span class="sxs-lookup"><span data-stu-id="58e00-190">`ICloudBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="58e00-191">`CloudBlockBlob` (需要 "inout" 繫結方向)</span><span class="sxs-lookup"><span data-stu-id="58e00-191">`CloudBlockBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="58e00-192">`CloudPageBlob` (需要 "inout" 繫結方向)</span><span class="sxs-lookup"><span data-stu-id="58e00-192">`CloudPageBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="58e00-193">`CloudAppendBlob` (需要 "inout" 繫結方向)</span><span class="sxs-lookup"><span data-stu-id="58e00-193">`CloudAppendBlob` (requires "inout" binding direction)</span></span>

<span data-ttu-id="58e00-194">如果預期文字 blob，您也可以繫結 tooa.NET`string`型別。</span><span class="sxs-lookup"><span data-stu-id="58e00-194">If text blobs are expected, you can also bind tooa .NET `string` type.</span></span> <span data-ttu-id="58e00-195">這只被建議如果 hello blob 大小很小，如 hello 整個 blob 內容會載入記憶體。</span><span class="sxs-lookup"><span data-stu-id="58e00-195">This is only recommended if hello blob size is small, as hello entire blob contents are loaded into memory.</span></span> <span data-ttu-id="58e00-196">通常，它是比 toouse`Stream`或`CloudBlockBlob`型別。</span><span class="sxs-lookup"><span data-stu-id="58e00-196">Generally, it is preferable toouse a `Stream` or `CloudBlockBlob` type.</span></span>

## <a name="trigger-sample"></a><span data-ttu-id="58e00-197">觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="58e00-197">Trigger sample</span></span>
<span data-ttu-id="58e00-198">假設您有下列定義的 blob 儲存體觸發程序的 function.json hello:</span><span class="sxs-lookup"><span data-stu-id="58e00-198">Suppose you have hello following function.json that defines a blob storage trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myBlob",
            "type": "blobTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection":"MyStorageAccount"
        }
    ]
}
```

<span data-ttu-id="58e00-199">請參閱記錄 hello toohello 受監視的容器加入每一個 blob 內容的 hello 特定語言的範例。</span><span class="sxs-lookup"><span data-stu-id="58e00-199">See hello language-specific sample that logs hello contents of each blob that is added toohello monitored container.</span></span>

* [<span data-ttu-id="58e00-200">C#</span><span class="sxs-lookup"><span data-stu-id="58e00-200">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="58e00-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="58e00-201">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a><span data-ttu-id="58e00-202">C# 中的 Blob 觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="58e00-202">Blob trigger examples in C#</span></span> #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding tooa CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a><span data-ttu-id="58e00-203">Node.js 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="58e00-203">Trigger example in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a><span data-ttu-id="58e00-204">使用 blob 輸出繫結</span><span class="sxs-lookup"><span data-stu-id="58e00-204">Using a blob output binding</span></span>

<span data-ttu-id="58e00-205">在.NET 函數中，您應該使用`out string`函式簽章中使用其中一個 hello hello 下列清單中的型別參數。</span><span class="sxs-lookup"><span data-stu-id="58e00-205">In .NET functions, you should either use a `out string` parameter in your function signature or use one of hello types in hello following list.</span></span> <span data-ttu-id="58e00-206">Node.js 函式，在您存取 hello 輸出 blob 使用`context.bindings.<name>`。</span><span class="sxs-lookup"><span data-stu-id="58e00-206">In Node.js functions, you access hello output blob using `context.bindings.<name>`.</span></span>

<span data-ttu-id="58e00-207">.NET 函式中，您可以輸出 tooany 的 hello 下列類型：</span><span class="sxs-lookup"><span data-stu-id="58e00-207">In .NET functions you can output tooany of hello following types:</span></span>

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a><span data-ttu-id="58e00-208">具有 blob 輸入和輸出的佇列觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="58e00-208">Queue trigger with blob input and output sample</span></span>
<span data-ttu-id="58e00-209">假設您有下列 function.json hello，定義[佇列儲存體觸發程序](functions-bindings-storage-queue.md)、 blob 儲存體輸入和輸出 blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="58e00-209">Suppose you have hello following function.json, that defines a [Queue Storage trigger](functions-bindings-storage-queue.md), a blob storage input, and a blob storage output.</span></span> <span data-ttu-id="58e00-210">請注意 hello 使用 hello`queueTrigger`中繼資料屬性。</span><span class="sxs-lookup"><span data-stu-id="58e00-210">Notice hello use of hello `queueTrigger` metadata property.</span></span> <span data-ttu-id="58e00-211">在輸入和輸出的 hello blob`path`屬性：</span><span class="sxs-lookup"><span data-stu-id="58e00-211">in hello blob input and output `path` properties:</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnection",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

<span data-ttu-id="58e00-212">請參閱複製 hello 輸入的 blob toohello 輸出 blob 的 hello 特定語言的範例。</span><span class="sxs-lookup"><span data-stu-id="58e00-212">See hello language-specific sample that copies hello input blob toohello output blob.</span></span>

* [<span data-ttu-id="58e00-213">C#</span><span class="sxs-lookup"><span data-stu-id="58e00-213">C#</span></span>](#incsharp)
* [<span data-ttu-id="58e00-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="58e00-214">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a><span data-ttu-id="58e00-215">C# 中的 blob 繫結範例</span><span class="sxs-lookup"><span data-stu-id="58e00-215">Blob binding example in C#</span></span> #

```cs
// Copy blob from input toooutput, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a><span data-ttu-id="58e00-216">Node.js 中的 blob 繫結範例</span><span class="sxs-lookup"><span data-stu-id="58e00-216">Blob binding example in Node.js</span></span>

```javascript
// Copy blob from input toooutput, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="58e00-217">後續步驟</span><span class="sxs-lookup"><span data-stu-id="58e00-217">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

