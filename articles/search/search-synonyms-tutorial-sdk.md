---
title: "aaaSynonyms 預覽 Azure 搜尋中的教學課程 |Microsoft 文件"
description: "新增 Azure 搜尋中的 hello 同義字預覽功能 tooan 索引。"
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
ms.openlocfilehash: 055c1cbafb945823a3dc4da0c522db236b1d192c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="synonym-preview-c-tutorial-for-azure-search"></a><span data-ttu-id="7a3d2-103">Azure 搜尋服務的同義字 (預覽) C# 教學課程</span><span class="sxs-lookup"><span data-stu-id="7a3d2-103">Synonym (preview) C# tutorial for Azure Search</span></span>

<span data-ttu-id="7a3d2-104">同義字展開查詢比對視為語意相等 toohello 輸入的詞彙的詞彙。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-104">Synonyms expand a query by matching on terms considered semantically equivalent toohello input term.</span></span> <span data-ttu-id="7a3d2-105">例如，您可以包含 hello 條款"automobile"或"vehicle"的"car"toomatch 文件。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-105">For example, you might want "car" toomatch documents containing hello terms "automobile" or "vehicle".</span></span>

<span data-ttu-id="7a3d2-106">在 Azure 搜尋服務中，同義字會定義於*同義字對應*中，透過*對應規則*讓相等的詞彙產生關聯。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-106">In Azure Search, synonyms are defined in a *synonym map*, through *mapping rules* that associate equivalent terms.</span></span> <span data-ttu-id="7a3d2-107">您可以建立多個同義字對應、 張貼為整個服務的資源可用 tooany 索引，然後參考 哪一個 toouse hello 欄位層級。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-107">You can create multiple synonym maps, post them as a service-wide resource available tooany index, and then reference which one toouse at hello field level.</span></span> <span data-ttu-id="7a3d2-108">在查詢時，除了 toosearching Azure 搜尋索引，會在同義字地圖中，查閱如果 hello 查詢中使用的欄位上指定的其中一個。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-108">At query time, in addition toosearching an index, Azure Search does a lookup in a synonym map, if one is specified on fields used in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="7a3d2-109">hello 同義字功能是目前在預覽，並僅支援在 hello 最新預覽版 API 和 SDK 版本 (api 版本 = 2016年-09-01-預覽，SDK 版本 4.x 預覽)。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-109">hello synonyms feature is currently in preview and only supported in hello latest preview API and SDK versions (api-version=2016-09-01-Preview, SDK version 4.x-preview).</span></span> <span data-ttu-id="7a3d2-110">目前 Azure 入口網站並不支援此功能。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-110">There is no Azure portal support at this time.</span></span> <span data-ttu-id="7a3d2-111">預覽 API 不受 SLA 約束，且預覽功能可能會變更，因此不建議在生產應用程式中使用它們。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-111">Preview APIs are not under SLA and preview features may change, so we do not recommend using them in production applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a3d2-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="7a3d2-112">Prerequisites</span></span>

<span data-ttu-id="7a3d2-113">教學課程需求 hello 如下：</span><span class="sxs-lookup"><span data-stu-id="7a3d2-113">Tutorial requirements include hello following:</span></span>

