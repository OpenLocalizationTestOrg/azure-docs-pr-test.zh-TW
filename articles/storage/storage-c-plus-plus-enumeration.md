---
title: "使用 Storage Client Library for C++ 列出 Azure 儲存體資源 | Microsoft Docs"
description: "了解如何使用 Microsoft Azure Storage Client Library for C++ 中的列表 API 來列舉容器、Blob、佇列、資料表和實體。"
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
ms.openlocfilehash: 4a4ac7938989f821c092379aff3085f5e440d1c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="list-azure-storage-resources-in-c"></a><span data-ttu-id="c2b77-103">以 C++ 列出 Azure 儲存體資源</span><span class="sxs-lookup"><span data-stu-id="c2b77-103">List Azure Storage resources in C++</span></span>
<span data-ttu-id="c2b77-104">列表作業是許多使用 Azure 儲存體的開發案例的關鍵。</span><span class="sxs-lookup"><span data-stu-id="c2b77-104">Listing operations are key to many development scenarios with Azure Storage.</span></span> <span data-ttu-id="c2b77-105">本文說明如何使用 Microsoft Azure Storage Client Library for C++ 中提供的列表 API，以最有效率的方式列舉 Azure 儲存體中的物件。</span><span class="sxs-lookup"><span data-stu-id="c2b77-105">This article describes how to most efficiently enumerate objects in Azure Storage using the listing APIs provided in the Microsoft Azure Storage Client Library for C++.</span></span>

