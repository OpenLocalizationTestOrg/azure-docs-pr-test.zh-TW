---
title: "上傳資料 (.NET - Azure 搜尋服務) | Microsoft Docs"
description: "了解如何使用 .NET SDK 將資料上傳至 Azure 搜尋服務中的索引。"
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: 
ms.assetid: 0e0e7e7b-7178-4c26-95c6-2fd1e8015aca
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/13/2017
ms.author: brjohnst
ms.openlocfilehash: bdd952869143c6ca6374bb9264db5bcba1f32b50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="upload-data-to-azure-search-using-the-net-sdk"></a><span data-ttu-id="0fb74-103">使用 .NET SDK 將資料上傳到 Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="0fb74-103">Upload data to Azure Search using the .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0fb74-104">概觀</span><span class="sxs-lookup"><span data-stu-id="0fb74-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="0fb74-105">.NET</span><span class="sxs-lookup"><span data-stu-id="0fb74-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="0fb74-106">REST</span><span class="sxs-lookup"><span data-stu-id="0fb74-106">REST</span></span>](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="0fb74-107">本文將說明如何使用 [Azure 搜尋服務 .NET SDK](https://aka.ms/search-sdk) 將資料匯入 Azure 搜尋服務索引。</span><span class="sxs-lookup"><span data-stu-id="0fb74-107">This article will show you how to use the [Azure Search .NET SDK](https://aka.ms/search-sdk) to import data into an Azure Search index.</span></span>

<span data-ttu-id="0fb74-108">在開始閱讀本逐步解說前，請先 [建立好 Azure 搜尋服務索引](search-what-is-an-index.md)。</span><span class="sxs-lookup"><span data-stu-id="0fb74-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span> <span data-ttu-id="0fb74-109">本文也假設您已建立 `SearchServiceClient` 物件，如 [使用 .NET SDK 建立 Azure 搜尋服務索引](search-create-index-dotnet.md#CreateSearchServiceClient)中所示。</span><span class="sxs-lookup"><span data-stu-id="0fb74-109">This article also assumes that you have already created a `SearchServiceClient` object, as shown in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span></span>

> [!NOTE]
> <span data-ttu-id="0fb74-110">本文中的所有範例程式碼均以 C# 撰寫。</span><span class="sxs-lookup"><span data-stu-id="0fb74-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="0fb74-111">您可以 [在 GitHub](http://aka.ms/search-dotnet-howto)找到完整的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="0fb74-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="0fb74-112">您也可以閱讀 [Azure 搜尋服務 .NET SDK](search-howto-dotnet-sdk.md)，以取得更詳細的範例程式碼逐步說明。</span><span class="sxs-lookup"><span data-stu-id="0fb74-112">You can also read about the [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of the sample code.</span></span>

<span data-ttu-id="0fb74-113">若要使用 .NET SDK 將文件發送到您的索引中，您必須：</span><span class="sxs-lookup"><span data-stu-id="0fb74-113">In order to push documents into your index using the .NET SDK, you will need to:</span></span>

1. <span data-ttu-id="0fb74-114">建立 `SearchIndexClient` 物件以連接到您的搜尋索引。</span><span class="sxs-lookup"><span data-stu-id="0fb74-114">Create a `SearchIndexClient` object to connect to your search index.</span></span>
2. <span data-ttu-id="0fb74-115">建立 `IndexBatch`，其中包含要新增、修改或刪除的文件。</span><span class="sxs-lookup"><span data-stu-id="0fb74-115">Create an `IndexBatch` containing the documents to be added, modified, or deleted.</span></span>
3. <span data-ttu-id="0fb74-116">呼叫 `SearchIndexClient` 的 `Documents.Index` 方法以將 `IndexBatch` 傳送到您的搜尋索引。</span><span class="sxs-lookup"><span data-stu-id="0fb74-116">Call the `Documents.Index` method of your `SearchIndexClient` to send the `IndexBatch` to your search index.</span></span>

