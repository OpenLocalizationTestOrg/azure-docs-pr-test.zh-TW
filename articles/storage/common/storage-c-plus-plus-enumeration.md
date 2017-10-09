---
title: "以 c + + 的儲存體用戶端程式庫 hello aaaList Azure 儲存體資源 |Microsoft 文件"
description: "了解如何 toouse hello 列出 Microsoft Azure 儲存體用戶端程式庫的應用程式開發介面對於 c + + tooenumerate 容器，blob、 佇列時，資料表和實體。"
documentationcenter: .net
services: storage
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: 33563639-2945-4567-9254-bc4a7e80698f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: dineshm
ms.openlocfilehash: a76a5ce3cd690f32914f8f0c1f64273f13c5063e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="list-azure-storage-resources-in-c"></a><span data-ttu-id="b60d6-103">以 C++ 列出 Azure 儲存體資源</span><span class="sxs-lookup"><span data-stu-id="b60d6-103">List Azure Storage resources in C++</span></span>
<span data-ttu-id="b60d6-104">列出作業是與 Azure 儲存體金鑰 toomany 開發案例。</span><span class="sxs-lookup"><span data-stu-id="b60d6-104">Listing operations are key toomany development scenarios with Azure Storage.</span></span> <span data-ttu-id="b60d6-105">本文說明如何 toomost 有效率地列舉使用 hello 列出應用程式開發介面的 c + + hello Microsoft Azure 儲存體用戶端程式庫中提供的 Azure 儲存體中的物件。</span><span class="sxs-lookup"><span data-stu-id="b60d6-105">This article describes how toomost efficiently enumerate objects in Azure Storage using hello listing APIs provided in hello Microsoft Azure Storage Client Library for C++.</span></span>

