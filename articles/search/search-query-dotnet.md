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
# <a name="query-your-azure-search-index-using-hello-net-sdk"></a>查詢您的 Azure 搜尋索引使用 hello.NET SDK
> [!div class="op_single_selector"]
> * [概觀](search-query-overview.md)
> * [入口網站](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

本文將告訴您如何 tooquery 索引使用 hello [Azure 搜尋.NET SDK](https://aka.ms/search-sdk)。

在開始閱讀本逐步解說前，請先[建立好 Azure 搜尋服務索引](search-what-is-an-index.md)，並[在索引中填入資料](search-what-is-data-import.md)。

> [!NOTE]
> 本文中的所有範例程式碼均以 C# 撰寫。 您可以找到 hello 完整的原始程式碼[GitHub 上](http://aka.ms/search-dotnet-howto)。 您也可以閱讀 hello [Azure 搜尋.NET SDK](search-howto-dotnet-sdk.md) for 的詳細逐步 hello 範例程式碼。

## <a name="identify-your-azure-search-services-query-api-key"></a>識別 Azure 搜尋服務的查詢 API 金鑰
既然您已經建立 Azure 搜尋索引，您會使用.NET SDK hello 就緒 tooissue 查詢。 首先，您將需要 tooobtain hello 查詢 api 金鑰所產生的其中一個 hello 您佈建的搜尋服務。 此 api 金鑰會傳送 hello.NET SDK 的每個要求 tooyour 服務。 擁有有效的索引鍵建立信任關係，針對每個要求，hello 應用程式正在傳送嗨要求和處理它的 hello 服務之間。

1. toofind 服務的 api 金鑰才能登入 toohello [Azure 入口網站](https://portal.azure.com/)
2. 移 tooyour Azure 搜尋服務的刀鋒視窗
3. 按一下 hello 「 金鑰 」 圖示

服務會有系統管理金鑰和查詢金鑰。

* 您的主要和次要*系統管理金鑰*tooall 作業，包括 hello 能力 toomanage hello 服務授與的完整權限、 建立和刪除索引、 索引子和資料來源。 有兩個索引鍵，讓您可以繼續 toouse hello 次要索引鍵，如果您決定 tooregenerate hello 主索引鍵，反之亦然。
* 您*查詢索引鍵*授與唯讀存取 tooindexes 和文件，並發出搜尋要求的 tooclient 通常分散式應用程式。

基於 hello 查詢索引，您可以使用您的查詢索引鍵的其中一個。 系統管理金鑰也可以用於查詢，但您應該查詢索引鍵使用您的應用程式程式碼中，這更如下所示 hello[最低權限原則](https://en.wikipedia.org/wiki/Principle_of_least_privilege)。

## <a name="create-an-instance-of-hello-searchindexclient-class"></a>建立 hello SearchIndexClient 類別的執行個體
以 hello Azure 搜尋.NET SDK tooissue 查詢，您將需要 toocreate hello 的執行個體`SearchIndexClient`類別。 這個類別有數個建構函式。 您想要的 hello 接受您的搜尋服務名稱、 索引名稱和`SearchCredentials`做為參數的物件。 `SearchCredentials` 會包裝您的 API 金鑰。

hello 的下列程式碼會建立新`SearchIndexClient`hello 「 旅館"索引 (在中建立[建立 Azure 搜尋索引，使用.NET SDK hello](search-create-index-dotnet.md)) 使用 hello 搜尋服務名稱和儲存在 hello 應用程式組態中的 api 金鑰值檔案 (`appsettings.json` hello hello 案例[範例應用程式](http://aka.ms/search-dotnet-howto)):

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

`SearchIndexClient` 具有 `Documents` 屬性。 這個屬性提供所有 hello 方法需要 tooquery Azure 搜尋索引。

## <a name="query-your-index"></a>查詢您的索引
搜尋以 hello.NET SDK 的很簡單，呼叫 hello`Documents.Search`方法上的您`SearchIndexClient`。 這個方法會採用的幾個參數，包括 hello 搜尋文字，連同`SearchParameters`可以是使用的 toofurther 縮小 hello 查詢的物件。

#### <a name="types-of-queries"></a>查詢類型
hello 兩個主要[查詢類型](search-query-overview.md#types-of-queries)您將使用是`search`和`filter`。 `search` 查詢會搜尋索引中所有可搜尋欄位的一或多個字詞。 `filter` 查詢可跨索引的所有可篩選欄位評估布林運算式。

搜尋和篩選器都是使用 hello`Documents.Search`方法。 搜尋查詢，請傳入 hello`searchText`參數，而篩選條件運算式可以傳入 hello`Filter`屬性 hello`SearchParameters`類別。 toofilter 而不必搜尋，只要將`"*"`hello`searchText`參數。 toosearch 但不會篩選，只保留 hello`Filter`屬性未設定，或請不要傳入`SearchParameters`所有執行個體。

#### <a name="example-queries"></a>查詢範例
下列範例程式碼的 hello 示範幾個不同的方式 tooquery hello 「 旅館"索引定義中[建立 Azure 搜尋索引，使用.NET SDK hello](search-create-index-dotnet.md#DefineIndex)。 請注意，hello 文件以 hello 搜尋結果傳回執行個體的 hello`Hotel`類別，定義在[在 Azure 搜尋中使用的資料匯入 hello.NET SDK](search-import-data-dotnet.md#HotelClass)。 hello 範例程式碼會使用`WriteDocuments`方法 toooutput hello 搜尋結果 toohello 主控台。 這個方法是 hello 下一節中所述。

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

## <a name="handle-search-results"></a>處理搜尋結果
hello`Documents.Search`方法會傳回`DocumentSearchResult`包含 hello hello 查詢結果的物件。 hello 前一節中的 hello 範例使用呼叫的方法`WriteDocuments`toooutput hello 搜尋結果 toohello 主控台：

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

以下是什麼 hello 結果看起來像是 hello hello 前一節中的查詢，假設 hello 「 旅館"索引填入資料中的 hello 範例[在 Azure 搜尋中使用的資料匯入 hello.NET SDK](search-import-data-dotnet.md):

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

上述的 hello 範例程式碼會使用 hello 主控台 toooutput 搜尋結果。 您同樣必須 toodisplay 搜尋結果在自己的應用程式。 請參閱[GitHub 上的這個範例](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample)toorender 搜尋結果中的 ASP.NET MVC 為基礎的 web 應用程式的方式的範例。