## <a name="create-an-instance-of-the-searchindexclient-class"></a><span data-ttu-id="0fb74-117">建立 SearchIndexClient 類別的執行個體</span><span class="sxs-lookup"><span data-stu-id="0fb74-117">Create an instance of the SearchIndexClient class</span></span>
<span data-ttu-id="0fb74-118">若要使用 Azure 搜尋服務 .NET SDK 將資料匯入索引，您必須建立 `SearchIndexClient` 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="0fb74-118">To import data into your index using the Azure Search .NET SDK, you will need to create an instance of the `SearchIndexClient` class.</span></span> <span data-ttu-id="0fb74-119">您可以自己建構此執行個體，但如果您已經有 `SearchServiceClient` 執行個體可呼叫其 `Indexes.GetClient` 方法，會更為輕鬆。</span><span class="sxs-lookup"><span data-stu-id="0fb74-119">You can construct this instance yourself, but it's easier if you already have a `SearchServiceClient` instance to call its `Indexes.GetClient` method.</span></span> <span data-ttu-id="0fb74-120">例如，以下是您可從名為 `serviceClient` 的 `SearchServiceClient` 為索引 "hotels" 取得 `SearchIndexClient` 的方法：</span><span class="sxs-lookup"><span data-stu-id="0fb74-120">For example, here is how you would obtain a `SearchIndexClient` for the index named "hotels" from a `SearchServiceClient` named `serviceClient`:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="0fb74-121">在一般搜尋應用程式中，索引的管理和填入是由搜尋查詢的個別元件所處理。</span><span class="sxs-lookup"><span data-stu-id="0fb74-121">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="0fb74-122">`Indexes.GetClient` 可以很輕易填入索引，因為它可以節省提供其他 `SearchCredentials` 的麻煩。</span><span class="sxs-lookup"><span data-stu-id="0fb74-122">`Indexes.GetClient` is convenient for populating an index because it saves you the trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="0fb74-123">執行方法是將用於建立 `SearchServiceClient` 的系統管理金鑰傳遞至新的 `SearchIndexClient`。</span><span class="sxs-lookup"><span data-stu-id="0fb74-123">It does this by passing the admin key that you used to create the `SearchServiceClient` to the new `SearchIndexClient`.</span></span> <span data-ttu-id="0fb74-124">但在執行查詢的應用程式中，最好直接建立 `SearchIndexClient` ，如此一來就可以傳遞查詢金鑰，而非系統管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="0fb74-124">However, in the part of your application that executes queries, it is better to create the `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="0fb74-125">這不僅符合 [最低權限原則](https://en.wikipedia.org/wiki/Principle_of_least_privilege) ，也可以讓您的應用程式更安全。</span><span class="sxs-lookup"><span data-stu-id="0fb74-125">This is consistent with the [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) and will help to make your application more secure.</span></span> <span data-ttu-id="0fb74-126">您可以在 [Azure 搜尋服務 REST API 參考](https://docs.microsoft.com/rest/api/searchservice/)找到系統管理金鑰及查詢金鑰的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0fb74-126">You can find out more about admin keys and query keys in the [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
> 
> 

<span data-ttu-id="0fb74-127">`SearchIndexClient` 具有 `Documents` 屬性。</span><span class="sxs-lookup"><span data-stu-id="0fb74-127">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="0fb74-128">此屬性提供您新增、修改、刪除或查詢索引中文件所需的所有方法。</span><span class="sxs-lookup"><span data-stu-id="0fb74-128">This property provides all the methods you need to add, modify, delete, or query documents in your index.</span></span>

