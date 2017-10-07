---
title: "aaaHow toouse Azure 搜尋.NET 應用程式 |Microsoft 文件"
description: "如何從.NET 應用程式的 toouse Azure 搜尋"
services: search
documentationcenter: 
author: brjohnstmsft
manager: jlembicz
editor: 
ms.assetid: 93653341-c05f-4cfd-be45-bb877f964fcb
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 8e13fbe5549547d65941b856ce5a90611261388f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-search-from-a-net-application"></a>如何從.NET 應用程式的 toouse Azure 搜尋
這篇文章會逐步解說 tooget 您啟動並執行以 hello [Azure 搜尋.NET SDK](https://aka.ms/search-sdk)。 您可以使用 hello.NET SDK tooimplement 豐富您的應用程式使用 Azure Search 中搜尋經驗。

## <a name="whats-in-hello-azure-search-sdk"></a>什麼是在 hello Azure 搜尋 SDK
hello SDK 包含用戶端程式庫`Microsoft.Azure.Search`。 您的索引、 資料來源和索引子，可讓您 toomanage，以及上傳和管理文件，並執行查詢，完全不需要包含 hello 細節的 HTTP 和 JSON toodeal。

hello 用戶端程式庫定義類別，例如`Index`， `Field`，和`Document`，以及等作業`Indexes.Create`和`Documents.Search`上 hello`SearchServiceClient`和`SearchIndexClient`類別。 這些類別會組織成下列命名空間的 hello:

* [Microsoft.Azure.Search](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [Microsoft.Azure.Search.Models](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

現在上市 hello hello Azure 搜尋.NET SDK 目前版本。 如果您想要 tooprovide 意見反應對我們 tooincorporate hello 未來的版本，請造訪我們[意見反應頁面](https://feedback.azure.com/forums/263029-azure-search/)。

hello.NET SDK 支援的版本為`2016-09-01`的 hello [Azure 搜尋 REST API](https://docs.microsoft.com/rest/api/searchservice/)。 此版本現在包含自訂分析器支援及 Azure Blob 和 Azure 資料表索引子支援。 預覽功能*不*此版本中，例如支援 JSON 和 CSV 檔案編製索引的一部分位於[預覽](search-api-2015-02-28-preview.md)，而且可透過較舊的 hello [hello.NET SDK 2.0 preview 版本](https://aka.ms/search-sdk-preview).

此 SDK 不支援[管理作業](https://docs.microsoft.com/rest/api/searchmanagement/)，例如建立及調整搜尋服務和管理 API 金鑰。 如果您需要 toomanage.NET 應用程式從您搜尋的資源，您可以使用 hello [Azure 搜尋.NET 管理 SDK](https://aka.ms/search-mgmt-sdk)。

## <a name="upgrading-toohello-latest-version-of-hello-sdk"></a>Toohello hello SDK 最新版本升級
如果您已經使用較舊版本的 hello Azure 搜尋.NET SDK，而且您想要 tooupgrade toohello 正式推出新版、[本文](search-dotnet-sdk-migration.md)說明如何。

## <a name="requirements-for-hello-sdk"></a>Hello SDK 的需求
1. Visual Studio 2017。
2. 擁有 Azure Search 服務。 在順序 toouse hello SDK，您將需要 hello 您的服務名稱和一或多個 API 金鑰。 [Hello 入口網站中建立服務](search-create-service-portal.md)將協助您完成這些步驟。
3. 下載 hello Azure 搜尋.NET SDK [NuGet 封裝](http://www.nuget.org/packages/Microsoft.Azure.Search)使用 Visual Studio 中的 管理 NuGet 封裝 」。 只要搜尋 hello 封裝名稱`Microsoft.Azure.Search`NuGet.org 上。

hello Azure 搜尋.NET SDK 支援以.NET Framework 4.6 hello 和.NET Core 為目標的應用程式。

## <a name="core-scenarios"></a>核心案例
有幾件事，您將需要 toodo 搜尋應用程式中。 本教學課程中涵蓋了這些主要情節：

* 建立索引
* 擴展文件以 hello 索引
* 使用全文檢索搜尋和篩選來搜尋文件

後面的 hello 範例程式碼將說明其中每一項。 您自己的應用程式中的可用 toouse hello 程式碼片段。

### <a name="overview"></a>概觀
hello 會瀏覽我們的範例應用程式會建立新的名為 「 旅館"，索引填入幾個文件，則會執行一些搜尋查詢。 以下是 hello 主程式，顯示 hello 整體流程：

```csharp
// This sample shows how toodelete, create, upload documents and query an index
static void Main(string[] args)
{
    IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
    IConfigurationRoot configuration = builder.Build();

    SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

    Console.WriteLine("{0}", "Deleting index...\n");
    DeleteHotelsIndexIfExists(serviceClient);

    Console.WriteLine("{0}", "Creating index...\n");
    CreateHotelsIndex(serviceClient);

    ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

    Console.WriteLine("{0}", "Uploading documents...\n");
    UploadDocuments(indexClient);

    ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

    RunQueries(indexClientForQueries);

    Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> 您可以找到 hello 範例應用程式上使用此逐步解說中的 hello 完整原始碼[GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo)。
> 
>

我們會逐步說明， 我們第一次需要新 toocreate `SearchServiceClient`。 此物件可讓您 toomanage 索引。 其中一個順序 tooconstruct，您需要 tooprovide 您的 Azure 搜尋服務名稱，以及管理 API 金鑰。 您可以輸入此資訊在 hello`appsettings.json`檔案的 hello[範例應用程式](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo)。

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

> [!NOTE]
> 如果您提供正確的索引鍵 （例如，查詢索引鍵管理金鑰所需的位置），hello`SearchServiceClient`將會擲回`CloudException`hello 錯誤訊息 「 禁止 」 hello 與第一次您呼叫作業方法，例如`Indexes.Create`。 如果發生這種情況 tooyou，請仔細檢查我們的 API 金鑰。
> 
> 

hello 接下來的幾個幾行呼叫方法 toocreate 名為 「 旅館 」，必須先刪除它，如果已經存在的索引。 稍後我們會逐項執行這些方法。

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

接下來，hello 索引需要 toobe 填入。 toodo，我們需要`SearchIndexClient`。 有兩種方式 tooobtain 其中一個： 建構，或呼叫`Indexes.GetClient`上 hello `SearchServiceClient`。 我們為了方便起見使用後者 hello。

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> 在一般搜尋應用程式中，索引的管理和填入是由搜尋查詢的個別元件所處理。 `Indexes.GetClient`填入索引，因為它會將儲存您的方便 hello 提供另一個問題`SearchCredentials`。 其做法是傳遞 hello 管理金鑰，您使用的 toocreate hello `SearchServiceClient` toohello 新`SearchIndexClient`。 不過，在 hello 部分中執行查詢的應用程式，它是較佳的 toocreate hello`SearchIndexClient`直接，讓您可以傳入的查詢索引鍵，而不是管理金鑰。 這是與 hello 最低權限原則一致，而且可協助您更安全的應用程式 toomake。 您可以 [在這裡](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization)深入了解系統管理金鑰和查詢金鑰。
> 
> 

現在，我們已經`SearchIndexClient`，我們可以擴展 hello 索引。 這要使用另一個方法來執行，稍後我們會逐項說明。

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

最後，我們會執行幾個搜尋查詢，並顯示 hello 結果。 這次我們使用不同的 `SearchIndexClient`：

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

我們要探討 hello`RunQueries`稍後方法。 以下是新 hello 程式碼 toocreate hello `SearchIndexClient`:

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

這次我們使用的查詢索引鍵，因為我們不需要寫入權限 toohello 索引。 您可以輸入此資訊在 hello`appsettings.json`檔案的 hello[範例應用程式](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo)。

如果您執行此應用程式具有有效的服務名稱和 API 金鑰，hello 輸出看起來應該像這樣：

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents toobe indexed...
    
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
    
    Complete.  Press any key tooend application...

這篇文章的 hello 結尾會提供 hello 完整 hello 應用程式的原始程式碼。

接下來，我們將接受 hello 所呼叫的方法進一步檢視`Main`。

### <a name="creating-an-index"></a>建立索引
在建立之後`SearchServiceClient`下, 一步 hello`Main`未是刪除 hello 「 旅館"的索引，如果已經存在。 是由下列方法 hello:

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

這個方法會使用指定的 hello `SearchServiceClient` toocheck 如果 hello 索引存在，而且如果是，刪除它。

> [!NOTE]
> 這篇文章中的 hello 範例程式碼為了簡單起見使用 hello Azure 搜尋.NET SDK 的 hello 同步方法。 我們建議您在自己的應用程式 tookeep 使用 hello 非同步方法加以擴充且回應迅速。 例如，在 hello 方法，您可以使用`ExistsAsync`和`DeleteAsync`而不是`Exists`和`Delete`。
> 
> 

接著，`Main` 會呼叫此方法建立新的 "hotels" 索引：

```csharp
private static void CreateHotelsIndex(SearchServiceClient serviceClient)
{
    var definition = new Index()
    {
        Name = "hotels",
        Fields = FieldBuilder.BuildForType<Hotel>()
    };

    serviceClient.Indexes.Create(definition);
}
```

這個方法會建立新`Index`物件及一串`Field`定義 hello hello 新索引的結構描述的物件。 每個欄位均有一個名稱、資料類型和一些屬性，以用於定義欄位的搜尋行為。 hello`FieldBuilder`類別會使用反映 toocreate 一份`Field`hello 索引藉由檢查物件 hello 公用屬性和屬性的指定 hello`Hotel`模型類別。 我們將探討 hello`Hotel`稍後類別。

> [!NOTE]
> 您一律可以建立 hello 清單`Field`物件，而使用非直接`FieldBuilder`視。 例如，您可能不想 toouse 模型類別，或您可能需要 toouse 現有的模型類別，您不想 toomodify 藉由加入屬性。
>
> 

此外 toofields，您也可以新增評分設定檔、 建議工具或 CORS 選項 toohello （省略來自 hello 範例為求簡潔） 的索引。 您可以找到 hello Index 物件和毛利的構成部分的詳細資訊，在 hello [SDK 參考](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index)，同時也 hello [Azure 搜尋 REST API 參考](https://docs.microsoft.com/rest/api/searchservice/)。

### <a name="populating-hello-index"></a>擴展 hello 索引
中的下一個步驟 hello `Main` toopopulate hello 新建的索引。 這是 hello 下列方法：

```csharp
private static void UploadDocuments(ISearchIndexClient indexClient)
{
    var hotels = new Hotel[]
    {
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
        },
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
        },
        new Hotel() 
        { 
            HotelId = "3", 
            BaseRate = 129.99,
            Description = "Close tootown hall and hello river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

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
}
```

此方法分四個部分。 hello 會先建立的陣列`Hotel`將做為輸入的資料 tooupload toohello 索引的物件。 為簡單起見，此資料採硬式編碼。 在您的應用程式中，資料可能會來自像是 SQL 資料庫的外部資料來源。

hello 第二個部分會建立`IndexBatch`包含 hello 文件。 您指定要在您建立，在此情況下所呼叫的 hello 階段 tooapply toohello 批次的 hello 作業`IndexBatch.Upload`。 hello 批次則上傳的 toohello Azure 搜尋索引 hello`Documents.Index`方法。

> [!NOTE]
> 在此範例中，我們只上傳文件。 如果您想 toomerge 變更為現有的文件或刪除文件，您可以藉由呼叫來建立批次`IndexBatch.Merge`， `IndexBatch.MergeOrUpload`，或`IndexBatch.Delete`改為。 您也可以藉由呼叫混合不同的作業，以單一批次`IndexBatch.New`，其可接受的集合`IndexAction`物件，其中每個會告訴 Azure 搜尋 tooperform 文件上的特定作業。 您可以建立每個`IndexAction`與它自己的作業，透過呼叫 hello 對應的方法，例如`IndexAction.Merge`， `IndexAction.Upload`，依此類推。
> 
> 

hello 第三個部分，這個方法是處理編製索引的重要的錯誤案例的 catch 區塊。 如果您的 Azure 搜尋服務失敗的 tooindex hello 的批次中的 hello 某些文件`IndexBatchException`，所擲回`Documents.Index`。 如果您在服務負載過重時編制文件的索引，就會發生此情況。 **我們強烈建議您在程式碼中明確處理此情況。** 您可以延遲，然後重試失敗，索引 hello 文件或您可以記錄並繼續像 hello 範例會執行，或者，您可以執行根據您的應用程式資料的一致性需求的其他項目。

> [!NOTE]
> 您可以使用 hello`FindFailedActionsToRetry`方法 tooconstruct 新批次包含只 hello 過先前的呼叫失敗的動作`Index`。 已記錄 hello 方法[這裡](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_)，而且沒有 tooproperly 如何使用它的討論[在 StackOverflow 上](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry)。
>
>

最後，hello`UploadDocuments`方法兩秒鐘的延遲。 索引會發生以非同步方式在 Azure 搜尋服務中，所以 hello 範例應用程式需要 toowait hello 文件可供搜尋簡短時間 tooensure。 通常只有在示範、測試和範例應用程式中，才需要這類延遲。

#### <a name="how-hello-net-sdk-handles-documents"></a>Hello.NET SDK 的文件的處理方式
您可能想知道 hello Azure 搜尋.NET SDK 無法 tooupload 之類的使用者定義的類別執行個體的方式`Hotel`toohello 索引。 toohelp 回答這個問題，讓我們看看 hello`Hotel`類別：

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// hello SerializePropertyNamesAsCamelCase attribute is defined in hello Azure Search .NET SDK.
// It ensures that Pascal-case property names in hello model class are mapped toocamel-case
// field names in hello index.
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [System.ComponentModel.DataAnnotations.Key]
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
}
```

hello 首先 toonotice 在於每一個公用屬性的`Hotel`對應 tooa 欄位在 hello 索引定義中，但有一點很重要： hello 名稱的每個公開時 hello 每個欄位的名稱會以小寫字母 （「 camel 命名法的情況"），啟動屬性`Hotel`開頭的大寫字母 （「 Pascal 大小寫 」）。 這是常見的案例中執行資料繫結其中 hello 目標結構描述是控制外部 hello hello 應用程式開發人員的.NET 應用程式。 而不是讓 tooviolate hello.NET 命名指導方針進行屬性名稱依照 camel 命名法的情況下，您可以告訴 hello SDK toomap hello 屬性名稱 toocamel 案例會自動以 hello`[SerializePropertyNamesAsCamelCase]`屬性。

> [!NOTE]
> hello Azure 搜尋.NET SDK 會使用 hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize 程式庫和您自訂的模型物件 tooand，從 JSON 還原序列化。 如有需要，您可以自訂這個序列化的過程。 如需詳細資訊，請參閱[使用 JSON.NET 自訂序列化](#JsonDotNet)。
> 
> 

hello 第二個東西 toonotice 是 hello 屬性例如`IsFilterable`， `IsSearchable`， `Key`，和`Analyzer`，裝飾每個公用屬性。 這些屬性都會直接對應 toohello [hello Azure 搜尋索引的對應屬性](https://docs.microsoft.com/rest/api/searchservice/create-index#request)。 hello`FieldBuilder`類別會使用這些 tooconstruct 欄位定義 hello 索引。

hello 第三個重要的是有關 hello`Hotel`類別是 hello hello 公用屬性資料類型。 這些屬性的 hello.NET 型別對應 tootheir hello 索引定義中的對等的欄位類型。 例如，hello`Category`字串屬性會對應 toohello`category`欄位的型別`Edm.String`。 有類似的型別對應之間`bool?`和`Edm.Boolean`，`DateTimeOffset?`和`Edm.DateTimeOffset`，等 hello 特定規則的 hello 型別對應都會記錄以 hello`Documents.Get`方法在 hello [Azure 搜尋.NET SDK參考](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_)。 hello`FieldBuilder`類別會負責這項對應，但仍然可以很有幫助 toounderstand 以防您需要 tootroubleshoot 序列化的任何問題。

此功能 toouse 雙向; 運作自己的類別為文件您也可以擷取搜尋結果，且擁有 hello SDK 自動還原序列化它們 tooa 類型的您的選擇，我們將會看到 hello 下一節。

> [!NOTE]
> hello Azure 搜尋.NET SDK 也支援動態具類型的文件使用 hello`Document`類別，這是索引鍵/值對應的欄位名稱 toofield 值。 您不知道 hello 索引結構描述在設計階段，或者它會是很不方便 toobind toospecific 模型類別，這是非常實用。 中的所有 hello 方法 hello SDK 文件處理都具有多載，搭配 hello`Document`類別，以及接受泛型型別參數的強型別多載。 只有 hello 後者可用在 hello 範例程式碼在本教學課程。 hello`Document`類別繼承自`Dictionary<string, object>`。 如需其他詳細資訊，請前往[這裡](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document)。
> 
> 

**為什麼您應該使用 Nullable 資料類型**

當設計您的模型類別 toomap tooan Azure 搜尋索引，我們建議您宣告實值類型的屬性，例如`bool`和`int`toobe 可為 null (例如，`bool?`而不是`bool`)。 如果您使用非 null 的屬性，您有太**保證**沒有文件索引中的包含 hello 對應欄位的 null 值。 Hello SDK 都 hello Azure 搜尋服務可協助您 tooenforce 這。

這不只是假設性的問題： 想像一下，讓您加入新欄位 tooan 現有索引型別的`Edm.Int32`。 在更新之後 hello 索引定義，所有文件必須針對該新欄位的 null 值 （因為所有類型都是可為 null 的 Azure 搜尋）。 若您搭配不可為 null，然後使用模型類別`int`該欄位的屬性，您會收到`JsonSerializationException`tooretrieve 文件時，就像這樣：

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

因此，我們建議您在模型類別中使用可為 Null 的類型，來做為最佳作法。

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a>使用 JSON.NET 自訂序列化
hello SDK 會使用 JSON.NET 進行序列化和還原序列化文件。 您可以自訂序列化和還原序列化如有需要定義您自己`JsonConverter`或`IContractResolver`(請參閱 hello [JSON.NET 文件](http://www.newtonsoft.com/json/help/html/Introduction.htm)如需詳細資訊)。 當您想 tooadapt 現有的模型類別，從您的應用程式與 Azure 搜尋中，以及其他更進階的案例搭配使用時，這非常有用。 例如，使用自訂序列化，您可以：

* 包含或排除模型類別的特定屬性儲存為文件欄位。
* 在程式碼的屬性名稱和索引的欄位名稱之間進行對應。
* 建立可用於將屬性 toodocument 欄位對應的自訂屬性。

您可以找到 hello GitHub 上的 Azure 搜尋.NET SDK 的 hello 單元測試中實作自訂序列化的範例。 [這個資料夾](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models)是好的起點。 它包含 hello 自訂序列化測試所使用的類別。

### <a name="searching-for-documents-in-hello-index"></a>搜尋文件以 hello 索引
hello hello 範例應用程式中的最後一個步驟是 toosearch hello 索引中的某些文件。 hello 下列方法會執行此動作：

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
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
}
```

每次執行查詢時，這個方法都會先建立新的 `SearchParameters` 物件。 這是使用的 toospecify hello 查詢，例如排序、 篩選、 分頁和 faceting 的其他選項。 在此方法中，我們正在設定 hello `Filter`， `Select`， `OrderBy`，和`Top`不同查詢的屬性。 所有的 hello`SearchParameters`屬性會記載[這裡](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters)。

hello 下一個步驟是 tooactually 執行 hello 搜尋查詢。 這是使用 hello`Documents.Search`方法。 針對每個查詢中，我們傳遞為字串 hello 搜尋文字 toouse (或`"*"`如果沒有任何搜尋文字)，再加上 hello 搜尋稍早建立的參數。 我們也指定`Hotel`hello 型別參數為`Documents.Search`，hello 搜尋結果中向 hello SDK toodeserialize 文件類型的物件至`Hotel`。

> [!NOTE]
> 您可以找到有關 hello 搜尋查詢運算式語法的詳細資訊[這裡](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search)。
> 
> 

最後，在每個查詢之後這個方法逐一查看所有 hello 相符項目在 hello 搜尋結果中，列印每個文件 toohello 主控台：

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

接著我們探討每個 hello 查詢。 以下是 hello 程式碼 tooexecute hello 第一個查詢：

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

在此情況下，我們要搜尋飯店符合 hello word"budget"，而且我們想 tooget 只傳回 hello 飯店名稱，為指定的 hello`Select`參數。 Hello 結果如下：

    Name: Roach Motel

接下來，我們想要每晚率小於 $150 toofind hello 旅館，只能傳回 hello 旅館識別碼和描述：

```csharp
parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

此查詢會使用 OData`$filter`運算式`baseRate lt 150`，toofilter hello hello 索引文件。 您可以進一步了解 Azure 搜尋支援的 OData 語法 hello[這裡](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search)。

以下是 hello hello 查詢結果：

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river

接下來，我們想 toofind hello 前兩個旅館，最近重新裝修，並顯示 hello 飯店名稱和最後一個 renovation 日期。 Hello 程式碼如下： 

```csharp
parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

在此情況下，我們一次使用 OData 語法 toospecify hello`OrderBy`參數做為`lastRenovationDate desc`。 我們也將設定`Top`too2 tooensure 我們只能取得 hello 前兩個文件。 之前，我們設定`Select`toospecify 應傳回哪些欄位。

Hello 結果如下：

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

最後，我們想 toofind hello 字"motel"相符的所有旅館：

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

以下是 hello 結果，包含所有欄位，因為我們並未指定 hello 和`Select`屬性：

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

這個步驟會完成 hello 教學課程中，但不在此停止。 **後續步驟** 會提供可深入了解 Azure 搜尋服務的其他資源。

## <a name="next-steps"></a>後續步驟
* 瀏覽 hello 的 hello 參考[.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)和[REST API](https://docs.microsoft.com/rest/api/searchservice/)。
* 使用 [影片與其他範例和教學課程](search-video-demo-tutorial-list.md)加深知識。
* 檢閱[命名慣例](https://docs.microsoft.com/rest/api/searchservice/Naming-rules)toolearn hello 規則命名各種物件。
* 檢閱 Azure 搜尋服務 [支援的資料類型](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) 。
