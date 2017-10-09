---
title: "在 Azure 搜尋 aaaHow tooimplement 多面向導覽 |Microsoft 文件"
description: "加入多面向導覽 tooapplications 與 Azure 搜尋中，在 Microsoft Azure 上裝載的雲端搜尋服務整合。"
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: cdf98fd4-63fd-4b50-b0b0-835cb08ad4d3
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 3/10/2017
ms.author: heidist
ms.openlocfilehash: c1e6bf9dc55d0044525db79e37d35a50ded5a736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-faceted-navigation-in-azure-search"></a>如何在 Azure 搜尋 tooimplement 多面向導覽
多面向導覽是一個篩選機制，它在搜尋應用程式中提供自動導向的向下鑽研導覽。 hello 詞彙 '多面向導覽' 可能不熟悉，但您可能使用它之前。 下列範例會顯示 hello，多面向導覽是而已 hello 類別使用 toofilter 結果。

 ![Azure 搜尋服務作業入口網站示範][1]

多面向導覽是替代項目點 toosearch。 它會提供方便的替代 tootyping 複雜搜尋運算式以手動方式。 多面向可協助您找到要找的項目，同時確保您不會得到沒有項目的結果。 身為開發人員，facet 可讓您公開 hello 最為實用的搜尋準則瀏覽搜尋主體。 在線上零售應用程式中，通常會根據品牌、部門 (童鞋)、尺寸、價格、熱門程度和評分來建置多面向導覽。 

實作多面向導覽會因各搜尋技術而不同。 在 Azure 搜尋服務中，多面向導覽會在查詢時使用您先前歸屬在結構描述中的欄位來建置。

-   在建置您的應用程式，必須先傳送查詢的 hello 查詢*facet 查詢參數*tooget hello 可用 facet 該文件的篩選值的結果集。

-   tooactually 修剪 hello 文件的結果集、 hello 應用程式還必須套用`$filter`運算式。

在您的應用程式開發，撰寫程式碼會建構查詢，即構成 hello 大量 hello 工作。 許多 hello 應用程式的行為如預期般從多面向導覽會提供 hello 服務，包括內建支援來定義範圍和取得 facet 結果中的計數。 hello 服務也包含實用的預設值，可協助您避免變得不便瀏覽結構。 

## <a name="sample-code-and-demo"></a>程式碼範例和示範
本文使用作業搜尋入口網站來作為範例。 hello 範例會實作為 ASP.NET MVC 應用程式。