## <a name="decide-which-indexing-action-to-use"></a><span data-ttu-id="0fb74-129">決定要使用的索引編製動作</span><span class="sxs-lookup"><span data-stu-id="0fb74-129">Decide which indexing action to use</span></span>
<span data-ttu-id="0fb74-130">若要使用 .NET SDK 匯入資料，您必須將資料封裝到 `IndexBatch` 物件中。</span><span class="sxs-lookup"><span data-stu-id="0fb74-130">To import data using the .NET SDK, you will need to package up your data into an `IndexBatch` object.</span></span> <span data-ttu-id="0fb74-131">`IndexBatch` 會封裝 `IndexAction` 物件集合，每個物件各包含一份文件和一個屬性，後者會告知 Azure 搜尋服務要對該文件執行什麼動作 (上傳、合併、刪除等)。</span><span class="sxs-lookup"><span data-stu-id="0fb74-131">An `IndexBatch` encapsulates a collection of `IndexAction` objects, each of which contains a document and a property that tells Azure Search what action to perform on that document (upload, merge, delete, etc).</span></span> <span data-ttu-id="0fb74-132">依據您在以下動作中所做的選擇，每個文件內只需包含某些欄位：</span><span class="sxs-lookup"><span data-stu-id="0fb74-132">Depending on which of the below actions you choose, only certain fields must be included for each document:</span></span>

| <span data-ttu-id="0fb74-133">動作</span><span class="sxs-lookup"><span data-stu-id="0fb74-133">Action</span></span> | <span data-ttu-id="0fb74-134">說明</span><span class="sxs-lookup"><span data-stu-id="0fb74-134">Description</span></span> | <span data-ttu-id="0fb74-135">每個文件的必要欄位</span><span class="sxs-lookup"><span data-stu-id="0fb74-135">Necessary fields for each document</span></span> | <span data-ttu-id="0fb74-136">注意事項</span><span class="sxs-lookup"><span data-stu-id="0fb74-136">Notes</span></span> |
| --- | --- | --- | --- |
| `Upload` |<span data-ttu-id="0fb74-137">`Upload` 動作類似「upsert」，如果是新文件，就會插入該文件，如果文件已經存在，就會更新/取代它。</span><span class="sxs-lookup"><span data-stu-id="0fb74-137">An `Upload` action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="0fb74-138">索引鍵以及其他任何您想要定義的欄位</span><span class="sxs-lookup"><span data-stu-id="0fb74-138">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="0fb74-139">在更新/取代現有文件時，要求中未指定的欄位會將其欄位設定為 `null`。</span><span class="sxs-lookup"><span data-stu-id="0fb74-139">When updating/replacing an existing document, any field that is not specified in the request will have its field set to `null`.</span></span> <span data-ttu-id="0fb74-140">即使先前已將欄位設定為非 null 值也是一樣。</span><span class="sxs-lookup"><span data-stu-id="0fb74-140">This occurs even when the field was previously set to a non-null value.</span></span> |
| `Merge` |<span data-ttu-id="0fb74-141">使用指定的欄位更新現有文件。</span><span class="sxs-lookup"><span data-stu-id="0fb74-141">Updates an existing document with the specified fields.</span></span> <span data-ttu-id="0fb74-142">如果文件不存在於索引中，合併就會失敗。</span><span class="sxs-lookup"><span data-stu-id="0fb74-142">If the document does not exist in the index, the merge will fail.</span></span> |<span data-ttu-id="0fb74-143">索引鍵以及其他任何您想要定義的欄位</span><span class="sxs-lookup"><span data-stu-id="0fb74-143">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="0fb74-144">您在合併中指定的任何欄位將取代文件中現有的欄位。</span><span class="sxs-lookup"><span data-stu-id="0fb74-144">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="0fb74-145">這包括類型 `DataType.Collection(DataType.String)`的欄位。</span><span class="sxs-lookup"><span data-stu-id="0fb74-145">This includes fields of type `DataType.Collection(DataType.String)`.</span></span> <span data-ttu-id="0fb74-146">例如，如果文件包含欄位 `tags` 且值為 `["budget"]`，而您使用值 `["economy", "pool"]` 針對 `tags` 執行合併，則 `tags` 欄位最後的值會是 `["economy", "pool"]`。</span><span class="sxs-lookup"><span data-stu-id="0fb74-146">For example, if the document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, the final value of the `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="0fb74-147">而不會是 `["budget", "economy", "pool"]`。</span><span class="sxs-lookup"><span data-stu-id="0fb74-147">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `MergeOrUpload` |<span data-ttu-id="0fb74-148">如果含有指定索引鍵的文件已經存在於索引中，則此動作的行為會類似 `Merge`。</span><span class="sxs-lookup"><span data-stu-id="0fb74-148">This action behaves like `Merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="0fb74-149">如果文件不存在，其行為會類似新文件的 `Upload` 。</span><span class="sxs-lookup"><span data-stu-id="0fb74-149">If the document does not exist, it behaves like `Upload` with a new document.</span></span> |<span data-ttu-id="0fb74-150">索引鍵以及其他任何您想要定義的欄位</span><span class="sxs-lookup"><span data-stu-id="0fb74-150">key, plus any other fields you wish to define</span></span> |- |
| `Delete` |<span data-ttu-id="0fb74-151">從索引中移除指定的文件。</span><span class="sxs-lookup"><span data-stu-id="0fb74-151">Removes the specified document from the index.</span></span> |<span data-ttu-id="0fb74-152">僅索引鍵</span><span class="sxs-lookup"><span data-stu-id="0fb74-152">key only</span></span> |<span data-ttu-id="0fb74-153">您指定的所有欄位 (索引鍵欄位除外) 都將被忽略。</span><span class="sxs-lookup"><span data-stu-id="0fb74-153">Any fields you specify other than the key field will be ignored.</span></span> <span data-ttu-id="0fb74-154">如果您想要從文件中移除個別欄位，請改用 `Merge` ，而且只需明確地將該欄位設為 null。</span><span class="sxs-lookup"><span data-stu-id="0fb74-154">If you want to remove an individual field from a document, use `Merge` instead and simply set the field explicitly to null.</span></span> |

