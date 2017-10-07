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
# <a name="upload-data-tooazure-search-using-hello-net-sdk"></a>上傳資料 tooAzure 搜尋使用 hello.NET SDK
> [!div class="op_single_selector"]
> * [概觀](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

這篇文章將示範如何 toouse hello [Azure 搜尋.NET SDK](https://aka.ms/search-sdk) tooimport 資料到 Azure 搜尋索引。

在開始閱讀本逐步解說前，請先 [建立好 Azure 搜尋服務索引](search-what-is-an-index.md)。 本文也假設您已經建立`SearchServiceClient`物件中所示[建立 Azure 搜尋索引，使用.NET SDK hello](search-create-index-dotnet.md#CreateSearchServiceClient)。

> [!NOTE]
> 本文中的所有範例程式碼均以 C# 撰寫。 您可以找到 hello 完整的原始程式碼[GitHub 上](http://aka.ms/search-dotnet-howto)。 您也可以閱讀 hello [Azure 搜尋.NET SDK](search-howto-dotnet-sdk.md) for 的詳細逐步 hello 範例程式碼。

在訂單 toopush 文件至您的索引使用 hello.NET SDK，您必須：

1. 建立`SearchIndexClient`物件 tooconnect tooyour 搜尋索引。
2. 建立`IndexBatch`包含 hello 文件 toobe 新增、 修改或刪除。
3. 呼叫 hello`Documents.Index`方法您`SearchIndexClient`toosend hello `IndexBatch` tooyour 搜尋索引。

## <a name="create-an-instance-of-hello-searchindexclient-class"></a>建立 hello SearchIndexClient 類別的執行個體
索引使用 tooimport 資料 hello Azure 搜尋.NET SDK，您就需要 toocreate hello 的執行個體`SearchIndexClient`類別。 您可以建構此執行個體，但它更容易如果您已經有`SearchServiceClient`執行個體 toocall 其`Indexes.GetClient`方法。 例如，以下是您想要如何取得`SearchIndexClient`hello 索引從名為 「 旅館"`SearchServiceClient`名為`serviceClient`:

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> 在一般搜尋應用程式中，索引的管理和填入是由搜尋查詢的個別元件所處理。 `Indexes.GetClient`填入索引，因為它會將儲存您的方便 hello 提供另一個問題`SearchCredentials`。 其做法是傳遞 hello 管理金鑰，您使用的 toocreate hello `SearchServiceClient` toohello 新`SearchIndexClient`。 不過，在 hello 部分中執行查詢的應用程式，它是較佳的 toocreate hello`SearchIndexClient`直接，讓您可以傳入的查詢索引鍵，而不是管理金鑰。 這是與 hello 一致[最低權限原則](https://en.wikipedia.org/wiki/Principle_of_least_privilege)，都能協助您更安全的應用程式 toomake。 您可以進一步了解系統管理金鑰和查詢索引鍵中 hello [Azure 搜尋 REST API 參考](https://docs.microsoft.com/rest/api/searchservice/)。
> 
> 

`SearchIndexClient` 具有 `Documents` 屬性。 這個屬性提供所有 hello 方法需要 tooadd、 修改、 刪除或查詢文件索引中。

## <a name="decide-which-indexing-action-toouse"></a>決定哪個索引動作 toouse
使用.NET SDK hello tooimport 資料，您需要 toopackage 組成資料到`IndexBatch`物件。 `IndexBatch`封裝的集合`IndexAction`物件，其中每個包含文件和屬性，會告訴 Azure 搜尋哪些動作 tooperform 文 （上傳、 合併、 刪除等等）。 取決於哪些 hello 下列您選擇的動作，只有特定欄位必須包含每個文件：

| 動作 | 說明 | 每個文件的必要欄位 | 注意事項 |
| --- | --- | --- | --- |
| `Upload` |`Upload`動作是類似 tooan"upsert"(如果它是新插入和更新/取代如果它存在 hello 文件。 |索引鍵，再加上您想 toodefine 的任何其他欄位 |當更新/取代現有的文件，hello 要求中未指定任何欄位將會有其欄位太設定`null`。 這是即使 hello 欄位先前設定 tooa 非 null 值。 |
| `Merge` |更新現有文件以 hello 指定欄位。 Hello 文件不存在 hello 索引中，如果 hello 合併將會失敗。 |索引鍵，再加上您想 toodefine 的任何其他欄位 |您在合併中指定任何欄位將會取代 hello hello 文件中的現有欄位。 這包括類型 `DataType.Collection(DataType.String)`的欄位。 例如，如果 hello 文件包含欄位`tags`值`["budget"]`和執行的合併值`["economy", "pool"]`的`tags`，hello hello 的最終值`tags`欄位就是`["economy", "pool"]`。 而不會是 `["budget", "economy", "pool"]`。 |
| `MergeOrUpload` |此動作的行為類似`Merge`如果 hello 索引中的文件以 hello 給定索引鍵已經存在。 如果 hello 文件不存在，它的行為類似`Upload`與新的文件。 |索引鍵，再加上您想 toodefine 的任何其他欄位 |- |
| `Delete` |從 hello 索引中移除 hello 指定文件。 |僅索引鍵 |您指定其他非 hello 索引鍵欄位將會忽略所有的欄位。 如果您想 tooremove 個別欄位從 文件，請使用`Merge`相反地，並直接將 hello 欄位明確 toonull。 |

您可以指定要與 toouse 何種動作 hello 各種的靜態方法的 hello`IndexBatch`和`IndexAction`類別 hello 下一節中所示。

## <a name="construct-your-indexbatch"></a>建構您的 IndexBatch
現在您知道哪些動作 tooperform 上您的文件時，您就準備好 tooconstruct hello `IndexBatch`。 如何 hello 範例所示 toocreate 具有幾個不同的動作的批次。 請注意我們的範例會使用自訂類別，稱為`Hotel`對應 tooa hello 「 旅館"索引中的文件。

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

在此情況下，我們會使用`Upload`， `MergeOrUpload`，和`Delete`我們搜尋指定的動作，hello hello 上呼叫的方法為`IndexAction`類別。

假設此 "hotels" 索引範例已填入幾份文件。 請注意如何我們沒有 toospecify hello 可能文件的所有欄位時使用`MergeOrUpload`以及我們僅指定 hello 文件索引鍵的方式 (`HotelId`) 時使用`Delete`。

此外，請注意，您可以只包含單一索引要求中 too1000 文件。

> [!NOTE]
> 在此範例中，我們會套用不同的動作 toodifferent 文件。 如果您想 tooperform hello 相同動作的 hello 批次，而不是呼叫中的所有文件`IndexBatch.New`，您可以使用 hello 其他的靜態方法`IndexBatch`。 例如，您可以藉由呼叫 `IndexBatch.Merge`、`IndexBatch.MergeOrUpload` 或 `IndexBatch.Delete` 來建立批次。 這些方法會採用文件 (在此範例中為類型 `Hotel` 的物件) 集合，而非 `IndexAction` 物件。
> 
> 

## <a name="import-data-toohello-index"></a>匯入資料 toohello 索引
既然您已初始化`IndexBatch`物件，您可以將它傳送 toohello 索引藉由呼叫`Documents.Index`上您`SearchIndexClient`物件。 下列範例會示範如何 hello toocall `Index`，以及您需要 tooperform 一些額外步驟：

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

請注意 hello `try` / `catch`周圍 hello 呼叫 toohello`Index`方法。 hello catch 區塊處理編製索引的重要的錯誤案例。 如果您的 Azure 搜尋服務失敗的 tooindex hello 的批次中的 hello 某些文件`IndexBatchException`，所擲回`Documents.Index`。 如果您在服務負載過重時編制文件的索引，就會發生此情況。 **我們強烈建議您在程式碼中明確處理此情況。** 您可以延遲，然後重試失敗，索引 hello 文件或您可以記錄並繼續像 hello 範例會執行，或者，您可以執行根據您的應用程式資料的一致性需求的其他項目。

最後，hello 範例的程式碼 hello 上面兩秒的延遲。 索引會發生以非同步方式在 Azure 搜尋服務中，所以 hello 範例應用程式需要 toowait hello 文件可供搜尋簡短時間 tooensure。 通常只有在示範、測試和範例應用程式中，才需要這類延遲。

<a name="HotelClass"></a>

### <a name="how-hello-net-sdk-handles-documents"></a>Hello.NET SDK 的文件的處理方式
您可能想知道 hello Azure 搜尋.NET SDK 無法 tooupload 之類的使用者定義的類別執行個體的方式`Hotel`toohello 索引。 toohelp 回答這個問題，讓我們看看 hello`Hotel`對應 toohello 索引結構描述中定義的類別[建立 Azure 搜尋索引，使用.NET SDK hello](search-create-index-dotnet.md#DefineIndex):

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

hello 首先 toonotice 在於每一個公用屬性的`Hotel`對應 tooa 欄位在 hello 索引定義中，但有一點很重要： hello 名稱的每個公開時 hello 每個欄位的名稱會以小寫字母 （「 camel 命名法的情況"），啟動屬性`Hotel`開頭的大寫字母 （「 Pascal 大小寫 」）。 這是常見的案例中執行資料繫結其中 hello 目標結構描述是控制外部 hello hello 應用程式開發人員的.NET 應用程式。 而不是讓 tooviolate hello.NET 命名指導方針進行屬性名稱依照 camel 命名法的情況下，您可以告訴 hello SDK toomap hello 屬性名稱 toocamel 案例會自動以 hello`[SerializePropertyNamesAsCamelCase]`屬性。

> [!NOTE]
> hello Azure 搜尋.NET SDK 會使用 hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize 程式庫和您自訂的模型物件 tooand，從 JSON 還原序列化。 如有需要，您可以自訂這個序列化的過程。 您可以在[使用 JSON.NET 自訂序列化](search-howto-dotnet-sdk.md#JsonDotNet)中找到詳細資訊。 一個範例是使用 hello hello`[JsonProperty]`屬性 hello`DescriptionFr`上述的 hello 範例程式碼中的屬性。
> 
> 

hello 第二個重要好處 hello`Hotel`類別是 hello hello 公用屬性資料類型。 這些屬性的 hello.NET 型別對應 tootheir hello 索引定義中的對等的欄位類型。 例如，hello`Category`字串屬性會對應 toohello`category`欄位的型別`DataType.String`。 `bool?` 與 `DataType.Boolean`、`DateTimeOffset?` 與 `DataType.DateTimeOffset` 等之間也有類似的類型對應。 hello hello 型別對應的特定規則都會記錄以 hello`Documents.Get`方法在 hello [Azure 搜尋.NET SDK 參考](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_)。

此功能 toouse 雙向; 運作自己的類別為文件您也可以擷取搜尋結果，且擁有 hello SDK 自動還原序列化這些 tooa 類型您選擇的 hello 中所示[下一篇文章](search-query-dotnet.md)。

> [!NOTE]
> hello Azure 搜尋.NET SDK 也支援動態具類型的文件使用 hello`Document`類別，這是索引鍵/值對應的欄位名稱 toofield 值。 您不知道 hello 索引結構描述在設計階段，或者它會是很不方便 toobind toospecific 模型類別，這是非常實用。 中的所有 hello 方法 hello SDK 文件處理都具有多載，搭配 hello`Document`類別，以及接受泛型型別參數的強型別多載。 只有 hello 後者這篇文章中的 hello 範例程式碼中使用。
> 
> 

**為什麼您應該使用 Nullable 資料類型**

當設計您的模型類別 toomap tooan Azure 搜尋索引，我們建議您宣告實值類型的屬性，例如`bool`和`int`toobe 可為 null (例如，`bool?`而不是`bool`)。 如果您使用非 null 的屬性，您有太**保證**沒有文件索引中的包含 hello 對應欄位的 null 值。 Hello SDK 都 hello Azure 搜尋服務可協助您 tooenforce 這。

這不只是假設性的問題： 想像一下，讓您加入新欄位 tooan 現有索引型別的`DataType.Int32`。 在更新之後 hello 索引定義，所有文件必須針對該新欄位的 null 值 （因為所有類型都是可為 null 的 Azure 搜尋）。 若您搭配不可為 null，然後使用模型類別`int`該欄位的屬性，您會收到`JsonSerializationException`tooretrieve 文件時，就像這樣：

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

因此，我們建議您在模型類別中使用可為 Null 的類型，來做為最佳作法。

## <a name="next-steps"></a>後續步驟
填入您的 Azure 搜尋索引之後, 會準備 toostart 發出查詢 toosearch 文件。 如需詳細資料，請參閱 [查詢 Azure 搜尋服務索引](search-query-overview.md) 。

