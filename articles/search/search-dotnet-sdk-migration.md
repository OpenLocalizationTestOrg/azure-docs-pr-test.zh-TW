---
title: "aaaUpgrading toohello Azure 搜尋.NET SDK 1.1 版 |Microsoft 文件"
description: "升級 toohello Azure 搜尋.NET SDK 1.1 版"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 66f89958-a320-4a24-87f9-69315848909f
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 291ae5731546e47b3c22c721d3552a79bdea80c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-net-sdk-version-3"></a>升級 toohello Azure 搜尋.NET SDK 版本 3
如果您使用版本 2.0 preview 或舊版的 hello [Azure 搜尋.NET SDK](https://aka.ms/search-sdk)，本文將協助您升級您的應用程式 toouse 第 3 版。

多個一般逐步解說中的 hello SDK 包括範例，請參閱[toouse Azure 搜尋.NET 應用程式如何](search-howto-dotnet-sdk.md)。

第 3 版的 hello Azure 搜尋.NET SDK 包含從舊版的某些變更。 這些變更大部分是次要變更，所以變更程式碼應該只需要最少的工作。 請參閱[步驟 tooupgrade](#UpgradeSteps)如需有關指示 toochange 您程式碼 toouse hello 新的 SDK 版本。

> [!NOTE]
> 如果您使用版本 1.0.2-preview 或更舊版本，您應該先升級 tooversion 1.1，然後再升級 tooversion 3。 請參閱[附錄： 步驟 tooupgrade tooversion 1.1](#UpgradeStepsV1)如需相關指示。
>
> 您的 Azure 搜尋服務執行個體支援多個 REST API 版本，包括 hello 最新版本。 您可以繼續 toouse 版本時，它不會再 hello 最新的其中一個，但我們建議您移轉您的程式碼 toouse hello 最新版本。 當使用 hello REST API，您必須指定 hello API 版本 hello api-version 參數透過每個要求中。 當使用 hello.NET SDK，hello 您所使用的 SDK hello 版本會決定 hello 對應 hello REST API 的版本。 如果您使用較舊的 SDK，您可以繼續 toorun 未變更該程式碼即使 hello 服務升級的 toosupport 較新的 API 版本。

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a>版本 3 的新功能
Hello Azure 搜尋.NET SDK 目標 hello 最新第 3 版上市 hello Azure 搜尋 REST API，特別是 2016年-09-01 版本。 這使得可能 toouse 許多新的 Azure 搜尋.NET 應用程式，包括 hello 下列功能：

* [自訂分析器](https://aka.ms/customanalyzers)
* [Azure Blob 儲存體](search-howto-indexing-azure-blob-storage.md)和 [Azure 表格儲存體](search-howto-indexing-azure-tables.md)索引子支援
* 透過 [欄位對應](search-indexer-field-mappings.md)
* Etag 支援 tooenable 安全並行更新的索引定義、 索引子和資料來源
* 支援以宣告方式建立索引欄位定義，而將模型類別，並使用新的 hello`FieldBuilder`類別。
* 對 .NET Core 和 .NET Portable Profile 111 的支援

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a>步驟 tooupgrade
首先，更新您 NuGet 參考`Microsoft.Azure.Search`使用任一 hello NuGet 封裝管理員主控台或藉由以滑鼠右鍵按一下您的專案參考和 Visual Studio 中選取 [管理 NuGet 封裝...]。

一旦 hello 新的封裝和其相依性，已下載 NuGet，請重建您的專案。 根據您的程式碼結構情況，它可能會順利重新建置。 如果是這樣，您已準備好 toogo ！

如果您的組建失敗，您應該會看到建置錯誤 hello 如下：

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' too'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

hello 下一個步驟是 toofix 這個組建錯誤。 請參閱[第 3 版中的重大變更](#ListOfChanges)如什麼情況會讓 hello 錯誤的詳細資訊及如何 toofix 它。

您可能會看到其他建置警告相關 tooobsolete 方法或屬性。 hello 警告將會包含在何種 toouse 改為 hello 的已被取代功能的指示。 例如，如果您的應用程式使用 hello`IndexingParameters.Base64EncodeKeys`屬性，您應該取得說明的警告`"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`

一旦您已修正任何建置錯誤，您可以變更 tooyour 應用程式 tootake 利用新的功能視。 Hello SDK 中的新功能的詳細[第 3 版的新](#WhatsNew)。

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a>版本 3 的重大變更
那里少量第 3 版中的重大變更，可能需要的程式碼變更此外 toorebuilding 您的應用程式。

### <a name="indexesgetclient-return-type"></a>Indexes.GetClient 傳回類型
hello`Indexes.GetClient`方法有新的傳回型別。 以往它會傳回`SearchIndexClient`，但這已經過`ISearchIndexClient`版本 2.0-預覽，以及變更會有透過 tooversion 3。 這是 toosupport 客戶想 toomock hello`GetClient`方法所傳回的模擬實作的單元測試`ISearchIndexClient`。

#### <a name="example"></a>範例
如果您的程式碼如下所示：

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

您可以將它變更 toothis toofix 任何建置錯誤：

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-toostrings"></a>AnalyzerName、 資料類型和其他人已不再隱含地轉換 toostrings
Hello 衍生自的 Azure 搜尋.NET SDK 中的許多類型`ExtensibleEnum`。 這些型別先前所有隱含地轉換 tootype `string`。 不過，在 hello 發現 bug`Object.Equals`實作這些類別，以及修正 hello bug 所需停用這項隱含轉換。 明確轉換太`string`仍然允許。

#### <a name="example"></a>範例
如果您的程式碼如下所示：

```csharp
var customTokenizerName = TokenizerName.Create("my_tokenizer"); 
var customTokenFilterName = TokenFilterName.Create("my_tokenfilter"); 
var customCharFilterName = CharFilterName.Create("my_charfilter"); 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        customTokenizerName,  
        new[] { customTokenFilterName },  
        new[] { customCharFilterName }), 
}; 
```

您可以將它變更 toothis toofix 任何建置錯誤：

```csharp
const string CustomTokenizerName = "my_tokenizer"; 
const string CustomTokenFilterName = "my_tokenfilter"; 
const string CustomCharFilterName = "my_charfilter"; 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        CustomTokenizerName,  
        new TokenFilterName[] { CustomTokenFilterName },  
        new CharFilterName[] { CustomCharFilterName })
}; 
```

### <a name="removed-obsolete-members"></a>移除過時的成員

您可能會看到建置錯誤相關的 toomethods 或內容所標示為版本 2.0 preview 中的過時並接著在第 3 版中移除。 如果您遇到此類錯誤時，以下是如何 tooresolve 它們：

- 如果您使用這個建構函式︰`ScoringParameter(string name, string value)`，請改用︰`ScoringParameter(string name, IEnumerable<string> values)`
- 如果您使用 hello`ScoringParameter.Value`屬性，使用 hello`ScoringParameter.Values`屬性或 hello`ToString`方法改為。
- 如果您使用 hello`SearchRequestOptions.RequestId`屬性，使用 hello`ClientRequestId`屬性改為。

### <a name="removed-preview-features"></a>已移除的預覽功能

如果您要從版本 2.0 preview tooversion 3 升級，請注意，JSON 和 CSV 剖析 Blob 的索引子的支援已經已移除，因為這些功能仍處於 preview。 具體來說，hello 遵循方法 hello`IndexingParametersExtensions`類別已被移除：

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

如果您的應用程式具有的硬式相依於這些功能，就能 tooupgrade tooversion 3 的 hello Azure 搜尋.NET SDK。 您可以繼續 toouse 版本 2.0 preview。 但請記住，**我們不建議在實際執行應用程式中使用預覽 SDK**。 預覽功能僅供評估，可能會變更。

## <a name="conclusion"></a>結論
如果您需要更多詳細資料上使用 hello Azure 搜尋.NET SDK，請參閱我們最近更新[How-to](search-howto-dotnet-sdk.md)。

我們歡迎您的意見反應 hello SDK 上。 如果您遇到問題，則可以免費 tooask 我們 hello 的說明[Azure 搜尋 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch)。 如果您發現 bug 時，您可以在 hello 提出問題[Azure.NET SDK GitHub 儲存機制](https://github.com/Azure/azure-sdk-for-net/issues)。 請確定 tooprefix 您問題的標題與 「 搜尋 SDK:"。

感謝您使用 Azure 搜尋服務！

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-tooupgrade-tooversion-11"></a>附錄： 步驟 tooupgrade tooversion 1.1
> [!NOTE]
> 本節適用於僅 toousers hello Azure 搜尋.NET SDK 版本 1.0.2-preview 和較舊。
> 
> 

首先，更新您 NuGet 參考`Microsoft.Azure.Search`使用任一 hello NuGet 封裝管理員主控台或藉由以滑鼠右鍵按一下您的專案參考和 Visual Studio 中選取 [管理 NuGet 封裝...]。

一旦 hello 新的封裝和其相依性，已下載 NuGet，請重建您的專案。

如果您先前使用版本 1.0.0-preview、 1.0.1-preview 或 1.0.2-preview，hello 組建應該成功，而且您已準備好 toogo ！

如果您先前使用版本 0.13.0-preview 或更舊版本，您應該會看到建置錯誤 hello 如下：

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: hello type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

hello 下一個步驟是一個 toofix hello 建置錯誤。 大部分都需要變更 hello SDK 中已重新命名某些類別和方法名稱。 [版本 1.1 的重大變更清單](#ListOfChangesV1) 一節包含這些名稱變更的清單。

如果您正在使用自訂類別 toomodel 文件中，且這些類別有不可為 null 的基本類型的屬性 (例如，`int`或`bool`C# 中)，其中您應該注意的 hello SDK hello 1.1 版本中沒有 bug 修正。 請參閱 [版本 1.1 的錯誤修正](#BugFixesV1) 一節以取得更多詳細資料。

最後，一旦您已修正任何建置錯誤，您可以變更 tooyour 應用程式 tootake 利用新的功能視。

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a>版本 1.1 的重大變更清單
hello 下列清單會依據排序 hello 可能性 hello 項變更會影響應用程式程式碼。

#### <a name="indexbatch-and-indexaction-changes"></a>IndexBatch 和 IndexAction 變更
`IndexBatch.Create`已重新命名過`IndexBatch.New`且不再具有`params`引數。 您可以針對混合不同類型動作 (合併、刪除等等) 的批次使用 `IndexBatch.New` 。 此外，還有新的靜態方法，建立批次的其中所有都 hello 動作是都 hello 相同： `Delete`， `Merge`， `MergeOrUpload`，和`Upload`。

`IndexAction` 不再具有公用建構函式且其屬性現在固定不變。 您應該用於不同用途建立動作 hello 新的靜態方法： `Delete`， `Merge`， `MergeOrUpload`，和`Upload`。 `IndexAction.Create` 已移除。 如果您使用可接受的文件 hello 多載時，請確定 toouse`Upload`改為。

##### <a name="example"></a>範例
如果您的程式碼如下所示：

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

您可以將它變更 toothis toofix 任何建置錯誤：

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

如果您想，您可以進一步加以簡化 toothis:

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a>IndexBatchException 變更
hello`IndexBatchException.IndexResponse`屬性已重新命名過`IndexingResults`，且其類型為現在`IList<IndexingResult>`。

##### <a name="example"></a>範例
如果您的程式碼如下所示：

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

您可以將它變更 toothis toofix 任何建置錯誤：

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a>作業方法變更
同步和非同步呼叫端，hello Azure 搜尋.NET SDK 中的每項作業會公開為一組方法多載。 hello 簽章與建構的這些方法多載版本中已經變更 1.1。

例如，hello hello SDK 的舊版本中的 < 取得索引統計資料 」 作業會公開這些簽章：

在 `IIndexOperations`中：

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

在 `IndexOperationsExtensions`中：

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

hello 方法簽章的 hello 相同的作業在 1.1 版看起來像這樣：

在 `IIndexesOperations`中：

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

在 `IndexesOperationsExtensions`中：

    // Simplified asynchronous operation
    public static Task<IndexGetStatisticsResult> GetStatisticsAsync(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        CancellationToken cancellationToken = default(CancellationToken));

    // Simplified synchronous operation
    public static IndexGetStatisticsResult GetStatistics(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions));

從 1.1 版開始，hello Azure 搜尋.NET SDK 會將組織作業方法以不同的方式：

* 選擇性參數現在模型化為預設參數，而不是其他方法多載。 這有時會大幅減少 hello 方法多載，數目。
* hello 擴充方法現在會隱藏許多 hello 多餘的詳細資料的 HTTP hello 呼叫端。 例如，較舊版本的 hello SDK 傳回的回應物件，與 HTTP 狀態碼，您通常不需要 toocheck 因為作業的方法擲回`CloudException`任何表示錯誤的狀態碼。 hello 新的擴充方法僅以傳回模型物件，儲存您 hello 麻煩 toounwrap 您的程式碼中。
* 相反地，hello 核心介面現在會公開方法可讓您有更多的控制層級 hello HTTP 如有需要。 您現在可以傳入要求，以及新的 hello 中包含的自訂 HTTP 標頭 toobe`AzureOperationResponse<T>`傳回類型可讓您直接存取 toohello`HttpRequestMessage`和`HttpResponseMessage`hello 作業。 `AzureOperationResponse`定義在 hello`Microsoft.Rest.Azure`命名空間，並取代`Hyak.Common.OperationResponse`。

#### <a name="scoringparameters-changes"></a>ScoringParameters 變更
新的類別，名為`ScoringParameter`已加入在最新 SDK toomake hello 它更容易 tooprovide 參數 tooscoring 設定檔中搜尋查詢。 先前 hello`ScoringProfiles`屬性 hello`SearchParameters`類別的型別是`IList<string>`;現在型別為`IList<ScoringParameter>`。

##### <a name="example"></a>範例
如果您的程式碼如下所示：

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

您可以將它變更 toothis toofix 任何建置錯誤： 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a>模型類別變更
因為 toohello 中所述的簽章變更[作業方法變更](#OperationMethodChanges)，許多類別在 hello`Microsoft.Azure.Search.Models`已重新命名或移除命名空間。 例如：

* `IndexDefinitionResponse` 已由 `AzureOperationResponse<Index>` 取代
* `DocumentSearchResponse`已重新命名過`DocumentSearchResult`
* `IndexResult`已重新命名過`IndexingResult`
* `Documents.Count()`現在會傳回`long`hello 文件計數，而不是`DocumentCountResponse`
* `IndexGetStatisticsResponse`已重新命名過`IndexGetStatisticsResult`
* `IndexListResponse`已重新命名過`IndexListResult`

toosummarize， `OperationResponse`-衍生存在於的 toowrap 已移除模型物件的類別。 hello 其餘的類別都已經將其從變更的後置詞`Response`太`Result`。

##### <a name="example"></a>範例
如果您的程式碼如下所示：

    IndexerGetStatusResponse statusResponse = null;

    try
    {
        statusResponse = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = statusResponse.ExecutionInfo.LastResult;

您可以將它變更 toothis toofix 任何建置錯誤：

    IndexerExecutionInfo status = null;

    try
    {
        status = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = status.LastResult;

##### <a name="response-classes-and-ienumerable"></a>回應類別和 IEnumerable
可能會影響您程式碼的其他變更，就是讓集合不再實作 `IEnumerable<T>`的回應類別。 相反地，您也可以直接存取 hello 集合屬性。 例如，如果您的程式碼如下所示：

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

您可以將它變更 toothis toofix 任何建置錯誤：

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a>Web 應用程式的特殊案例
如果您有 web 應用程式，會將序列化`DocumentSearchResponse`直接 toosend 搜尋結果 toohello 瀏覽器，您將需要 toochange 程式碼或 hello 結果不會正確序列化。 例如，如果您的程式碼如下所示：

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

您可以變更它藉由取得 hello `.Results` hello 搜尋回應 toofix 搜尋結果呈現的屬性：

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

您必須 toolook 這種情況下的在程式碼中自行;**hello 編譯器不會警告您**因為`JsonResult.Data`的型別`object`。

#### <a name="cloudexception-changes"></a>CloudException 變更
hello`CloudException`類別已經從 hello`Hyak.Common`命名空間 toohello`Microsoft.Rest.Azure`命名空間。 此外，其`Error`屬性已重新命名過`Body`。

#### <a name="searchserviceclient-and-searchindexclient-changes"></a>SearchServiceClient 和 SearchIndexClient 變更
hello hello 的型別`Credentials`屬性已經從`SearchCredentials`tooits 基底類別， `ServiceClientCredentials`。 如果您需要 tooaccess hello`SearchCredentials`的`SearchIndexClient`或`SearchServiceClient`，請使用新 hello`SearchCredentials`屬性。

在舊版的 hello SDK，`SearchServiceClient`和`SearchIndexClient`具有建構函式所花費`HttpClient`參數。 這些建構函式已由使用 `HttpClientHandler` 的建構函式和 `DelegatingHandler` 物件的陣列取代。 這使得更容易 tooinstall 自訂處理常式 toopre 處理 HTTP 要求如有必要。

最後，hello 建構函式所花費`Uri`和`SearchCredentials`已變更。 例如，如果您的程式碼如下所示：

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

您可以將它變更 toothis toofix 任何建置錯誤：

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

也請注意 hello 類型 hello 認證參數已太變更`ServiceClientCredentials`。 這是您的程式碼，因為不太可能 tooaffect`SearchCredentials`衍生自`ServiceClientCredentials`。

#### <a name="passing-a-request-id"></a>傳送要求 ID
在舊版的 hello SDK 中，您可以設定要求識別碼 hello 上`SearchServiceClient`或`SearchIndexClient`而且它會包含在每個要求 toohello REST API。 這是用於疑難排解問題與您的搜尋服務，如果您需要 toocontact 支援。 不過，它會針對每個作業更實用的 tooset 的唯一要求 ID，而不是不是 toouse hello 相同識別碼的所有作業。 基於這個理由，hello`SetClientRequestId`方法`SearchServiceClient`和`SearchIndexClient`已移除。 相反地，您可以將傳遞的要求識別碼 tooeach 作業方法 hello 透過選擇性`SearchRequestOptions`參數。

> [!NOTE]
> 在 hello SDK 未來版本中，我們將加入新 hello 用戶端上的物件，全域設定要求識別碼的機制，與其他 Azure Sdk 所使用的 hello 方法一致。
> 
> 

#### <a name="example"></a>範例
如果您的程式碼如下所示：

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

您可以將它變更 toothis toofix 任何建置錯誤：

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a>介面名稱變更
hello 作業群組介面名稱具有所有已變更的 toobe 及其對應的屬性名稱與一致：

* hello 的型別`ISearchServiceClient.Indexes`從重新命名`IIndexOperations`太`IIndexesOperations`。
* hello 的型別`ISearchServiceClient.Indexers`從重新命名`IIndexerOperations`太`IIndexersOperations`。
* hello 的型別`ISearchServiceClient.DataSources`從重新命名`IDataSourceOperations`太`IDataSourcesOperations`。
* hello 的型別`ISearchIndexClient.Documents`從重新命名`IDocumentOperations`太`IDocumentsOperations`。

這項變更是不太可能 tooaffect 您程式碼，除非您建立這些介面用於測試目的模擬。

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a>版本 1.1 的錯誤修正
在舊版的自訂模型類別 hello Azure 搜尋.NET SDK 相關 tooserialization 時發生錯誤。 當您建立自訂模型類別與不可為 null 的實值類型的屬性，可能會發生 hello bug。

#### <a name="steps-tooreproduce"></a>步驟 tooreproduce
建立具有不可為 null 值類型的屬性的自訂模型類別。 例如，加入類型 `int` 而不是 `int?` 的公用 `UnitCount` 屬性。

如果索引文件以 hello 該類型的預設值 (例如，0 代表`int`)，hello 欄位將 Azure 搜尋中傳回 null。 如果您後續搜尋該文件，hello`Search`呼叫會擲回`JsonSerializationException`抱怨不能轉換`null`太`int`。

此外，如預期般自從 null 寫入 toohello 索引，而不是預期的 hello 值後，篩選器可能無法運作。

#### <a name="fix-details"></a>修正詳細資料
Hello SDK 1.1 版中，我們已修正此問題。 現在，如果您有一個如下的模型類別：

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

您設定和`IntValue`too0 的值現在正確序列化為 0 hello 網路上及儲存為 hello 索引中為 0。 來回行程也如預期般運作。

沒有一個潛在的問題 toobe 留意這種方法： 如果您使用的模型型別不可為 null 的屬性時，您有太**保證**沒有文件索引中的包含 hello 對應欄位的 null 值。 Hello SDK 都 hello Azure 搜尋 REST API 將協助您 tooenforce 這。

這不只是假設性的問題： 想像一下，讓您加入新欄位 tooan 現有索引型別的`Edm.Int32`。 在更新之後 hello 索引定義，所有文件必須針對該新欄位的 null 值 （因為所有類型都是可為 null 的 Azure 搜尋）。 若您搭配不可為 null，然後使用模型類別`int`該欄位的屬性，您會收到`JsonSerializationException`tooretrieve 文件時，就像這樣：

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

基於這個原因，我們仍然建議您在模型類別中使用可為 null 的類型做為最佳作法。

如需有關這個 bug 及 hello 修正程式的詳細資訊，請參閱[此問題在 GitHub 上的](https://github.com/Azure/azure-sdk-for-net/issues/1063)。