<span data-ttu-id="0fb74-155">您可以指定要搭配 `IndexBatch` 不同靜態方法及 `IndexAction` 類別使用的動作，如下一節所示。</span><span class="sxs-lookup"><span data-stu-id="0fb74-155">You can specify what action you want to use with the various static methods of the `IndexBatch` and `IndexAction` classes, as shown in the next section.</span></span>

## <a name="construct-your-indexbatch"></a><span data-ttu-id="0fb74-156">建構您的 IndexBatch</span><span class="sxs-lookup"><span data-stu-id="0fb74-156">Construct your IndexBatch</span></span>
<span data-ttu-id="0fb74-157">您現在已經知道可對文件執行哪些動作，並準備好建構 `IndexBatch`。</span><span class="sxs-lookup"><span data-stu-id="0fb74-157">Now that you know which actions to perform on your documents, you are ready to construct the `IndexBatch`.</span></span> <span data-ttu-id="0fb74-158">下方範例示範如何使用不同動作建立批次。</span><span class="sxs-lookup"><span data-stu-id="0fb74-158">The example below shows how to create a batch with a few different actions.</span></span> <span data-ttu-id="0fb74-159">請注意，我們的範例使用稱為 `Hotel` 的自訂類別，其對應到 "hotels" 索引中的文件。</span><span class="sxs-lookup"><span data-stu-id="0fb74-159">Note that our example uses a custom class called `Hotel` that maps to a document in the "hotels" index.</span></span>

