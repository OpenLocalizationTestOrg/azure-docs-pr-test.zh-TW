---
title: "Azure 搜尋服務的同義字預覽教學課程 | Microsoft Docs"
description: "將同義字預覽功能新增至 Azure 搜尋服務中的索引。"
services: search
manager: jhubbard
documentationcenter: 
author: HeidiSteen
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 03/31/2017
ms.author: heidist
ms.openlocfilehash: 014959ed471f796d2184f0f8ff10d15cdc8a2ec6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="synonym-preview-c-tutorial-for-azure-search"></a><span data-ttu-id="5699b-103">Azure 搜尋服務的同義字 (預覽) C# 教學課程</span><span class="sxs-lookup"><span data-stu-id="5699b-103">Synonym (preview) C# tutorial for Azure Search</span></span>

<span data-ttu-id="5699b-104">同義字可藉由比對在語意上視為等於輸入詞彙的詞彙來展開查詢。</span><span class="sxs-lookup"><span data-stu-id="5699b-104">Synonyms expand a query by matching on terms considered semantically equivalent to the input term.</span></span> <span data-ttu-id="5699b-105">例如，您可能希望 "car" 比對包含 "automobile" 或 "vehicle" 詞彙的文件。</span><span class="sxs-lookup"><span data-stu-id="5699b-105">For example, you might want "car" to match documents containing the terms "automobile" or "vehicle".</span></span>

<span data-ttu-id="5699b-106">在 Azure 搜尋服務中，同義字會定義於*同義字對應*中，透過*對應規則*讓相等的詞彙產生關聯。</span><span class="sxs-lookup"><span data-stu-id="5699b-106">In Azure Search, synonyms are defined in a *synonym map*, through *mapping rules* that associate equivalent terms.</span></span> <span data-ttu-id="5699b-107">您可以建立多個同義字對應、將它們張貼為可供任何索引使用的全服務資源，然後參照哪一個要在欄位層級使用。</span><span class="sxs-lookup"><span data-stu-id="5699b-107">You can create multiple synonym maps, post them as a service-wide resource available to any index, and then reference which one to use at the field level.</span></span> <span data-ttu-id="5699b-108">查詢時，除了搜尋索引，Azure 搜尋服務會查閱同義字對應 (如果在查詢中使用的欄位上指定一個同義字對應)。</span><span class="sxs-lookup"><span data-stu-id="5699b-108">At query time, in addition to searching an index, Azure Search does a lookup in a synonym map, if one is specified on fields used in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="5699b-109">同義字功能目前處於預覽狀態，只在最新的預覽 API 和 SDK 版本 (api-version=2016-09-01-Preview, SDK version 4.x-preview) 中提供支援。</span><span class="sxs-lookup"><span data-stu-id="5699b-109">The synonyms feature is currently in preview and only supported in the latest preview API and SDK versions (api-version=2016-09-01-Preview, SDK version 4.x-preview).</span></span> <span data-ttu-id="5699b-110">這一次沒有 Azure 入口網站支援。</span><span class="sxs-lookup"><span data-stu-id="5699b-110">There is no Azure portal support at this time.</span></span> <span data-ttu-id="5699b-111">預覽 API 不受 SLA 約束，且預覽功能可能會變更，因此不建議在生產應用程式中使用它們。</span><span class="sxs-lookup"><span data-stu-id="5699b-111">Preview APIs are not under SLA and preview features may change, so we do not recommend using them in production applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5699b-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="5699b-112">Prerequisites</span></span>

<span data-ttu-id="5699b-113">教學課程包含下列需求︰</span><span class="sxs-lookup"><span data-stu-id="5699b-113">Tutorial requirements include the following:</span></span>