> [!NOTE]
> <span data-ttu-id="b60d6-106">本指南的目標 hello Azure 儲存體用戶端程式庫的 c + + 版本 2.x，可透過[NuGet](http://www.nuget.org/packages/wastorage)或[GitHub](https://github.com/Azure/azure-storage-cpp)。</span><span class="sxs-lookup"><span data-stu-id="b60d6-106">This guide targets hello Azure Storage Client Library for C++ version 2.x, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

<span data-ttu-id="b60d6-107">hello 儲存體用戶端程式庫提供各種方法 toolist 或 Azure 儲存體中的查詢物件。</span><span class="sxs-lookup"><span data-stu-id="b60d6-107">hello Storage Client Library provides a variety of methods toolist or query objects in Azure Storage.</span></span> <span data-ttu-id="b60d6-108">本文解決 hello 下列案例：</span><span class="sxs-lookup"><span data-stu-id="b60d6-108">This article addresses hello following scenarios:</span></span>

* <span data-ttu-id="b60d6-109">列出帳戶中的容器</span><span class="sxs-lookup"><span data-stu-id="b60d6-109">List containers in an account</span></span>
* <span data-ttu-id="b60d6-110">列出容器或虛擬 Blob 目錄中的 Blob</span><span class="sxs-lookup"><span data-stu-id="b60d6-110">List blobs in a container or virtual blob directory</span></span>
* <span data-ttu-id="b60d6-111">列出帳戶中的佇列</span><span class="sxs-lookup"><span data-stu-id="b60d6-111">List queues in an account</span></span>
* <span data-ttu-id="b60d6-112">列出帳戶中的資料表</span><span class="sxs-lookup"><span data-stu-id="b60d6-112">List tables in an account</span></span>
* <span data-ttu-id="b60d6-113">查詢資料表中的實體</span><span class="sxs-lookup"><span data-stu-id="b60d6-113">Query entities in a table</span></span>

<span data-ttu-id="b60d6-114">每個方法會使用不同案例的不同多載來顯示。</span><span class="sxs-lookup"><span data-stu-id="b60d6-114">Each of these methods is shown using different overloads for different scenarios.</span></span>

## <a name="asynchronous-versus-synchronous"></a><span data-ttu-id="b60d6-115">同步與非同步</span><span class="sxs-lookup"><span data-stu-id="b60d6-115">Asynchronous versus synchronous</span></span>
<span data-ttu-id="b60d6-116">因為 c + + 的儲存體用戶端程式庫 hello 之上 hello [REST c + + 程式庫](https://github.com/Microsoft/cpprestsdk)，我們使用原本就支援非同步作業[pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html)。</span><span class="sxs-lookup"><span data-stu-id="b60d6-116">Because hello Storage Client Library for C++ is built on top of hello [C++ REST library](https://github.com/Microsoft/cpprestsdk), we inherently support asynchronous operations by using [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span></span> <span data-ttu-id="b60d6-117">例如：</span><span class="sxs-lookup"><span data-stu-id="b60d6-117">For example:</span></span>

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

<span data-ttu-id="b60d6-118">同步作業包裝 hello 對應的非同步作業：</span><span class="sxs-lookup"><span data-stu-id="b60d6-118">Synchronous operations wrap hello corresponding asynchronous operations:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

<span data-ttu-id="b60d6-119">如果您正在使用多個執行緒的應用程式或服務，我們建議您使用 hello 非同步 Api 而不用直接建立執行緒 toocall hello 同步處理應用程式開發介面，會大幅影響您的效能。</span><span class="sxs-lookup"><span data-stu-id="b60d6-119">If you are working with multiple threading applications or services, we recommend that you use hello async APIs directly instead of creating a thread toocall hello sync APIs, which significantly impacts your performance.</span></span>

## <a name="segmented-listing"></a><span data-ttu-id="b60d6-120">分段列表</span><span class="sxs-lookup"><span data-stu-id="b60d6-120">Segmented listing</span></span>
<span data-ttu-id="b60d6-121">hello 標尺的雲端儲存體需要分割的清單。</span><span class="sxs-lookup"><span data-stu-id="b60d6-121">hello scale of cloud storage requires segmented listing.</span></span> <span data-ttu-id="b60d6-122">例如，在 Azure blob 容器中可有超過 100 萬個 Blob，或在 Azure 資料表中可有超過 10 億個實體。</span><span class="sxs-lookup"><span data-stu-id="b60d6-122">For example, you can have over a million blobs in an Azure blob container or over a billion entities in an Azure Table.</span></span> <span data-ttu-id="b60d6-123">這些不是理論上的數字，而是實際的客戶使用量案例。</span><span class="sxs-lookup"><span data-stu-id="b60d6-123">These are not theoretical numbers, but real customer usage cases.</span></span>

<span data-ttu-id="b60d6-124">因此，這是不可行 toolist 單一回應中的所有物件。</span><span class="sxs-lookup"><span data-stu-id="b60d6-124">It is therefore impractical toolist all objects in a single response.</span></span> <span data-ttu-id="b60d6-125">反而，您可以使用分頁列出物件。</span><span class="sxs-lookup"><span data-stu-id="b60d6-125">Instead, you can list objects using paging.</span></span> <span data-ttu-id="b60d6-126">每個 hello 列出應用程式開發介面有*分割*多載。</span><span class="sxs-lookup"><span data-stu-id="b60d6-126">Each of hello listing APIs has a *segmented* overload.</span></span>

<span data-ttu-id="b60d6-127">hello 分割的清單作業回應包括：</span><span class="sxs-lookup"><span data-stu-id="b60d6-127">hello response for a segmented listing operation includes:</span></span>

* <span data-ttu-id="b60d6-128"><i>_segment</i>，其中包含 hello 的單一呼叫 toohello 列出 API 傳回的結果集。</span><span class="sxs-lookup"><span data-stu-id="b60d6-128"><i>_segment</i>, which contains hello set of results returned for a single call toohello listing API.</span></span>
* <span data-ttu-id="b60d6-129">*continuation_token*，toohello 下一次呼叫傳遞順序 tooget hello 下一頁結果中。</span><span class="sxs-lookup"><span data-stu-id="b60d6-129">*continuation_token*, which is passed toohello next call in order tooget hello next page of results.</span></span> <span data-ttu-id="b60d6-130">當有沒有更多結果 tooreturn 時，hello 接續 token 為 null。</span><span class="sxs-lookup"><span data-stu-id="b60d6-130">When there are no more results tooreturn, hello continuation token is null.</span></span>

<span data-ttu-id="b60d6-131">例如，一般呼叫 toolist 容器中的所有 blob 可能看都起來像是下列程式碼片段的 hello。</span><span class="sxs-lookup"><span data-stu-id="b60d6-131">For example, a typical call toolist all blobs in a container may look like hello following code snippet.</span></span> <span data-ttu-id="b60d6-132">會提供 hello 程式碼我們[範例](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span><span class="sxs-lookup"><span data-stu-id="b60d6-132">hello code is available in our [samples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span></span>

```cpp
// List blobs in hello blob container
azure::storage::continuation_token token;
do
{
    azure::storage::list_blob_item_segment segment = container.list_blobs_segmented(token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_diretory(it->as_directory());
    }
}

    token = segment.continuation_token();
}
while (!token.empty());
```

<span data-ttu-id="b60d6-133">請注意 hello 參數可以控制在網頁中傳回結果的 hello 數目*max_results*在 hello 多載中的每個應用程式開發介面，例如：</span><span class="sxs-lookup"><span data-stu-id="b60d6-133">Note that hello number of results returned in a page can be controlled by hello parameter *max_results* in hello overload of each API, for example:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

<span data-ttu-id="b60d6-134">如果您未指定 hello *max_results*參數，會傳回最大值 too5000 結果的單一頁面中的 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="b60d6-134">If you do not specify hello *max_results* parameter, hello default maximum value of up too5000 results is returned in a single page.</span></span>

<span data-ttu-id="b60d6-135">也請注意，對 Azure 資料表儲存體的查詢可能會傳回任何記錄或較少的記錄比 hello hello 值*max_results*參數所指定，即使不是空的 hello 接續 token。</span><span class="sxs-lookup"><span data-stu-id="b60d6-135">Also note that a query against Azure Table storage may return no records, or fewer records than hello value of hello *max_results* parameter that you specified, even if hello continuation token is not empty.</span></span> <span data-ttu-id="b60d6-136">其中一個原因可能是該 hello 查詢無法在五秒內完成。</span><span class="sxs-lookup"><span data-stu-id="b60d6-136">One reason might be that hello query could not complete in five seconds.</span></span> <span data-ttu-id="b60d6-137">只要 hello 接續 token 不是空的 hello 查詢仍應繼續執行，您的程式碼不應該假設 hello 大小的結果區段。</span><span class="sxs-lookup"><span data-stu-id="b60d6-137">As long as hello continuation token is not empty, hello query should continue, and your code should not assume hello size of segment results.</span></span>

<span data-ttu-id="b60d6-138">hello 建議的模式，在大部分情況下的撰寫程式碼已分割，藉以提供明確的清單，或查詢，進行與 hello 服務 tooeach 要求的回應方式。</span><span class="sxs-lookup"><span data-stu-id="b60d6-138">hello recommended coding pattern for most scenarios is segmented listing, which provides explicit progress of listing or querying, and how hello service responds tooeach request.</span></span> <span data-ttu-id="b60d6-139">特別是對於 c + + 應用程式或服務，較低層級的 hello 列出進度的控制項可以協助控制記憶體和效能。</span><span class="sxs-lookup"><span data-stu-id="b60d6-139">Particularly for C++ applications or services, lower-level control of hello listing progress may help control memory and performance.</span></span>

## <a name="greedy-listing"></a><span data-ttu-id="b60d6-140">窮盡列表</span><span class="sxs-lookup"><span data-stu-id="b60d6-140">Greedy listing</span></span>
<span data-ttu-id="b60d6-141">舊版的 hello c + + 的儲存體用戶端程式庫 (版本 0.5.0 預覽及更早版本) 包含非分割清單應用程式開發介面的資料表和佇列，如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="b60d6-141">Earlier versions of hello Storage Client Library for C++ (versions 0.5.0 Preview and earlier) included non-segmented listing APIs for tables and queues, as in hello following example:</span></span>

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

<span data-ttu-id="b60d6-142">這些方法已做為分段 API 的包裝函式實作。</span><span class="sxs-lookup"><span data-stu-id="b60d6-142">These methods were implemented as wrappers of segmented APIs.</span></span> <span data-ttu-id="b60d6-143">分割清單的每個回應，hello 程式碼會附加 hello 結果 tooa 向量，並掃描 hello 完整容器之後，傳回所有結果。</span><span class="sxs-lookup"><span data-stu-id="b60d6-143">For each response of segmented listing, hello code appended hello results tooa vector and returned all results after hello full containers were scanned.</span></span>

<span data-ttu-id="b60d6-144">這種方法可能運作時 hello 儲存體帳戶或資料表包含少數的物件。</span><span class="sxs-lookup"><span data-stu-id="b60d6-144">This approach might work when hello storage account or table contains a small number of objects.</span></span> <span data-ttu-id="b60d6-145">不過，增加的 hello 物件數目，hello 所需的記憶體可能會增加無限制，因為仍在記憶體中的所有結果。</span><span class="sxs-lookup"><span data-stu-id="b60d6-145">However, with an increase in hello number of objects, hello memory required could increase without limit, because all results remained in memory.</span></span> <span data-ttu-id="b60d6-146">一項列出作業可能需要很長的時間，在哪一個 hello 期間呼叫端具有其進度的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b60d6-146">One listing operation can take a very long time, during which hello caller had no information about its progress.</span></span>

<span data-ttu-id="b60d6-147">這些窮盡列出 hello SDK 中的應用程式開發介面請勿存在於 C#、 Java 或 hello JavaScript Node.js 環境。</span><span class="sxs-lookup"><span data-stu-id="b60d6-147">These greedy listing APIs in hello SDK do not exist in C#, Java, or hello JavaScript Node.js environment.</span></span> <span data-ttu-id="b60d6-148">tooavoid hello 潛在的問題使用這些窮盡 Api，它們會在中移除版本 0.6.0 預覽。</span><span class="sxs-lookup"><span data-stu-id="b60d6-148">tooavoid hello potential issues of using these greedy APIs, we removed them in version 0.6.0 Preview.</span></span>

<span data-ttu-id="b60d6-149">如果您的程式碼呼叫這些窮盡 API：</span><span class="sxs-lookup"><span data-stu-id="b60d6-149">If your code is calling these greedy APIs:</span></span>

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

<span data-ttu-id="b60d6-150">您應修改您的程式碼 toouse hello 分割列出應用程式開發介面：</span><span class="sxs-lookup"><span data-stu-id="b60d6-150">Then you should modify your code toouse hello segmented listing APIs:</span></span>

```cpp
azure::storage::continuation_token token;
do
{
    azure::storage::table_query_segment segment = table.execute_query_segmented(query, token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
    {
        process_entity(*it);
    }

    token = segment.continuation_token();
} while (!token.empty());
```

<span data-ttu-id="b60d6-151">藉由指定 hello *max_results* hello 區段的參數，您就可以平衡要求 hello 數目與您的應用程式的記憶體使用量 toomeet 效能考量之間。</span><span class="sxs-lookup"><span data-stu-id="b60d6-151">By specifying hello *max_results* parameter of hello segment, you can balance between hello numbers of requests and memory usage toomeet performance considerations for your application.</span></span>

<span data-ttu-id="b60d6-152">此外，如果您使用不同客層之的清單的 Api，但 hello 資料儲存在 「 窮盡 」 樣式中的本機集合，我們也強烈建議您重構您的程式碼 toohandle 仔細大規模的本機集合中儲存資料。</span><span class="sxs-lookup"><span data-stu-id="b60d6-152">Additionally, if you're using segmented listing APIs, but store hello data in a local collection in a "greedy" style, we also strongly recommend that you refactor your code toohandle storing data in a local collection carefully at scale.</span></span>

## <a name="lazy-listing"></a><span data-ttu-id="b60d6-153">延遲列表</span><span class="sxs-lookup"><span data-stu-id="b60d6-153">Lazy listing</span></span>
<span data-ttu-id="b60d6-154">雖然窮盡清單產生潛在問題，並方便如果 hello 容器中沒有太多物件。</span><span class="sxs-lookup"><span data-stu-id="b60d6-154">Although greedy listing raised potential issues, it is convenient if there are not too many objects in hello container.</span></span>

<span data-ttu-id="b60d6-155">如果您也使用 C# 或 Oracle Java Sdk，您應該熟悉 hello 可列舉的程式設計模型，它提供了延遲樣式清單，其中 hello 的特定位移的資料會只擷取在必要時。</span><span class="sxs-lookup"><span data-stu-id="b60d6-155">If you're also using C# or Oracle Java SDKs, you should be familiar with hello Enumerable programming model, which offers a lazy-style listing, where hello data at a certain offset is only fetched if it is required.</span></span> <span data-ttu-id="b60d6-156">C + + hello 迭代器為基礎的範本也會提供類似的方法。</span><span class="sxs-lookup"><span data-stu-id="b60d6-156">In C++, hello iterator-based template also provides a similar approach.</span></span>

<span data-ttu-id="b60d6-157">典型的延遲列表 API (以 **list_blobs** 為例) 如下所示：</span><span class="sxs-lookup"><span data-stu-id="b60d6-157">A typical lazy listing API, using **list_blobs** as an example, looks like this:</span></span>

```cpp
list_blob_item_iterator list_blobs() const;
```

<span data-ttu-id="b60d6-158">會使用 hello 延遲清單模式的一般程式碼片段看起來可能像這樣：</span><span class="sxs-lookup"><span data-stu-id="b60d6-158">A typical code snippet that uses hello lazy listing pattern might look like this:</span></span>

```cpp
// List blobs in hello blob container
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_directory(it->as_directory());
    }
}
```

<span data-ttu-id="b60d6-159">請注意，延遲列表僅可用於同步模式。</span><span class="sxs-lookup"><span data-stu-id="b60d6-159">Note that lazy listing is only available in synchronous mode.</span></span>

<span data-ttu-id="b60d6-160">相較於窮盡列表，延遲列表只會在必要時提取資料。</span><span class="sxs-lookup"><span data-stu-id="b60d6-160">Compared with greedy listing, lazy listing fetches data only when necessary.</span></span> <span data-ttu-id="b60d6-161">Hello 幕後提取資料從 Azure 儲存體 hello 的下一個迭代器將移至下一個區段時，才。</span><span class="sxs-lookup"><span data-stu-id="b60d6-161">Under hello covers, it fetches data from Azure Storage only when hello next iterator moves into next segment.</span></span> <span data-ttu-id="b60d6-162">因此，記憶體使用量控制界限大小，且 hello 作業將會十分快速。</span><span class="sxs-lookup"><span data-stu-id="b60d6-162">Therefore, memory usage is controlled with a bounded size, and hello operation is fast.</span></span>

<span data-ttu-id="b60d6-163">延遲清單應用程式開發介面包含在 hello 儲存體用戶端程式庫的 c + + 的版本 2.2.0。</span><span class="sxs-lookup"><span data-stu-id="b60d6-163">Lazy listing APIs are included in hello Storage Client Library for C++ in version 2.2.0.</span></span>

## <a name="conclusion"></a><span data-ttu-id="b60d6-164">結論</span><span class="sxs-lookup"><span data-stu-id="b60d6-164">Conclusion</span></span>
<span data-ttu-id="b60d6-165">在本文中，我們討論過 c + + 應用程式開發介面清單 hello 儲存體用戶端程式庫中的各種物件的不同多的載。</span><span class="sxs-lookup"><span data-stu-id="b60d6-165">In this article, we discussed different overloads for listing APIs for various objects in hello Storage Client Library for C++ .</span></span> <span data-ttu-id="b60d6-166">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="b60d6-166">toosummarize:</span></span>

* <span data-ttu-id="b60d6-167">在多個執行緒的案例中，強烈建議使用非同步 API。</span><span class="sxs-lookup"><span data-stu-id="b60d6-167">Async APIs are strongly recommended under multiple threading scenarios.</span></span>
* <span data-ttu-id="b60d6-168">在大部分的案例中，建議使用分段列表。</span><span class="sxs-lookup"><span data-stu-id="b60d6-168">Segmented listing is recommended for most scenarios.</span></span>
* <span data-ttu-id="b60d6-169">延遲的清單是依現狀 hello 文件庫中的同步案例中的便利包裝函式。</span><span class="sxs-lookup"><span data-stu-id="b60d6-169">Lazy listing is provided in hello library as a convenient wrapper in synchronous scenarios.</span></span>
* <span data-ttu-id="b60d6-170">窮盡清單不建議使用，並已經移除了 hello 程式庫。</span><span class="sxs-lookup"><span data-stu-id="b60d6-170">Greedy listing is not recommended and has been removed from hello library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b60d6-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b60d6-171">Next steps</span></span>
<span data-ttu-id="b60d6-172">如需 c + + Azure 儲存體和用戶端程式庫的詳細資訊，請參閱下列資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="b60d6-172">For more information about Azure Storage and Client Library for C++, see hello following resources.</span></span>

* [<span data-ttu-id="b60d6-173">如何 toouse 從 c + + 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="b60d6-173">How toouse Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="b60d6-174">如何 toouse 從 c + + 的資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="b60d6-174">How toouse Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="b60d6-175">如何 toouse 佇列儲存體從 c + +</span><span class="sxs-lookup"><span data-stu-id="b60d6-175">How toouse Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="b60d6-176">Azure Storage Client Library for C++ API 文件。</span><span class="sxs-lookup"><span data-stu-id="b60d6-176">Azure Storage Client Library for C++ API documentation.</span></span>](http://azure.github.io/azure-storage-cpp/)
* [<span data-ttu-id="b60d6-177">Azure 儲存體團隊部落格</span><span class="sxs-lookup"><span data-stu-id="b60d6-177">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="b60d6-178">Azure 儲存體文件</span><span class="sxs-lookup"><span data-stu-id="b60d6-178">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)