```csharp
var actions =
    new IndexAction<Hotel>[]
    {
        IndexAction.Upload(
            new Hotel()
            {
                HotelId = "1",
                BaseRate = 199.0,
                Description = "Best hotel in town",
                DescriptionFr = "Meilleur hôtel en ville",
                HotelName = "Fancy Stay",
                Category = "Luxury",
                Tags = new[] { "pool", "view", "wifi", "concierge" },
                ParkingIncluded = false,
                SmokingAllowed = false,
                LastRenovationDate = new DateTimeOffset(2010, 6, 27, 0, 0, 0, TimeSpan.Zero),
                Rating = 5,
                Location = GeographyPoint.Create(47.678581, -122.131577)
            }),
        IndexAction.Upload(
            new Hotel()
            {
                HotelId = "2",
                BaseRate = 79.99,
                Description = "Cheapest hotel in town",
                DescriptionFr = "Hôtel le moins cher en ville",
                HotelName = "Roach Motel",
                Category = "Budget",
                Tags = new[] { "motel", "budget" },
                ParkingIncluded = true,
                SmokingAllowed = true,
                LastRenovationDate = new DateTimeOffset(1982, 4, 28, 0, 0, 0, TimeSpan.Zero),
                Rating = 1,
                Location = GeographyPoint.Create(49.678581, -122.131577)
            }),
        IndexAction.MergeOrUpload(
            new Hotel()
            {
                HotelId = "3",
                BaseRate = 129.99,
                Description = "Close to town hall and the river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

<span data-ttu-id="0fb74-160">在此案例中，我們使用了 `Upload`、`MergeOrUpload`和 `Delete` 作為搜尋動作，如同對 `IndexAction` 類別呼叫的方法所指定。</span><span class="sxs-lookup"><span data-stu-id="0fb74-160">In this case, we are using `Upload`, `MergeOrUpload`, and `Delete` as our search actions, as specified by the methods called on the `IndexAction` class.</span></span>

<span data-ttu-id="0fb74-161">假設此 "hotels" 索引範例已填入幾份文件。</span><span class="sxs-lookup"><span data-stu-id="0fb74-161">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="0fb74-162">請留意我們在使用 `MergeOrUpload` 時是如何不必指定所有可能的文件欄位，以及在使用 `Delete` 時如何僅指定文件索引鍵 (`HotelId`)。</span><span class="sxs-lookup"><span data-stu-id="0fb74-162">Note how we did not have to specify all the possible document fields when using `MergeOrUpload` and how we only specified the document key (`HotelId`) when using `Delete`.</span></span>

<span data-ttu-id="0fb74-163">另請注意，每個索引編製要求中最多只能包含 1000 份文件。</span><span class="sxs-lookup"><span data-stu-id="0fb74-163">Also, note that you can only include up to 1000 documents in a single indexing request.</span></span>

> [!NOTE]
> <span data-ttu-id="0fb74-164">在此範例中，我們在不同文件中套用了不同動作。</span><span class="sxs-lookup"><span data-stu-id="0fb74-164">In this example, we are applying different actions to different documents.</span></span> <span data-ttu-id="0fb74-165">如果您要在批次中所有文件執行相同動作，而不要呼叫 `IndexBatch.New`，則可以使用 `IndexBatch` 的其他靜態方法。</span><span class="sxs-lookup"><span data-stu-id="0fb74-165">If you wanted to perform the same actions across all documents in the batch, instead of calling `IndexBatch.New`, you could use the other static methods of `IndexBatch`.</span></span> <span data-ttu-id="0fb74-166">例如，您可以藉由呼叫 `IndexBatch.Merge`、`IndexBatch.MergeOrUpload` 或 `IndexBatch.Delete` 來建立批次。</span><span class="sxs-lookup"><span data-stu-id="0fb74-166">For example, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete`.</span></span> <span data-ttu-id="0fb74-167">這些方法會採用文件 (在此範例中為類型 `Hotel` 的物件) 集合，而非 `IndexAction` 物件。</span><span class="sxs-lookup"><span data-stu-id="0fb74-167">These methods take a collection of documents (objects of type `Hotel` in this example) instead of `IndexAction` objects.</span></span>
> 
> 

## <a name="import-data-to-the-index"></a><span data-ttu-id="0fb74-168">將資料匯入索引</span><span class="sxs-lookup"><span data-stu-id="0fb74-168">Import data to the index</span></span>
<span data-ttu-id="0fb74-169">您現在已將 `IndexBatch` 物件初始化，便可在 `SearchIndexClient` 物件上呼叫 `Documents.Index`，將其傳送到索引。</span><span class="sxs-lookup"><span data-stu-id="0fb74-169">Now that you have an initialized `IndexBatch` object, you can send it to the index by calling `Documents.Index` on your `SearchIndexClient` object.</span></span> <span data-ttu-id="0fb74-170">下列範例示範如何呼叫 `Index`，以及您必須執行的幾個額外步驟：</span><span class="sxs-lookup"><span data-stu-id="0fb74-170">The following example shows how to call `Index`, as well as some extra steps you will need to perform:</span></span>