* [<span data-ttu-id="5699b-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5699b-114">Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="5699b-115">Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="5699b-115">Azure Search service</span></span>](search-create-service-portal.md)
* [<span data-ttu-id="5699b-116">預覽版本的 Microsoft.Azure.Search .NET 程式庫</span><span class="sxs-lookup"><span data-stu-id="5699b-116">Preview version of Microsoft.Azure.Search .NET library</span></span>](https://aka.ms/search-sdk-preview)
* [<span data-ttu-id="5699b-117">如何從 .NET 應用程式使用 Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="5699b-117">How to use Azure Search from a .NET Application</span></span>](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a><span data-ttu-id="5699b-118">概觀</span><span class="sxs-lookup"><span data-stu-id="5699b-118">Overview</span></span>

<span data-ttu-id="5699b-119">之前與之後查詢會示範同義字的值。</span><span class="sxs-lookup"><span data-stu-id="5699b-119">Before-and-after queries demonstrate the value of synonyms.</span></span> <span data-ttu-id="5699b-120">在本教學課程中，我們使用可執行查詢並傳回範例索引結果的範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="5699b-120">In this tutorial, we use a sample application that executes queries and returns results on a sample index.</span></span> <span data-ttu-id="5699b-121">範例應用程式會建立名為 "hotels" 並已填入兩份文件的小型索引。</span><span class="sxs-lookup"><span data-stu-id="5699b-121">The sample application creates a small index named "hotels" populated with two documents.</span></span> <span data-ttu-id="5699b-122">此應用程式會使用未出現在索引中的詞彙和詞句來執行搜尋查詢，啟用同義字功能，然後再次發出相同的搜尋。</span><span class="sxs-lookup"><span data-stu-id="5699b-122">The application executes search queries using terms and phrases that do not appear in the index, enables the synonyms feature, then issues the same searches again.</span></span> <span data-ttu-id="5699b-123">下列程式碼示範整體流程。</span><span class="sxs-lookup"><span data-stu-id="5699b-123">The code below demonstrates the overall flow.</span></span>

```csharp
  static void Main(string[] args)
  {
      SearchServiceClient serviceClient = CreateSearchServiceClient();

      Console.WriteLine("{0}", "Cleaning up resources...\n");
      CleanupResources(serviceClient);

      Console.WriteLine("{0}", "Creating index...\n");
      CreateHotelsIndex(serviceClient);

      ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

      Console.WriteLine("{0}", "Uploading documents...\n");
      UploadDocuments(indexClient);

      ISearchIndexClient indexClientForQueries = CreateSearchIndexClient();

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Adding synonyms...\n");
      UploadSynonyms(serviceClient);
      EnableSynonymsInHotelsIndex(serviceClient);
      Thread.Sleep(10000); // Wait for the changes to propagate

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Complete.  Press any key to end application...\n");

      Console.ReadKey();
  }
```
<span data-ttu-id="5699b-124">[如何從 .NET 應用程式使用 Azure 搜尋服務](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)會說明用來建立及填入範例索引的步驟。</span><span class="sxs-lookup"><span data-stu-id="5699b-124">The steps to create and populate the sample index are explained in [How to use Azure Search from a .NET Application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

## <a name="before-queries"></a><span data-ttu-id="5699b-125">「之前」查詢</span><span class="sxs-lookup"><span data-stu-id="5699b-125">"Before" queries</span></span>

<span data-ttu-id="5699b-126">在 `RunQueriesWithNonExistentTermsInIndex` 中，我們使用 "five star"、"internet" 和 "economy AND hotel" 發出搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="5699b-126">In `RunQueriesWithNonExistentTermsInIndex`, we issue search queries with "five star", "internet", and "economy AND hotel".</span></span>
```csharp
Console.WriteLine("Search the entire index for the phrase \"five star\":\n");
results = indexClient.Documents.Search<Hotel>("\"five star\"", parameters);
WriteDocuments(results);

Console.WriteLine("Search the entire index for the term 'internet':\n");
results = indexClient.Documents.Search<Hotel>("internet", parameters);
WriteDocuments(results);

Console.WriteLine("Search the entire index for the terms 'economy' AND 'hotel':\n");
results = indexClient.Documents.Search<Hotel>("economy AND hotel", parameters);
WriteDocuments(results);
```
<span data-ttu-id="5699b-127">這兩份經過檢索的文件都不包含這些詞彙，所以我們會從第一個 `RunQueriesWithNonExistentTermsInIndex` 取得下列輸出。</span><span class="sxs-lookup"><span data-stu-id="5699b-127">Neither of the two indexed documents contain the terms, so we get the following output from the first `RunQueriesWithNonExistentTermsInIndex`.</span></span>
~~~
Search the entire index for the phrase "five star":

no document matched

Search the entire index for the term 'internet':

no document matched

Search the entire index for the terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a><span data-ttu-id="5699b-128">啟用同義字</span><span class="sxs-lookup"><span data-stu-id="5699b-128">Enable synonyms</span></span>

<span data-ttu-id="5699b-129">啟用同義字的程序包含兩步驟。</span><span class="sxs-lookup"><span data-stu-id="5699b-129">Enabling synonyms is a two-step process.</span></span> <span data-ttu-id="5699b-130">我們會先定義和上傳同義字規則，然後再設定要使用這些規則的欄位。</span><span class="sxs-lookup"><span data-stu-id="5699b-130">We first define and upload synonym rules and then configure fields to use them.</span></span> <span data-ttu-id="5699b-131">`UploadSynonyms` 和 `EnableSynonymsInHotelsIndex` 會簡要說明此程序。</span><span class="sxs-lookup"><span data-stu-id="5699b-131">The process is outlined in `UploadSynonyms` and `EnableSynonymsInHotelsIndex`.</span></span>

1. <span data-ttu-id="5699b-132">將同義字對應新增到您的搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="5699b-132">Add a synonym map to your search service.</span></span> <span data-ttu-id="5699b-133">在 `UploadSynonyms` 中，我們會在同義字對應'desc-synonymmap' 中定義四個規則並上傳至服務。</span><span class="sxs-lookup"><span data-stu-id="5699b-133">In `UploadSynonyms`, we define four rules in our synonym map 'desc-synonymmap' and upload to the service.</span></span>
```csharp
    var synonymMap = new SynonymMap()
    {
        Name = "desc-synonymmap",
        Format = "solr",
        Synonyms = "hotel, motel\n
                    internet,wifi\n
                    five star=>luxury\n
                    economy,inexpensive=>budget"
    };

    serviceClient.SynonymMaps.CreateOrUpdate(synonymMap);
```
<span data-ttu-id="5699b-134">同義字對應必須符合開放原始碼標準 `solr` 格式。</span><span class="sxs-lookup"><span data-stu-id="5699b-134">A synonym map must conform to the open source standard `solr` format.</span></span> <span data-ttu-id="5699b-135">[Azure 搜尋服務中的同義字](search-synonyms.md)的 `Apache Solr synonym format`一節會說明此格式。</span><span class="sxs-lookup"><span data-stu-id="5699b-135">The format is explained in [Synonyms in Azure Search](search-synonyms.md) under the section `Apache Solr synonym format`.</span></span>

2. <span data-ttu-id="5699b-136">設定可搜尋的欄位，以使用索引定義中的同義字對應。</span><span class="sxs-lookup"><span data-stu-id="5699b-136">Configure searchable fields to use the synonym map in the index definition.</span></span> <span data-ttu-id="5699b-137">在 `EnableSynonymsInHotelsIndex` 中，我們會將 `synonymMaps` 屬性設定為新上傳的同義字對應名稱，以在 `category` 和 `tags` 兩個欄位上啟用同義字。</span><span class="sxs-lookup"><span data-stu-id="5699b-137">In `EnableSynonymsInHotelsIndex`, we enable synonyms on two fields `category` and `tags` by setting the `synonymMaps` property to the name of the newly uploaded synonym map.</span></span>
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
<span data-ttu-id="5699b-138">當您新增同義字對應時，不需要重建索引。</span><span class="sxs-lookup"><span data-stu-id="5699b-138">When you add a synonym map, index rebuilds are not required.</span></span> <span data-ttu-id="5699b-139">您可以將同義字對應新增到您的服務，然後修改任何索引中的現有欄位定義，以使用新的同義字對應。</span><span class="sxs-lookup"><span data-stu-id="5699b-139">You can add a synonym map to your service, and then amend existing field definitions in any index to use the new synonym map.</span></span> <span data-ttu-id="5699b-140">新增屬性對於索引可用性沒有任何影響。</span><span class="sxs-lookup"><span data-stu-id="5699b-140">The addition of new attributes has no impact on index availability.</span></span> <span data-ttu-id="5699b-141">停用欄位的同義字也是如此。</span><span class="sxs-lookup"><span data-stu-id="5699b-141">The same applies in disabling synonyms for a field.</span></span> <span data-ttu-id="5699b-142">您只要將 `synonymMaps` 屬性設定為空白清單。</span><span class="sxs-lookup"><span data-stu-id="5699b-142">You can simply set the `synonymMaps` property to an empty list.</span></span>
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a><span data-ttu-id="5699b-143">「之後」查詢</span><span class="sxs-lookup"><span data-stu-id="5699b-143">"After" queries</span></span>

<span data-ttu-id="5699b-144">上傳同義字對應並將索引更新為使用同義字對應之後，第二個 `RunQueriesWithNonExistentTermsInIndex` 就會呼叫下列輸出︰</span><span class="sxs-lookup"><span data-stu-id="5699b-144">After the synonym map is uploaded and the index is updated to use the synonym map, the second `RunQueriesWithNonExistentTermsInIndex` call outputs the following:</span></span>

~~~
Search the entire index for the phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search the entire index for the term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search the entire index for the terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
<span data-ttu-id="5699b-145">第一個查詢會尋找 `five star=>luxury` 規則所產生的文件。</span><span class="sxs-lookup"><span data-stu-id="5699b-145">The first query finds the document from the rule `five star=>luxury`.</span></span> <span data-ttu-id="5699b-146">第二個查詢會使用 `internet,wifi` 展開搜尋，而第三個查詢會同時使用 `hotel, motel` 和 `economy,inexpensive=>budget` 來尋找相符的文件。</span><span class="sxs-lookup"><span data-stu-id="5699b-146">The second query expands the search using `internet,wifi` and the third using both `hotel, motel` and `economy,inexpensive=>budget` in finding the documents they matched.</span></span>

<span data-ttu-id="5699b-147">新增同義字會全然改變搜尋經驗。</span><span class="sxs-lookup"><span data-stu-id="5699b-147">Adding synonyms completely changes the search experience.</span></span> <span data-ttu-id="5699b-148">在本教學課程中，即使我們索引中的文件有關聯，原始查詢也無法傳回有意義的結果。</span><span class="sxs-lookup"><span data-stu-id="5699b-148">In this tutorial, the original queries failed to return meaningful results even though the documents in our index were relevant.</span></span> <span data-ttu-id="5699b-149">啟用同義字，我們就可以展開索引以包含常用的詞彙，而不需變更索引中的基礎資料。</span><span class="sxs-lookup"><span data-stu-id="5699b-149">By enabling synonyms, we can expand an index to include terms in common use, with no changes to underlying data in the index.</span></span>

## <a name="sample-application-source-code"></a><span data-ttu-id="5699b-150">範例應用程式的原始程式碼</span><span class="sxs-lookup"><span data-stu-id="5699b-150">Sample application source code</span></span>
<span data-ttu-id="5699b-151">您可以在 [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) 上尋找本逐步解說中所用範例應用程式的完整原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="5699b-151">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5699b-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5699b-152">Next steps</span></span>

* <span data-ttu-id="5699b-153">檢閱[如何在 Azure 搜尋服務中使用同義字](search-synonyms.md)</span><span class="sxs-lookup"><span data-stu-id="5699b-153">Review [How to use synonyms in Azure Search](search-synonyms.md)</span></span>
* <span data-ttu-id="5699b-154">檢閱[同義字 REST API 文件](https://aka.ms/rgm6rq)</span><span class="sxs-lookup"><span data-stu-id="5699b-154">Review [Synonyms REST API documentation](https://aka.ms/rgm6rq)</span></span>
* <span data-ttu-id="5699b-155">瀏覽 [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) 及 [REST API](https://docs.microsoft.com/rest/api/searchservice/) 參考文章。</span><span class="sxs-lookup"><span data-stu-id="5699b-155">Browse the references for the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
