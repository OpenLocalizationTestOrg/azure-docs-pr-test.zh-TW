---
title: "查詢索引 (.NET API - Azure 搜尋服務) | Microsoft Docs"
description: "在 Azure 搜尋服務中建立搜尋查詢，並使用搜尋參數來篩選及排序搜尋結果。"
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
ms.openlocfilehash: 52bd0fd4cf70401dcf881c7f28d5cd91397bb059
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="query-your-azure-search-index-using-the-net-sdk"></a><span data-ttu-id="f787f-103">使用 .NET SDK 查詢 Azure 搜尋服務索引</span><span class="sxs-lookup"><span data-stu-id="f787f-103">Query your Azure Search index using the .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f787f-104">概觀</span><span class="sxs-lookup"><span data-stu-id="f787f-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="f787f-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="f787f-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="f787f-106">.NET</span><span class="sxs-lookup"><span data-stu-id="f787f-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="f787f-107">REST</span><span class="sxs-lookup"><span data-stu-id="f787f-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="f787f-108">本文將說明如何使用 [Azure 搜尋服務 .NET SDK](https://aka.ms/search-sdk)查詢索引。</span><span class="sxs-lookup"><span data-stu-id="f787f-108">This article will show you how to query an index using the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span>

<span data-ttu-id="f787f-109">在開始閱讀本逐步解說前，請先[建立好 Azure 搜尋服務索引](search-what-is-an-index.md)，並[在索引中填入資料](search-what-is-data-import.md)。</span><span class="sxs-lookup"><span data-stu-id="f787f-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f787f-110">本文中的所有範例程式碼均以 C# 撰寫。</span><span class="sxs-lookup"><span data-stu-id="f787f-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="f787f-111">您可以 [在 GitHub](http://aka.ms/search-dotnet-howto)找到完整的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="f787f-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="f787f-112">您也可以閱讀 [Azure 搜尋服務 .NET SDK](search-howto-dotnet-sdk.md)，以取得更詳細的範例程式碼逐步說明。</span><span class="sxs-lookup"><span data-stu-id="f787f-112">You can also read about the [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of the sample code.</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="f787f-113">識別 Azure 搜尋服務的查詢 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="f787f-113">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="f787f-114">現在您已建立 Azure 搜尋服務索引，便差不多可以使用 .NET SDK 發出查詢。</span><span class="sxs-lookup"><span data-stu-id="f787f-114">Now that you have created an Azure Search index, you are almost ready to issue queries using the .NET SDK.</span></span> <span data-ttu-id="f787f-115">首先，必須取得一個為您佈建的搜尋服務所產生的查詢 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="f787f-115">First, you will need to obtain one of the query api-keys that was generated for the search service you provisioned.</span></span> <span data-ttu-id="f787f-116">.NET SDK 將會在每個要求上將此 API 金鑰傳送給您的服務。</span><span class="sxs-lookup"><span data-stu-id="f787f-116">The .NET SDK will send this api-key on every request to your service.</span></span> <span data-ttu-id="f787f-117">擁有有效的金鑰就能為每個要求在傳送要求之應用程式與處理要求之服務間建立信任。</span><span class="sxs-lookup"><span data-stu-id="f787f-117">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="f787f-118">若要尋找服務的 API 金鑰，您可以登入 [Azure 入口網站](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="f787f-118">To find your service's api-keys you can sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="f787f-119">前往 Azure 搜尋服務的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f787f-119">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="f787f-120">按一下 [金鑰] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f787f-120">Click on the "Keys" icon</span></span>

<span data-ttu-id="f787f-121">服務會有系統管理金鑰和查詢金鑰。</span><span class="sxs-lookup"><span data-stu-id="f787f-121">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="f787f-122">主要和次要系統管理金鑰  會授與所有作業的完整權限，包括管理服務以及建立和刪除索引、索引子與資料來源的能力。</span><span class="sxs-lookup"><span data-stu-id="f787f-122">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="f787f-123">由於有兩個金鑰，因此如果您決定重新產生主要金鑰，您可以繼續使用次要金鑰，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="f787f-123">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="f787f-124">查詢金鑰  會授與索引和文件的唯讀存取權，且通常會分派給發出搜尋要求的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="f787f-124">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="f787f-125">若要查詢索引，您可以使用其中一個查詢金鑰。</span><span class="sxs-lookup"><span data-stu-id="f787f-125">For the purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="f787f-126">系統管理金鑰也可以用於進行查詢，但是您應該在應用程式的程式碼中使用查詢金鑰，因為查詢金鑰更加符合 [最低權限準則](https://en.wikipedia.org/wiki/Principle_of_least_privilege)。</span><span class="sxs-lookup"><span data-stu-id="f787f-126">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows the [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="create-an-instance-of-the-searchindexclient-class"></a><span data-ttu-id="f787f-127">建立 SearchIndexClient 類別的執行個體</span><span class="sxs-lookup"><span data-stu-id="f787f-127">Create an instance of the SearchIndexClient class</span></span>
<span data-ttu-id="f787f-128">若要使用 Azure 搜尋服務 .NET SDK 來發出查詢，您必須建立 `SearchIndexClient` 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="f787f-128">To issue queries with the Azure Search .NET SDK, you will need to create an instance of the `SearchIndexClient` class.</span></span> <span data-ttu-id="f787f-129">這個類別有數個建構函式。</span><span class="sxs-lookup"><span data-stu-id="f787f-129">This class has several constructors.</span></span> <span data-ttu-id="f787f-130">您需要的建構函式會取得您的搜尋服務名稱和 `SearchCredentials` 物件作為參數。</span><span class="sxs-lookup"><span data-stu-id="f787f-130">The one you want takes your search service name, index name, and a `SearchCredentials` object as parameters.</span></span> <span data-ttu-id="f787f-131">`SearchCredentials` 會包裝您的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="f787f-131">`SearchCredentials` wraps your api-key.</span></span>

<span data-ttu-id="f787f-132">下方程式碼會使用搜尋服務名稱的值，以及儲存於應用程式設定檔中的 API 金鑰 (在[範例應用程式](http://aka.ms/search-dotnet-howto)的情況下為 `appsettings.json`)，為 "hotels" 索引 (建立於[使用 .NET SDK 建立 Azure 搜尋服務索引](search-create-index-dotnet.md)) 建立新的 `SearchIndexClient`：</span><span class="sxs-lookup"><span data-stu-id="f787f-132">The code below creates a new `SearchIndexClient` for the "hotels" index (created in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md)) using values for the search service name and api-key that are stored in the application's config file (`appsettings.json` in the case of the [sample application](http://aka.ms/search-dotnet-howto)):</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="f787f-133">`SearchIndexClient` 具有 `Documents` 屬性。</span><span class="sxs-lookup"><span data-stu-id="f787f-133">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="f787f-134">此屬性會提供您查詢 Azure 搜尋服務索引所需的所有方法。</span><span class="sxs-lookup"><span data-stu-id="f787f-134">This property provides all the methods you need to query Azure Search indexes.</span></span>

## <a name="query-your-index"></a><span data-ttu-id="f787f-135">查詢您的索引</span><span class="sxs-lookup"><span data-stu-id="f787f-135">Query your index</span></span>
<span data-ttu-id="f787f-136">使用 .NET SDK 進行搜尋就和在您的 `SearchIndexClient` 呼叫 `Documents.Search` 方法一樣簡單。</span><span class="sxs-lookup"><span data-stu-id="f787f-136">Searching with the .NET SDK is as simple as calling the `Documents.Search` method on your `SearchIndexClient`.</span></span> <span data-ttu-id="f787f-137">此方法會採用一些參數，包括搜尋文字，以及可進一步縮小查詢範圍的 `SearchParameters` 物件。</span><span class="sxs-lookup"><span data-stu-id="f787f-137">This method takes a few parameters, including the search text, along with a `SearchParameters` object that can be used to further refine the query.</span></span>

#### <a name="types-of-queries"></a><span data-ttu-id="f787f-138">查詢類型</span><span class="sxs-lookup"><span data-stu-id="f787f-138">Types of Queries</span></span>
<span data-ttu-id="f787f-139">您將會使用的兩個主要[查詢類型](search-query-overview.md#types-of-queries)是 `search` 和 `filter`。</span><span class="sxs-lookup"><span data-stu-id="f787f-139">The two main [query types](search-query-overview.md#types-of-queries) you will use are `search` and `filter`.</span></span> <span data-ttu-id="f787f-140">`search` 查詢會搜尋索引中所有可搜尋欄位的一或多個字詞。</span><span class="sxs-lookup"><span data-stu-id="f787f-140">A `search` query searches for one or more terms in all *searchable* fields in your index.</span></span> <span data-ttu-id="f787f-141">`filter` 查詢可跨索引的所有可篩選欄位評估布林運算式。</span><span class="sxs-lookup"><span data-stu-id="f787f-141">A `filter` query evaluates a boolean expression over all *filterable* fields in an index.</span></span>

<span data-ttu-id="f787f-142">搜尋和篩選均使用 `Documents.Search` 方法執行。</span><span class="sxs-lookup"><span data-stu-id="f787f-142">Both searches and filters are performed using the `Documents.Search` method.</span></span> <span data-ttu-id="f787f-143">搜尋查詢可在 `searchText` 參數中傳遞，而篩選運算式可在 `SearchParameters` 類別的 `Filter` 屬性中傳遞。</span><span class="sxs-lookup"><span data-stu-id="f787f-143">A search query can be passed in the `searchText` parameter, while a filter expression can be passed in the `Filter` property of the `SearchParameters` class.</span></span> <span data-ttu-id="f787f-144">若要篩選而不進行搜尋，只要為 `searchText` 參數傳遞 `"*"` 即可。</span><span class="sxs-lookup"><span data-stu-id="f787f-144">To filter without searching, just pass `"*"` for the `searchText` parameter.</span></span> <span data-ttu-id="f787f-145">若要在不進行篩選的情況下搜尋，則只要將 `Filter` 屬性保留在未設定狀態，或完全不要傳入 `SearchParameters` 執行個體。</span><span class="sxs-lookup"><span data-stu-id="f787f-145">To search without filtering, just leave the `Filter` property unset, or do not pass in a `SearchParameters` instance at all.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="f787f-146">查詢範例</span><span class="sxs-lookup"><span data-stu-id="f787f-146">Example Queries</span></span>
<span data-ttu-id="f787f-147">下列範例程式碼示範幾個不同方式，來查詢 [使用.NET SDK 建立 Azure 搜尋服務索引](search-create-index-dotnet.md#DefineIndex)中定義的 "hotels" 索引。</span><span class="sxs-lookup"><span data-stu-id="f787f-147">The following sample code shows a few different ways to query the "hotels" index defined in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#DefineIndex).</span></span> <span data-ttu-id="f787f-148">請注意，隨著搜尋結果傳回的文件是 `Hotel` 類別的執行個體，其定義於 [在 Azure 搜尋服務中使用 .NET SDK 匯入資料](search-import-data-dotnet.md#HotelClass)。</span><span class="sxs-lookup"><span data-stu-id="f787f-148">Note that the documents returned with the search results are instances of the `Hotel` class, which was defined in [Data Import in Azure Search using the .NET SDK](search-import-data-dotnet.md#HotelClass).</span></span> <span data-ttu-id="f787f-149">範例程式碼運用 `WriteDocuments` 方法將搜尋結果輸出到主控台。</span><span class="sxs-lookup"><span data-stu-id="f787f-149">The sample code makes use of a `WriteDocuments` method to output the search results to the console.</span></span> <span data-ttu-id="f787f-150">下一節將說明此方法。</span><span class="sxs-lookup"><span data-stu-id="f787f-150">This method is described in the next section.</span></span>

```csharp
SearchParameters parameters;
DocumentSearchResult<Hotel> results;

Console.WriteLine("Search the entire index for the term 'budget' and return only the hotelName field:\n");

parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);

Console.Write("Apply a filter to the index to find hotels cheaper than $150 per night, ");
Console.WriteLine("and return the hotelId and description:\n");

parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.Write("Search the entire index, order by a specific field (lastRenovationDate) ");
Console.Write("in descending order, take the top two results, and show only hotelName and ");
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

Console.WriteLine("Search the entire index for the term 'motel':\n");

parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

## <a name="handle-search-results"></a><span data-ttu-id="f787f-151">處理搜尋結果</span><span class="sxs-lookup"><span data-stu-id="f787f-151">Handle search results</span></span>
<span data-ttu-id="f787f-152">`Documents.Search` 方法會傳回包含查詢結果的 `DocumentSearchResult` 物件。</span><span class="sxs-lookup"><span data-stu-id="f787f-152">The `Documents.Search` method returns a `DocumentSearchResult` object that contains the results of the query.</span></span> <span data-ttu-id="f787f-153">前一章節中的範例使用稱為 `WriteDocuments` 的方法將搜尋結果輸出到主控台：</span><span class="sxs-lookup"><span data-stu-id="f787f-153">The example in the previous section used a method called `WriteDocuments` to output the search results to the console:</span></span>

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

<span data-ttu-id="f787f-154">以下是前一節查詢結果的可能樣貌，此處假設 "hotels" 索引是以 [在 Azure 搜尋服務中使用 .NET SDK 匯入資料](search-import-data-dotnet.md)中的範例資料填入：</span><span class="sxs-lookup"><span data-stu-id="f787f-154">Here is what the results look like for the queries in the previous section, assuming the "hotels" index is populated with the sample data in [Data Import in Azure Search using the .NET SDK](search-import-data-dotnet.md):</span></span>

```
Search the entire index for the term 'budget' and return only the hotelName field:

Name: Roach Motel

Apply a filter to the index to find hotels cheaper than $150 per night, and return the hotelId and description:

ID: 2   Description: Cheapest hotel in town
ID: 3   Description: Close to town hall and the river

Search the entire index, order by a specific field (lastRenovationDate) in descending order, take the top two results, and show only hotelName and lastRenovationDate:

Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Search the entire index for the term 'motel':

ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
```

<span data-ttu-id="f787f-155">上方的範例程式碼使用主控台來輸出搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="f787f-155">The sample code above uses the console to output search results.</span></span> <span data-ttu-id="f787f-156">您同樣需要在自己的應用程式中顯示搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="f787f-156">You will likewise need to display search results in your own application.</span></span> <span data-ttu-id="f787f-157">如需範例以了解如何在 ASP.NET MVC 架構的 Web 應用程式中轉譯搜尋結果，請參閱 [GitHub 上的此範例](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) 。</span><span class="sxs-lookup"><span data-stu-id="f787f-157">See [this sample on GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) for an example of how to render search results in an ASP.NET MVC-based web application.</span></span>