```csharp
try
{
    indexClient.Documents.Index(batch);
}
catch (IndexBatchException e)
{
    // Sometimes when your Search service is under load, indexing will fail for some of the documents in
    // the batch. Depending on your application, you can take compensating actions like delaying and
    // retrying. For this simple demo, we just log the failed document keys and continue.
    Console.WriteLine(
        "Failed to index some of the documents: {0}",
        String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
}

Console.WriteLine("Waiting for documents to be indexed...\n");
Thread.Sleep(2000);
```

<span data-ttu-id="0fb74-171">請留意對 `Index` 方法的呼叫前後的 `try`/`catch`。</span><span class="sxs-lookup"><span data-stu-id="0fb74-171">Note the `try`/`catch` surrounding the call to the `Index` method.</span></span> <span data-ttu-id="0fb74-172">Catch 區塊會處理索引編製的重大錯誤案例。</span><span class="sxs-lookup"><span data-stu-id="0fb74-172">The catch block handles an important error case for indexing.</span></span> <span data-ttu-id="0fb74-173">如果您的 Azure Search 服務無法將 Batch 中的一些文件編制索引，則 `Documents.Index` 會擲回 `IndexBatchException`。</span><span class="sxs-lookup"><span data-stu-id="0fb74-173">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="0fb74-174">如果您在服務負載過重時編制文件的索引，就會發生此情況。</span><span class="sxs-lookup"><span data-stu-id="0fb74-174">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="0fb74-175">**我們強烈建議您在程式碼中明確處理此情況。**</span><span class="sxs-lookup"><span data-stu-id="0fb74-175">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="0fb74-176">您可以延遲，然後重新嘗試將失敗的文件編制索引，或像範例一樣加以記錄並繼續，或是根據您應用程式的資料一致性需求執行其他操作。</span><span class="sxs-lookup"><span data-stu-id="0fb74-176">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

<span data-ttu-id="0fb74-177">最後，上方範例中的程式碼會延遲兩秒。</span><span class="sxs-lookup"><span data-stu-id="0fb74-177">Finally, the code in the example above delays for two seconds.</span></span> <span data-ttu-id="0fb74-178">您的 Azure 搜尋服務中會發生非同步索引編製，因此範例應用程式必須稍待一會，才能確定文件已準備好可供搜尋。</span><span class="sxs-lookup"><span data-stu-id="0fb74-178">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span></span> <span data-ttu-id="0fb74-179">通常只有在示範、測試和範例應用程式中，才需要這類延遲。</span><span class="sxs-lookup"><span data-stu-id="0fb74-179">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

<a name="HotelClass"></a>

