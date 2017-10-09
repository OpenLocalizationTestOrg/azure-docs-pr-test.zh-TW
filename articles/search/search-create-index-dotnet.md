---
title: "aaa\"建立索引 (.NET API-Azure 搜尋) |Microsoft 文件 」"
description: "使用 hello Azure 搜尋.NET SDK 程式碼中建立索引。"
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 3a851647-fc7b-4fb6-8506-6aaa519e77cd
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 7fa4030b8c3565bc02b1d6bb4426331657cf3a5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-net-sdk"></a>建立 Azure 搜尋索引使用 hello.NET SDK
> [!div class="op_single_selector"]
> * [概觀](search-what-is-an-index.md)
> * [入口網站](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

本文將逐步引導您建立 Azure 搜尋的 hello 程序[索引](https://docs.microsoft.com/rest/api/searchservice/Create-Index)使用 hello [Azure 搜尋.NET SDK](https://aka.ms/search-sdk)。

在按照本指南進行並建立索引錢，請先 [建立好 Azure 搜尋服務](search-create-service-portal.md)。

> [!NOTE]
> 本文中的所有範例程式碼均以 C# 撰寫。 您可以找到 hello 完整的原始程式碼[GitHub 上](http://aka.ms/search-dotnet-howto)。 您也可以閱讀 hello [Azure 搜尋.NET SDK](search-howto-dotnet-sdk.md) for 的詳細逐步 hello 範例程式碼。


## <a name="identify-your-azure-search-services-admin-api-key"></a>識別 Azure 搜尋服務的系統管理 API 金鑰
現在您已佈建 Azure 搜尋服務，您就就緒 tooissue 要求對使用.NET SDK hello 您服務端點。 首先，您將需要 tooobtain hello 管理 api 金鑰所產生的其中一個 hello 您佈建的搜尋服務。 此 api 金鑰會傳送 hello.NET SDK 的每個要求 tooyour 服務。 擁有有效的索引鍵建立信任關係，針對每個要求，hello 應用程式正在傳送嗨要求和處理它的 hello 服務之間。

1. toofind 服務的 api 金鑰，登入 toohello [Azure 入口網站](https://portal.azure.com/)
2. 移 tooyour Azure 搜尋服務的刀鋒視窗
3. 按一下 hello 「 金鑰 」 圖示

服務會有系統管理金鑰和查詢金鑰。

* 您的主要和次要*系統管理金鑰*tooall 作業，包括 hello 能力 toomanage hello 服務授與的完整權限、 建立和刪除索引、 索引子和資料來源。 有兩個索引鍵，讓您可以繼續 toouse hello 次要索引鍵，如果您決定 tooregenerate hello 主索引鍵，反之亦然。
* 您*查詢索引鍵*授與唯讀存取 tooindexes 和文件，並發出搜尋要求的 tooclient 通常分散式應用程式。

基於 hello 建立索引，您可以使用主要或次要管理金鑰。

<a name="CreateSearchServiceClient"></a>

## <a name="create-an-instance-of-hello-searchserviceclient-class"></a>建立 hello SearchServiceClient 類別的執行個體
使用 toostart hello Azure 搜尋.NET SDK，您就需要 toocreate hello 的執行個體`SearchServiceClient`類別。 這個類別有數個建構函式。 您想要的 hello 接受您的搜尋服務名稱和`SearchCredentials`做為參數的物件。 `SearchCredentials` 會包裝您的 API 金鑰。

hello 的下列程式碼會建立新`SearchServiceClient`使用 hello 搜尋服務名稱和儲存在 hello 應用程式組態檔中的 api 金鑰值 (`appsettings.json` hello hello 案例[範例應用程式](http://aka.ms/search-dotnet-howto)):

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

`SearchServiceClient` 具有 `Indexes` 屬性。 這個屬性提供所有 hello 方法，您需要 toocreate、 清單、 更新或刪除 Azure 搜尋索引。

> [!NOTE]
> hello`SearchServiceClient`類別管理連線 tooyour 搜尋服務。 在開啟的連接過多的順序 tooavoid，您應該嘗試 tooshare 的單一執行個體`SearchServiceClient`盡可能在您應用程式中。 其方法是安全執行緒 tooenable 這類共用。
> 
> 

<a name="DefineIndex"></a>

## <a name="define-your-azure-search-index"></a>定義 Azure 搜尋服務索引
單一呼叫 toohello`Indexes.Create`方法會建立您的索引。 這個方法會將 `Index` 物件作為參數，來定義您的 Azure 搜尋服務索引。 您需要 toocreate`Index`物件，並將它初始化，如下所示：

1. 設定 hello`Name`屬性 hello`Index`物件 toohello 名稱的索引。
2. 設定 hello`Fields`屬性 hello`Index`物件 tooan 陣列`Field`物件。 最簡單方式 toocreate hello hello`Field`物件是由呼叫 hello`FieldBuilder.BuildForType`方法，傳遞 hello 型別參數的模型類別。 模型類別具有對應索引的 toohello 欄位的屬性。 這可讓您從您的模型類別的搜尋索引 tooinstances toobind 文件。

> [!NOTE]
> 如果您不打算 toouse 模型類別，仍然可以藉由建立定義您的索引`Field`直接物件。 您可以提供 hello hello 欄位 toohello 建構函式名稱，以及 hello 資料類型 （或字串欄位的分析器）。 您也可以設定其他屬性，例如 `IsSearchable`、`IsFilterable` 等屬性。
>
>

很重要時，設計您的索引，因為每個欄位必須指派 hello 您搜尋的使用者經驗和商務需求謹記在心[適當屬性](https://docs.microsoft.com/rest/api/searchservice/Create-Index)。 這些屬性控制的搜尋功能 （篩選、 排序等全文檢索搜尋的 faceting） 套用 toowhich 欄位。 您未明確設定任何屬性，hello`Field`類別預設 toodisabling hello 對應搜尋功能，除非您特別啟用它。

在我們的範例中，我們已將索引命名為 "hotels"，並使用模型類別定義欄位。 Hello 模型類別的每個屬性具有屬性會決定 hello hello 對應索引欄位的搜尋相關行為。 hello 模型類別定義，如下所示：

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

我們已仔細選擇 hello 根據我們認為將用於應用程式的方式每一個屬性的屬性。 例如，很可能搜尋飯店的人將興趣關鍵字比對上 hello`description`欄位中，因此我們加入 hello 啟用該欄位的全文檢索搜尋`IsSearchable`屬性 toohello`Description`屬性。

請注意在類型的索引中剛好只有一個欄位`string`必須 hello 指定為 hello*金鑰*欄位加 hello`Key`屬性 (請參閱`HotelId`hello 上述範例中)。

上述的 hello 索引定義會使用語言分析器 hello`description_fr`欄位，因為它是預定的 toostore 法文文字。 請參閱[hello 語言支援主題](https://docs.microsoft.com/rest/api/searchservice/Language-support)以及 hello 對應[部落格文章](https://azure.microsoft.com/blog/language-support-in-azure-search/)如需語言分析器的詳細資訊。

> [!NOTE]
> 根據預設，模型類別中每個屬性的 hello 名稱會做為 hello hello hello 索引中的對應欄位的名稱。 如果您想 toomap 所有的屬性名稱 toocamel 案例欄位名稱，將以 hello hello 類別標記`SerializePropertyNamesAsCamelCase`屬性。 如果您想要 toomap tooa 不同名稱，您可以使用 hello`JsonProperty`屬性類似 hello`DescriptionFr`上述的屬性。 hello`JsonProperty`屬性會優先於 hello`SerializePropertyNamesAsCamelCase`屬性。
> 
> 

現在，我們定義了模型類別，可以非常輕鬆地建立索引定義︰

```csharp
var definition = new Index()
{
    Name = "hotels",
    Fields = FieldBuilder.BuildForType<Hotel>()
};
```

## <a name="create-hello-index"></a>建立 hello 索引
既然您已初始化`Index`物件，您可以建立 hello 索引只是藉由呼叫`Indexes.Create`上您`SearchServiceClient`物件：

```csharp
serviceClient.Indexes.Create(definition);
```

成功的要求，hello 方法會傳回一般。 如果沒有問題 hello 要求，例如無效的參數，將會擲回 hello 方法`CloudException`。

當您完成時具有索引，且想 toodelete 它時，只需要呼叫 hello`Indexes.Delete`方法上的您`SearchServiceClient`。 比方說，這是我們會 delete hello 「 旅館"索引的方式：

```csharp
serviceClient.Indexes.Delete("hotels");
```

> [!NOTE]
> 這篇文章中的 hello 範例程式碼為了簡單起見使用 hello Azure 搜尋.NET SDK 的 hello 同步方法。 我們建議您在自己的應用程式 tookeep 使用 hello 非同步方法加以擴充且回應迅速。 例如，在 hello 上面的範例可以使用`CreateAsync`和`DeleteAsync`而不是`Create`和`Delete`。
> 
> 

## <a name="next-steps"></a>後續步驟
建立 Azure 搜尋索引之後, 您就可以開始太[將內容上傳到 hello 索引](search-what-is-data-import.md)這樣就可以搜尋您的資料。