-   請參閱和測試 hello 工作示範線上在[Azure 搜尋作業入口網站示範](http://azjobsdemo.azurewebsites.net/)。

-   下載 hello 程式碼從 hello [GitHub 上的 Azure 範例儲存機制](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs)。

## <a name="get-started"></a>開始使用
如果您是新 toosearch 開發，hello 最佳方式 toothink 的多面向導覽是，它會顯示 hello 自我引導搜尋的可能性。 它是向下鑽研搜尋體驗的一種，基於預先定義的篩選條件，可以藉由「指向並按一下」的動作快速縮減搜尋結果。 

### <a name="interaction-model"></a>互動模型

hello 搜尋經驗，針對多面向導覽是反覆執行，讓我們開始了解以回應 toouser 動作在展開的查詢的序列。

hello 開始點就是提供多面向導覽，通常會放在 hello 位於周邊視覺範圍上的應用程式頁面。 多面向導覽通常是樹狀結構，且每個值有核取方塊，或可點選的文字。 

1. 傳送 tooAzure 搜尋查詢會指定透過一或多個 facet 查詢參數的 hello 多面向導覽結構。 Hello 查詢可能會包含執行個體， `facet=Rating`，可能與`:values`或`:sort`選項 toofurther 精簡 hello 簡報。
2. hello 展示層會轉譯提供多面向導覽中，使用 hello facet hello 要求上指定的搜尋頁面。
3. 您指定多面向導覽結構，其中包含評等，按一下"4"tooindicate 應顯示只為等級 4 或更新版本的產品。 
4. 傳送，回應 hello 應用程式包含的查詢`$filter=Rating ge 4` 
5. hello 展示層更新 hello 頁面顯示減少的結果集，其中包含只符合 hello 新的篩選條件的項目 (在此情況下，產品評等為 4 與更新版本)。

面向是查詢參數，但不要將它與查詢輸入混淆了。 它在查詢中不是當作選取準則。 相反地，將 facet 查詢參數視為恢復 hello 回應中的輸入 toohello 導覽結構。 您提供每一個 facet 查詢參數，Azure 搜尋會評估多少文件位於 hello 部分結果的每個 facet 的值。

請注意 hello`$filter`在步驟 4 中。 hello 篩選器是多面向導覽的重要層面。 雖然 facet 和篩選無關 hello 應用程式開發介面中，您會需要您想要這兩個 toodeliver hello 經驗。 

### <a name="app-design-pattern"></a>應用程式設計模式

在應用程式程式碼 hello 模式是 toouse facet 查詢參數 tooreturn hello 多面向導覽結構以及 facet 結果加上 $filter 運算式。  hello 篩選運算式的控制代碼 hello 按一下 hello facet 的值上的事件。 考慮的 hello `$filter` hello hello 實際修剪背後的程式碼搜尋結果的運算式傳回 toohello 展示層。 按一下紅色 hello 色彩透過實作提供色彩 facet，`$filter`運算式會選取有紅色的色彩的項目。 

### <a name="query-basics"></a>查詢基本概念

在 Azure 搜尋服務中，要求是透過一或多個查詢參數 (如需個別的詳細描述，請參閱 [搜尋文件](http://msdn.microsoft.com/library/azure/dn798927.aspx) ) 指定。 無 hello 查詢參數是必要的但您必須至少有一個有效查詢 toobe 的順序。

有效位數，辨識 hello 能力 toofilter 出不相關的叫用，可以透過完成一或多個這些運算式：

-   **搜尋=**  
    此參數 hello 值構成 hello 搜尋運算式。 它可能為單一的文字，或包括多個名詞和運算子的複雜搜尋運算式。 Hello 在伺服器上，搜尋運算式用於全文檢索搜尋，查詢可搜尋符合的詞彙中，次序順序傳回結果的 hello 索引中的欄位。 如果您設定`search`toonull，是透過 hello 整個索引的查詢執行 (也就是`search=*`)。 In this case，hello 的其他項目查詢，例如`$filter`或計分設定檔，會影響傳回的文件的主要因素 hello `($filter`) 以及依照何種 (`scoringProfile`或`$orderby`)。

-   **$filter=**  
    篩選是強大的機制，來限制根據特定文件屬性的 hello 值的搜尋結果的 hello 大小。 A`$filter`會先評估，後面接著 faceting 邏輯，以產生 hello 可用的值及針對每個值對應的計數

複雜的搜尋運算式降低 hello hello 查詢效能。 可能的話，請使用格式建構的篩選運算式 tooincrease 有效位數，而且改善查詢效能。

toobetter 了解如何篩選器加入更多有效位數，請比較複雜的搜尋運算式 tooone 包含篩選條件運算式：

-   `GET /indexes/hotel/docs?search=lodging budget +Seattle –motel +parking`
-   `GET /indexes/hotel/docs?search=lodging&$filter=City eq ‘Seattle’ and Parking and Type ne ‘motel’`

這兩個查詢有效，但 hello 第二種是如果您想要尋求非屋與位於西雅圖的暫止。
-   hello 第一個查詢依賴特定文字被提及或字串欄位名稱、 描述和包含可搜尋資料的任何其他欄位中未提及。
-   hello 第二個查詢會尋找精確比對結構化資料，且可能 toobe 更為精確。

在包含多面向導覽的應用程式中，請確定每個透過多面向導覽結構進行的使用者動作都伴隨搜尋結果縮減。 toonarrow 結果，請使用篩選條件運算式。

<a name="howtobuildit"></a>

## <a name="build-a-faceted-navigation-app"></a>建置多面向導覽應用程式
您可以實作多面向導覽使用 Azure 搜尋在應用程式程式碼會建置 hello 搜尋要求。 hello 多面向導覽依賴您先前定義的結構描述中的項目。

在搜尋索引中預先定義為 hello`Facetable [true|false]`屬性編製索引，在選取的欄位 tooenable 上設定或停用在多面向導覽結構中的使用。 若沒有 `"Facetable" = true`，該欄位就不能在多面向導覽中使用。

在程式碼中的 hello 展示層提供 hello 使用者體驗。 它應該會列出 hello 的 hello 多面向導覽，例如 hello 標籤、 值、 核取方塊及 hello 計數的構成部分。 hello Azure 搜尋 REST API 是無從驗證平台，因此，使用任何語言和您想要的平台。 hello 重點是 tooinclude UI 項目支援累加式的重新整理，更新的 UI 狀態與選取每一個額外的 facet。 

在查詢時，應用程式程式碼會建立要求，其中包含`facet=[string]`，提供由 hello 欄位 toofacet 要求參數。 一個查詢可以有多個面向，例如 `&facet=color&facet=category&facet=rating`，每個面向都以 & 符號分隔。

應用程式程式碼也必須建構`$filter`運算式 toohandle hello 按一下多面向導覽中的事件。 A`$filter`減少 hello 搜尋結果中，使用 hello facet 的值做為篩選準則。

Azure 搜尋傳回 hello 搜尋結果中，根據一個或多個輸入，以及更新 toohello 多面向導覽結構的詞彙。 在 Azure 搜尋服務中，多面向導覽是單一層級的結構，其中包含面向值及其找到結果的計數。

我們在 hello 下列各節，深入了解 toobuild 每個部分。

<a name="buildindex"></a>

## <a name="build-hello-index"></a>建立 hello 索引
啟用 faceting hello 在索引中，透過此索引屬性-欄位為基礎： `"Facetable": true`。  
根據預設，所有可能用於多面向導覽的欄位類型為 `Facetable` 。 這類的欄位類型包括`Edm.String`， `Edm.DateTimeOffset`，和所有 hello 數值的欄位型別 (基本上，所有的欄位類型都是可進行 facet 處理除了`Edm.GeographyPoint`，這不能用於在多面向導覽)。 

當建立索引時，多面向導覽的最佳作法超出 tooexplicitly 開啟 faceting 永遠不應該當做 facet 使用的欄位。  特別是，單一值、 識別碼或產品名稱，例如字串欄位應該設定太`"Facetable": false`tooprevent 其意外 （並沒有作用） 使用的多面向導覽。 開啟關閉您不需要在其中 faceting 可協助確保 hello 索引的 hello 大小很小，以及將通常會改善效能。

以下是 hello 作業入口網站示範範例應用程式的某些屬性 tooreduce hello 大小修剪 hello 結構描述的一部分：

```json
{
  ...
  "name": "nycjobs",
  "fields": [
    { “name”: "id",                 "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "job_id",             "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "agency",              "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "posting_type",        "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "num_of_positions",    "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "business_title",      "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "civil_service_title", "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "title_code_no",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "level",               "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_from",   "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_to",     "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_frequency",    "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "work_location",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
…
    { “name”: "geo_location",        "type": "Edm.GeographyPoint",     "searchable": false, "filterable": true, ...  "facetable": false, ... },
    { “name”: "tags",                "type": "Collection(Edm.String)", "searchable": true,  "filterable": true, ...  "facetable": true, ...  }
  ],
…
}
```

如您所見 hello 範例結構描述中`Facetable`功能是關閉的字串欄位不應該做為 facet，例如識別碼值。 開啟關閉您不需要在其中 faceting 可協助確保 hello 索引的 hello 大小很小，以及將通常會改善效能。

> [!TIP]
> 最佳做法，包括 hello 完整的每個欄位的索引屬性集。 雖然`Facetable`預設為開啟的幾乎所有的欄位，刻意設定每個屬性可協助您仔細思考每個結構描述決策 hello 含意。 

<a name="checkdata"></a>

## <a name="check-hello-data"></a>檢查 hello 資料
hello 資料的品質有直接影響 hello 多面向導覽結構是否會具體化您所預期的。 它也會影響 hello 輕鬆建構篩選 tooreduce hello 結果集。

如果您想 toofacet 品牌或價格，每份文件應包含的值*BrandName*和*ProductPrice*屬於有效、 一致且有效率當做篩選選項。

以下是針對哪些 tooscrub 的幾個提醒：

* 為您想要依 toofacet 每個欄位，請詢問自己是否包含在搜尋中自我引導適合做為篩選的值。 hello 值應該是簡短、 描述性，和足以特殊 toooffer 競爭選項之間的明確選項。
* 拼字錯誤或近似符合的值。 如果 facet 上色彩，以及欄位的值包括橙色和 Ornage （拼字錯誤）、 根據 hello 色彩欄位 facet 將會收取兩者。
* 混合大小寫的文字對多面向導覽也會遭成嚴重影響 (orange 和 Orange 為兩個不同的值)。 
* 單一的單複數形態 hello 相同的值可以針對每個會導致不同的 facet。

您可以想像，勤加注意準備 hello 資料是有效的多面向導覽的重要層面。

<a name="presentationlayer"></a>

## <a name="build-hello-ui"></a>建置 hello UI
使用從 hello 展示層可以說明您在發現需求，否則可能會遺漏，並且了解哪些功能基本 toohello 搜尋經驗。

多面向導覽，以您的 web 或應用程式頁面會顯示 hello 多面向導覽結構、 偵測到在 hello 頁面上，使用者輸入和插入 hello 變更項目。 

Web 應用程式，AJAX 常用於 hello 展示層因為它可讓您 toorefresh 累加變更。 您也可以使用 ASP.NET MVC 或任何其他視覺效果平台都可以透過 HTTP 連線 tooan Azure 搜尋服務。 hello 範例應用程式參考整篇文章-hello **Azure 搜尋作業入口網站示範**– 發生 toobe ASP.NET MVC 應用程式。

在 hello 範例中，多面向導覽是內建 hello 搜尋結果頁面。 下列範例取自 hello hello`index.cshtml`檔案 hello 範例應用程式，顯示 hello 靜態 HTML 結構 hello 搜尋上顯示多面向導覽的結果頁面。 建立或送出搜尋文字，或選取或清除 facet 時以動態方式重建 hello 別的 facet 清單。

```html
<div class="widget sidebar-widget jobs-filter-widget">
  <h5 class="widget-title">Filter Results</h5>
    <p id="filterReset"></p>
    <div class="widget-content">

      <h6 id="businessTitleFacetTitle">Business Title</h6>
      <ul class="filter-list" id="business_title_facets">
      </ul>

      <h6>Location</h6>
      <ul class="filter-list" id="posting_type_facets">
      </ul>

      <h6>Posting Type</h6>
      <ul class="filter-list" id="posting_type_facets"></ul>

      <h6>Minimum Salary</h6>
      <ul class="filter-list" id="salary_range_facets">
      </ul>

  </div>
</div>
```

下列程式碼片段從 hello hello`index.cshtml`頁面會動態建立 hello HTML toodisplay hello 第一個 facet，商務標題。 類似的函式動態建立 hello HTML hello 其他方面。 每一個 facet 都有標籤及顯示 hello 數目來傳回 facet 所找到的項目計數。

```js
function UpdateBusinessTitleFacets(data) {
  var facetResultsHTML = '';
  for (var i = 0; i < data.length; i++) {
    facetResultsHTML += '<li><a href="javascript:void(0)" onclick="ChooseBusinessTitleFacet(\'' + data[i].Value + '\');">' + data[i].Value + ' (' + data[i].Count + ')</span></a></li>';
  }

  $("#business_title_facets").html(facetResultsHTML);
}
```

> [!TIP]
> 當您設計 hello 搜尋結果頁面時，請記住 tooadd 清除 facet 的機制。 如果您加入核取方塊，您可以輕鬆地查看 tooclear hello 的篩選器。 針對其他配置，您可能需要階層模式或其他具創意的方法。 例如，在 hello 作業搜尋入口網站範例應用程式，您可以按一下 hello`[X]`之後所選的 facet tooclear hello facet。

<a name="buildquery"></a>

## <a name="build-hello-query"></a>建立 hello 查詢
hello 來建立查詢所撰寫的程式碼應指定有效的查詢，包括搜尋運算式、 facet、 篩選、 計分設定檔 – 任何項目中的所有部分都使用 tooformulate 要求。 在本節中，我們探討其中 facet 放入查詢時，以及如何使用篩選條件的 facet toodeliver 以減少結果集。

請注意，面向在此範例應用程式中是必要的。 hello hello 作業入口網站的示範中的搜尋經驗是針對設計多面向導覽和篩選。 hello 顯著放置在 hello 頁面上的多面向導覽示範其重要性。 

範例通常是很好的起點 toobegin。 下列範例取自 hello hello`JobsSearch.cs`檔案，建立 facet 瀏覽的要求會根據商務標題、 位置、 張貼型別和最低薪資的組建。 

```cs
SearchParameters sp = new SearchParameters()
{
  ...
  // Add facets
  Facets = new List<String>() { "business_title", "posting_type", "level", "salary_range_from,interval:50000" },
};
```

設定 tooa 欄位 facet 查詢參數，而且根據 hello 資料類型，可以進一步由進行參數化，其中包含以逗號分隔清單`count:<integer>`， `sort:<>`， `interval:<integer>`，和`values:<list>`。 當設定範圍時，針對數值資料支援值清單。 如需用量詳細資訊，請參閱 [搜尋文件 (Azure 搜尋服務 API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) 。

Facet，以及應用程式所構成的 hello 要求也應建置篩選 toonarrow 向 hello 組 facet 值選取項目所根據的候選文件。 對於 bike 存放區中，多面向導覽提供線索 tooquestions 喜歡*何種色彩、 製造商和類型的自行車可用？*。 篩選功能可解答「哪些單車確實是位於此價格帶內的紅色登山車？」之類的問題。 當您按一下應顯示紅色的產品，"Red"tooindicate hello 下一個查詢 hello 應用程式會傳送包含`$filter=Color eq ‘Red’`。

下列程式碼片段從 hello hello`JobsSearch.cs`頁面新增選取的 hello 商務標題 toohello 篩選器，如果您選取從 hello 商務標題 facet 的值。

```cs
if (businessTitleFacet != "")
  filter = "business_title eq '" + businessTitleFacet + "'";
```

<a name="tips"></a> 

## <a name="tips-and-best-practices"></a>秘訣和最佳作法

### <a name="indexing-tips"></a>編製索引的秘訣
**在不使用搜尋方塊的情況下改善索引效率**

如果您的應用程式只會使用多面向導覽 （也就是沒有搜尋方塊中），您可以將標記為 hello 欄位`searchable=false`， `facetable=true` tooproduce 更精簡的索引。 此外，索引只會整個 facet 的值，與沒有文字分隔或 hello 元件部分的多字值的索引。

**指定可做為面向的欄位**

前文提過該 hello hello 索引的結構描述決定哪些欄位可用 toouse 做為 facet。 Hello 查詢假設欄位可進行 facet 處理，指定由哪個欄位 toofacet。 您已經 faceting hello 欄位提供 hello 標籤底下顯示 hello 值。 

顯示每個標籤底下的 hello 值是從 hello 索引擷取。 例如，如果 hello facet 欄位是*色彩*，可用於其他篩選的 hello 值為 hello 該欄位值為紅色、 黑色，以及其他等等。

數值和日期時間只對值，您可以明確設定值 hello facet 欄位 (例如， `facet=Rating,values:1|2|3|4|5`)。 這些欄位類型 toosimplify hello 分離 facet 結果的連續範圍 （可能是數值或時間週期為基礎的範圍） 到允許的值清單。 

**依預設您只能擁有一個多面向導覽層級** 

如附註所說明，階層中沒有直接支援巢狀面向。 根據預設，Azure 搜尋服務中的多面向導覽僅支援單層篩選。 不過有因應措施。 您可以在 `Collection(Edm.String)` 中利用各階層各一個進入點來編碼階層面向。 實作這個因應措施已超出本文的 hello 範圍。 

### <a name="querying-tips"></a>查詢秘訣
**驗證欄位**

如果您建立的 facet 以動態方式根據不受信任的使用者輸入的 hello 清單時，驗證確定 hello hello 多面向的欄位名稱是否有效。 或者，當建置使用 Url 逸出 hello 名稱`Uri.EscapeDataString()`在.NET 中或在您的平台選擇的對等的 hello。

### <a name="filtering-tips"></a>篩選秘訣
**使用篩選條件提高搜尋精準度**

使用篩選條件。 如果您依賴單獨詞幹分析可能會導致文件 toobe 只搜尋運算式會傳回任何欄位中不具有 hello 精確 facet 的值。

**使用篩選條件提高搜尋效能**

篩選器縮小 hello 組搜尋候選文件，並排除排名。 如果您有大型文件集，使用經過挑選的面向向下切入通常能讓您的效能提升。
  
**篩選 hello 多面向欄位**

在多面向向下鑽研，您通常想 tooonly 包含文件有任何位置不在跨所有可搜尋的欄位在特定的 （多面向） 欄位中，hello facet 的值。 加入篩選，以控制程式只在 hello 多面向的欄位相符的值為 hello 服務 toosearch 強調 hello 目標欄位。

**使用更多篩選條件修剪面向結果**

Facet 結果是找到符合 facet 字詞的 hello 搜尋結果中的文件。 在下列範例中的，在搜尋結果中的 hello*雲端運算*，254 項目也具有*內部規格*做為內容的類型。 項目毋須互斥。 如果項目符合 hello 這兩個篩選準則，計算每個。 這種重複狀況時，可能在 faceting`Collection(Edm.String)`欄位，而這通常是用 tooimplement 文件標記。

        Search term: "cloud computing"
        Content type
           Internal specification (254)
           Video (10) 

一般情況下，如果您發現 facet 結果會一致地太大，我們建議您加入其他篩選 toogive 使用者縮小 hello 搜尋更多的選項。

### <a name="tips-about-result-count"></a>關於結果計數的秘訣

**限制 hello hello facet 導覽中的項目數目**

Hello 導覽樹狀目錄中每個 facet 欄位，沒有預設的 10 個值的限制。 這個預設值就導覽結構的有意義，因為它會將 hello 值清單 tooa 大小容易管理。 您可以藉由指派值 toocount 覆寫 hello 預設值。

* `&facet=city,count:5`指定只有 hello 前五個城市位於 hello 上方的等級結果會傳回做為 facet 結果。 請設想具有搜尋字詞「機場」和 32 個符合項的查詢範例。 如果 hello 查詢指定`&facet=city,count:5`，只有 hello 前五個唯一的城市與 hello 搜尋結果中的大部分文件中包含的 hello hello facet 結果。

請注意 hello 區分 facet 結果和搜尋結果。 搜尋結果的所有符合 hello 查詢 hello 文件。 Facet 結果的 hello 比對每個 facet 的值。 在 hello 範例中，搜尋結果會包含不在 hello facet 分類清單 (在本例中為 5) 的城市名稱。 當您清除面向或選擇「城市」以外的其他面向時，系統會顯示透過多面向導覽篩選出的結果。 

> [!NOTE]
> 當有一種類型以上時討論 `count` 可能會讓人混淆。 hello 下表提供如何使用 Azure 搜尋 API、 程式碼範例和文件中的 hello 詞彙的簡短摘要。 

* `@colorFacet.count`<br/>
  呈現程式碼中，您應該看到 hello facet，facet 結果使用的 toodisplay hello 數目的計數參數。 在 facet 結果中，計數會指出 hello 符合 hello facet 一詞或範圍的文件的數目。
* `&facet=City,count:12`<br/>
  在 facet 查詢中，您可以設定計數 tooa 值。  hello 預設值為 10，但您可以將其高或較低。 設定`count:12`取得文件計數的 hello facet 結果中的前 12 相符項目。
* "`@odata.count`"<br/>
  Hello 查詢回應，這個值會表示 hello hello 搜尋結果中的相符項目數目。 平均而言，大於 hello 總和的組合，因為 toohello 符合 hello 的搜尋詞彙的項目存在的所有 facet 結果，但有 facet 值相符的項目。

**取得面向結果中的計數**

當您新增篩選條件 tooa 多面向查詢時，您可能想 tooretain hello facet 陳述式 (例如， `facet=Rating&$filter=Rating ge 4`)。 技術上來說，facet = 評等不需要但 4 及更新版本，讓它維持在傳回 hello 的評等的 facet 值的計數。 例如，如果您按一下"4"，並且在 hello 查詢包含一個篩選大於或等於的太"4"，計數會傳回每個評等為 4 及更新版本。  

**確實取得精確的面向計數**

在某些情況下，您可能會發現 facet 計數不符 hello 結果集 (請參閱[Azure 搜尋 （論壇貼文） 中的多面向導覽](https://social.msdn.microsoft.com/Forums/azure/06461173-ea26-4e6a-9545-fbbd7ee61c8f/faceting-on-azure-search?forum=azuresearch))。

Facet 計數可能會因為 toohello 分區化架構不正確。 每個搜尋索引有多個分區，以及每個分區的文件計數，也就結合成單一結果，以報告 hello 前 n 個 facet。 如果某些分區有許多相符的值，而有些則擁有較少，您可能會發現某些 facet 值遺漏或下計數 hello 結果中。

雖然這種行為無法變更在任何時間，如果您今天出現這種行為，您可以解決它以人為方式因而誇大 hello 計數：<number> tooa 大型數字 tooenforce 完整報告每個分區。 如果 hello 計數值： 是大於或等於 toohello 數字的 hello 欄位中的唯一值，保證精確的結果。 不過，當文件計數很高的時候，則會有效能的負面影響，因此請謹慎使用此選項。

### <a name="user-interface-tips"></a>使用者介面秘訣
**針對多面向導覽中的各欄位新增標籤**

Hello HTML 或表單中通常會定義標籤 (`index.cshtml` hello 範例應用程式中)。 Azure 搜尋服務中沒有適用於多面向導覽標籤或任何其他中繼資料的 API。

<a name="rangefacets"></a>

## <a name="filter-based-on-a-range"></a>根據範圍進行篩選
透過值範圍進行面向化是常見的搜尋應用程式需求。 範圍支援數值資料與日期時間值。 您可以在 [搜尋文件 (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx)中閱讀各方法的相關資訊。

Azure Search 透過提供兩種方法進行範圍運算，來簡化範圍建構。 對於這兩種方法，Azure 搜尋會建立適當的範圍，提供您所提供的 hello 輸入 hello。 例如，如果您指定 10|20|30 的值範圍，它會自動建立 0-10、10-20、20-30 的範圍。 您的應用程式可以選擇性地移除任何空白間隔。 

**方法 1： 使用 hello 間隔參數**  
$10 增量 tooset 價格 facet，您會指定：`&facet=price,interval:10`

**方法 2︰使用值清單**  
針對數值資料，您可以使用值清單。  請考慮 hello facet 範圍`listPrice` 欄位中，呈現，如下所示：

  ![範例值清單][5]

toospecify facet 範圍喜歡 hello 中 hello 前面螢幕擷取畫面，請使用值清單：

    facet=listPrice,values:10|25|100|500|1000|2500

使用 0 做為起點，作為端點，hello 清單中的值，然後再加以剪裁 hello 前一個範圍 toocreate 離散間隔的內建的每個範圍。 Azure 搜尋服務會將這些動作做為多面向導覽的一部分來執行。 您沒有 toowrite 建構每個間隔的程式碼。

### <a name="build-a-filter-for-a-range"></a>針對範圍建置篩選條件
根據您選取的範圍 toofilter 文件，您可以使用 hello`"ge"`和`"lt"`篩選定義 hello 端點 hello 範圍的兩段式運算式中的運算子。 例如，如果您選擇 hello 範圍 10 到 25 的`listPrice`的欄位，就是 hello 篩選`$filter=listPrice ge 10 and listPrice lt 25`。 Hello 範例程式碼，在 hello 篩選條件運算式會使用**priceFrom**和**priceTo**參數 tooset hello 端點。 

  ![查詢某範圍的值][6]

<a name="geofacets"></a> 

## <a name="filter-based-on-distance"></a>根據距離進行篩選
它的通用 toosee 篩選可協助您選擇商店、 餐廳或目的地的鄰近 tooyour 目前位置。 這類型的篩選條件看起來像是多面向導覽，但實際上只是篩選條件。 對於那些特別要尋找特定設計問題之實作建議的使用者，我們會在此處說明。

搜尋服務中有兩種地理空間函式，**geo.distance** 與 **geo.intersects**。

* hello **geo.distance**函式以公里為單位傳回 hello 距離兩個點之間。 一個點是一個欄位，而另一個則 hello 篩選條件一部分傳遞的常數。 
* hello **geo.intersects**函數會傳回 true，如果在給定的多邊形內，則指定的點。 hello 點是欄位，hello 多邊形會指定為座標做為 hello 篩選條件一部分傳遞的常數清單。

您可以在 [OData 運算式語法 (Azure Search)](http://msdn.microsoft.com/library/azure/dn798921.aspx)中找到篩選條件範例。

<a name="tryitout"></a>

## <a name="try-hello-demo"></a>請嘗試 hello 示範
hello Azure 搜尋作業入口網站示範包含參考本文章中的 hello 範例。

-   請參閱和測試 hello 工作示範線上在[Azure 搜尋作業入口網站示範](http://azjobsdemo.azurewebsites.net/)。

-   下載 hello 程式碼從 hello [GitHub 上的 Azure 範例儲存機制](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs)。

當您使用的搜尋結果時，觀賞 hello URL 查詢建構中的變更。 當您選取每個此應用程式就會發生 tooappend facet toohello URI。

1. toouse hello 對應功能的 hello 示範應用程式取得 Bing 地圖服務金鑰從 hello [Bing 地圖服務開發人員中心](https://www.bingmapsportal.com/)。 將它貼入 hello hello 中的現有金鑰`index.cshtml`頁面。 hello `BingApiKey` hello 中設定`Web.config`不是檔案。 

2. 執行 hello 應用程式。 導覽 hello 選擇性，或關閉 hello 對話方塊。
   
3. 輸入搜尋詞彙，例如 「 分析師 」，然後按一下 hello 搜尋圖示。 hello 查詢執行速度快速。
   
   多面向導覽結構也會傳回與 hello 搜尋結果。 Hello 搜尋結果 頁面上，在 hello 多面向導覽結構會包含每個 facet 結果的計數。 我們並未選取任何面向，因此會傳回所有符合的結果。
   
   ![選取面向之前的搜尋結果][11]

4. 按一下 [職稱]、[位置] 或 [最低工資]。 Facet null hello 初始搜尋，但因為他們接受的值，則會修剪 hello 搜尋結果不再符合的項目。
   
   ![選取面向之後的搜尋結果][12]

5. tooclear hello 多面向查詢，以便您可以嘗試不同的查詢行為，請按一下 hello `[X]` hello 選取 facet tooclear hello facet 之後。
   
<a name="nextstep"></a>

## <a name="learn-more"></a>詳細資訊
觀賞[深入了解 Azure 搜尋服務](http://channel9.msdn.com/Events/TechEd/Europe/2014/DBI-B410)。 在 45:25，沒有示範如何 tooimplement facet。

更多深入多面向導覽的設計原則的詳細資訊，我們建議下列連結查看 hello:

* [多面向搜尋的設計](http://www.uie.com/articles/faceted_search/)
* [設計模式：多面向導覽](http://alistapart.com/article/design-patterns-faceted-navigation)


<!--Anchors-->
[How toobuild it]: #howtobuildit
[Build hello presentation layer]: #presentationlayer
[Build hello index]: #buildindex
[Check for data quality]: #checkdata
[Build hello query]: #buildquery
[Tips on how toocontrol faceted navigation]: #tips
[Faceted navigation based on range values]: #rangefacets
[Faceted navigation based on GeoPoints]: #geofacets
[Try it out]: #tryitout

<!--Image references-->
[1]: ./media/search-faceted-navigation/azure-search-faceting-example.PNG
[2]: ./media/search-faceted-navigation/Facet-2-CSHTML.PNG
[3]: ./media/search-faceted-navigation/Facet-3-schema.PNG
[4]: ./media/search-faceted-navigation/Facet-4-SearchMethod.PNG
[5]: ./media/search-faceted-navigation/Facet-5-Prices.PNG
[6]: ./media/search-faceted-navigation/Facet-6-buildfilter.PNG
[7]: ./media/search-faceted-navigation/Facet-7-appstart.png
[8]: ./media/search-faceted-navigation/Facet-8-appbike.png
[9]: ./media/search-faceted-navigation/Facet-9-appbikefaceted.png
[10]: ./media/search-faceted-navigation/Facet-10-appTitle.png
[11]: ./media/search-faceted-navigation/faceted-search-before-facets.png
[12]: ./media/search-faceted-navigation/faceted-search-after-facets.png

<!--Link references-->
[Designing for Faceted Search]: http://www.uie.com/articles/faceted_search/
[Design Patterns: Faceted Navigation]: http://alistapart.com/article/design-patterns-faceted-navigation
[Create your first application]: search-create-first-solution.md
[OData expression syntax (Azure Search)]: http://msdn.microsoft.com/library/azure/dn798921.aspx
[Azure Search Adventure Works Demo]: https://azuresearchadventureworksdemo.codeplex.com/
[http://www.odata.org/documentation/odata-version-2-0/overview/]: http://www.odata.org/documentation/odata-version-2-0/overview/ 
[Faceting on Azure Search forum post]: ../faceting-on-azure-search.md?forum=azuresearch
[Search Documents (Azure Search API)]: http://msdn.microsoft.com/library/azure/dn798927.aspx