### <a name="how-the-net-sdk-handles-documents"></a><span data-ttu-id="0fb74-180">.NET SDK 如何處理文件</span><span class="sxs-lookup"><span data-stu-id="0fb74-180">How the .NET SDK handles documents</span></span>
<span data-ttu-id="0fb74-181">您可能想知道 Azure 搜尋服務 .NET SDK 如何能夠將使用者定義的類別執行個體 (例如 `Hotel` 上傳至索引。</span><span class="sxs-lookup"><span data-stu-id="0fb74-181">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span></span> <span data-ttu-id="0fb74-182">若要協助回答該問題，請查看 `Hotel` 類別，其對應到 [使用 .NET SDK 建立 Azure 搜尋服務索引](search-create-index-dotnet.md#DefineIndex)中定義的索引結構描述：</span><span class="sxs-lookup"><span data-stu-id="0fb74-182">To help answer that question, let's look at the `Hotel` class, which maps to the index schema defined in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#DefineIndex):</span></span>

```csharp
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }

    // ToString() method omitted for brevity...
}
```

<span data-ttu-id="0fb74-183">首先要注意的是，每個 `Hotel` 的公用屬性會對應索引定義中的欄位，但這之中有一項關鍵的差異：每個欄位的名稱會以小寫字母 (「駝峰式命名法」) 為開頭，而每個 `Hotel` 的公用屬性名稱會以大小字母 (「巴斯卡命名法」) 為開頭。</span><span class="sxs-lookup"><span data-stu-id="0fb74-183">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="0fb74-184">這在執行資料繫結、而目標結構描述在應用程式開發人員控制範圍之外的 .NET 應用程式中很常見。</span><span class="sxs-lookup"><span data-stu-id="0fb74-184">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span></span> <span data-ttu-id="0fb74-185">與其違反 .NET 命名方針，使屬性名稱為駝峰式命名法，您可以改用 `[SerializePropertyNamesAsCamelCase]` 屬性，告訴 SDK 自動將屬性名稱對應至駝峰式命名法。</span><span class="sxs-lookup"><span data-stu-id="0fb74-185">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="0fb74-186">Azure 搜尋服務 .NET SDK 使用 [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) 程式庫來將您的自訂模型物件序列化到 JSON 中，以及將您在 JSON 中的自訂模型物件還原序列化。</span><span class="sxs-lookup"><span data-stu-id="0fb74-186">The Azure Search .NET SDK uses the [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library to serialize and deserialize your custom model objects to and from JSON.</span></span> <span data-ttu-id="0fb74-187">如有需要，您可以自訂這個序列化的過程。</span><span class="sxs-lookup"><span data-stu-id="0fb74-187">You can customize this serialization if needed.</span></span> <span data-ttu-id="0fb74-188">您可以在[使用 JSON.NET 自訂序列化](search-howto-dotnet-sdk.md#JsonDotNet)中找到詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0fb74-188">You can find more details in [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span></span> <span data-ttu-id="0fb74-189">其中一個範例就是上方範例程式碼中在 `DescriptionFr` 屬性使用 `[JsonProperty]` 屬性的方式。</span><span class="sxs-lookup"><span data-stu-id="0fb74-189">One example of this is the use of the `[JsonProperty]` attribute on the `DescriptionFr` property in the sample code above.</span></span>
> 
> 

<span data-ttu-id="0fb74-190">第二個要注意的是，`Hotel` 類別為公用屬性的資料類型。</span><span class="sxs-lookup"><span data-stu-id="0fb74-190">The second important thing about the `Hotel` class are the data types of the public properties.</span></span> <span data-ttu-id="0fb74-191">這些屬性的 .NET 類型會對應至索引定義中，與其相當的欄位類型。</span><span class="sxs-lookup"><span data-stu-id="0fb74-191">The .NET types of these properties map to their equivalent field types in the index definition.</span></span> <span data-ttu-id="0fb74-192">例如，`Category` 字串屬性會對應至 `category` 欄位 (此欄位屬於 `DataType.String` 類型)。</span><span class="sxs-lookup"><span data-stu-id="0fb74-192">For example, the `Category` string property maps to the `category` field, which is of type `DataType.String`.</span></span> <span data-ttu-id="0fb74-193">`bool?` 與 `DataType.Boolean`、`DateTimeOffset?` 與 `DataType.DateTimeOffset` 等之間也有類似的類型對應。</span><span class="sxs-lookup"><span data-stu-id="0fb74-193">There are similar type mappings between `bool?` and `DataType.Boolean`, `DateTimeOffset?` and `DataType.DateTimeOffset`, and so forth.</span></span> <span data-ttu-id="0fb74-194">類型對應的特定規則和 `Documents.Get` 方法已一起記載於 [Azure 搜尋服務 .NET SDK 參考](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_)。</span><span class="sxs-lookup"><span data-stu-id="0fb74-194">The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span>

<span data-ttu-id="0fb74-195">將您自己的類別用作文件的功能雙向均適用；您也可以擷取搜尋結果，然後讓 SDK 將結果自動還原序列化為您選擇的類型，如 [下一篇文章](search-query-dotnet.md)所示。</span><span class="sxs-lookup"><span data-stu-id="0fb74-195">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as shown in the [next article](search-query-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0fb74-196">Azure 搜尋服務 .NET SDK 還支援使用 `Document` 類別的動態類型文件，也就是欄位名稱與欄位值的索引鍵/值對應。</span><span class="sxs-lookup"><span data-stu-id="0fb74-196">The Azure Search .NET SDK also supports dynamically-typed documents using the `Document` class, which is a key/value mapping of field names to field values.</span></span> <span data-ttu-id="0fb74-197">當您在設計階段卻不知道索引的結構描述時，這很實用，否則要繫結到特定模型類別會很麻煩。</span><span class="sxs-lookup"><span data-stu-id="0fb74-197">This is useful in scenarios where you don't know the index schema at design-time, or where it would be inconvenient to bind to specific model classes.</span></span> <span data-ttu-id="0fb74-198">SDK 中所有處理文件的方法，都有可搭配 `Document` 類別使用的多載，以及使用泛型類型參數的強類型多載。</span><span class="sxs-lookup"><span data-stu-id="0fb74-198">All the methods in the SDK that deal with documents have overloads that work with the `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="0fb74-199">本文的範例程式碼只使用了後者。</span><span class="sxs-lookup"><span data-stu-id="0fb74-199">Only the latter are used in the sample code in this article.</span></span>
> 
> 

<span data-ttu-id="0fb74-200">**為什麼您應該使用 Nullable 資料類型**</span><span class="sxs-lookup"><span data-stu-id="0fb74-200">**Why you should use nullable data types**</span></span>

<span data-ttu-id="0fb74-201">當您將自己的模型類別設計為可對應至 Azure 搜尋服務索引時，建議您將 `bool` 和 `int` 等的值類型屬性宣告為可為 Null (例如宣告為 `bool?`，而不是 `bool`)。</span><span class="sxs-lookup"><span data-stu-id="0fb74-201">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="0fb74-202">如果您使用不可為 Null 的屬性，則必須保證  索引中沒有任何文件的對應欄位包含 Null 值。</span><span class="sxs-lookup"><span data-stu-id="0fb74-202">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="0fb74-203">SDK 和 Azure 搜尋服務都不會協助您強制執行這項規定。</span><span class="sxs-lookup"><span data-stu-id="0fb74-203">Neither the SDK nor the Azure Search service will help you to enforce this.</span></span>

<span data-ttu-id="0fb74-204">這不只是假設性的問題：如果您在類型為 `DataType.Int32` 的現有索引中新增欄位，</span><span class="sxs-lookup"><span data-stu-id="0fb74-204">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `DataType.Int32`.</span></span> <span data-ttu-id="0fb74-205">更新索引定義之後，所有文件對於該新的欄位具有 null 值 (因為所有類型在 Azure 搜尋服務中都可為 null)。</span><span class="sxs-lookup"><span data-stu-id="0fb74-205">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="0fb74-206">如果您接著對該欄位使用 `int` 屬性不可為 Null 的模型類別，就會在嘗試擷取文件時得到類似這樣的 `JsonSerializationException`：</span><span class="sxs-lookup"><span data-stu-id="0fb74-206">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="0fb74-207">因此，我們建議您在模型類別中使用可為 Null 的類型，來做為最佳作法。</span><span class="sxs-lookup"><span data-stu-id="0fb74-207">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fb74-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0fb74-208">Next steps</span></span>
<span data-ttu-id="0fb74-209">在填入 Azure 搜尋服務索引後，您就可以開始發出查詢來搜尋文件。</span><span class="sxs-lookup"><span data-stu-id="0fb74-209">After populating your Azure Search index, you will be ready to start issuing queries to search for documents.</span></span> <span data-ttu-id="0fb74-210">如需詳細資料，請參閱 [查詢 Azure 搜尋服務索引](search-query-overview.md) 。</span><span class="sxs-lookup"><span data-stu-id="0fb74-210">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>