> [!NOTE]
> <span data-ttu-id="c2b77-106">本指南以 Azure Storage Client Library for C++ 2.x 版為對象 (其可透過 [NuGet](http://www.nuget.org/packages/wastorage) 或 [GitHub](https://github.com/Azure/azure-storage-cpp) 取得)。</span><span class="sxs-lookup"><span data-stu-id="c2b77-106">This guide targets the Azure Storage Client Library for C++ version 2.x, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

<span data-ttu-id="c2b77-107">Storage Client Library 提供各種方法來列出或查詢 Azure 儲存體中的物件。</span><span class="sxs-lookup"><span data-stu-id="c2b77-107">The Storage Client Library provides a variety of methods to list or query objects in Azure Storage.</span></span> <span data-ttu-id="c2b77-108">本文說明下列案例：</span><span class="sxs-lookup"><span data-stu-id="c2b77-108">This article addresses the following scenarios:</span></span>

* <span data-ttu-id="c2b77-109">列出帳戶中的容器</span><span class="sxs-lookup"><span data-stu-id="c2b77-109">List containers in an account</span></span>
* <span data-ttu-id="c2b77-110">列出容器或虛擬 Blob 目錄中的 Blob</span><span class="sxs-lookup"><span data-stu-id="c2b77-110">List blobs in a container or virtual blob directory</span></span>
* <span data-ttu-id="c2b77-111">列出帳戶中的佇列</span><span class="sxs-lookup"><span data-stu-id="c2b77-111">List queues in an account</span></span>
* <span data-ttu-id="c2b77-112">列出帳戶中的資料表</span><span class="sxs-lookup"><span data-stu-id="c2b77-112">List tables in an account</span></span>
* <span data-ttu-id="c2b77-113">查詢資料表中的實體</span><span class="sxs-lookup"><span data-stu-id="c2b77-113">Query entities in a table</span></span>

<span data-ttu-id="c2b77-114">每個方法會使用不同案例的不同多載來顯示。</span><span class="sxs-lookup"><span data-stu-id="c2b77-114">Each of these methods is shown using different overloads for different scenarios.</span></span>

## <a name="asynchronous-versus-synchronous"></a><span data-ttu-id="c2b77-115">同步與非同步</span><span class="sxs-lookup"><span data-stu-id="c2b77-115">Asynchronous versus synchronous</span></span>
<span data-ttu-id="c2b77-116">因為 Storage Client Library for C++ 的建置基礎為 [C++ REST 程式庫](https://github.com/Microsoft/cpprestsdk)，所以我們原本就使用 [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html) 支援非同步作業。</span><span class="sxs-lookup"><span data-stu-id="c2b77-116">Because the Storage Client Library for C++ is built on top of the [C++ REST library](https://github.com/Microsoft/cpprestsdk), we inherently support asynchronous operations by using [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span></span> <span data-ttu-id="c2b77-117">例如：</span><span class="sxs-lookup"><span data-stu-id="c2b77-117">For example:</span></span>

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

<span data-ttu-id="c2b77-118">同步作業會包裝對應的非同步作業：</span><span class="sxs-lookup"><span data-stu-id="c2b77-118">Synchronous operations wrap the corresponding asynchronous operations:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

<span data-ttu-id="c2b77-119">如果您正在使用多個執行緒的應用程式或服務，建議您直接使用非同步 API，而不是建立執行緒來呼叫同步 API，這會大幅影響您的效能。</span><span class="sxs-lookup"><span data-stu-id="c2b77-119">If you are working with multiple threading applications or services, we recommend that you use the async APIs directly instead of creating a thread to call the sync APIs, which significantly impacts your performance.</span></span>

## <a name="segmented-listing"></a><span data-ttu-id="c2b77-120">分段列表</span><span class="sxs-lookup"><span data-stu-id="c2b77-120">Segmented listing</span></span>
<span data-ttu-id="c2b77-121">雲端儲存體的級別需要分段列表。</span><span class="sxs-lookup"><span data-stu-id="c2b77-121">The scale of cloud storage requires segmented listing.</span></span> <span data-ttu-id="c2b77-122">例如，在 Azure blob 容器中可有超過 100 萬個 Blob，或在 Azure 資料表中可有超過 10 億個實體。</span><span class="sxs-lookup"><span data-stu-id="c2b77-122">For example, you can have over a million blobs in an Azure blob container or over a billion entities in an Azure Table.</span></span> <span data-ttu-id="c2b77-123">這些不是理論上的數字，而是實際的客戶使用量案例。</span><span class="sxs-lookup"><span data-stu-id="c2b77-123">These are not theoretical numbers, but real customer usage cases.</span></span>

<span data-ttu-id="c2b77-124">因此，列出單一回應中的所有物件並不切實際。</span><span class="sxs-lookup"><span data-stu-id="c2b77-124">It is therefore impractical to list all objects in a single response.</span></span> <span data-ttu-id="c2b77-125">反而，您可以使用分頁列出物件。</span><span class="sxs-lookup"><span data-stu-id="c2b77-125">Instead, you can list objects using paging.</span></span> <span data-ttu-id="c2b77-126">每個列表 API 都有 *分段* 多載。</span><span class="sxs-lookup"><span data-stu-id="c2b77-126">Each of the listing APIs has a *segmented* overload.</span></span>

<span data-ttu-id="c2b77-127">分段列表作業的回應包含：</span><span class="sxs-lookup"><span data-stu-id="c2b77-127">The response for a segmented listing operation includes:</span></span>

* <span data-ttu-id="c2b77-128"><i>_segment</i>，其中包含針對列表 API 的單一呼叫所傳回的結果集。</span><span class="sxs-lookup"><span data-stu-id="c2b77-128"><i>_segment</i>, which contains the set of results returned for a single call to the listing API.</span></span>
* <span data-ttu-id="c2b77-129">continuation_token，其會傳遞給下一個呼叫，以便取得下一頁的結果。</span><span class="sxs-lookup"><span data-stu-id="c2b77-129">*continuation_token*, which is passed to the next call in order to get the next page of results.</span></span> <span data-ttu-id="c2b77-130">沒有可傳回的結果時，接續 Token 為 null。</span><span class="sxs-lookup"><span data-stu-id="c2b77-130">When there are no more results to return, the continuation token is null.</span></span>

<span data-ttu-id="c2b77-131">例如，列出容器中所有 Blob 的典型呼叫可能如下列程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="c2b77-131">For example, a typical call to list all blobs in a container may look like the following code snippet.</span></span> <span data-ttu-id="c2b77-132">此程式碼可在我們的 [範例](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp)中取得：</span><span class="sxs-lookup"><span data-stu-id="c2b77-132">The code is available in our [samples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span></span>

```cpp
// List blobs in the blob container
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

<span data-ttu-id="c2b77-133">請注意，一個頁面傳回的結果數目可由每個 API 的多載中的參數 max_results 所控制，例如：</span><span class="sxs-lookup"><span data-stu-id="c2b77-133">Note that the number of results returned in a page can be controlled by the parameter *max_results* in the overload of each API, for example:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

<span data-ttu-id="c2b77-134">如果您未指定 max_results 參數，則會在單一頁面中傳回多達 5000 筆結果的預設最大值。</span><span class="sxs-lookup"><span data-stu-id="c2b77-134">If you do not specify the *max_results* parameter, the default maximum value of up to 5000 results is returned in a single page.</span></span>

<span data-ttu-id="c2b77-135">也請注意，對 Azure 資料表儲存體的查詢可能不會傳回任何記錄，或傳回少於您指定之 max_results 參數值的記錄 (即使接續 Token 不是空的)。</span><span class="sxs-lookup"><span data-stu-id="c2b77-135">Also note that a query against Azure Table storage may return no records, or fewer records than the value of the *max_results* parameter that you specified, even if the continuation token is not empty.</span></span> <span data-ttu-id="c2b77-136">其中一個原因可能是查詢無法在五秒內完成。</span><span class="sxs-lookup"><span data-stu-id="c2b77-136">One reason might be that the query could not complete in five seconds.</span></span> <span data-ttu-id="c2b77-137">只要接續 Token 不是空的，查詢就應該繼續進行，而您的程式碼不得假設區段結果的大小。</span><span class="sxs-lookup"><span data-stu-id="c2b77-137">As long as the continuation token is not empty, the query should continue, and your code should not assume the size of segment results.</span></span>

<span data-ttu-id="c2b77-138">大多數案例的建議編碼模式為分段列表，可以提供明確的列表或查詢進度，以及服務回應每個要求的方式。</span><span class="sxs-lookup"><span data-stu-id="c2b77-138">The recommended coding pattern for most scenarios is segmented listing, which provides explicit progress of listing or querying, and how the service responds to each request.</span></span> <span data-ttu-id="c2b77-139">尤其是 C++ 應用程式或服務，列表進度的較低層級控制項有助於控制記憶體和效能。</span><span class="sxs-lookup"><span data-stu-id="c2b77-139">Particularly for C++ applications or services, lower-level control of the listing progress may help control memory and performance.</span></span>

## <a name="greedy-listing"></a><span data-ttu-id="c2b77-140">窮盡列表</span><span class="sxs-lookup"><span data-stu-id="c2b77-140">Greedy listing</span></span>
<span data-ttu-id="c2b77-141">舊版的 Storage Client Library for C++ (0.5.0 預覽版或更早版本) 包含了適用於資料表和佇列的非分段列表 API，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="c2b77-141">Earlier versions of the Storage Client Library for C++ (versions 0.5.0 Preview and earlier) included non-segmented listing APIs for tables and queues, as in the following example:</span></span>

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

<span data-ttu-id="c2b77-142">這些方法已做為分段 API 的包裝函式實作。</span><span class="sxs-lookup"><span data-stu-id="c2b77-142">These methods were implemented as wrappers of segmented APIs.</span></span> <span data-ttu-id="c2b77-143">對於分段列表的每個回應，程式碼會將結果附加至向量，並傳回掃描完整容器後的所有結果。</span><span class="sxs-lookup"><span data-stu-id="c2b77-143">For each response of segmented listing, the code appended the results to a vector and returned all results after the full containers were scanned.</span></span>

<span data-ttu-id="c2b77-144">當儲存體帳戶或資料表包含少量物件時，這個方法可能有用。</span><span class="sxs-lookup"><span data-stu-id="c2b77-144">This approach might work when the storage account or table contains a small number of objects.</span></span> <span data-ttu-id="c2b77-145">不過，隨著物件數目的增加，所需的記憶體可能會無所限制的增加，因為所有結果都會保留在記憶體中。</span><span class="sxs-lookup"><span data-stu-id="c2b77-145">However, with an increase in the number of objects, the memory required could increase without limit, because all results remained in memory.</span></span> <span data-ttu-id="c2b77-146">一項列表作業可能需要很長的時間，在這段期間內呼叫端沒有其進度的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c2b77-146">One listing operation can take a very long time, during which the caller had no information about its progress.</span></span>

<span data-ttu-id="c2b77-147">SDK 中的這些窮盡列表 API 不存在於 C#、Java 或 JavaScript Node.js 環境中。</span><span class="sxs-lookup"><span data-stu-id="c2b77-147">These greedy listing APIs in the SDK do not exist in C#, Java, or the JavaScript Node.js environment.</span></span> <span data-ttu-id="c2b77-148">為了避免使用這些窮盡 API 的潛在問題，我們已在 0.6.0 預覽版中予以移除。</span><span class="sxs-lookup"><span data-stu-id="c2b77-148">To avoid the potential issues of using these greedy APIs, we removed them in version 0.6.0 Preview.</span></span>

<span data-ttu-id="c2b77-149">如果您的程式碼呼叫這些窮盡 API：</span><span class="sxs-lookup"><span data-stu-id="c2b77-149">If your code is calling these greedy APIs:</span></span>

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

<span data-ttu-id="c2b77-150">您就應該修改程式碼以使用分段列表 API：</span><span class="sxs-lookup"><span data-stu-id="c2b77-150">Then you should modify your code to use the segmented listing APIs:</span></span>

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

<span data-ttu-id="c2b77-151">指定區段的 max_results 參數，即可平衡要求數目與記憶體使用量，以符合您的應用程式的效能考量。</span><span class="sxs-lookup"><span data-stu-id="c2b77-151">By specifying the *max_results* parameter of the segment, you can balance between the numbers of requests and memory usage to meet performance considerations for your application.</span></span>

<span data-ttu-id="c2b77-152">此外，如果您使用分段列表 API，但以「窮盡」樣式將資料儲存在本機集合中，也強烈建議您重整您的程式碼，以便仔細地將資料大規模儲存在本機集合中。</span><span class="sxs-lookup"><span data-stu-id="c2b77-152">Additionally, if you're using segmented listing APIs, but store the data in a local collection in a "greedy" style, we also strongly recommend that you refactor your code to handle storing data in a local collection carefully at scale.</span></span>

## <a name="lazy-listing"></a><span data-ttu-id="c2b77-153">延遲列表</span><span class="sxs-lookup"><span data-stu-id="c2b77-153">Lazy listing</span></span>
<span data-ttu-id="c2b77-154">雖然窮盡列表引發了潛在的問題，但如果容器中沒有太多物件，則很方便。</span><span class="sxs-lookup"><span data-stu-id="c2b77-154">Although greedy listing raised potential issues, it is convenient if there are not too many objects in the container.</span></span>

<span data-ttu-id="c2b77-155">如果您也使用 C# 或 Oracle Java SDK，您應該熟悉可提供延遲樣式列表的「可列舉」程式設計模型，其中特定位移的資料只會在必要時提取。</span><span class="sxs-lookup"><span data-stu-id="c2b77-155">If you're also using C# or Oracle Java SDKs, you should be familiar with the Enumerable programming model, which offers a lazy-style listing, where the data at a certain offset is only fetched if it is required.</span></span> <span data-ttu-id="c2b77-156">在 C++ 中，以迭代器為基礎的範本也會提供類似的方法。</span><span class="sxs-lookup"><span data-stu-id="c2b77-156">In C++, the iterator-based template also provides a similar approach.</span></span>

<span data-ttu-id="c2b77-157">典型的延遲列表 API (以 **list_blobs** 為例) 如下所示：</span><span class="sxs-lookup"><span data-stu-id="c2b77-157">A typical lazy listing API, using **list_blobs** as an example, looks like this:</span></span>

```cpp
list_blob_item_iterator list_blobs() const;
```

<span data-ttu-id="c2b77-158">使用延遲列表模式的典型程式碼片段可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="c2b77-158">A typical code snippet that uses the lazy listing pattern might look like this:</span></span>

```cpp
// List blobs in the blob container
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

<span data-ttu-id="c2b77-159">請注意，延遲列表僅可用於同步模式。</span><span class="sxs-lookup"><span data-stu-id="c2b77-159">Note that lazy listing is only available in synchronous mode.</span></span>

<span data-ttu-id="c2b77-160">相較於窮盡列表，延遲列表只會在必要時提取資料。</span><span class="sxs-lookup"><span data-stu-id="c2b77-160">Compared with greedy listing, lazy listing fetches data only when necessary.</span></span> <span data-ttu-id="c2b77-161">實際上，只有在下一個迭代器移至下一個區段時，它才會從 Azure 儲存體提取資料。</span><span class="sxs-lookup"><span data-stu-id="c2b77-161">Under the covers, it fetches data from Azure Storage only when the next iterator moves into next segment.</span></span> <span data-ttu-id="c2b77-162">因此，記憶體使用量會控制在有限的大小內，且作業速度很快。</span><span class="sxs-lookup"><span data-stu-id="c2b77-162">Therefore, memory usage is controlled with a bounded size, and the operation is fast.</span></span>

<span data-ttu-id="c2b77-163">延遲列表 API 已包含在 Storage Client Library for C++ 2.2.0 版中。</span><span class="sxs-lookup"><span data-stu-id="c2b77-163">Lazy listing APIs are included in the Storage Client Library for C++ in version 2.2.0.</span></span>

## <a name="conclusion"></a><span data-ttu-id="c2b77-164">結論</span><span class="sxs-lookup"><span data-stu-id="c2b77-164">Conclusion</span></span>
<span data-ttu-id="c2b77-165">在本文中，我們針對 Storage Client Library for C++ 中的各種物件，討論了列表 API 的不同多載。</span><span class="sxs-lookup"><span data-stu-id="c2b77-165">In this article, we discussed different overloads for listing APIs for various objects in the Storage Client Library for C++ .</span></span> <span data-ttu-id="c2b77-166">總結：</span><span class="sxs-lookup"><span data-stu-id="c2b77-166">To summarize:</span></span>

* <span data-ttu-id="c2b77-167">在多個執行緒的案例中，強烈建議使用非同步 API。</span><span class="sxs-lookup"><span data-stu-id="c2b77-167">Async APIs are strongly recommended under multiple threading scenarios.</span></span>
* <span data-ttu-id="c2b77-168">在大部分的案例中，建議使用分段列表。</span><span class="sxs-lookup"><span data-stu-id="c2b77-168">Segmented listing is recommended for most scenarios.</span></span>
* <span data-ttu-id="c2b77-169">程式庫中提供的延遲列表是同步案例中的方便包裝函式。</span><span class="sxs-lookup"><span data-stu-id="c2b77-169">Lazy listing is provided in the library as a convenient wrapper in synchronous scenarios.</span></span>
* <span data-ttu-id="c2b77-170">不建議使用窮盡列表，並已從程式庫中移除。</span><span class="sxs-lookup"><span data-stu-id="c2b77-170">Greedy listing is not recommended and has been removed from the library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2b77-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c2b77-171">Next steps</span></span>
<span data-ttu-id="c2b77-172">如需 Azure Storage Client Library for C++ 的詳細資訊，請參閱下列資源。</span><span class="sxs-lookup"><span data-stu-id="c2b77-172">For more information about Azure Storage and Client Library for C++, see the following resources.</span></span>

* [<span data-ttu-id="c2b77-173">如何使用 C++ 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="c2b77-173">How to use Blob Storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="c2b77-174">如何使用 C++ 的資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="c2b77-174">How to use Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="c2b77-175">如何使用 C++ 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="c2b77-175">How to use Queue Storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="c2b77-176">Azure Storage Client Library for C++ API 文件。</span><span class="sxs-lookup"><span data-stu-id="c2b77-176">Azure Storage Client Library for C++ API documentation.</span></span>](http://azure.github.io/azure-storage-cpp/)
* [<span data-ttu-id="c2b77-177">Azure 儲存體團隊部落格</span><span class="sxs-lookup"><span data-stu-id="c2b77-177">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="c2b77-178">Azure 儲存體文件</span><span class="sxs-lookup"><span data-stu-id="c2b77-178">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)