* [<span data-ttu-id="7a3d2-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7a3d2-114">Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="7a3d2-115">Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="7a3d2-115">Azure Search service</span></span>](search-create-service-portal.md)
* [<span data-ttu-id="7a3d2-116">預覽版本的 Microsoft.Azure.Search .NET 程式庫</span><span class="sxs-lookup"><span data-stu-id="7a3d2-116">Preview version of Microsoft.Azure.Search .NET library</span></span>](https://aka.ms/search-sdk-preview)
* [<span data-ttu-id="7a3d2-117">如何從.NET 應用程式的 toouse Azure 搜尋</span><span class="sxs-lookup"><span data-stu-id="7a3d2-117">How toouse Azure Search from a .NET Application</span></span>](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a><span data-ttu-id="7a3d2-118">概觀</span><span class="sxs-lookup"><span data-stu-id="7a3d2-118">Overview</span></span>

<span data-ttu-id="7a3d2-119">前-和-後查詢示範 hello 值的同義字。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-119">Before-and-after queries demonstrate hello value of synonyms.</span></span> <span data-ttu-id="7a3d2-120">在本教學課程中，我們使用可執行查詢並傳回範例索引結果的範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-120">In this tutorial, we use a sample application that executes queries and returns results on a sample index.</span></span> <span data-ttu-id="7a3d2-121">hello 範例應用程式會建立名為 「 旅館"填入 兩份文件的小型索引。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-121">hello sample application creates a small index named "hotels" populated with two documents.</span></span> <span data-ttu-id="7a3d2-122">hello 應用程式執行搜尋查詢，使用詞彙並不會出現在 hello 索引中的片語，以及 hello 同義字 」 功能，則問題 hello 相同搜尋一次。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-122">hello application executes search queries using terms and phrases that do not appear in hello index, enables hello synonyms feature, then issues hello same searches again.</span></span> <span data-ttu-id="7a3d2-123">hello 的下列程式碼示範 hello 整體流程。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-123">hello code below demonstrates hello overall flow.</span></span>

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
      Thread.Sleep(10000); // Wait for hello changes toopropagate

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");

      Console.ReadKey();
  }
```
<span data-ttu-id="7a3d2-124">hello 步驟 toocreate 並填入 hello 範例索引中會說明[toouse Azure 搜尋.NET 應用程式如何](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-124">hello steps toocreate and populate hello sample index are explained in [How toouse Azure Search from a .NET Application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

## <a name="before-queries"></a><span data-ttu-id="7a3d2-125">「之前」查詢</span><span class="sxs-lookup"><span data-stu-id="7a3d2-125">"Before" queries</span></span>

<span data-ttu-id="7a3d2-126">在 `RunQueriesWithNonExistentTermsInIndex` 中，我們使用 "five star"、"internet" 和 "economy AND hotel" 發出搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-126">In `RunQueriesWithNonExistentTermsInIndex`, we issue search queries with "five star", "internet", and "economy AND hotel".</span></span>
```csharp
Console.WriteLine("Search hello entire index for hello phrase \"five star\":\n");
results = indexClient.Documents.Search<Hotel>("\"five star\"", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello term 'internet':\n");
results = indexClient.Documents.Search<Hotel>("internet", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello terms 'economy' AND 'hotel':\n");
results = indexClient.Documents.Search<Hotel>("economy AND hotel", parameters);
WriteDocuments(results);
```
<span data-ttu-id="7a3d2-127">Hello 兩個索引的文件都不包含 hello 詞彙，所以我們取得 hello 以下第一次輸出從 hello `RunQueriesWithNonExistentTermsInIndex`。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-127">Neither of hello two indexed documents contain hello terms, so we get hello following output from hello first `RunQueriesWithNonExistentTermsInIndex`.</span></span>
~~~
Search hello entire index for hello phrase "five star":

no document matched

Search hello entire index for hello term 'internet':

no document matched

Search hello entire index for hello terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a><span data-ttu-id="7a3d2-128">啟用同義字</span><span class="sxs-lookup"><span data-stu-id="7a3d2-128">Enable synonyms</span></span>

<span data-ttu-id="7a3d2-129">啟用同義字的程序包含兩步驟。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-129">Enabling synonyms is a two-step process.</span></span> <span data-ttu-id="7a3d2-130">我們先定義和上傳的同義字規則，然後設定 欄位 toouse 它們。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-130">We first define and upload synonym rules and then configure fields toouse them.</span></span> <span data-ttu-id="7a3d2-131">hello 程序中所述`UploadSynonyms`和`EnableSynonymsInHotelsIndex`。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-131">hello process is outlined in `UploadSynonyms` and `EnableSynonymsInHotelsIndex`.</span></span>

1. <span data-ttu-id="7a3d2-132">新增同義字對應 tooyour 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-132">Add a synonym map tooyour search service.</span></span> <span data-ttu-id="7a3d2-133">在`UploadSynonyms`，我們在我們的同義資料表對應 ' desc synonymmap' 中定義四個規則，並上傳 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-133">In `UploadSynonyms`, we define four rules in our synonym map 'desc-synonymmap' and upload toohello service.</span></span>
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
<span data-ttu-id="7a3d2-134">同義字對應必須符合 toohello 開放原始碼標準`solr`格式。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-134">A synonym map must conform toohello open source standard `solr` format.</span></span> <span data-ttu-id="7a3d2-135">hello 格式述[在 Azure 搜尋的同義字](search-synonyms.md)hello 區段下方`Apache Solr synonym format`。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-135">hello format is explained in [Synonyms in Azure Search](search-synonyms.md) under hello section `Apache Solr synonym format`.</span></span>

2. <span data-ttu-id="7a3d2-136">設定可搜尋的欄位 toouse hello 同義字對應 hello 索引定義中。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-136">Configure searchable fields toouse hello synonym map in hello index definition.</span></span> <span data-ttu-id="7a3d2-137">在`EnableSynonymsInHotelsIndex`，我們會啟用兩個欄位上的同義字`category`和`tags`所設定的 hello `synonymMaps` hello 屬性 toohello 名稱新上傳的同義資料表對應。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-137">In `EnableSynonymsInHotelsIndex`, we enable synonyms on two fields `category` and `tags` by setting hello `synonymMaps` property toohello name of hello newly uploaded synonym map.</span></span>
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
<span data-ttu-id="7a3d2-138">當您新增同義字對應時，不需要重建索引。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-138">When you add a synonym map, index rebuilds are not required.</span></span> <span data-ttu-id="7a3d2-139">您可以新增同義字對應 tooyour 服務，並再修改任何索引 toouse hello 新同義字對應中的現有欄位定義。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-139">You can add a synonym map tooyour service, and then amend existing field definitions in any index toouse hello new synonym map.</span></span> <span data-ttu-id="7a3d2-140">hello 加入的新的屬性索引可用性沒有任何影響。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-140">hello addition of new attributes has no impact on index availability.</span></span> <span data-ttu-id="7a3d2-141">hello 一樣中停用欄位的同義字。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-141">hello same applies in disabling synonyms for a field.</span></span> <span data-ttu-id="7a3d2-142">您可以直接將 hello`synonymMaps`屬性 tooan 空白清單。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-142">You can simply set hello `synonymMaps` property tooan empty list.</span></span>
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a><span data-ttu-id="7a3d2-143">「之後」查詢</span><span class="sxs-lookup"><span data-stu-id="7a3d2-143">"After" queries</span></span>

<span data-ttu-id="7a3d2-144">Hello 同義字對應上傳並 hello 索引是更新的 toouse hello 同義字對應之後，第二個 hello`RunQueriesWithNonExistentTermsInIndex`呼叫輸出 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="7a3d2-144">After hello synonym map is uploaded and hello index is updated toouse hello synonym map, hello second `RunQueriesWithNonExistentTermsInIndex` call outputs hello following:</span></span>

~~~
Search hello entire index for hello phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
<span data-ttu-id="7a3d2-145">hello 尋找 hello hello 規則的文件的第一個查詢`five star=>luxury`。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-145">hello first query finds hello document from hello rule `five star=>luxury`.</span></span> <span data-ttu-id="7a3d2-146">hello 第二個查詢會展開 hello 搜尋使用`internet,wifi`和 hello 第三個同時使用`hotel, motel`和`economy,inexpensive=>budget`相符尋找 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-146">hello second query expands hello search using `internet,wifi` and hello third using both `hotel, motel` and `economy,inexpensive=>budget` in finding hello documents they matched.</span></span>

<span data-ttu-id="7a3d2-147">新增同義字完全變更 hello 搜尋經驗。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-147">Adding synonyms completely changes hello search experience.</span></span> <span data-ttu-id="7a3d2-148">在本教學課程中，hello 原始查詢會失敗 tooreturn 有意義的結果，即使我們的索引中的 hello 文件已相關。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-148">In this tutorial, hello original queries failed tooreturn meaningful results even though hello documents in our index were relevant.</span></span> <span data-ttu-id="7a3d2-149">藉由啟用同義字，我們可以展開條款共同搭配，hello 索引中的任何變更 toounderlying 資料索引 tooinclude。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-149">By enabling synonyms, we can expand an index tooinclude terms in common use, with no changes toounderlying data in hello index.</span></span>

## <a name="sample-application-source-code"></a><span data-ttu-id="7a3d2-150">範例應用程式的原始程式碼</span><span class="sxs-lookup"><span data-stu-id="7a3d2-150">Sample application source code</span></span>
<span data-ttu-id="7a3d2-151">您可以找到 hello 範例應用程式上使用此逐步解說中的 hello 完整原始碼[GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms)。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-151">You can find hello full source code of hello sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a3d2-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a3d2-152">Next steps</span></span>

* <span data-ttu-id="7a3d2-153">檢閱[如何在 Azure 搜尋 toouse 同義字](search-synonyms.md)</span><span class="sxs-lookup"><span data-stu-id="7a3d2-153">Review [How toouse synonyms in Azure Search](search-synonyms.md)</span></span>
* <span data-ttu-id="7a3d2-154">檢閱[同義字 REST API 文件](https://aka.ms/rgm6rq)</span><span class="sxs-lookup"><span data-stu-id="7a3d2-154">Review [Synonyms REST API documentation](https://aka.ms/rgm6rq)</span></span>
* <span data-ttu-id="7a3d2-155">瀏覽 hello 的 hello 參考[.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)和[REST API](https://docs.microsoft.com/rest/api/searchservice/)。</span><span class="sxs-lookup"><span data-stu-id="7a3d2-155">Browse hello references for hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
