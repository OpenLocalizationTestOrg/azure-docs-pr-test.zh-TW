---
title: "Azure Functions Blob 儲存體繫結 | Microsoft Docs"
description: "瞭解如何在 Azure Functions 中使用「Azure 儲存體」觸發程序和繫結。"
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
ms.openlocfilehash: 8d8f510ec906c0e0420ec48d45d88b93c144658a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-blob-storage-bindings"></a><span data-ttu-id="b5539-104">Azure Functions Blob 儲存體繫結</span><span class="sxs-lookup"><span data-stu-id="b5539-104">Azure Functions Blob storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="b5539-105">本文說明如何在 Azure Functions 中設定及使用 Azure Blob 儲存體繫結。</span><span class="sxs-lookup"><span data-stu-id="b5539-105">This article explains how to configure and work with Azure Blob storage bindings in Azure Functions.</span></span> <span data-ttu-id="b5539-106">Azure Functions 支援適用於 Azure Blob 儲存體的觸發程序、輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="b5539-106">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="b5539-107">如需所有繫結中可用的功能，請參閱 [Azure Functions 觸發程序和繫結概念](functions-triggers-bindings.md)。</span><span class="sxs-lookup"><span data-stu-id="b5539-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> <span data-ttu-id="b5539-108">不支援[僅限 blob 儲存體帳戶](../storage/common/storage-create-storage-account.md#blob-storage-accounts)。</span><span class="sxs-lookup"><span data-stu-id="b5539-108">A [blob only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts) is not supported.</span></span> <span data-ttu-id="b5539-109">Blob 儲存體觸發程序和繫結需要一般用途的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b5539-109">Blob storage triggers and bindings require a general-purpose storage account.</span></span> 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a><span data-ttu-id="b5539-110">Blob 儲存體觸發程序和繫結</span><span class="sxs-lookup"><span data-stu-id="b5539-110">Blob storage triggers and bindings</span></span>

<span data-ttu-id="b5539-111">使用 Azure Blob 儲存體觸發程序，就會在偵測到新的或更新的 blob 時呼叫您的函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="b5539-111">Using the Azure Blob storage trigger, your function code is called when a new or updated blob is detected.</span></span> <span data-ttu-id="b5539-112">Blob 內容會當成函式輸入提供。</span><span class="sxs-lookup"><span data-stu-id="b5539-112">The blob contents are provided as input to the function.</span></span>

<span data-ttu-id="b5539-113">使用 Functions 入口網站中的 [整合] 索引標籤定義 Blob 儲存體觸發程序。</span><span class="sxs-lookup"><span data-stu-id="b5539-113">Define a blob storage trigger using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="b5539-114">該入口網站會在 *function.json* 的 **bindings** 區段中建立下列定義：</span><span class="sxs-lookup"><span data-stu-id="b5539-114">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
    "name": "<The name used to identify the trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container to monitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

<span data-ttu-id="b5539-115">使用 `blob` 將 blob 輸入和輸出繫結定義為繫結類型：</span><span class="sxs-lookup"><span data-stu-id="b5539-115">Blob input and output bindings are defined using `blob` as the binding type:</span></span>

```json
{
  "name": "<The name used to identify the blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* <span data-ttu-id="b5539-116">`path` 屬性支援繫結運算式和篩選參數。</span><span class="sxs-lookup"><span data-stu-id="b5539-116">The `path` property supports binding expressions and filter parameters.</span></span> <span data-ttu-id="b5539-117">請參閱[名稱模式](#pattern)。</span><span class="sxs-lookup"><span data-stu-id="b5539-117">See [Name patterns](#pattern).</span></span>
* <span data-ttu-id="b5539-118">`connection` 屬性必須包含應用程式設定的名稱，其中包含儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="b5539-118">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="b5539-119">在 Azure 入口網站中，當您選取儲存體帳戶時，[整合] 索引標籤中的標準編輯器可設定此應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="b5539-119">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="b5539-120">當您在使用情況方案中使用 blob 觸發程序時，函數應用程式進入閒置狀態之後，處理新 blob 最多會有 10 分鐘的延遲。</span><span class="sxs-lookup"><span data-stu-id="b5539-120">When you're using a blob trigger on a Consumption plan, there can be up to a 10-minute delay in processing new blobs after a function app has gone idle.</span></span> <span data-ttu-id="b5539-121">在函數應用程式開始執行之後，會立即處理 blob。</span><span class="sxs-lookup"><span data-stu-id="b5539-121">After the function app is running, blobs are processed immediately.</span></span> <span data-ttu-id="b5539-122">為了避免發生此初始延遲，請考慮下列做法︰</span><span class="sxs-lookup"><span data-stu-id="b5539-122">To avoid this initial delay, consider one of the following options:</span></span>
> - <span data-ttu-id="b5539-123">使用 App Service 方案並啟用「永遠開啟」。</span><span class="sxs-lookup"><span data-stu-id="b5539-123">Use an App Service plan with Always On enabled.</span></span>
> - <span data-ttu-id="b5539-124">使用其他機制來觸發 blob 處理，像是包含 blob 名稱的佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="b5539-124">Use another mechanism to trigger the blob processing, such as a queue message that contains the blob name.</span></span> <span data-ttu-id="b5539-125">如需範例，請參閱[具有 blob 輸入繫結的佇列觸發程序](#input-sample)。</span><span class="sxs-lookup"><span data-stu-id="b5539-125">For an example, see [Queue trigger with blob input binding](#input-sample).</span></span>

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="b5539-126">名稱模式</span><span class="sxs-lookup"><span data-stu-id="b5539-126">Name patterns</span></span>
<span data-ttu-id="b5539-127">您可以在 `path` 屬性中，指定可篩選或繫結運算式的 blob 名稱模式。</span><span class="sxs-lookup"><span data-stu-id="b5539-127">You can specify a blob name pattern in the `path` property, which can be a filter or binding expression.</span></span> <span data-ttu-id="b5539-128">請參閱[繫結運算式和模式](functions-triggers-bindings.md#binding-expressions-and-patterns)。</span><span class="sxs-lookup"><span data-stu-id="b5539-128">See [Binding expressions and patterns](functions-triggers-bindings.md#binding-expressions-and-patterns).</span></span>

<span data-ttu-id="b5539-129">例如，若要篩選至以 "original" 字串開頭的 blob，請使用下列定義。</span><span class="sxs-lookup"><span data-stu-id="b5539-129">For example, to filter to blobs that start with the string "original," use the following definition.</span></span> <span data-ttu-id="b5539-130">此路徑會在 *input* 容器中尋找名為 *original-Blob1.txt* 的 blob，且函式程式碼中的 `name` 變數值為 `Blob1`。</span><span class="sxs-lookup"><span data-stu-id="b5539-130">This path finds a blob named *original-Blob1.txt* in the *input* container, and the value of the `name` variable in function code is `Blob1`.</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="b5539-131">若要分別繫結至 blob 檔案名稱和副檔名，請使用兩個模式。</span><span class="sxs-lookup"><span data-stu-id="b5539-131">To bind to the blob file name and extension separately, use two patterns.</span></span> <span data-ttu-id="b5539-132">此路徑也會尋找名為 *original-Blob1.txt* 的 blob，且函式程式碼中的 `blobname` 和 `blobextension` 變數值為 *original-Blob1* 和 *txt*。</span><span class="sxs-lookup"><span data-stu-id="b5539-132">This path also finds a blob named *original-Blob1.txt*, and the value of the `blobname` and `blobextension` variables in function code are *original-Blob1* and *txt*.</span></span>

```json
"path": "input/{blobname}.{blobextension}",
```

<span data-ttu-id="b5539-133">您可以使用檔案副檔名的固定值來限制 blob 的類型。</span><span class="sxs-lookup"><span data-stu-id="b5539-133">You can restrict the file type of blobs by using a fixed value for the file extension.</span></span> <span data-ttu-id="b5539-134">例如，若只要在 .png 檔案上觸發，請使用下列模式：</span><span class="sxs-lookup"><span data-stu-id="b5539-134">For instance, to trigger only on .png files, use the following pattern:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="b5539-135">大括號是名稱模式中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="b5539-135">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="b5539-136">若要指定名稱中包含大括號的 blob 名稱，您可以使用兩個大括號來逸出大括號。</span><span class="sxs-lookup"><span data-stu-id="b5539-136">To specify blob names that have curly braces in the name, you can escape the braces using two braces.</span></span> <span data-ttu-id="b5539-137">下列範例會在 *images* 容器中尋找名為 *{20140101}-soundfile.mp3* 的 blob，且函式程式碼中的 `name` 變數值為 *soundfile.mp3*。</span><span class="sxs-lookup"><span data-stu-id="b5539-137">The following example finds a blob named *{20140101}-soundfile.mp3* in the *images* container, and the `name` variable value in the function code is *soundfile.mp3*.</span></span> 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a><span data-ttu-id="b5539-138">觸發程序中繼資料</span><span class="sxs-lookup"><span data-stu-id="b5539-138">Trigger metadata</span></span>

<span data-ttu-id="b5539-139">Blob 觸發程序提供數個中繼資料屬性。</span><span class="sxs-lookup"><span data-stu-id="b5539-139">The blob trigger provides several metadata properties.</span></span> <span data-ttu-id="b5539-140">這些屬性可作為其他繫結中繫結運算式的一部分或程式碼中的參數使用。</span><span class="sxs-lookup"><span data-stu-id="b5539-140">These properties can be used as part of bindings expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="b5539-141">這些值的語意與 [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet) 相同。</span><span class="sxs-lookup"><span data-stu-id="b5539-141">These values have the same semantics as [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span></span>

- <span data-ttu-id="b5539-142">**BlobTrigger**：</span><span class="sxs-lookup"><span data-stu-id="b5539-142">**BlobTrigger**.</span></span> <span data-ttu-id="b5539-143">輸入 `string`。</span><span class="sxs-lookup"><span data-stu-id="b5539-143">Type `string`.</span></span> <span data-ttu-id="b5539-144">觸發的 blob 路徑</span><span class="sxs-lookup"><span data-stu-id="b5539-144">The triggering blob path</span></span>
- <span data-ttu-id="b5539-145">**URI**：</span><span class="sxs-lookup"><span data-stu-id="b5539-145">**Uri**.</span></span> <span data-ttu-id="b5539-146">輸入 `System.Uri`。</span><span class="sxs-lookup"><span data-stu-id="b5539-146">Type `System.Uri`.</span></span> <span data-ttu-id="b5539-147">Blob 的主要位置 URI。</span><span class="sxs-lookup"><span data-stu-id="b5539-147">The blob's URI for the primary location.</span></span>
- <span data-ttu-id="b5539-148">**屬性**：</span><span class="sxs-lookup"><span data-stu-id="b5539-148">**Properties**.</span></span> <span data-ttu-id="b5539-149">輸入 `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`。</span><span class="sxs-lookup"><span data-stu-id="b5539-149">Type `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span></span> <span data-ttu-id="b5539-150">Blob 的系統屬性。</span><span class="sxs-lookup"><span data-stu-id="b5539-150">The blob's system properties.</span></span>
- <span data-ttu-id="b5539-151">**中繼資料**：</span><span class="sxs-lookup"><span data-stu-id="b5539-151">**Metadata**.</span></span> <span data-ttu-id="b5539-152">輸入 `IDictionary<string,string>`。</span><span class="sxs-lookup"><span data-stu-id="b5539-152">Type `IDictionary<string,string>`.</span></span> <span data-ttu-id="b5539-153">Blob 的使用者定義中繼資料。</span><span class="sxs-lookup"><span data-stu-id="b5539-153">The user-defined metadata for the blob.</span></span>

<a name="receipts"></a>

### <a name="blob-receipts"></a><span data-ttu-id="b5539-154">Blob 回條</span><span class="sxs-lookup"><span data-stu-id="b5539-154">Blob receipts</span></span>
<span data-ttu-id="b5539-155">Azure Functions 執行階段可確保不會針對一樣新或更新的 blob 多次呼叫 blob 觸發程序函式。</span><span class="sxs-lookup"><span data-stu-id="b5539-155">The Azure Functions runtime ensures that no blob trigger function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="b5539-156">為了判斷指定的 blob 版本是否已處理過，它會維護 *blob 回條*。</span><span class="sxs-lookup"><span data-stu-id="b5539-156">To determine if a given blob version has been processed, it maintains *blob receipts*.</span></span>

<span data-ttu-id="b5539-157">Azure Functions 會將 blob 回條儲存在您函數應用程式 (`AzureWebJobsStorage` 應用程式設定所定義) 的 Azure 儲存體帳戶中名為 *azure-webjobs-hosts*的容器中。</span><span class="sxs-lookup"><span data-stu-id="b5539-157">Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in the Azure storage account for your function app (defined by the app setting `AzureWebJobsStorage`).</span></span> <span data-ttu-id="b5539-158">Blob 回條具有下列資訊：</span><span class="sxs-lookup"><span data-stu-id="b5539-158">A blob receipt has the following information:</span></span>

* <span data-ttu-id="b5539-159">已觸發的函數 ("&lt;函數應用程式名稱>.Functions.&lt;函數名稱>"，例如："MyFunctionApp.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="b5539-159">The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "MyFunctionApp.Functions.CopyBlob")</span></span>
* <span data-ttu-id="b5539-160">容器名稱</span><span class="sxs-lookup"><span data-stu-id="b5539-160">The container name</span></span>
* <span data-ttu-id="b5539-161">Blob 類型 ("BlockBlob" 或 "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="b5539-161">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="b5539-162">Blob 名稱</span><span class="sxs-lookup"><span data-stu-id="b5539-162">The blob name</span></span>
* <span data-ttu-id="b5539-163">ETag (Blob 版本識別碼，例如："0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="b5539-163">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="b5539-164">要強制重新處理某個 Blob，可以從 *azure-webjobs-hosts* 容器中手動刪除該 Blob 的 Blob 回條。</span><span class="sxs-lookup"><span data-stu-id="b5539-164">To force reprocessing of a blob, delete the blob receipt for that blob from the *azure-webjobs-hosts* container manually.</span></span>

<a name="poison"></a>

### <a name="handling-poison-blobs"></a><span data-ttu-id="b5539-165">處理有害的 blob</span><span class="sxs-lookup"><span data-stu-id="b5539-165">Handling poison blobs</span></span>
<span data-ttu-id="b5539-166">當指定 blob 的 blob 觸發程序函式失敗時，Azure Functions 預設一共會重試該函式 5 次。</span><span class="sxs-lookup"><span data-stu-id="b5539-166">When a blob trigger function fails for a given blob, Azure Functions retries that function a total of 5 times by default.</span></span> 

<span data-ttu-id="b5539-167">如果 5 次嘗試全都失敗，Azure Functions 會將訊息新增至名為 *webjobs-blobtrigger-poison* 的儲存體佇列。</span><span class="sxs-lookup"><span data-stu-id="b5539-167">If all 5 tries fail, Azure Functions adds a message to a Storage queue named *webjobs-blobtrigger-poison*.</span></span> <span data-ttu-id="b5539-168">適用於有害 Blob 的佇列訊息是一個 JSON 物件，其中包含下列屬性：</span><span class="sxs-lookup"><span data-stu-id="b5539-168">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="b5539-169">FunctionId (格式為 *&lt;function app name>*.Functions.*&lt;function name>*)</span><span class="sxs-lookup"><span data-stu-id="b5539-169">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="b5539-170">BlobType ("BlockBlob" 或 "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="b5539-170">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="b5539-171">ContainerName</span><span class="sxs-lookup"><span data-stu-id="b5539-171">ContainerName</span></span>
* <span data-ttu-id="b5539-172">BlobName</span><span class="sxs-lookup"><span data-stu-id="b5539-172">BlobName</span></span>
* <span data-ttu-id="b5539-173">ETag (Blob 版本識別碼，例如："0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="b5539-173">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

### <a name="blob-polling-for-large-containers"></a><span data-ttu-id="b5539-174">大型容器的 Blob 輪詢</span><span class="sxs-lookup"><span data-stu-id="b5539-174">Blob polling for large containers</span></span>
<span data-ttu-id="b5539-175">如果所監看的 blob 容器包含超過 10,000 個 blob，Functions 執行階段會掃描記錄檔以監看新增或變更的 blob。</span><span class="sxs-lookup"><span data-stu-id="b5539-175">If the blob container being monitored contains more than 10,000 blobs, the Functions runtime scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="b5539-176">此程序不是即時。</span><span class="sxs-lookup"><span data-stu-id="b5539-176">This process is not real time.</span></span> <span data-ttu-id="b5539-177">可能直到建立 Blob 之後數分鐘或更久，才會觸發函數。</span><span class="sxs-lookup"><span data-stu-id="b5539-177">A function might not get triggered until several minutes or longer after the blob is created.</span></span> <span data-ttu-id="b5539-178">此外，[會以「最大努力」建立儲存體記錄](/rest/api/storageservices/About-Storage-Analytics-Logging)。</span><span class="sxs-lookup"><span data-stu-id="b5539-178">In addition, [storage logs are created on a "best effort"](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span></span> <span data-ttu-id="b5539-179">並不保證會擷取所有的事件。</span><span class="sxs-lookup"><span data-stu-id="b5539-179">There is no guarantee that all events are captured.</span></span> <span data-ttu-id="b5539-180">在某些情況下可能會遺失記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b5539-180">Under some conditions, logs may be missed.</span></span> <span data-ttu-id="b5539-181">如果您需要更快或更可靠的 Blob 處理，請考慮在建立 Blob 時建立[佇列訊息](../storage/queues/storage-dotnet-how-to-use-queues.md)。</span><span class="sxs-lookup"><span data-stu-id="b5539-181">If you require faster or more reliable blob processing, consider creating a [queue message](../storage/queues/storage-dotnet-how-to-use-queues.md) when you create the blob.</span></span> <span data-ttu-id="b5539-182">然後，使用[佇列觸發程序](functions-bindings-storage-queue.md) (而不是 blob 觸發程序) 處理該 blob。</span><span class="sxs-lookup"><span data-stu-id="b5539-182">Then, use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger to process the blob.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a><span data-ttu-id="b5539-183">使用 blob 觸發程序和輸入繫結</span><span class="sxs-lookup"><span data-stu-id="b5539-183">Using a blob trigger and input binding</span></span>
<span data-ttu-id="b5539-184">在 .NET 函式中，使用方法參數 (例如`Stream paramName`) 存取 blob 資料。</span><span class="sxs-lookup"><span data-stu-id="b5539-184">In .NET functions, access the blob data using a method parameter such as `Stream paramName`.</span></span> <span data-ttu-id="b5539-185">其中，`paramName` 是您在[觸發程序設定](#trigger)中指定的值。</span><span class="sxs-lookup"><span data-stu-id="b5539-185">Here, `paramName` is the value you specified in the [trigger configuration](#trigger).</span></span> <span data-ttu-id="b5539-186">在 Node.js 函式中，使用 `context.bindings.<name>` 存取 blob 的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="b5539-186">In Node.js functions, access the input blob data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="b5539-187">在 .NET 中，您可以繫結至下列清單中的任何類型。</span><span class="sxs-lookup"><span data-stu-id="b5539-187">In .NET, you can bind to any of the types in the list below.</span></span> <span data-ttu-id="b5539-188">如果用作輸入繫結，其中一些類型需要 *function.json* 中的 `inout` 繫結方向。</span><span class="sxs-lookup"><span data-stu-id="b5539-188">If used as an input binding, some of these types require an `inout` binding direction in *function.json*.</span></span> <span data-ttu-id="b5539-189">標準編輯器不支援此方向，因此您必須使用進階編輯器。</span><span class="sxs-lookup"><span data-stu-id="b5539-189">This direction is not supported by the standard editor, so you must use the advanced editor.</span></span>

* `TextReader`
* `Stream`
* <span data-ttu-id="b5539-190">`ICloudBlob` (需要 "inout" 繫結方向)</span><span class="sxs-lookup"><span data-stu-id="b5539-190">`ICloudBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="b5539-191">`CloudBlockBlob` (需要 "inout" 繫結方向)</span><span class="sxs-lookup"><span data-stu-id="b5539-191">`CloudBlockBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="b5539-192">`CloudPageBlob` (需要 "inout" 繫結方向)</span><span class="sxs-lookup"><span data-stu-id="b5539-192">`CloudPageBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="b5539-193">`CloudAppendBlob` (需要 "inout" 繫結方向)</span><span class="sxs-lookup"><span data-stu-id="b5539-193">`CloudAppendBlob` (requires "inout" binding direction)</span></span>

<span data-ttu-id="b5539-194">如果預期為文字 blob，您也可以繫結至 .NET `string` 類型。</span><span class="sxs-lookup"><span data-stu-id="b5539-194">If text blobs are expected, you can also bind to a .NET `string` type.</span></span> <span data-ttu-id="b5539-195">由於會將整個 blob 內容載入記憶體中，因此只有在 blob 大小很小時才建議這樣做。</span><span class="sxs-lookup"><span data-stu-id="b5539-195">This is only recommended if the blob size is small, as the entire blob contents are loaded into memory.</span></span> <span data-ttu-id="b5539-196">一般而言，最好使用 `Stream` 或 `CloudBlockBlob` 類型。</span><span class="sxs-lookup"><span data-stu-id="b5539-196">Generally, it is preferable to use a `Stream` or `CloudBlockBlob` type.</span></span>

## <a name="trigger-sample"></a><span data-ttu-id="b5539-197">觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="b5539-197">Trigger sample</span></span>
<span data-ttu-id="b5539-198">假設您有下列 function.json，定義了 blob 儲存體觸發程序：</span><span class="sxs-lookup"><span data-stu-id="b5539-198">Suppose you have the following function.json that defines a blob storage trigger:</span></span>

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

<span data-ttu-id="b5539-199">請參閱會將每個新增的 Blob 內容記錄到受監視容器的語言特定範例。</span><span class="sxs-lookup"><span data-stu-id="b5539-199">See the language-specific sample that logs the contents of each blob that is added to the monitored container.</span></span>

* [<span data-ttu-id="b5539-200">C#</span><span class="sxs-lookup"><span data-stu-id="b5539-200">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="b5539-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="b5539-201">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a><span data-ttu-id="b5539-202">C# 中的 Blob 觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="b5539-202">Blob trigger examples in C#</span></span> #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding to a CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a><span data-ttu-id="b5539-203">Node.js 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="b5539-203">Trigger example in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a><span data-ttu-id="b5539-204">使用 blob 輸出繫結</span><span class="sxs-lookup"><span data-stu-id="b5539-204">Using a blob output binding</span></span>

<span data-ttu-id="b5539-205">在 .NET 函式中，您應該在函式簽章中使用 `out string` 參數，或使用下列清單中的其中一個類型。</span><span class="sxs-lookup"><span data-stu-id="b5539-205">In .NET functions, you should either use a `out string` parameter in your function signature or use one of the types in the following list.</span></span> <span data-ttu-id="b5539-206">在 Node.js 函式中，您使用 `context.bindings.<name>` 存取輸出 blob。</span><span class="sxs-lookup"><span data-stu-id="b5539-206">In Node.js functions, you access the output blob using `context.bindings.<name>`.</span></span>

<span data-ttu-id="b5539-207">在 .NET 函式中，您可以輸出至下列任何類型：</span><span class="sxs-lookup"><span data-stu-id="b5539-207">In .NET functions you can output to any of the following types:</span></span>

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a><span data-ttu-id="b5539-208">具有 blob 輸入和輸出的佇列觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="b5539-208">Queue trigger with blob input and output sample</span></span>
<span data-ttu-id="b5539-209">假設您有下列 function.json，定義了[佇列儲存體觸發程序](functions-bindings-storage-queue.md)、blob 儲存體輸入和 blob 儲存體輸出。</span><span class="sxs-lookup"><span data-stu-id="b5539-209">Suppose you have the following function.json, that defines a [Queue Storage trigger](functions-bindings-storage-queue.md), a blob storage input, and a blob storage output.</span></span> <span data-ttu-id="b5539-210">請注意 `queueTrigger` 中繼資料屬性</span><span class="sxs-lookup"><span data-stu-id="b5539-210">Notice the use of the `queueTrigger` metadata property.</span></span> <span data-ttu-id="b5539-211">在 blob 輸入和輸出 `path` 屬性中的使用方式：</span><span class="sxs-lookup"><span data-stu-id="b5539-211">in the blob input and output `path` properties:</span></span>

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

<span data-ttu-id="b5539-212">請參閱將輸入 blob 複製到輸出 blob 的語言特定範例。</span><span class="sxs-lookup"><span data-stu-id="b5539-212">See the language-specific sample that copies the input blob to the output blob.</span></span>

* [<span data-ttu-id="b5539-213">C#</span><span class="sxs-lookup"><span data-stu-id="b5539-213">C#</span></span>](#incsharp)
* [<span data-ttu-id="b5539-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="b5539-214">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a><span data-ttu-id="b5539-215">C# 中的 blob 繫結範例</span><span class="sxs-lookup"><span data-stu-id="b5539-215">Blob binding example in C#</span></span> #

```cs
// Copy blob from input to output, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a><span data-ttu-id="b5539-216">Node.js 中的 blob 繫結範例</span><span class="sxs-lookup"><span data-stu-id="b5539-216">Blob binding example in Node.js</span></span>

```javascript
// Copy blob from input to output, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="b5539-217">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b5539-217">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

