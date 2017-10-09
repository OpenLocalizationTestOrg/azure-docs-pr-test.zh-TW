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
# <a name="synonym-preview-c-tutorial-for-azure-search"></a>Azure 搜尋服務的同義字 (預覽) C# 教學課程

同義字展開查詢比對視為語意相等 toohello 輸入的詞彙的詞彙。 例如，您可以包含 hello 條款"automobile"或"vehicle"的"car"toomatch 文件。

在 Azure 搜尋服務中，同義字會定義於*同義字對應*中，透過*對應規則*讓相等的詞彙產生關聯。 您可以建立多個同義字對應、 張貼為整個服務的資源可用 tooany 索引，然後參考 哪一個 toouse hello 欄位層級。 在查詢時，除了 toosearching Azure 搜尋索引，會在同義字地圖中，查閱如果 hello 查詢中使用的欄位上指定的其中一個。

> [!NOTE]
> hello 同義字功能是目前在預覽，並僅支援在 hello 最新預覽版 API 和 SDK 版本 (api 版本 = 2016年-09-01-預覽，SDK 版本 4.x 預覽)。 目前 Azure 入口網站並不支援此功能。 預覽 API 不受 SLA 約束，且預覽功能可能會變更，因此不建議在生產應用程式中使用它們。

## <a name="prerequisites"></a>必要條件

教學課程需求 hello 如下：

* [Visual Studio](https://www.visualstudio.com/downloads/)
* [Azure 搜尋服務](search-create-service-portal.md)
* [預覽版本的 Microsoft.Azure.Search .NET 程式庫](https://aka.ms/search-sdk-preview)
* [如何從.NET 應用程式的 toouse Azure 搜尋](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a>概觀

前-和-後查詢示範 hello 值的同義字。 在本教學課程中，我們使用可執行查詢並傳回範例索引結果的範例應用程式。 hello 範例應用程式會建立名為 「 旅館"填入 兩份文件的小型索引。 hello 應用程式執行搜尋查詢，使用詞彙並不會出現在 hello 索引中的片語，以及 hello 同義字 」 功能，則問題 hello 相同搜尋一次。 hello 的下列程式碼示範 hello 整體流程。

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
hello 步驟 toocreate 並填入 hello 範例索引中會說明[toouse Azure 搜尋.NET 應用程式如何](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)。

## <a name="before-queries"></a>「之前」查詢

在 `RunQueriesWithNonExistentTermsInIndex` 中，我們使用 "five star"、"internet" 和 "economy AND hotel" 發出搜尋查詢。
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
Hello 兩個索引的文件都不包含 hello 詞彙，所以我們取得 hello 以下第一次輸出從 hello `RunQueriesWithNonExistentTermsInIndex`。
~~~
Search hello entire index for hello phrase "five star":

no document matched

Search hello entire index for hello term 'internet':

no document matched

Search hello entire index for hello terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a>啟用同義字

啟用同義字的程序包含兩步驟。 我們先定義和上傳的同義字規則，然後設定 欄位 toouse 它們。 hello 程序中所述`UploadSynonyms`和`EnableSynonymsInHotelsIndex`。

1. 新增同義字對應 tooyour 搜尋服務。 在`UploadSynonyms`，我們在我們的同義資料表對應 ' desc synonymmap' 中定義四個規則，並上傳 toohello 服務。
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
同義字對應必須符合 toohello 開放原始碼標準`solr`格式。 hello 格式述[在 Azure 搜尋的同義字](search-synonyms.md)hello 區段下方`Apache Solr synonym format`。

2. 設定可搜尋的欄位 toouse hello 同義字對應 hello 索引定義中。 在`EnableSynonymsInHotelsIndex`，我們會啟用兩個欄位上的同義字`category`和`tags`所設定的 hello `synonymMaps` hello 屬性 toohello 名稱新上傳的同義資料表對應。
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
當您新增同義字對應時，不需要重建索引。 您可以新增同義字對應 tooyour 服務，並再修改任何索引 toouse hello 新同義字對應中的現有欄位定義。 hello 加入的新的屬性索引可用性沒有任何影響。 hello 一樣中停用欄位的同義字。 您可以直接將 hello`synonymMaps`屬性 tooan 空白清單。
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a>「之後」查詢

Hello 同義字對應上傳並 hello 索引是更新的 toouse hello 同義字對應之後，第二個 hello`RunQueriesWithNonExistentTermsInIndex`呼叫輸出 hello 下列：

~~~
Search hello entire index for hello phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
hello 尋找 hello hello 規則的文件的第一個查詢`five star=>luxury`。 hello 第二個查詢會展開 hello 搜尋使用`internet,wifi`和 hello 第三個同時使用`hotel, motel`和`economy,inexpensive=>budget`相符尋找 hello 文件。

新增同義字完全變更 hello 搜尋經驗。 在本教學課程中，hello 原始查詢會失敗 tooreturn 有意義的結果，即使我們的索引中的 hello 文件已相關。 藉由啟用同義字，我們可以展開條款共同搭配，hello 索引中的任何變更 toounderlying 資料索引 tooinclude。

## <a name="sample-application-source-code"></a>範例應用程式的原始程式碼
您可以找到 hello 範例應用程式上使用此逐步解說中的 hello 完整原始碼[GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms)。

## <a name="next-steps"></a>後續步驟

* 檢閱[如何在 Azure 搜尋 toouse 同義字](search-synonyms.md)
* 檢閱[同義字 REST API 文件](https://aka.ms/rgm6rq)
* 瀏覽 hello 的 hello 參考[.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)和[REST API](https://docs.microsoft.com/rest/api/searchservice/)。
