---
title: "aaa 」 上傳資料 (.NET 的 Azure 搜尋) |Microsoft 文件 」"
description: "了解如何在 Azure 搜尋中使用 tooupload 資料 tooan 索引 hello.NET SDK。"
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
ms.openlocfilehash: 78ddbefb522884d1f61cb275c25c091487aee639
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-net-sdk"></a><span data-ttu-id="f03c5-103">上傳資料 tooAzure 搜尋使用 hello.NET SDK</span><span class="sxs-lookup"><span data-stu-id="f03c5-103">Upload data tooAzure Search using hello .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f03c5-104">概觀</span><span class="sxs-lookup"><span data-stu-id="f03c5-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="f03c5-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f03c5-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="f03c5-106">REST</span><span class="sxs-lookup"><span data-stu-id="f03c5-106">REST</span></span>](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="f03c5-107">這篇文章將示範如何 toouse hello [Azure 搜尋.NET SDK](https://aka.ms/search-sdk) tooimport 資料到 Azure 搜尋索引。</span><span class="sxs-lookup"><span data-stu-id="f03c5-107">This article will show you how toouse hello [Azure Search .NET SDK](https://aka.ms/search-sdk) tooimport data into an Azure Search index.</span></span>

<span data-ttu-id="f03c5-108">在開始閱讀本逐步解說前，請先 [建立好 Azure 搜尋服務索引](search-what-is-an-index.md)。</span><span class="sxs-lookup"><span data-stu-id="f03c5-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span> <span data-ttu-id="f03c5-109">本文也假設您已經建立`SearchServiceClient`物件中所示[建立 Azure 搜尋索引，使用.NET SDK hello](search-create-index-dotnet.md#CreateSearchServiceClient)。</span><span class="sxs-lookup"><span data-stu-id="f03c5-109">This article also assumes that you have already created a `SearchServiceClient` object, as shown in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span></span>

> [!NOTE]
> <span data-ttu-id="f03c5-110">本文中的所有範例程式碼均以 C# 撰寫。</span><span class="sxs-lookup"><span data-stu-id="f03c5-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="f03c5-111">您可以找到 hello 完整的原始程式碼[GitHub 上](http://aka.ms/search-dotnet-howto)。</span><span class="sxs-lookup"><span data-stu-id="f03c5-111">You can find hello full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="f03c5-112">您也可以閱讀 hello [Azure 搜尋.NET SDK](search-howto-dotnet-sdk.md) for 的詳細逐步 hello 範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="f03c5-112">You can also read about hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of hello sample code.</span></span>

<span data-ttu-id="f03c5-113">在訂單 toopush 文件至您的索引使用 hello.NET SDK，您必須：</span><span class="sxs-lookup"><span data-stu-id="f03c5-113">In order toopush documents into your index using hello .NET SDK, you will need to:</span></span>

1. <span data-ttu-id="f03c5-114">建立`SearchIndexClient`物件 tooconnect tooyour 搜尋索引。</span><span class="sxs-lookup"><span data-stu-id="f03c5-114">Create a `SearchIndexClient` object tooconnect tooyour search index.</span></span>
2. <span data-ttu-id="f03c5-115">建立`IndexBatch`包含 hello 文件 toobe 新增、 修改或刪除。</span><span class="sxs-lookup"><span data-stu-id="f03c5-115">Create an `IndexBatch` containing hello documents toobe added, modified, or deleted.</span></span>
3. <span data-ttu-id="f03c5-116">呼叫 hello`Documents.Index`方法您`SearchIndexClient`toosend hello `IndexBatch` tooyour 搜尋索引。</span><span class="sxs-lookup"><span data-stu-id="f03c5-116">Call hello `Documents.Index` method of your `SearchIndexClient` toosend hello `IndexBatch` tooyour search index.</span></span>

## <a name="create-an-instance-of-hello-searchindexclient-class"></a><span data-ttu-id="f03c5-117">建立 hello SearchIndexClient 類別的執行個體</span><span class="sxs-lookup"><span data-stu-id="f03c5-117">Create an instance of hello SearchIndexClient class</span></span>
<span data-ttu-id="f03c5-118">索引使用 tooimport 資料 hello Azure 搜尋.NET SDK，您就需要 toocreate hello 的執行個體`SearchIndexClient`類別。</span><span class="sxs-lookup"><span data-stu-id="f03c5-118">tooimport data into your index using hello Azure Search .NET SDK, you will need toocreate an instance of hello `SearchIndexClient` class.</span></span> <span data-ttu-id="f03c5-119">您可以建構此執行個體，但它更容易如果您已經有`SearchServiceClient`執行個體 toocall 其`Indexes.GetClient`方法。</span><span class="sxs-lookup"><span data-stu-id="f03c5-119">You can construct this instance yourself, but it's easier if you already have a `SearchServiceClient` instance toocall its `Indexes.GetClient` method.</span></span> <span data-ttu-id="f03c5-120">例如，以下是您想要如何取得`SearchIndexClient`hello 索引從名為 「 旅館"`SearchServiceClient`名為`serviceClient`:</span><span class="sxs-lookup"><span data-stu-id="f03c5-120">For example, here is how you would obtain a `SearchIndexClient` for hello index named "hotels" from a `SearchServiceClient` named `serviceClient`:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="f03c5-121">在一般搜尋應用程式中，索引的管理和填入是由搜尋查詢的個別元件所處理。</span><span class="sxs-lookup"><span data-stu-id="f03c5-121">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="f03c5-122">`Indexes.GetClient`填入索引，因為它會將儲存您的方便 hello 提供另一個問題`SearchCredentials`。</span><span class="sxs-lookup"><span data-stu-id="f03c5-122">`Indexes.GetClient` is convenient for populating an index because it saves you hello trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="f03c5-123">其做法是傳遞 hello 管理金鑰，您使用的 toocreate hello `SearchServiceClient` toohello 新`SearchIndexClient`。</span><span class="sxs-lookup"><span data-stu-id="f03c5-123">It does this by passing hello admin key that you used toocreate hello `SearchServiceClient` toohello new `SearchIndexClient`.</span></span> <span data-ttu-id="f03c5-124">不過，在 hello 部分中執行查詢的應用程式，它是較佳的 toocreate hello`SearchIndexClient`直接，讓您可以傳入的查詢索引鍵，而不是管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="f03c5-124">However, in hello part of your application that executes queries, it is better toocreate hello `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="f03c5-125">這是與 hello 一致[最低權限原則](https://en.wikipedia.org/wiki/Principle_of_least_privilege)，都能協助您更安全的應用程式 toomake。</span><span class="sxs-lookup"><span data-stu-id="f03c5-125">This is consistent with hello [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) and will help toomake your application more secure.</span></span> <span data-ttu-id="f03c5-126">您可以進一步了解系統管理金鑰和查詢索引鍵中 hello [Azure 搜尋 REST API 參考](https://docs.microsoft.com/rest/api/searchservice/)。</span><span class="sxs-lookup"><span data-stu-id="f03c5-126">You can find out more about admin keys and query keys in hello [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
> 
> 

<span data-ttu-id="f03c5-127">`SearchIndexClient` 具有 `Documents` 屬性。</span><span class="sxs-lookup"><span data-stu-id="f03c5-127">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="f03c5-128">這個屬性提供所有 hello 方法需要 tooadd、 修改、 刪除或查詢文件索引中。</span><span class="sxs-lookup"><span data-stu-id="f03c5-128">This property provides all hello methods you need tooadd, modify, delete, or query documents in your index.</span></span>

## <a name="decide-which-indexing-action-toouse"></a><span data-ttu-id="f03c5-129">決定哪個索引動作 toouse</span><span class="sxs-lookup"><span data-stu-id="f03c5-129">Decide which indexing action toouse</span></span>
<span data-ttu-id="f03c5-130">使用.NET SDK hello tooimport 資料，您需要 toopackage 組成資料到`IndexBatch`物件。</span><span class="sxs-lookup"><span data-stu-id="f03c5-130">tooimport data using hello .NET SDK, you will need toopackage up your data into an `IndexBatch` object.</span></span> <span data-ttu-id="f03c5-131">`IndexBatch`封裝的集合`IndexAction`物件，其中每個包含文件和屬性，會告訴 Azure 搜尋哪些動作 tooperform 文 （上傳、 合併、 刪除等等）。</span><span class="sxs-lookup"><span data-stu-id="f03c5-131">An `IndexBatch` encapsulates a collection of `IndexAction` objects, each of which contains a document and a property that tells Azure Search what action tooperform on that document (upload, merge, delete, etc).</span></span> <span data-ttu-id="f03c5-132">取決於哪些 hello 下列您選擇的動作，只有特定欄位必須包含每個文件：</span><span class="sxs-lookup"><span data-stu-id="f03c5-132">Depending on which of hello below actions you choose, only certain fields must be included for each document:</span></span>

| <span data-ttu-id="f03c5-133">動作</span><span class="sxs-lookup"><span data-stu-id="f03c5-133">Action</span></span> | <span data-ttu-id="f03c5-134">說明</span><span class="sxs-lookup"><span data-stu-id="f03c5-134">Description</span></span> | <span data-ttu-id="f03c5-135">每個文件的必要欄位</span><span class="sxs-lookup"><span data-stu-id="f03c5-135">Necessary fields for each document</span></span> | <span data-ttu-id="f03c5-136">注意事項</span><span class="sxs-lookup"><span data-stu-id="f03c5-136">Notes</span></span> |
| --- | --- | --- | --- |
| `Upload` |<span data-ttu-id="f03c5-137">`Upload`動作是類似 tooan"upsert"(如果它是新插入和更新/取代如果它存在 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="f03c5-137">An `Upload` action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="f03c5-138">索引鍵，再加上您想 toodefine 的任何其他欄位</span><span class="sxs-lookup"><span data-stu-id="f03c5-138">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="f03c5-139">當更新/取代現有的文件，hello 要求中未指定任何欄位將會有其欄位太設定`null`。</span><span class="sxs-lookup"><span data-stu-id="f03c5-139">When updating/replacing an existing document, any field that is not specified in hello request will have its field set too`null`.</span></span> <span data-ttu-id="f03c5-140">這是即使 hello 欄位先前設定 tooa 非 null 值。</span><span class="sxs-lookup"><span data-stu-id="f03c5-140">This occurs even when hello field was previously set tooa non-null value.</span></span> |
| `Merge` |<span data-ttu-id="f03c5-141">更新現有文件以 hello 指定欄位。</span><span class="sxs-lookup"><span data-stu-id="f03c5-141">Updates an existing document with hello specified fields.</span></span> <span data-ttu-id="f03c5-142">Hello 文件不存在 hello 索引中，如果 hello 合併將會失敗。</span><span class="sxs-lookup"><span data-stu-id="f03c5-142">If hello document does not exist in hello index, hello merge will fail.</span></span> |<span data-ttu-id="f03c5-143">索引鍵，再加上您想 toodefine 的任何其他欄位</span><span class="sxs-lookup"><span data-stu-id="f03c5-143">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="f03c5-144">您在合併中指定任何欄位將會取代 hello hello 文件中的現有欄位。</span><span class="sxs-lookup"><span data-stu-id="f03c5-144">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="f03c5-145">這包括類型 `DataType.Collection(DataType.String)`的欄位。</span><span class="sxs-lookup"><span data-stu-id="f03c5-145">This includes fields of type `DataType.Collection(DataType.String)`.</span></span> <span data-ttu-id="f03c5-146">例如，如果 hello 文件包含欄位`tags`值`["budget"]`和執行的合併值`["economy", "pool"]`的`tags`，hello hello 的最終值`tags`欄位就是`["economy", "pool"]`。</span><span class="sxs-lookup"><span data-stu-id="f03c5-146">For example, if hello document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, hello final value of hello `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="f03c5-147">而不會是 `["budget", "economy", "pool"]`。</span><span class="sxs-lookup"><span data-stu-id="f03c5-147">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `MergeOrUpload` |<span data-ttu-id="f03c5-148">此動作的行為類似`Merge`如果 hello 索引中的文件以 hello 給定索引鍵已經存在。</span><span class="sxs-lookup"><span data-stu-id="f03c5-148">This action behaves like `Merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="f03c5-149">如果 hello 文件不存在，它的行為類似`Upload`與新的文件。</span><span class="sxs-lookup"><span data-stu-id="f03c5-149">If hello document does not exist, it behaves like `Upload` with a new document.</span></span> |<span data-ttu-id="f03c5-150">索引鍵，再加上您想 toodefine 的任何其他欄位</span><span class="sxs-lookup"><span data-stu-id="f03c5-150">key, plus any other fields you wish toodefine</span></span> |- |
| `Delete` |<span data-ttu-id="f03c5-151">從 hello 索引中移除 hello 指定文件。</span><span class="sxs-lookup"><span data-stu-id="f03c5-151">Removes hello specified document from hello index.</span></span> |<span data-ttu-id="f03c5-152">僅索引鍵</span><span class="sxs-lookup"><span data-stu-id="f03c5-152">key only</span></span> |<span data-ttu-id="f03c5-153">您指定其他非 hello 索引鍵欄位將會忽略所有的欄位。</span><span class="sxs-lookup"><span data-stu-id="f03c5-153">Any fields you specify other than hello key field will be ignored.</span></span> <span data-ttu-id="f03c5-154">如果您想 tooremove 個別欄位從 文件，請使用`Merge`相反地，並直接將 hello 欄位明確 toonull。</span><span class="sxs-lookup"><span data-stu-id="f03c5-154">If you want tooremove an individual field from a document, use `Merge` instead and simply set hello field explicitly toonull.</span></span> |

<span data-ttu-id="f03c5-155">您可以指定要與 toouse 何種動作 hello 各種的靜態方法的 hello`IndexBatch`和`IndexAction`類別 hello 下一節中所示。</span><span class="sxs-lookup"><span data-stu-id="f03c5-155">You can specify what action you want toouse with hello various static methods of hello `IndexBatch` and `IndexAction` classes, as shown in hello next section.</span></span>

## <a name="construct-your-indexbatch"></a><span data-ttu-id="f03c5-156">建構您的 IndexBatch</span><span class="sxs-lookup"><span data-stu-id="f03c5-156">Construct your IndexBatch</span></span>
<span data-ttu-id="f03c5-157">現在您知道哪些動作 tooperform 上您的文件時，您就準備好 tooconstruct hello `IndexBatch`。</span><span class="sxs-lookup"><span data-stu-id="f03c5-157">Now that you know which actions tooperform on your documents, you are ready tooconstruct hello `IndexBatch`.</span></span> <span data-ttu-id="f03c5-158">如何 hello 範例所示 toocreate 具有幾個不同的動作的批次。</span><span class="sxs-lookup"><span data-stu-id="f03c5-158">hello example below shows how toocreate a batch with a few different actions.</span></span> <span data-ttu-id="f03c5-159">請注意我們的範例會使用自訂類別，稱為`Hotel`對應 tooa hello 「 旅館"索引中的文件。</span><span class="sxs-lookup"><span data-stu-id="f03c5-159">Note that our example uses a custom class called `Hotel` that maps tooa document in hello "hotels" index.</span></span>

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
                Description = "Close tootown hall and hello river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

<span data-ttu-id="f03c5-160">在此情況下，我們會使用`Upload`， `MergeOrUpload`，和`Delete`我們搜尋指定的動作，hello hello 上呼叫的方法為`IndexAction`類別。</span><span class="sxs-lookup"><span data-stu-id="f03c5-160">In this case, we are using `Upload`, `MergeOrUpload`, and `Delete` as our search actions, as specified by hello methods called on hello `IndexAction` class.</span></span>

<span data-ttu-id="f03c5-161">假設此 "hotels" 索引範例已填入幾份文件。</span><span class="sxs-lookup"><span data-stu-id="f03c5-161">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="f03c5-162">請注意如何我們沒有 toospecify hello 可能文件的所有欄位時使用`MergeOrUpload`以及我們僅指定 hello 文件索引鍵的方式 (`HotelId`) 時使用`Delete`。</span><span class="sxs-lookup"><span data-stu-id="f03c5-162">Note how we did not have toospecify all hello possible document fields when using `MergeOrUpload` and how we only specified hello document key (`HotelId`) when using `Delete`.</span></span>

<span data-ttu-id="f03c5-163">此外，請注意，您可以只包含單一索引要求中 too1000 文件。</span><span class="sxs-lookup"><span data-stu-id="f03c5-163">Also, note that you can only include up too1000 documents in a single indexing request.</span></span>

> [!NOTE]
> <span data-ttu-id="f03c5-164">在此範例中，我們會套用不同的動作 toodifferent 文件。</span><span class="sxs-lookup"><span data-stu-id="f03c5-164">In this example, we are applying different actions toodifferent documents.</span></span> <span data-ttu-id="f03c5-165">如果您想 tooperform hello 相同動作的 hello 批次，而不是呼叫中的所有文件`IndexBatch.New`，您可以使用 hello 其他的靜態方法`IndexBatch`。</span><span class="sxs-lookup"><span data-stu-id="f03c5-165">If you wanted tooperform hello same actions across all documents in hello batch, instead of calling `IndexBatch.New`, you could use hello other static methods of `IndexBatch`.</span></span> <span data-ttu-id="f03c5-166">例如，您可以藉由呼叫 `IndexBatch.Merge`、`IndexBatch.MergeOrUpload` 或 `IndexBatch.Delete` 來建立批次。</span><span class="sxs-lookup"><span data-stu-id="f03c5-166">For example, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete`.</span></span> <span data-ttu-id="f03c5-167">這些方法會採用文件 (在此範例中為類型 `Hotel` 的物件) 集合，而非 `IndexAction` 物件。</span><span class="sxs-lookup"><span data-stu-id="f03c5-167">These methods take a collection of documents (objects of type `Hotel` in this example) instead of `IndexAction` objects.</span></span>
> 
> 

## <a name="import-data-toohello-index"></a><span data-ttu-id="f03c5-168">匯入資料 toohello 索引</span><span class="sxs-lookup"><span data-stu-id="f03c5-168">Import data toohello index</span></span>
<span data-ttu-id="f03c5-169">既然您已初始化`IndexBatch`物件，您可以將它傳送 toohello 索引藉由呼叫`Documents.Index`上您`SearchIndexClient`物件。</span><span class="sxs-lookup"><span data-stu-id="f03c5-169">Now that you have an initialized `IndexBatch` object, you can send it toohello index by calling `Documents.Index` on your `SearchIndexClient` object.</span></span> <span data-ttu-id="f03c5-170">下列範例會示範如何 hello toocall `Index`，以及您需要 tooperform 一些額外步驟：</span><span class="sxs-lookup"><span data-stu-id="f03c5-170">hello following example shows how toocall `Index`, as well as some extra steps you will need tooperform:</span></span>

```csharp
try
{
    indexClient.Documents.Index(batch);
}
catch (IndexBatchException e)
{
    // Sometimes when your Search service is under load, indexing will fail for some of hello documents in
    // hello batch. Depending on your application, you can take compensating actions like delaying and
    // retrying. For this simple demo, we just log hello failed document keys and continue.
    Console.WriteLine(
        "Failed tooindex some of hello documents: {0}",
        String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
}

Console.WriteLine("Waiting for documents toobe indexed...\n");
Thread.Sleep(2000);
```

<span data-ttu-id="f03c5-171">請注意 hello `try` / `catch`周圍 hello 呼叫 toohello`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="f03c5-171">Note hello `try`/`catch` surrounding hello call toohello `Index` method.</span></span> <span data-ttu-id="f03c5-172">hello catch 區塊處理編製索引的重要的錯誤案例。</span><span class="sxs-lookup"><span data-stu-id="f03c5-172">hello catch block handles an important error case for indexing.</span></span> <span data-ttu-id="f03c5-173">如果您的 Azure 搜尋服務失敗的 tooindex hello 的批次中的 hello 某些文件`IndexBatchException`，所擲回`Documents.Index`。</span><span class="sxs-lookup"><span data-stu-id="f03c5-173">If your Azure Search service fails tooindex some of hello documents in hello batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="f03c5-174">如果您在服務負載過重時編制文件的索引，就會發生此情況。</span><span class="sxs-lookup"><span data-stu-id="f03c5-174">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="f03c5-175">**我們強烈建議您在程式碼中明確處理此情況。**</span><span class="sxs-lookup"><span data-stu-id="f03c5-175">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="f03c5-176">您可以延遲，然後重試失敗，索引 hello 文件或您可以記錄並繼續像 hello 範例會執行，或者，您可以執行根據您的應用程式資料的一致性需求的其他項目。</span><span class="sxs-lookup"><span data-stu-id="f03c5-176">You can delay and then retry indexing hello documents that failed, or you can log and continue like hello sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

<span data-ttu-id="f03c5-177">最後，hello 範例的程式碼 hello 上面兩秒的延遲。</span><span class="sxs-lookup"><span data-stu-id="f03c5-177">Finally, hello code in hello example above delays for two seconds.</span></span> <span data-ttu-id="f03c5-178">索引會發生以非同步方式在 Azure 搜尋服務中，所以 hello 範例應用程式需要 toowait hello 文件可供搜尋簡短時間 tooensure。</span><span class="sxs-lookup"><span data-stu-id="f03c5-178">Indexing happens asynchronously in your Azure Search service, so hello sample application needs toowait a short time tooensure that hello documents are available for searching.</span></span> <span data-ttu-id="f03c5-179">通常只有在示範、測試和範例應用程式中，才需要這類延遲。</span><span class="sxs-lookup"><span data-stu-id="f03c5-179">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

<a name="HotelClass"></a>

### <a name="how-hello-net-sdk-handles-documents"></a><span data-ttu-id="f03c5-180">Hello.NET SDK 的文件的處理方式</span><span class="sxs-lookup"><span data-stu-id="f03c5-180">How hello .NET SDK handles documents</span></span>
<span data-ttu-id="f03c5-181">您可能想知道 hello Azure 搜尋.NET SDK 無法 tooupload 之類的使用者定義的類別執行個體的方式`Hotel`toohello 索引。</span><span class="sxs-lookup"><span data-stu-id="f03c5-181">You may be wondering how hello Azure Search .NET SDK is able tooupload instances of a user-defined class like `Hotel` toohello index.</span></span> <span data-ttu-id="f03c5-182">toohelp 回答這個問題，讓我們看看 hello`Hotel`對應 toohello 索引結構描述中定義的類別[建立 Azure 搜尋索引，使用.NET SDK hello](search-create-index-dotnet.md#DefineIndex):</span><span class="sxs-lookup"><span data-stu-id="f03c5-182">toohelp answer that question, let's look at hello `Hotel` class, which maps toohello index schema defined in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#DefineIndex):</span></span>

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

<span data-ttu-id="f03c5-183">hello 首先 toonotice 在於每一個公用屬性的`Hotel`對應 tooa 欄位在 hello 索引定義中，但有一點很重要： hello 名稱的每個公開時 hello 每個欄位的名稱會以小寫字母 （「 camel 命名法的情況"），啟動屬性`Hotel`開頭的大寫字母 （「 Pascal 大小寫 」）。</span><span class="sxs-lookup"><span data-stu-id="f03c5-183">hello first thing toonotice is that each public property of `Hotel` corresponds tooa field in hello index definition, but with one crucial difference: hello name of each field starts with a lower-case letter ("camel case"), while hello name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="f03c5-184">這是常見的案例中執行資料繫結其中 hello 目標結構描述是控制外部 hello hello 應用程式開發人員的.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f03c5-184">This is a common scenario in .NET applications that perform data-binding where hello target schema is outside hello control of hello application developer.</span></span> <span data-ttu-id="f03c5-185">而不是讓 tooviolate hello.NET 命名指導方針進行屬性名稱依照 camel 命名法的情況下，您可以告訴 hello SDK toomap hello 屬性名稱 toocamel 案例會自動以 hello`[SerializePropertyNamesAsCamelCase]`屬性。</span><span class="sxs-lookup"><span data-stu-id="f03c5-185">Rather than having tooviolate hello .NET naming guidelines by making property names camel-case, you can tell hello SDK toomap hello property names toocamel-case automatically with hello `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="f03c5-186">hello Azure 搜尋.NET SDK 會使用 hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize 程式庫和您自訂的模型物件 tooand，從 JSON 還原序列化。</span><span class="sxs-lookup"><span data-stu-id="f03c5-186">hello Azure Search .NET SDK uses hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library tooserialize and deserialize your custom model objects tooand from JSON.</span></span> <span data-ttu-id="f03c5-187">如有需要，您可以自訂這個序列化的過程。</span><span class="sxs-lookup"><span data-stu-id="f03c5-187">You can customize this serialization if needed.</span></span> <span data-ttu-id="f03c5-188">您可以在[使用 JSON.NET 自訂序列化](search-howto-dotnet-sdk.md#JsonDotNet)中找到詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f03c5-188">You can find more details in [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span></span> <span data-ttu-id="f03c5-189">一個範例是使用 hello hello`[JsonProperty]`屬性 hello`DescriptionFr`上述的 hello 範例程式碼中的屬性。</span><span class="sxs-lookup"><span data-stu-id="f03c5-189">One example of this is hello use of hello `[JsonProperty]` attribute on hello `DescriptionFr` property in hello sample code above.</span></span>
> 
> 

<span data-ttu-id="f03c5-190">hello 第二個重要好處 hello`Hotel`類別是 hello hello 公用屬性資料類型。</span><span class="sxs-lookup"><span data-stu-id="f03c5-190">hello second important thing about hello `Hotel` class are hello data types of hello public properties.</span></span> <span data-ttu-id="f03c5-191">這些屬性的 hello.NET 型別對應 tootheir hello 索引定義中的對等的欄位類型。</span><span class="sxs-lookup"><span data-stu-id="f03c5-191">hello .NET types of these properties map tootheir equivalent field types in hello index definition.</span></span> <span data-ttu-id="f03c5-192">例如，hello`Category`字串屬性會對應 toohello`category`欄位的型別`DataType.String`。</span><span class="sxs-lookup"><span data-stu-id="f03c5-192">For example, hello `Category` string property maps toohello `category` field, which is of type `DataType.String`.</span></span> <span data-ttu-id="f03c5-193">`bool?` 與 `DataType.Boolean`、`DateTimeOffset?` 與 `DataType.DateTimeOffset` 等之間也有類似的類型對應。</span><span class="sxs-lookup"><span data-stu-id="f03c5-193">There are similar type mappings between `bool?` and `DataType.Boolean`, `DateTimeOffset?` and `DataType.DateTimeOffset`, and so forth.</span></span> <span data-ttu-id="f03c5-194">hello hello 型別對應的特定規則都會記錄以 hello`Documents.Get`方法在 hello [Azure 搜尋.NET SDK 參考](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_)。</span><span class="sxs-lookup"><span data-stu-id="f03c5-194">hello specific rules for hello type mapping are documented with hello `Documents.Get` method in hello [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span>

<span data-ttu-id="f03c5-195">此功能 toouse 雙向; 運作自己的類別為文件您也可以擷取搜尋結果，且擁有 hello SDK 自動還原序列化這些 tooa 類型您選擇的 hello 中所示[下一篇文章](search-query-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="f03c5-195">This ability toouse your own classes as documents works in both directions; You can also retrieve search results and have hello SDK automatically deserialize them tooa type of your choice, as shown in hello [next article](search-query-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f03c5-196">hello Azure 搜尋.NET SDK 也支援動態具類型的文件使用 hello`Document`類別，這是索引鍵/值對應的欄位名稱 toofield 值。</span><span class="sxs-lookup"><span data-stu-id="f03c5-196">hello Azure Search .NET SDK also supports dynamically-typed documents using hello `Document` class, which is a key/value mapping of field names toofield values.</span></span> <span data-ttu-id="f03c5-197">您不知道 hello 索引結構描述在設計階段，或者它會是很不方便 toobind toospecific 模型類別，這是非常實用。</span><span class="sxs-lookup"><span data-stu-id="f03c5-197">This is useful in scenarios where you don't know hello index schema at design-time, or where it would be inconvenient toobind toospecific model classes.</span></span> <span data-ttu-id="f03c5-198">中的所有 hello 方法 hello SDK 文件處理都具有多載，搭配 hello`Document`類別，以及接受泛型型別參數的強型別多載。</span><span class="sxs-lookup"><span data-stu-id="f03c5-198">All hello methods in hello SDK that deal with documents have overloads that work with hello `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="f03c5-199">只有 hello 後者這篇文章中的 hello 範例程式碼中使用。</span><span class="sxs-lookup"><span data-stu-id="f03c5-199">Only hello latter are used in hello sample code in this article.</span></span>
> 
> 

<span data-ttu-id="f03c5-200">**為什麼您應該使用 Nullable 資料類型**</span><span class="sxs-lookup"><span data-stu-id="f03c5-200">**Why you should use nullable data types**</span></span>

<span data-ttu-id="f03c5-201">當設計您的模型類別 toomap tooan Azure 搜尋索引，我們建議您宣告實值類型的屬性，例如`bool`和`int`toobe 可為 null (例如，`bool?`而不是`bool`)。</span><span class="sxs-lookup"><span data-stu-id="f03c5-201">When designing your own model classes toomap tooan Azure Search index, we recommend declaring properties of value types such as `bool` and `int` toobe nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="f03c5-202">如果您使用非 null 的屬性，您有太**保證**沒有文件索引中的包含 hello 對應欄位的 null 值。</span><span class="sxs-lookup"><span data-stu-id="f03c5-202">If you use a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="f03c5-203">Hello SDK 都 hello Azure 搜尋服務可協助您 tooenforce 這。</span><span class="sxs-lookup"><span data-stu-id="f03c5-203">Neither hello SDK nor hello Azure Search service will help you tooenforce this.</span></span>

<span data-ttu-id="f03c5-204">這不只是假設性的問題： 想像一下，讓您加入新欄位 tooan 現有索引型別的`DataType.Int32`。</span><span class="sxs-lookup"><span data-stu-id="f03c5-204">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `DataType.Int32`.</span></span> <span data-ttu-id="f03c5-205">在更新之後 hello 索引定義，所有文件必須針對該新欄位的 null 值 （因為所有類型都是可為 null 的 Azure 搜尋）。</span><span class="sxs-lookup"><span data-stu-id="f03c5-205">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="f03c5-206">若您搭配不可為 null，然後使用模型類別`int`該欄位的屬性，您會收到`JsonSerializationException`tooretrieve 文件時，就像這樣：</span><span class="sxs-lookup"><span data-stu-id="f03c5-206">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="f03c5-207">因此，我們建議您在模型類別中使用可為 Null 的類型，來做為最佳作法。</span><span class="sxs-lookup"><span data-stu-id="f03c5-207">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f03c5-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f03c5-208">Next steps</span></span>
<span data-ttu-id="f03c5-209">填入您的 Azure 搜尋索引之後, 會準備 toostart 發出查詢 toosearch 文件。</span><span class="sxs-lookup"><span data-stu-id="f03c5-209">After populating your Azure Search index, you will be ready toostart issuing queries toosearch for documents.</span></span> <span data-ttu-id="f03c5-210">如需詳細資料，請參閱 [查詢 Azure 搜尋服務索引](search-query-overview.md) 。</span><span class="sxs-lookup"><span data-stu-id="f03c5-210">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>

