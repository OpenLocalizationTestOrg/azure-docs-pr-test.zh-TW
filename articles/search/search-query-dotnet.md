---
title: "aaa\"查詢索引 (.NET API-Azure 搜尋) |Microsoft 文件 」"
description: "建置在 Azure 搜尋的搜尋查詢，並使用搜尋參數 toofilter 和排序搜尋結果。"
services: search
manager: jhubbard
documentationcenter: 
author: brjohnstmsft
ms.assetid: 12c3efba-ea99-4187-9d2d-f63b5ec7040d
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/19/2017
ms.author: brjohnst
ms.openlocfilehash: 8b3ba1cd1270aad038fb48d9053fcff35d243e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-net-sdk"></a><span data-ttu-id="95bed-103">查詢您的 Azure 搜尋索引使用 hello.NET SDK</span><span class="sxs-lookup"><span data-stu-id="95bed-103">Query your Azure Search index using hello .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="95bed-104">概觀</span><span class="sxs-lookup"><span data-stu-id="95bed-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="95bed-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="95bed-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="95bed-106">.NET</span><span class="sxs-lookup"><span data-stu-id="95bed-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="95bed-107">REST</span><span class="sxs-lookup"><span data-stu-id="95bed-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="95bed-108">本文將告訴您如何 tooquery 索引使用 hello [Azure 搜尋.NET SDK](https://aka.ms/search-sdk)。</span><span class="sxs-lookup"><span data-stu-id="95bed-108">This article will show you how tooquery an index using hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span>

<span data-ttu-id="95bed-109">在開始閱讀本逐步解說前，請先[建立好 Azure 搜尋服務索引](search-what-is-an-index.md)，並[在索引中填入資料](search-what-is-data-import.md)。</span><span class="sxs-lookup"><span data-stu-id="95bed-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span>

> [!NOTE]
> <span data-ttu-id="95bed-110">本文中的所有範例程式碼均以 C# 撰寫。</span><span class="sxs-lookup"><span data-stu-id="95bed-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="95bed-111">您可以找到 hello 完整的原始程式碼[GitHub 上](http://aka.ms/search-dotnet-howto)。</span><span class="sxs-lookup"><span data-stu-id="95bed-111">You can find hello full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="95bed-112">您也可以閱讀 hello [Azure 搜尋.NET SDK](search-howto-dotnet-sdk.md) for 的詳細逐步 hello 範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="95bed-112">You can also read about hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of hello sample code.</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="95bed-113">識別 Azure 搜尋服務的查詢 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="95bed-113">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="95bed-114">既然您已經建立 Azure 搜尋索引，您會使用.NET SDK hello 就緒 tooissue 查詢。</span><span class="sxs-lookup"><span data-stu-id="95bed-114">Now that you have created an Azure Search index, you are almost ready tooissue queries using hello .NET SDK.</span></span> <span data-ttu-id="95bed-115">首先，您將需要 tooobtain hello 查詢 api 金鑰所產生的其中一個 hello 您佈建的搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="95bed-115">First, you will need tooobtain one of hello query api-keys that was generated for hello search service you provisioned.</span></span> <span data-ttu-id="95bed-116">此 api 金鑰會傳送 hello.NET SDK 的每個要求 tooyour 服務。</span><span class="sxs-lookup"><span data-stu-id="95bed-116">hello .NET SDK will send this api-key on every request tooyour service.</span></span> <span data-ttu-id="95bed-117">擁有有效的索引鍵建立信任關係，針對每個要求，hello 應用程式正在傳送嗨要求和處理它的 hello 服務之間。</span><span class="sxs-lookup"><span data-stu-id="95bed-117">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="95bed-118">toofind 服務的 api 金鑰才能登入 toohello [Azure 入口網站](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="95bed-118">toofind your service's api-keys you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="95bed-119">移 tooyour Azure 搜尋服務的刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="95bed-119">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="95bed-120">按一下 hello 「 金鑰 」 圖示</span><span class="sxs-lookup"><span data-stu-id="95bed-120">Click on hello "Keys" icon</span></span>

<span data-ttu-id="95bed-121">服務會有系統管理金鑰和查詢金鑰。</span><span class="sxs-lookup"><span data-stu-id="95bed-121">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="95bed-122">您的主要和次要*系統管理金鑰*tooall 作業，包括 hello 能力 toomanage hello 服務授與的完整權限、 建立和刪除索引、 索引子和資料來源。</span><span class="sxs-lookup"><span data-stu-id="95bed-122">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="95bed-123">有兩個索引鍵，讓您可以繼續 toouse hello 次要索引鍵，如果您決定 tooregenerate hello 主索引鍵，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="95bed-123">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="95bed-124">您*查詢索引鍵*授與唯讀存取 tooindexes 和文件，並發出搜尋要求的 tooclient 通常分散式應用程式。</span><span class="sxs-lookup"><span data-stu-id="95bed-124">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="95bed-125">基於 hello 查詢索引，您可以使用您的查詢索引鍵的其中一個。</span><span class="sxs-lookup"><span data-stu-id="95bed-125">For hello purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="95bed-126">系統管理金鑰也可以用於查詢，但您應該查詢索引鍵使用您的應用程式程式碼中，這更如下所示 hello[最低權限原則](https://en.wikipedia.org/wiki/Principle_of_least_privilege)。</span><span class="sxs-lookup"><span data-stu-id="95bed-126">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows hello [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="create-an-instance-of-hello-searchindexclient-class"></a><span data-ttu-id="95bed-127">建立 hello SearchIndexClient 類別的執行個體</span><span class="sxs-lookup"><span data-stu-id="95bed-127">Create an instance of hello SearchIndexClient class</span></span>
<span data-ttu-id="95bed-128">以 hello Azure 搜尋.NET SDK tooissue 查詢，您將需要 toocreate hello 的執行個體`SearchIndexClient`類別。</span><span class="sxs-lookup"><span data-stu-id="95bed-128">tooissue queries with hello Azure Search .NET SDK, you will need toocreate an instance of hello `SearchIndexClient` class.</span></span> <span data-ttu-id="95bed-129">這個類別有數個建構函式。</span><span class="sxs-lookup"><span data-stu-id="95bed-129">This class has several constructors.</span></span> <span data-ttu-id="95bed-130">您想要的 hello 接受您的搜尋服務名稱、 索引名稱和`SearchCredentials`做為參數的物件。</span><span class="sxs-lookup"><span data-stu-id="95bed-130">hello one you want takes your search service name, index name, and a `SearchCredentials` object as parameters.</span></span> <span data-ttu-id="95bed-131">`SearchCredentials` 會包裝您的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="95bed-131">`SearchCredentials` wraps your api-key.</span></span>

<span data-ttu-id="95bed-132">hello 的下列程式碼會建立新`SearchIndexClient`hello 「 旅館"索引 (在中建立[建立 Azure 搜尋索引，使用.NET SDK hello](search-create-index-dotnet.md)) 使用 hello 搜尋服務名稱和儲存在 hello 應用程式組態中的 api 金鑰值檔案 (`appsettings.json` hello hello 案例[範例應用程式](http://aka.ms/search-dotnet-howto)):</span><span class="sxs-lookup"><span data-stu-id="95bed-132">hello code below creates a new `SearchIndexClient` for hello "hotels" index (created in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md)) using values for hello search service name and api-key that are stored in hello application's config file (`appsettings.json` in hello case of hello [sample application](http://aka.ms/search-dotnet-howto)):</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="95bed-133">`SearchIndexClient` 具有 `Documents` 屬性。</span><span class="sxs-lookup"><span data-stu-id="95bed-133">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="95bed-134">這個屬性提供所有 hello 方法需要 tooquery Azure 搜尋索引。</span><span class="sxs-lookup"><span data-stu-id="95bed-134">This property provides all hello methods you need tooquery Azure Search indexes.</span></span>

## <a name="query-your-index"></a><span data-ttu-id="95bed-135">查詢您的索引</span><span class="sxs-lookup"><span data-stu-id="95bed-135">Query your index</span></span>
<span data-ttu-id="95bed-136">搜尋以 hello.NET SDK 的很簡單，呼叫 hello`Documents.Search`方法上的您`SearchIndexClient`。</span><span class="sxs-lookup"><span data-stu-id="95bed-136">Searching with hello .NET SDK is as simple as calling hello `Documents.Search` method on your `SearchIndexClient`.</span></span> <span data-ttu-id="95bed-137">這個方法會採用的幾個參數，包括 hello 搜尋文字，連同`SearchParameters`可以是使用的 toofurther 縮小 hello 查詢的物件。</span><span class="sxs-lookup"><span data-stu-id="95bed-137">This method takes a few parameters, including hello search text, along with a `SearchParameters` object that can be used toofurther refine hello query.</span></span>

#### <a name="types-of-queries"></a><span data-ttu-id="95bed-138">查詢類型</span><span class="sxs-lookup"><span data-stu-id="95bed-138">Types of Queries</span></span>
<span data-ttu-id="95bed-139">hello 兩個主要[查詢類型](search-query-overview.md#types-of-queries)您將使用是`search`和`filter`。</span><span class="sxs-lookup"><span data-stu-id="95bed-139">hello two main [query types](search-query-overview.md#types-of-queries) you will use are `search` and `filter`.</span></span> <span data-ttu-id="95bed-140">`search` 查詢會搜尋索引中所有可搜尋欄位的一或多個字詞。</span><span class="sxs-lookup"><span data-stu-id="95bed-140">A `search` query searches for one or more terms in all *searchable* fields in your index.</span></span> <span data-ttu-id="95bed-141">`filter` 查詢可跨索引的所有可篩選欄位評估布林運算式。</span><span class="sxs-lookup"><span data-stu-id="95bed-141">A `filter` query evaluates a boolean expression over all *filterable* fields in an index.</span></span>

<span data-ttu-id="95bed-142">搜尋和篩選器都是使用 hello`Documents.Search`方法。</span><span class="sxs-lookup"><span data-stu-id="95bed-142">Both searches and filters are performed using hello `Documents.Search` method.</span></span> <span data-ttu-id="95bed-143">搜尋查詢，請傳入 hello`searchText`參數，而篩選條件運算式可以傳入 hello`Filter`屬性 hello`SearchParameters`類別。</span><span class="sxs-lookup"><span data-stu-id="95bed-143">A search query can be passed in hello `searchText` parameter, while a filter expression can be passed in hello `Filter` property of hello `SearchParameters` class.</span></span> <span data-ttu-id="95bed-144">toofilter 而不必搜尋，只要將`"*"`hello`searchText`參數。</span><span class="sxs-lookup"><span data-stu-id="95bed-144">toofilter without searching, just pass `"*"` for hello `searchText` parameter.</span></span> <span data-ttu-id="95bed-145">toosearch 但不會篩選，只保留 hello`Filter`屬性未設定，或請不要傳入`SearchParameters`所有執行個體。</span><span class="sxs-lookup"><span data-stu-id="95bed-145">toosearch without filtering, just leave hello `Filter` property unset, or do not pass in a `SearchParameters` instance at all.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="95bed-146">查詢範例</span><span class="sxs-lookup"><span data-stu-id="95bed-146">Example Queries</span></span>
<span data-ttu-id="95bed-147">下列範例程式碼的 hello 示範幾個不同的方式 tooquery hello 「 旅館"索引定義中[建立 Azure 搜尋索引，使用.NET SDK hello](search-create-index-dotnet.md#DefineIndex)。</span><span class="sxs-lookup"><span data-stu-id="95bed-147">hello following sample code shows a few different ways tooquery hello "hotels" index defined in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#DefineIndex).</span></span> <span data-ttu-id="95bed-148">請注意，hello 文件以 hello 搜尋結果傳回執行個體的 hello`Hotel`類別，定義在[在 Azure 搜尋中使用的資料匯入 hello.NET SDK](search-import-data-dotnet.md#HotelClass)。</span><span class="sxs-lookup"><span data-stu-id="95bed-148">Note that hello documents returned with hello search results are instances of hello `Hotel` class, which was defined in [Data Import in Azure Search using hello .NET SDK](search-import-data-dotnet.md#HotelClass).</span></span> <span data-ttu-id="95bed-149">hello 範例程式碼會使用`WriteDocuments`方法 toooutput hello 搜尋結果 toohello 主控台。</span><span class="sxs-lookup"><span data-stu-id="95bed-149">hello sample code makes use of a `WriteDocuments` method toooutput hello search results toohello console.</span></span> <span data-ttu-id="95bed-150">這個方法是 hello 下一節中所述。</span><span class="sxs-lookup"><span data-stu-id="95bed-150">This method is described in hello next section.</span></span>

```csharp
SearchParameters parameters;
DocumentSearchResult<Hotel> results;

Console.WriteLine("Search hello entire index for hello term 'budget' and return only hello hotelName field:\n");

parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);

Console.Write("Apply a filter toohello index toofind hotels cheaper than $150 per night, ");
Console.WriteLine("and return hello hotelId and description:\n");

parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.Write("Search hello entire index, order by a specific field (lastRenovationDate) ");
Console.Write("in descending order, take hello top two results, and show only hotelName and ");
Console.WriteLine("lastRenovationDate:\n");

parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello term 'motel':\n");

parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

## <a name="handle-search-results"></a><span data-ttu-id="95bed-151">處理搜尋結果</span><span class="sxs-lookup"><span data-stu-id="95bed-151">Handle search results</span></span>
<span data-ttu-id="95bed-152">hello`Documents.Search`方法會傳回`DocumentSearchResult`包含 hello hello 查詢結果的物件。</span><span class="sxs-lookup"><span data-stu-id="95bed-152">hello `Documents.Search` method returns a `DocumentSearchResult` object that contains hello results of hello query.</span></span> <span data-ttu-id="95bed-153">hello 前一節中的 hello 範例使用呼叫的方法`WriteDocuments`toooutput hello 搜尋結果 toohello 主控台：</span><span class="sxs-lookup"><span data-stu-id="95bed-153">hello example in hello previous section used a method called `WriteDocuments` toooutput hello search results toohello console:</span></span>

```csharp
private static void WriteDocuments(DocumentSearchResult<Hotel> searchResults)
{
    foreach (SearchResult<Hotel> result in searchResults.Results)
    {
        Console.WriteLine(result.Document);
    }

    Console.WriteLine();
}
```

<span data-ttu-id="95bed-154">以下是什麼 hello 結果看起來像是 hello hello 前一節中的查詢，假設 hello 「 旅館"索引填入資料中的 hello 範例[在 Azure 搜尋中使用的資料匯入 hello.NET SDK](search-import-data-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="95bed-154">Here is what hello results look like for hello queries in hello previous section, assuming hello "hotels" index is populated with hello sample data in [Data Import in Azure Search using hello .NET SDK](search-import-data-dotnet.md):</span></span>

```
Search hello entire index for hello term 'budget' and return only hello hotelName field:

Name: Roach Motel

Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello hotelId and description:

ID: 2   Description: Cheapest hotel in town
ID: 3   Description: Close tootown hall and hello river

Search hello entire index, order by a specific field (lastRenovationDate) in descending order, take hello top two results, and show only hotelName and lastRenovationDate:

Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Search hello entire index for hello term 'motel':

ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
```

<span data-ttu-id="95bed-155">上述的 hello 範例程式碼會使用 hello 主控台 toooutput 搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="95bed-155">hello sample code above uses hello console toooutput search results.</span></span> <span data-ttu-id="95bed-156">您同樣必須 toodisplay 搜尋結果在自己的應用程式。</span><span class="sxs-lookup"><span data-stu-id="95bed-156">You will likewise need toodisplay search results in your own application.</span></span> <span data-ttu-id="95bed-157">請參閱[GitHub 上的這個範例](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample)toorender 搜尋結果中的 ASP.NET MVC 為基礎的 web 應用程式的方式的範例。</span><span class="sxs-lookup"><span data-stu-id="95bed-157">See [this sample on GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) for an example of how toorender search results in an ASP.NET MVC-based web application.</span></span>

