---
title: "搜尋服務 REST API 版本 2015年-02-28-preview aaaAzure |Microsoft 文件"
description: "Azure 搜尋服務 REST API Version 2015-02-28-Preview 包含自然語言分析器和 moreLikeThis 搜尋等實驗性功能。"
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a>Azure 搜尋服務 REST API：版本 2015-02-28-Preview
這篇文章是 hello 參考文件集`api-version=2015-02-28-Preview`。 這個預覽擴充 hello 正式推出新版， [api 版本 = 2015年-02-28](https://msdn.microsoft.com/library/dn798935.aspx)，藉由提供下列實驗性功能的 hello:

* `moreLikeThis`查詢參數 hello[搜尋文件](#SearchDocs)應用程式開發介面。 它會找到相關 tooanother 特定文件的其他文件。

少數的其他組件 hello `2015-02-28-Preview` REST API 的說明文件。 其中包含：

* [評分設定檔](search-api-scoring-profiles-2015-02-28-preview.md)
* [索引子](search-api-indexers-2015-02-28-preview.md)

Azure 搜尋服務可以在多個版本中使用。 請參閱太[搜尋服務版本控制](http://msdn.microsoft.com/library/azure/dn864560.aspx)如需詳細資訊。

## <a name="apis-in-this-document"></a>本文件中的 API
Azure 搜尋服務 API 對 API 作業支援兩種 URL 語法：簡單和 OData (如需詳細資訊，請參閱 [OData 支援 (Azure 搜尋 API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) )。 hello 下列清單顯示 hello 簡單的語法。

[建立索引](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[更新索引](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[取得索引](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[列出索引](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[取得索引統計資料](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[測試分析器](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[删除索引](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[新增、刪除及更新索引內的資料](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[搜尋文件](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[查閱文件](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[文件計數](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[建議](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a>索引操作
您可以針對指定的索引資源，透過簡單的 HTTP 要求 (POST、GET、PUT、DELETE)，在 Azure 搜尋服務中建立與管理索引。 toocreate 索引，請先 POST 描述 hello 索引結構描述的 JSON 文件。 hello 結構描述定義 hello 欄位 hello 索引、 其資料類型，以及如何使用它們 （例如，在全文檢索搜尋、 篩選、 排序或面相化）。 它也會定義評分設定檔，建議工具和其他屬性 tooconfigure hello 索引的行為 hello。

hello 下列範例說明用於搜尋飯店資訊與 hello 描述欄位中使用兩種語言所定義的結構描述。 請注意屬性如何控制 hello 欄位的使用方式。 例如 hello`hotelId`當做 hello 文件索引鍵 (`"key": true`)，會從全文檢索搜尋中排除 (`"searchable": false`)。

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

建立 hello 索引之後，您將上傳會擴展 hello 索引的文件。 請參閱 [新增或更新文件](#AddOrUpdateDocuments) ，以取得這個後續步驟。

在 Azure 搜尋的影片介紹 tooindexing，請參閱 hello[頻道 9 雲端涵蓋的時段，對 Azure 搜尋](http://go.microsoft.com/fwlink/p/?LinkId=511509)。

<a name="CreateIndex"></a>

## <a name="create-index"></a>建立索引
索引是 hello 組織和搜尋 Azure 搜尋中的文件的主要方式，類似 toohow 資料表中組織記錄資料庫。 每個索引有全部符合 toohello 索引結構描述 （欄位名稱、 資料類型和屬性），但是索引也會指定定義其他搜尋行為的其他建構 （建議工具、 計分設定檔和 CORS 選項） 的文件的集合。

您可以使用簡單的 HTTP POST 或 PUT 要求，在 Azure 搜尋服務中建立新的索引。 hello hello 要求主體是指定 hello 索引和組態資訊的 JSON 結構描述。

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

或者，您可以使用 PUT，並在 hello URI 上指定 hello 索引名稱。 如果 hello 索引不存在，則會建立。

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

建立索引決定 hello hello 文件結構的儲存，而且在搜尋操作中使用。 填入 hello 索引是以個別的作業。 針對此步驟，您可以使用[索引子](https://msdn.microsoft.com/library/azure/mt183328.aspx) (適用於支援的資料類型) 或是[新增、更新或刪除文件](https://msdn.microsoft.com/library/azure/dn798930.aspx)作業。 發佈 hello 文件時，會產生 hello 反向索引。

**請注意**: hello 允許索引的數目上限依定價層而異。 hello 免費服務允許向上 too3 索引。 標準服務允許每個服務有 50 個索引。 如需詳細資訊，請參閱 [限制條件](http://msdn.microsoft.com/library/azure/dn798934.aspx) 。

**要求**

所有服務要求都需使用 HTTPS。 hello **Create Index**要求可以使用 POST 或 PUT 方法建構。 使用 POST 時，您必須提供 hello 索引結構描述定義以及 hello 要求主體中的索引名稱。 使用 PUT，hello 索引名稱會是 hello URL 的一部分。 如果 hello 索引不存在，它會建立它。 如果已經存在，則更新的 toohello 新定義。

hello 索引名稱必須是小寫、 以字母或數字開頭、 不含斜線或點，和不超過 128 個字元。 Hello 索引名稱開頭是字母或數字後, hello 其餘部分 hello 名稱可以包含任何字母、 數字和連字號，只要 hello 連字號不連續。

hello`api-version`需要。 如需可用版本清單，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。

**要求標頭**

hello 下列清單描述所需的 hello 和選擇性要求標頭。

* `Content-Type`：必要。 設定得`application/json`
* `api-key`：必要。 hello`api-key`是用來
* 驗證 hello 要求 tooyour 搜尋服務。 它是字串值、 唯一 tooyour 服務。 hello **Create Index**要求必須包含`api-key`標頭設定 tooyour 管理金鑰 （為相對於的 tooa 查詢索引鍵）。

您也需要 hello 服務名稱 tooconstruct hello 要求 URL。 您可以取得這兩個 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。 請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。

<a name="RequestData"></a>
**要求本文語法**

hello hello 要求主體包含結構描述定義，其中包括 hello 清單會送入此索引的文件中的資料欄位、 資料型別、 屬性，以及選擇性的計分設定檔清單會比對文件在使用的 tooscore查詢時間。

請注意，針對 POST 要求，您必須指定 hello 索引名稱 hello 要求主體中。

Hello 索引中只能有一個索引鍵欄位。 它有 toobe 字串欄位。 此欄位會顯示 hello hello 索引內所儲存的每個文件的唯一識別項。

hello 主要部份索引 hello 如下：

* `name`
* `fields` 將提供給此索引，包括名稱、資料類型及屬性，以用來定義該欄位上允許的動作。
* `suggesters` 可用於自動完成或自動提示查詢。
* `scoringProfiles` 可用於自訂搜尋分數評等。 如需詳細資訊，請參閱 [新增評分記錄檔](https://msdn.microsoft.com/library/azure/dn798928.aspx) 。
* `analyzers``charFilters`， `tokenizers`，`tokenFilters`用的 toodefine 文件/查詢如何分解為可編索引/可搜尋的語彙基元。 如需詳細資料，請參閱 [Azure 搜尋服務中的分析](https://aka.ms//azsanalysis) 。
* `defaultScoringProfile`使用 toooverwrite hello 預設計分行為。
* `corsOptions`tooallow 您對索引執行跨原始查詢。

hello 建構 hello 要求裝載的語法如下所示。 本主題稍後會提供範例要求。

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

**索引屬性**

hello 設定下列屬性可以建立索引時。 如需評分和評分設定檔的詳細資訊，請參閱 [新增評分設定檔](https://msdn.microsoft.com/library/azure/dn798928.aspx)。

`name`-設定 hello hello 欄位的名稱。

`type`-設定 hello hello 欄位的資料類型。

`searchable`-將標示 hello 欄位為全文檢索搜尋功能。 這表示它將在索引設定期間執行像是斷字的分析。 如果您設定`searchable`欄位 tooa 值，例如"sunny day"，在內部會分成 hello 個別的語彙基元"sunny"和 「 日 」。 這樣就能針對這些字詞進行全文檢索搜尋。 類型 `Edm.String` 或 `Collection(Edm.String)` 的欄位會預設為 `searchable`。 其他類型的欄位不能是 `searchable`。

* **請注意**:`searchable`欄位會耗用額外的空間索引，因為 Azure 搜尋會儲存 hello 全文檢索搜尋的欄位值的其他語彙基元化的版本。 如果您希望 toosave 空間索引，您不需要包含在搜尋中欄位 toobe、 設定`searchable`太`false`。

`filterable`-可讓參考中的 hello 欄位 toobe`$filter`查詢。 `filterable` 處理字串的方式與 `searchable` 不同。 類型 `Edm.String` 或 `Collection(Edm.String)` 的欄位 (它們是 `filterable`) 不會執行斷字功能，因此，只會針對完全相符的項目進行比較。 例如，如果您將這類欄位`f`太"sunny day"，`$filter=f eq 'sunny'`會尋找相符的項目，但`$filter=f eq 'sunny day'`會。 所有欄位都會預設為 `filterable` 。

`sortable`-Hello 系統根據預設依分數排序結果，但在許多經驗的使用者會想 toosort hello 文件中的欄位。 類型 `Collection(Edm.String)` 的欄位不能是 `sortable`。 所有的其他欄位都會預設為 `sortable` 。

`facetable`- 通常用於搜尋結果的呈現方式，其中包括依類別排序的點閱數 (例如，搜尋數位相機，然後依照品牌、百萬像素、價格等項目來查看點閱數)。 此選項無法與類型 `Edm.GeographyPoint`的欄位搭配使用。 所有的其他欄位都會預設為 `facetable` 。

* **注意**：類型 `Edm.String` 的欄位 (它們是 `filterable`、`sortable` 或 `facetable`) 長度上限為 32 KB。 這是因為這類欄位會被視為單一搜尋詞彙，並在 Azure 搜尋詞彙的 hello 最大長度為 32 KB。 如果您需要 toostore 文字超過這個單一字串欄位中，您將需要 tooexplicitly 設定`filterable`， `sortable`，和`facetable`太`false`索引定義中。
* **請注意**： 如果欄位有無 hello 上述屬性設定太`true`(`searchable`， `filterable`， `sortable`，或`facetable`) hello 欄位有效地排除 hello 反向索引。 針對查詢中未使用，但需要在搜尋結果中使用的欄位來說，此選項非常實用。 這類欄位排除 hello 索引可改善效能。

`key`-標記 hello 欄位為包含 hello 索引內的文件的唯一識別碼。 只有一個欄位必須被選為 hello`key`欄位，它必須是型別`Edm.String`。 索引鍵欄位可以是直接透過 hello 的文件使用的 toolook[查閱 API](#LookupAPI)。

`retrievable`-設定是否可以在搜尋結果中傳回 hello 欄位。  當您想 toouse 欄位 （例如，邊界） 要做為篩選、 排序或計分機制，但不是想 hello 欄位 toobe 可見 toohello 終端使用者，這非常有用。 針對 `true` for `key` 。

`analyzer`-設定在搜尋時間及建立索引時 hello hello 分析器 toouse hello 欄位的名稱。 Hello 允許一組值，請參閱[分析器](https://msdn.microsoft.com/library/mt605304.aspx)。 此選項只可以搭配 `searchable` 欄位使用，而無法與 `searchAnalyzer` 或 `indexAnalyzer` 一起設定。  Hello 分析器選擇之後，就無法變更 hello 欄位中。

`searchAnalyzer`-設定 hello hello 分析器次 hello 欄位搜尋使用的名稱。 Hello 允許一組值，請參閱[分析器](https://msdn.microsoft.com/library/mt605304.aspx)。 此選項只能與 `searchable` 欄位搭配使用。 它必須設定搭配`indexAnalyzer`而且不能設定以及 hello`analyzer`選項。 此分析器可在現有欄位上更新。

`indexAnalyzer`-設定 hello hello 分析器 hello 欄位建立索引時使用的名稱。 Hello 允許一組值，請參閱[分析器](https://msdn.microsoft.com/library/mt605304.aspx)。 此選項只能與 `searchable` 欄位搭配使用。 它必須設定搭配`searchAnalyzer`而且不能設定以及 hello`analyzer`選項。 Hello 分析器選擇之後，就無法變更 hello 欄位中。

`suggesters`-設定 hello 搜尋模式和 hello 內容來源的 hello 建議的欄位。 如需詳細資訊，請參閱 [建議工具](#Suggesters) 。

`scoringProfiles` - 定義自訂評分行為，讓您能夠影響搜尋結果中哪些項目的出現機率會比較高。 評分設定檔是由欄位權數和函式所組成。 請參閱[新增計分設定檔](https://msdn.microsoft.com/library/azure/dn798928.aspx)如需有關使用計分設定檔中的 hello 屬性。

<!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**語言支援**

可搜尋的欄位最常執行的分析是斷字、文字正規化，以及篩選出字詞。 根據預設，在 Azure 搜尋可搜尋的欄位都會經過分析，以 hello [Apache Lucene 標準分析器](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html)文字分解為下列項目["Unicode 文字分割"](http://unicode.org/reports/tr29/)規則。 此外，hello 標準分析器會將所有字元 tootheir 小寫的形式。 索引的文件和搜尋詞彙會編製索引和查詢處理期間經歷 hello 分析。

Azure 搜尋支援多種語言。 每一種語言都需要非標準的文字分析器，以負責指定語言的特性。 Azure 搜尋服務提供兩種類型的分析器：

* 由 Lucene 所支援的 35 種分析器。
* 由專屬的 Microsoft 自然語言處理技術所支援的 50 種分析器，此技術同樣用於 Office 和 Bing 中。

有些開發人員可能會偏好 hello Lucene 的更熟悉、 簡單、 開放原始碼方案。 Lucene 分析器位於更快、 但 hello Microsoft 分析器具有進階的功能，例如詞形、 word decompounding （在語言，例如德文、 丹麥文、 荷蘭文、 瑞典文、 挪威文、 愛沙尼亞文、 完成、 匈牙利文、 斯洛伐克文） 和實體辨識 (Url電子郵件、 日期、 數字)。 可能的話，您應該執行這兩個 hello Microsoft 和 Lucene 分析器 toodecide 哪一個是更適合的比較。

***比較它們的方法***

英文版的 hello Lucene 分析器會擴充 hello 標準分析器。 它會從字組中移除所有格 (結尾的 's)、為每個 [Porter 詞幹演算法](http://tartarus.org/~martin/PorterStemmer/)套用詞幹，然後移除英文[停用字詞](http://en.wikipedia.org/wiki/Stop_words)。

相較之下，hello Microsoft 分析器執行詞形而不是詞幹分析。 這表示它可以把變形和不規則的字詞形式處理得更好，以得到相關性更強的搜尋結果 (如需詳細資訊，請參閱 [Azure 搜尋 MVA 簡報](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) 的模組 7)。

索引包含 Microsoft 分析器平均是兩個 toothree 時間低於 Lucene 的對應項，視 hello 語言而定。 平均大小的查詢應不至大幅影響搜尋效能。

***組態***

Hello 索引定義中的每個欄位，您可以設定 hello`analyzer`屬性，指定的語言和廠商 tooan 分析器名稱。 索引與搜尋該欄位時，就會套用相同的分析器 hello。
例如，您可以個別欄位的英文、 法文和西班牙文旅館說明在 hello 中並排存在於相同的索引。 使用 hello ['searchFields' 查詢參數](#SearchQueryParameters)toospecify 針對哪些語言特有的欄位 toosearch 在查詢中。 您可以檢閱查詢範例，包括 hello`analyzer`屬性[搜尋文件](#SearchDocs)。 

***分析器清單***

以下是支援的語言與 Lucene 和 Microsoft 分析器名稱 hello 清單。

<table style="font-size:12">
    <tr>
        <th>語言</th>
        <th>Microsoft 分析器名稱</th>
        <th>Lucene 分析器名稱</th>
    </tr>
    <tr>
        <td>阿拉伯文</td>
        <td>ar.microsoft</td>
        <td>ar.lucene</td>        
    </tr>
    <tr>
        <td>亞美尼亞文</td>
        <td></td>
        <td>hy.lucene</td>
      </tr>
    <tr>
        <td>孟加拉文</td>
        <td>bn.microsoft</td>
        <td></td>
    </tr>
      <tr>
        <td>巴斯克文</td>
        <td></td>
        <td>eu.lucene</td>
    </tr>
      <tr>
         <td>保加利亞文</td>
        <td>bg.microsoft</td>
        <td>bg.lucene</td>
      </tr>
      <tr>
        <td>卡達隆尼亞文</td>
        <td>ca.microsoft</td>
        <td>ca.lucene</td>          
      </tr>
    <tr>
        <td>簡體中文</td>
        <td>zh-Hans.microsoft</td>
        <td>zh-Hans.lucene</td>        
    </tr>
    <tr>
        <td>繁體中文</td>
        <td>zh-Hant.microsoft</td>
        <td>zh-Hant.lucene</td>        
    <tr>
    <tr>
        <td>克羅埃西亞文</td>
        <td>hr.microsoft</td>
        <td/></td>
    </tr>
    <tr>
        <td>捷克文</td>
        <td>cs.microsoft</td>
        <td>cs.lucene</td>        
    </tr>    
    <tr>
        <td>丹麥文</td>
        <td>da.microsoft</td>
        <td>da.lucene</td>        
    </tr>    
    <tr>
        <td>荷蘭文</td>
        <td>nl.microsoft</td>
        <td>nl.lucene</td>    
    </tr>    
    <tr>
        <td>English</td>        
        <td>en.microsoft</td>
        <td>en.lucene</td>        
    </tr>
    <tr>
        <td>愛沙尼亞文</td>
        <td>et.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>芬蘭文</td>
        <td>fi.microsoft</td>
        <td>fi.lucene</td>        
    </tr>    
    <tr>
        <td>法文</td>
        <td>fr.microsoft</td>
        <td>fr.lucene</td>        
    </tr>
    <tr>
        <td>加里斯亞文</td>
        <td></td>
        <td>gl.lucene</td>        
      </tr>
    <tr>
        <td>德文</td>
        <td>de.microsoft</td>
        <td>de.lucene</td>        
    </tr>
    <tr>
        <td>希臘文</td>
        <td>el.microsoft</td>
        <td>el.lucene</td>        
    </tr>
    <tr>
        <td>古吉拉特文</td>
        <td>gu.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>希伯來文</td>
        <td>he.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>北印度文</td>
        <td>hi.microsoft</td>
        <td>hi.lucene</td>        
    </tr>
    <tr>
        <td>匈牙利文</td>        
        <td>hu.microsoft</td>
        <td>hu.lucene</td>
    </tr>
    <tr>
        <td>冰島文</td>
        <td>is.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>印尼文 (Bahasa)</td>
        <td>id.microsoft</td>
        <td>id.lucene</td>        
    </tr>
    <tr>
        <td>愛爾蘭文</td>
        <td></td>
          <td>ga.lucene</td>
    </tr>
    <tr>
        <td>義大利文</td>
        <td>it.microsoft</td>
        <td>it.lucene</td>        
    </tr>
    <tr>
        <td>日文</td>
        <td>ja.microsoft</td>
        <td>ja.lucene</td>

    </tr>
    <tr>
        <td>坎那達文</td>
        <td>ka.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>韓文</td>
        <td>ko.microsoft</td>
        <td>ko.lucene</td>
    </tr>
    <tr>
        <td>拉脫維亞文</td>        
        <td>lv.microsoft</td>
        <td>lv.lucene</td>    
    </tr>
    <tr>
        <td>立陶宛文</td>
        <td>lt.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>馬來亞拉姆文</td>
        <td>ml.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>馬來文 (拉丁)</td>
        <td>ms.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>馬拉提文</td>
        <td>mr.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>挪威文</td>
        <td>nb.microsoft</td>
        <td>no.lucene</td>        
    </tr>
      <tr>
        <td>波斯文</td>
        <td></td>
        <td>fa.lucene</td>        
      </tr>
    <tr>
        <td>波蘭文</td>
        <td>pl.microsoft</td>
        <td>pl.lucene</td>        
    </tr>
    <tr>
        <td>葡萄牙文 (巴西)</td>
        <td>pt-Br.microsoft</td>
        <td>pt-Br.lucene</td>        
    </tr>
    <tr>
        <td>葡萄牙文 (葡萄牙)</td>
        <td>pt-Pt.microsoft</td>        
        <td>pt-Pt.lucene</td>
    </tr>
    <tr>
        <td>旁遮普文</td>
        <td>pa.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>羅馬尼亞文</td>
        <td>ro.microsoft</td>
        <td>ro.lucene</td>
    </tr>
    <tr>
        <td>俄文</td>
        <td>ru.microsoft</td>
        <td>ru.lucene</td>    
    </tr>
    <tr>
        <td>塞爾維亞文 (斯拉夫)</td>
        <td>sr-cyrillic.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>塞爾維亞文 (拉丁)</td>
        <td>sr-latin.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>斯洛伐克文</td>
        <td>sk.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>斯洛維尼亞文</td>
        <td>sl.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>西班牙文</td>
        <td>es.microsoft</td>
        <td>es.lucene</td>
    </tr>
    <tr>
        <td>瑞典文</td>
        <td>sv.microsoft</td>
        <td>sv.lucene</td>
    </tr>

    <tr>
        <td>坦米爾文</td>
        <td>ta.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>特拉古文</td>
        <td>te.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>泰文</td>
        <td>th.microsoft</td>
        <td>th.lucene</td>
    </tr>
    <tr>
        <td>土耳其文</td>
        <td>tr.microsoft</td>
        <td>tr.lucene</td>        
    </tr>
    <tr>
        <td>烏克蘭文</td>
        <td>uk.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>烏都文</td>
        <td>ur.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>越南文</td>
        <td>vi.microsoft</td>
        <td></td>
    </tr>
    <td colspan="3">此外，Azure 搜尋服務還提供無從驗證語言的分析器設定</td>
    <tr>
        <td>標準 ASCII 摺疊</td>
        <td>standardasciifolding.lucene</td>
        <td>
        <ul>
            <li>Unicode 文字分割 (標準的 Tokenizer)</li>
            <li>ASCII 摺疊篩選器的轉換不屬於第一個 127 ASCII 字元 toohello 組與其 ASCII 相等項到 Unicode 字元。 這在移除讀音符號時非常有用。</li>
        </ul>
        </td>
    </tr>
</table>

所有名稱加上 <i>lucene</i> 註解的分析器都是由 [Apache Lucene 的語言分析器](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html)所提供。 可以找到 hello ASCII 摺疊篩選器的詳細資訊[這裡](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html)。

**建議工具**

A`suggester`定義索引中的哪些欄位會使用的 toosupport 搜尋中的自動完成。 部分搜尋字串通常傳送 toohello[建議 API](#Suggestions) hello 使用者輸入搜尋查詢，而 hello API 會傳回一組建議的片語。 建議您在 hello 索引中定義的工具會決定哪些欄位是使用的 toobuild hello 預先輸入的搜尋詞彙。 如需組態詳細資料，請參閱[建議工具](#Suggesters)。

**評分設定檔**

A`scoringProfile`定義自訂計分行為，可讓您影響較高 hello 搜尋結果中出現的項目。 評分設定檔是由欄位權數和函式所組成。 toouse 它們，您指定設定檔在 hello 查詢字串的名稱。

預設的計分設定檔運作背後 hello 場景 toocompute 結果集中的每個項目的搜尋分數。 您可以使用 hello 內部且未命名評分設定檔。 或者，設定`defaultScoringProfile`toouse 為 hello 預設值，每當 hello 查詢字串中未指定自訂設定檔時叫用自訂設定檔。

請參閱[新增評分設定檔 tooa 搜尋索引 (Azure 搜尋服務 REST API)](search-api-scoring-profiles-2015-02-28-preview.md)如需詳細資訊。

**CORS 選項**

用戶端 Javascript 無法呼叫任何應用程式開發介面，根據預設，因為 hello 瀏覽器會防止所有跨原始要求。 啟用 CORS （跨原始資源共用） 設定 hello`corsOptions`屬性 tooallow 跨原始查詢 tooyour 索引。 請注意，基於安全緣故，只有查詢 API 支援 CORS。 適用於 CORS，您可以設定下列選項的 hello:

* `allowedOrigins`（必要）： 這是會被授與存取 tooyour 索引的原始來源清單。 這表示任何從該來源提供的 Javascript 程式碼會被允許 tooquery 您的索引 （假設其提供 hello 正確的 API 金鑰）。 每個來源一般而言都會 hello 表單`protocol://fully-qualified-domain-name:port`雖然 hello 連接埠常會被省略。 如需詳細資訊，請參閱 [這篇文章](http://go.microsoft.com/fwlink/?LinkId=330822) 。
  * 如果您想要 tooallow 存取 tooall 原始來源，包含`*`做為單一項目在 hello`allowedOrigins`陣列。 請注意， **不建議針對生產搜尋服務使用這個做法。** 但是，如果是基於開發或偵錯目的，它就非常實用。
* `maxAgeInSeconds`（選擇性）： 瀏覽器使用這個值 toodetermine hello 持續時間 （以秒為單位） toocache CORS 預檢回應。 這必須是非負數的整數。 hello 較大的這個值就會越 hello 更佳的效能，但 CORS 原則變更 tootake 效果花費的 hello 較長。 若未設定，即會使用預設持續期間 5 分鐘。

<a name="CreateUpdateIndexExample"></a>
**要求本文範例**

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

**回應**

要求成功：「201 已建立」。

根據預設 hello 回應主體會包含 hello JSON hello 索引定義所建立。 如果 hello`Prefer`要求標頭設定得`return=minimal`hello 回應主體會是空白，hello 成功狀態碼將會是 「 204 沒有內容 」 而不是 「 201 已建立 」。 這是無論 PUT 或 POST 是使用的 toocreate hello 索引，則為 true。

**備註**

目前針對索引結構描述更新提供有限支援。 目前不支援任何需要重新編製索引的結構描述更新 (例如，變更欄位類型)。 雖然無法變更現有欄位，或已刪除，則新欄位可以隨時加入 tooan 現有的索引。 當加入新的欄位時，hello 索引中的所有現有文件會自動提供該欄位的 null 值。 新文件加入 toohello 索引之前，將耗用額外的儲存空間。

<a name="Suggesters"></a>

## <a name="suggesters"></a>建議工具
在 Azure 搜尋中的 hello 建議功能是提供一份潛在回應 toopartial 字串輸入的搜尋方塊中輸入搜尋詞彙的自動填寫或自動完成查詢功能。 當您使用商業 Web 搜尋引擎時，您可能已經注意到查詢建議：在 Bing 中輸入 ".NET" 會產生 ".NET 4.5"、".NET Framework 3.5" 等等的詞彙清單。 使用 hello 搜尋服務 REST API 時，自訂的 Azure 搜尋應用程式中實作建議需要 hello 下列：

* 藉由新增啟用建議**建議工具**叫用您在索引中，提供 hello 名稱、 搜尋模式和欄位清單的預先輸入的建構。 例如，如果您指定"cityName"做為來源欄位，輸入部分搜尋字串"Sea"將會導致 「 西雅圖 」、"Seaside"和"Seatac"（三個都是實際城市名稱） 提供做查詢建議 toohello 使用者。
* 叫用呼叫 hello 建議[建議 API](#Suggestions)應用程式程式碼中。 通常部分搜尋字串 hello 使用者輸入搜尋查詢，而此 API 會傳回一組建議的片語傳送 toohello 服務。

這篇文章說明如何 tooconfigure**建議工具**。 您也應該檢閱 hello[建議 API](#Suggestions)的建議工具的使用方式的詳細資料。

**用法**

`Suggesters`hello 索引中建立和使用時效果最佳 toosuggest 特定文件，而不是鬆散的詞彙或片語。 hello 最佳候選項目欄位是標題、 名稱和其他相對較短的片語，可以識別項目。 不太有效的是重複的欄位 (例如，類別和標記) 或非常長的欄位 (例如，說明或註解欄位)。

Hello 索引定義的一部分，您可以加入單一建議工具 toohello`suggesters`集合。 這些屬性定義的建議工具 hello 如下：

* `name`: hello hello 建議工具名稱。 呼叫 hello 時，使用 hello hello 建議工具名稱`suggest`應用程式開發介面。
* `searchMode`: hello 用策略 toosearch 候選片語。 hello 只有目前支援的模式是`analyzingInfixMatching`，它會執行彈性比對片語 hello 開頭或 hello 中間的句子。
* `sourceFields`： 一或多個欄位清單的 hello 內容來源的 hello 的建議。 只有類型 `Edm.String` 和 `Collection(Edm.String)` 的欄位可以用來做為提供建議的來源。 您只能使用未設定自訂語言分析器的欄位。

**建議工具範例**

建議工具是 hello 索引的一部分。 只能有一個建議工具可以存在於 hello `suggesters` hello 目前版本，與 hello 並列中的集合的欄位集合和`scoringProfiles`。

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> 如果您使用 hello Azure 搜尋公用預覽版本`suggesters`取代較舊的布林值屬性 (`"suggestions": false`)，僅支援簡短字串 （3-25 個字元） 前置詞建議。 一個取代， `suggesters`，支援中置比對的 hello 開頭或欄位內容的 hello 中間尋找相符詞彙具有較佳的搜尋字串中的錯誤容錯性。 從 hello 上市版本開始，這是現在 hello 唯一 hello 建議應用程式開發介面的實作。 較舊的 hello`suggestions`屬性中導入`api-version=2014-07-31-Preview`toowork 繼續在該版本中，但不是在 hello 操作`2015-02-28`或更新版本的 Azure 搜尋。
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a>更新索引
您可以在 Azure 搜尋服務中，使用 HTTP PUT 要求來更新現有的索引。 更新可以加入新欄位 toohello 現有結構描述、 修改 CORS 選項，以及修改計分設定檔。 如需詳細資訊，請參閱 [新增評分設定檔](https://msdn.microsoft.com/library/azure/dn798928.aspx) 。 您可以指定 hello 索引 tooupdate hello 名稱 hello 要求 URI:

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**重要事項：**索引結構描述更新的支援是有限的 toooperations 不需要重建 hello 搜尋索引。 目前不支援任何需要重新編製索引的結構描述更新 (例如，變更欄位類型)。 儘管無法變更或刪除現有欄位，但可隨時新增欄位。 hello 一樣太`suggesters`。 Tooa 建議工具在 hello 時間 hello 欄位會新增，但無法從移除欄位，可能會加入新欄位`suggesters`，無法加入現有的欄位太`suggesters`。

當加入新欄位 tooan 索引，hello 索引中的所有現有文件會自動提供該欄位的 null 值。 新文件加入 toohello 索引之前，將耗用額外的儲存空間。

**要求**

所有服務要求都需使用 HTTPS。 hello**更新索引**要求使用 HTTP PUT 建構。 使用 PUT，hello 索引名稱會是 hello URL 的一部分。 如果 hello 索引不存在，它會建立它。 如果 hello 索引已經存在，則更新的 toohello 新定義。

hello 索引名稱必須是小寫、 以字母或數字開頭、 不含斜線或點，和不超過 128 個字元。 Hello 索引名稱開頭是字母或數字後, hello 其餘部分 hello 名稱可以包含任何字母、 數字和連字號，只要 hello 連字號不連續。

`api-version=[string]` (必要)。 hello 預覽版本`api-version=2015-02-28-Preview`。 如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。

**要求標頭**

hello 下列清單描述所需的 hello 和選擇性要求標頭。

* `Content-Type`：必要。 設定得`application/json`
* `api-key`：必要。 hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。 它是字串值、 唯一 tooyour 服務。 hello**更新索引**要求必須包含`api-key`標頭設定 tooyour 管理金鑰 （為相對於的 tooa 查詢索引鍵）。

您也需要 hello 服務名稱 tooconstruct hello 要求 URL。 您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。 請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。

**要求本文的語法**

在更新現有的索引，hello 主體必須包含原始結構描述定義 hello，加上您要新增，hello 新欄位，以及 hello 修改計分設定檔，建議工具和 CORS 選項，如果有的話。 如果您未修改 hello 計分設定檔和 CORS 選項，您必須包含 hello hello 索引建立時的原始資料。 更新 hello 最佳模式 toouse 一般是使用 GET tooretrieve hello 索引定義，請修改它，然後使用 PUT 予以更新。

使用方便 hello 結構描述語法的 toocreate 索引在此處重現。 如需更多詳細資訊，請參閱 [建立索引](#CreateIndex) 。

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


**回應**

要求成功：「204 沒有內容」。

根據預設 hello 回應主體是空的。 不過，如果 hello`Prefer`要求標頭設定得`return=representation`，hello 回應主體會包含已更新的 hello 索引定義的 hello JSON。 Hello 成功狀態碼將會在此情況下，「 200 確定 」。

**使用自訂分析器來更新索引定義**

定義分析器、權杖化工具、語彙基元篩選或字元篩選之後，即無法進行修改。 新的可以 tooan 現有的索引，才加入 hello`allowIndexDowntime`旗標設定 tootrue hello 索引更新要求中： 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

請注意，這項作業將會放入您的離線索引至少幾秒，導致您的索引和查詢要求 toofail。 Hello 索引的效能和寫入可用性可以是障礙者數分鐘之後更新 hello 索引時，或較長時間非常大的索引。

<a name="ListIndexes"></a>

## <a name="list-indexes"></a>列出索引
hello**列出索引**作業會傳回一份 hello 索引目前在您的 Azure 搜尋服務。

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

**要求**

所有服務要求都需使用 HTTPS。 hello**列出索引**要求可以使用 hello GET 方法建構。

`api-version=[string]` (必要)。 hello 預覽版本`api-version=2015-02-28-Preview`。 如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。

**要求標頭**

hello 下列清單描述所需的 hello 和選擇性要求標頭。

* `api-key`：必要。 hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。 它是字串值、 唯一 tooyour 服務。 hello**列出索引**要求必須包含`api-key`組 tooan 管理金鑰 （為相對於的 tooa 查詢索引鍵）。

您也需要 hello 服務名稱 tooconstruct hello 要求 URL。 您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。 請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。

**要求本文**

無。

**回應**

回應成功時會傳回狀態碼：200 OK。

下列為回應本文的範例：

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

請注意，您可以篩選您感興趣的 toojust hello 屬性下的 hello 回應。 例如，如果您想要一份索引名稱，使用 hello OData`$select`查詢選項：

    GET /indexes?api-version=2015-02-28-Preview&$select=name

在此情況下，hello 回應 hello 上述範例中會出現，如下所示：

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

如果您的搜尋服務中有大量索引，這是很有用的技巧 toosave 頻寬。

<a name="GetIndex"></a>

## <a name="get-index"></a>取得索引
hello**取得索引**作業會從 Azure 搜尋取得 hello 索引定義。

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**要求**

服務要求需要使用 HTTPS。 hello**取得索引**要求可以使用 hello GET 方法建構。

hello [索引名稱] hello 要求 URI 中的指定從 hello 索引集合的索引 tooreturn。

`api-version=[string]` (必要)。 hello 預覽版本`api-version=2015-02-28-Preview`。 如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。

**要求標頭**

hello 下列清單描述所需的 hello 和選擇性要求標頭。

* `api-key`: hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。 它是字串值、 唯一 tooyour 服務。 hello**取得索引**要求必須包含`api-key`組 tooan 管理金鑰 （為相對於的 tooa 查詢索引鍵）。

您也需要 hello 服務名稱 tooconstruct hello 要求 URL。 您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。 請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。

**要求本文**

無。

**回應**

回應成功時會傳回狀態碼：200 OK。

請參閱 hello 範例 JSON 中[建立和更新索引](#CreateUpdateIndexExample)hello 回應裝載的範例。

<a name="DeleteIndex"></a>

## <a name="delete-index"></a>删除索引
hello**刪除索引**作業會從您的 Azure 搜尋服務移除索引和相關聯的文件。 您可以從 hello hello Azure 入口網站中的服務儀表板或 hello API 來取得 hello 索引名稱。 如需詳細資訊，請參閱 [列出索引](#ListIndexes) 。

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**要求**

服務要求需要使用 HTTPS。 hello**刪除索引**要求可以使用 hello DELETE 方法建構。

hello [索引名稱] hello 要求 URI 中的指定從 hello 索引集合的索引 toodelete。

`api-version=[string]` (必要)。 hello 預覽版本`api-version=2015-02-28-Preview`。 如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。

**要求標頭**

hello 下列清單描述所需的 hello 和選擇性要求標頭。

* `api-key`：必要。 hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。 它是字串值，唯一 tooyour 服務 URL。 hello**刪除索引**要求必須包含`api-key`標頭設定 tooyour 管理金鑰 （為相對於的 tooa 查詢索引鍵）。

您也需要 hello 服務名稱 tooconstruct hello 要求 URL。 您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。 請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。

**要求本文**

無。

**回應**

狀態碼：回應成功時會傳回「204 沒有內容」。

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a>取得索引統計資料
hello**取得索引統計資料**作業從 Azure 搜尋會傳回 hello 目前的索引，再加上的存放裝置使用量的文件計數。

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> 文件計數和儲存體大小的統計資料會每隔幾分鐘收集，不會即時收集。 因此，此 API 所傳回的 hello 統計資料可能無法反映新的索引作業所造成的變更中。
> 
> 

**要求**

所有服務要求都需要使用 HTTPS。 hello**取得索引統計資料**要求可以使用 hello GET 方法建構。

hello 要求 URI 中的 hello [索引名稱] 會告知 hello 服務 tooreturn 索引統計資料的 hello 指定的索引。

`api-version=[string]` (必要)。 hello 預覽版本`api-version=2015-02-28-Preview`。 如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。

**要求標頭**

hello 下列清單描述所需的 hello 和選擇性要求標頭。

* `api-key`: hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。 它是字串值、 唯一 tooyour 服務。 hello**取得索引統計資料**要求必須包含`api-key`組 tooan 管理金鑰 （為相對於的 tooa 查詢索引鍵）。

您也需要 hello 服務名稱 tooconstruct hello 要求 URL。 您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。 請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。

**要求本文**

無。

**回應**

回應成功時會傳回狀態碼：200 OK。

hello 回應主體是在 hello 下列格式：

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a>測試分析器
hello**分析 API**分析器為語彙基元所分隔的文字會顯示。

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**要求**

所有服務要求都需要使用 HTTPS。 hello**分析 API**要求可以使用 hello POST 方法建構。

`api-version=[string]` (必要)。 hello 預覽版本`api-version=2015-02-28-Preview`。 如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。

**要求標頭**

hello 下列清單描述所需的 hello 和選擇性要求標頭。

* `api-key`: hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。 它是字串值、 唯一 tooyour 服務。 hello**分析 API**要求必須包含`api-key`組 tooan 管理金鑰 （為相對於的 tooa 查詢索引鍵）。

您也必須 hello 索引名稱與 hello 服務名稱 tooconstruct hello 要求 URL。 您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。 請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。

**要求本文**

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

或

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

hello `analyzer_name`， `tokenizer_name`，`token_filter_name`和`char_filter_name`hello 索引需要 toobe 的預先定義或自訂的分析器、 tokenizer、 語彙基元的篩選器和 char 篩選有效的名稱。 toolearn 解 hello 語彙分析程序，請參閱[Azure 搜尋中的分析](https://aka.ms/azsanalysis)。

**回應**

回應成功時會傳回狀態碼：200 OK。

hello 回應主體是在 hello 下列格式：

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

**分析 API 範例**

**要求**

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

**回應**

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a>文件操作
在 Azure 搜尋中，索引會儲存在 hello 雲端，並使用您上傳 toohello 服務的 JSON 文件填入。 您上傳的所有 hello 文件的各都構成 hello 主體的搜尋資料的分類。 文件會包含欄位，其中一些欄位會在它們上傳時語彙基元化為搜尋字詞。 hello `/docs` hello Azure 搜尋 API 中的 URL 區段代表 hello 集合中索引的文件。 例如上傳的 hello 集合上執行的所有作業，合併、 刪除或查詢文件都需要單一的索引，因此 hello Url hello 內容中的位置，這些作業一律會以啟動`/indexes/[index name]/docs`指定的索引名稱。

應用程式程式碼必須產生 JSON 文件 tooupload tooAzure 搜尋，或者您可以使用[索引子](https://msdn.microsoft.com/library/dn946891.aspx)tooload 文件，如果 hello 資料來源是 Azure SQL Database 或 Azure Cosmos DB。 通常，索引是從您提供的單一資料集填入。

您應該計劃讓每個項目，您會想 toosearch 一份文件。 電影出租應用程式可能是每部電影有一份文件、店面應用程式可能是每個 SKU 有一份文件、線上課程應用程式可能是每個課程有一份文件、研究公司可能會在他們的存放庫中針對每份學術報告有一份文件，依此類推。

文件是由一或多個欄位所組成。 欄位包含已由 Azure 搜尋服務語彙基元化為搜尋字詞的文字，以及非語彙基元化或非文字的值 (這類值可用於篩選器或評分設定檔)。 hello 名稱、 資料類型，以及支援每個欄位的搜尋功能取決於 hello 索引結構描述。 其中每個索引結構描述中的 hello 欄位必須指定為識別碼，以及每個文件必須具有唯一識別該文件 hello 索引中的 hello 識別碼欄位的值。 所有其他文件欄位是選擇性的若未將預設 tooa null 值。 請注意，null 值不會佔用 hello 搜尋索引中的空間。

您可以上傳文件之前，您必須已經建立 hello 索引 hello 服務上。 如需這第一個步驟的詳細資訊，請參閱 [建立索引](#CreateIndex) 。

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a>新增、更新或刪除文件
您可以使用 HTTP POST，從指定的索引上傳、合併、合併或上傳，或者刪除文件。 對於大量的更新中，批次 （每個批次 too1000 文件） 或 16MB 批次的文件的建議。

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**要求**

所有服務要求都需使用 HTTPS。 您可以使用 HTTP POST，從指定的索引上傳、合併、合併或上傳，或者刪除文件。

hello 要求 URI 包含 [索引名稱] 中，指定哪些索引 toopost 文件。 您只可以一次張貼的文件 tooone 索引。

`api-version=[string]` (必要)。 hello 預覽版本`api-version=2015-02-28-Preview`。 如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。

**要求標頭**

hello 下列清單描述所需的 hello 和選擇性要求標頭。

* `Content-Type`：必要。 設定得`application/json`
* `api-key`：必要。 hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。 它是字串值、 唯一 tooyour 服務。 hello**加入文件**要求必須包含`api-key`標頭設定 tooyour 管理金鑰 （為相對於的 tooa 查詢索引鍵）。

您也需要 hello 服務名稱 tooconstruct hello 要求 URL。 您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。 請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。

**要求本文**

hello hello 要求主體包含一或多個文件 toobe 編製索引。 文件是透過唯一的索引鍵來識別。 每份文件都會與下列某個動作相關聯：上傳、合併、合併或上傳，或是刪除。 上傳要求必須包含 hello 文件資料做為索引鍵/值組集合。

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> 文件索引鍵可以只包含字母、數字、連字號 ("-")、底線 ("_")，及等號 ("=")。 如需詳細資訊，請參閱 [命名規則](https://msdn.microsoft.com/library/azure/dn857353.aspx)。
> 
> 

**文件動作**

* `upload`： 上傳動作是類似 tooan"upsert"(如果它是新插入和更新/取代如果它存在 hello 文件。 請注意在 hello 更新情況下會取代所有欄位。
* `merge`： 現有文件以 hello 合併更新指定的欄位。 如果 hello 文件不存在，hello 合併將會失敗。 您在合併中指定任何欄位將會取代 hello hello 文件中的現有欄位。 這包括類型 `Collection(Edm.String)`的欄位。 例如，如果 hello 文件包含的欄位值的"tags"`["budget"]`和執行的合併值`["economy", "pool"]`hello 「 標記 」 欄位 hello 最終值將會是 「 標記 」， `["economy", "pool"]`。 而**不**會是 `["budget", "economy", "pool"]`。
* `mergeOrUpload`： 行為類似`merge`如果 hello 索引中的文件以 hello 給定索引鍵已經存在。 如果 hello 文件不存在，其行為類似`upload`與新的文件。
* `delete`: Delete 會移除 hello 索引中的 hello 指定文件。 請注意，所有的欄位您指定在`delete`hello 索引鍵欄位以外的作業將會被忽略。 如果您想 tooremove 個別欄位從 文件，請使用`merge`相反地，並直接將 hello 欄位明確太`null`。

**回應**

成功回應時會傳回的狀態碼 200 (OK)，表示所有項目都已成功編製索引。 這會由 hello`status`屬性所設定的所有項目，以及 hello tootrue `statusCode` tooeither 201 （適用於新上傳的文件） 」 或 「 200 （如合併或刪除文件） 所設定的屬性：

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

至少有一個項目未成功建立索引時會傳回狀態碼 207 (多狀態)。 未索引的項目具有 hello`status`欄位設定 toofalse。 hello`errorMessage`和`statusCode`屬性會指出 hello hello 索引錯誤的原因：

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

下表中的 hello 說明的 hello 各種個別文件可以 hello 回應中傳回的狀態碼。 請注意一些表示 hello 要求本身的問題，而其他人指出暫時性錯誤狀況。 您應該在延遲之後重試的 hello 後者。

<table style="font-size:12">
    <tr>
        <th>狀態碼</th>
        <th>意義</th>
        <th>可重試</th>
        <th>注意事項</th>
    </tr>
    <tr>
        <td>200</td>
        <td>已成功修改或刪除文件。</td>
        <td>n/a</td>
        <td>刪除作業為<a href="https://en.wikipedia.org/wiki/Idempotence">等冪</a>。 也就是說，即使文件索引鍵不存在於 hello 索引中，刪除作業嘗試以該金鑰會導致 200 狀態碼。</td>
    </tr>
    <tr>
        <td>201</td>
        <td>已成功建立文件。</td>
        <td>n/a</td>
        <td></td>
    </tr>
    <tr>
        <td>400</td>
        <td>導致無法進行索引的 hello 文件時發生錯誤。</td>
        <td>否</td>
        <td>hello 回應 hello 錯誤訊息將指出的錯誤與 hello 文件。</td>
    </tr>
    <tr>
        <td>404</td>
        <td>無法合併 hello 文件，因為 hello 給定索引鍵不存在於 hello 索引。</td>
        <td>否</td>
        <td>此錯誤不會發生於上傳，因為它們會建立新文件，並且不會發生於刪除，因為它們是<a href="https://en.wikipedia.org/wiki/Idempotence">等冪</a>。</td>
    </tr>
    <tr>
        <td>409</td>
        <td>嘗試 tooindex 文件時偵測到版本發生衝突。</td>
        <td>是</td>
        <td>當您考慮 tooindex hello 相同文件超過一次同時，也可能會發生。</td>
    </tr>
    <tr>
        <td>422</td>
        <td>hello 索引是暫時無法使用，因為它已更新與 hello 'allowIndexDowntime' 旗標集 too'true'。</td>
        <td>是</td>
        <td></td>
    </tr>
    <tr>
        <td>503</td>
        <td>您的搜尋服務是暫時無法使用，可能是因為 tooheavy 負載。</td>
        <td>是</td>
        <td>您的程式碼應等待重試一次在此情況下，或您可能會延長 hello 服務無法使用。</td>
    </tr>
</table> 

**請注意**： 如果您的用戶端程式碼經常發生 207 回應，一個可能的原因是 hello 系統是否承受負載。 您可以藉由檢查 hello 確認`statusCode`503 的屬性。 如果這是 hello 案例，我們建議您***節流索引要求***。 否則，如果索引的流量不會處理並減少，hello 系統可能會開始拒絕所有要求，出現 503 錯誤。

狀態碼 429 表示您已超過每個索引的文件的 hello 數目配額。 您必須建立新的索引，或進行升級以取得更高的容量限制。

**範例：**

    {
      "value": [
        {
          "@search.action": "upload",
          "hotelId": "1",
          "baseRate": 199.0,
          "description": "Best hotel in town",
          "description_fr": "Meilleur hôtel en ville",
          "hotelName": "Fancy Stay",
          "category": "Luxury",
          "tags": ["pool", "view", "wifi", "concierge"],
          "parkingIncluded": false,
          "smokingAllowed": false,
          "lastRenovationDate": "2010-06-27T00:00:00Z",
          "rating": 5,
          "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
          "@search.action": "upload",
          "hotelId": "2",
          "baseRate": 79.99,
          "description": "Cheapest hotel in town",
          "description_fr": "Hôtel le moins cher en ville",
          "hotelName": "Roach Motel",
          "category": "Budget",
          "tags": ["motel", "budget"],
          "parkingIncluded": true,
          "smokingAllowed": true,
          "lastRenovationDate": "1982-04-28T00:00:00Z",
          "rating": 1,
          "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a>搜尋文件
A**搜尋**作業發出為 GET 或 POST 要求，並指定參數，以提供選取相符文件的 hello 準則。

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**當 toouse 張貼而不是 GET**

當您使用 HTTP GET toocall hello**搜尋**API，您需要 toobe 注意 hello hello 要求 URL 長度不能超過 8 KB。 這對大部分的應用程式通常已足夠。 不過，有些應用程式會產生非常大型的查詢或 OData 篩選條件運算式。 對於這些應用程式而言，使用 HTTP POST 是較好的選擇，因為它允許比 GET 更大型的篩選與查詢。 使用 POST、 hello 條款或在查詢子句數目 hello 限制因素，不 hello 的 hello 原始查詢因為 POST hello 要求大小限制為大約 16 MB 的大小。

> [!NOTE]
> 即使 hello POST 要求的大小限制是非常大，搜尋查詢及篩選條件運算式不能任意複雜。 如需搜尋查詢和篩選複雜性限制的詳細資訊，請參閱 [Lucene 查詢語法](https://msdn.microsoft.com/library/mt589323.aspx)和 [OData 運算式語法](https://msdn.microsoft.com/library/dn798921.aspx)。
> 
> 

**要求**

服務要求需要使用 HTTPS。 hello**搜尋**要求可以使用 hello GET 或 POST 方法建構。

hello 要求 URI 中指定的索引 tooquery，符合 hello 參數的所有文件。 Hello hello 大小寫的 GET 要求中的查詢字串上指定參數，並在 hello 要求在 hello 情況下，使用 post 要求主體要求。

最佳作法是建立 GET 要求時，請記住太[要作 URL 編碼](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx)參數呼叫時直接 hello REST API 的特定查詢。 針對 **搜尋** 作業，這包括：

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

在上述查詢參數的 hello 只建議 URL 編碼。 如果您不小心 URL 編碼 hello 整個查詢字串 （所有項目之後 hello？），要求將會中斷。

此外，URL 編碼必要時才呼叫的 hello 直接使用 REST API 取得。 呼叫時，無編碼的 URL 是必要**搜尋**使用 POST，或在使用 hello [.NET 用戶端程式庫](https://msdn.microsoft.com/library/dn951165.aspx)，處理 URL 編碼方式。

<a name="SearchQueryParameters"></a>
**查詢參數**

**搜尋** 會接受數個可提供查詢準則以及指定搜尋行為的參數。 您提供這些 hello URL 中的參數呼叫時，查詢字串**搜尋**透過 GET，以及當呼叫 hello 要求主體中的 JSON 屬性**搜尋**透過 POST。 某些參數的 hello 語法是 GET 和 POST 之間稍有不同。 這些差異已適當在以下標示：

`search=[string]`（選用）-hello 文字 toosearch 的。 除非指定 `searchFields`，否則預設會搜尋所有的 `searchable` 欄位。 搜尋時`searchable`欄位，hello 搜尋文字本身會 token 化，因此可以由空白字元分隔多個詞彙 (例如： `search=hello world`)。 toomatch 任何詞彙中，使用`*`（這可以是布林值篩選查詢很有用）。 省略這個參數具有相同效果與將它設定太 hello`*`。 請參閱[簡單查詢語法](https://msdn.microsoft.com/library/dn798920.aspx)hello 搜尋語法的詳細資料。

* **請注意**: hello 結果有時會令人意外查詢整個`searchable`欄位。 hello tokenizer 邏輯 toohandle 案例常見 tooEnglish 中包括文字像是所有格符號、 逗號等數字。例如，`search=123,456`會比對單一字詞 123456，而不是 hello 個別字詞 123 與 456，因為逗號會做為千分位分隔符號的英文中大型數字。 基於這個理由，我們建議泛空白字元，而不是標點符號 tooseparate 詞彙在 hello`search`參數。

`searchMode=any|all`(選擇性，預設值太`any`)-是否為相符的順序 toocount hello 文件中，則必須符合任何或所有 hello 搜尋詞彙。

`searchFields=[string]`（選用）-指定文字的逗號分隔的欄位名稱 toosearch hello 清單。 目標欄位必須標記為 `searchable`。

`queryType=simple|full`(選擇性的預設值太`simple`)-時設定太 「 簡單的 」 的搜尋文字會解譯使用允許的符號，例如簡單的查詢語言 +、 * 及""。 預設會跨越每份文件中的所有可搜尋欄位 (或以 `searchFields`表示的欄位) 評估查詢。 Hello 查詢型別時設定太`full`搜尋的文字會解譯使用 hello 可讓特定的欄位和加權搜尋 Lucene 查詢語言。 請參閱[簡單查詢語法](https://msdn.microsoft.com/library/dn798920.aspx)和[Lucene 的查詢語法](https://msdn.microsoft.com/library/mt589323.aspx)上 hello 搜尋語法的詳細資料。 

> [!NOTE]
> 範圍 hello Lucene 改用 $filter 提供類似的功能不支援的查詢語言中的搜尋。
> 
> 

`moreLikeThis=[key]` (選用) **重要：**此功能僅適用於 `2015-02-28-Preview`。 這個選項不能包含 hello 文字搜尋參數，查詢中`search=[string]`。 hello`moreLikeThis`參數會尋找類似 hello 文件索引鍵所指定的 toohello 文件的文件。 當使用已搜尋要求`moreLikeThis`，根據 hello 頻率和罕見的 hello 來源文件中的條款所產生的搜尋詞彙清單。 這些詞彙會接著使用的 toomake hello 要求。 根據預設，hello 的所有內容`searchable`欄位視為除非`searchFields`是使用的 toorestrict 會搜尋的欄位。  

`$skip=#`（選用）-hello 數字的搜尋結果 tooskip;不能大於 100000 的。 如果您需要 tooscan 文件順序，但不能使用`$skip`到期 toothis 限制，請考慮使用`$orderby`完全排序索引鍵和`$filter`改為使用範圍查詢。

> [!NOTE]
> 使用 POST 呼叫**搜尋**時，此參數的名稱會是 `skip` 而不是 `$skip`。
> 
> 

`$top=#`（選用）-hello 數字的搜尋結果 tooretrieve。 這可以用於搭配`$skip`tooimplement 用戶端分頁搜尋結果。

> [!NOTE]
> 使用 POST 呼叫**搜尋**時，此參數的名稱會是 `top` 而不是 `$top`。
> 
> 

`$count=true|false`(選擇性，預設值太`false`)-指定是否 toofetch hello 結果的總計數。 這是符合 hello 的所有文件的 hello 計數`search`和`$filter`參數，忽略`$top`和`$skip`。 將此值設定為太`true`可能會造成效能影響。 請注意，傳回 hello 計數是近似值。

> [!NOTE]
> 使用 POST 呼叫**搜尋**時，此參數的名稱會是 `count` 而不是 `$count`。
> 
> 

`$orderby=[string]`（選用）-根據以逗號分隔的運算式 toosort hello 結果的清單。 每個運算式可以是欄位名稱，或是呼叫 toohello`geo.distance()`函式。 每個運算式後面可以接著`asc`tooindicated 遞增，和`desc`tooindicate 遞減。 hello 預設為遞增順序。 繫結將會 hello 文件相符分數所中斷。 如果沒有`$orderby`指定，則 hello 預設排序順序依照文件相符分數遞減。 針對 `$orderby`，有 32 個子句的限制。

> [!NOTE]
> 使用 POST 呼叫**搜尋**時，此參數的名稱會是 `orderby` 而不是 `$orderby`。
> 
> 

`$select=[string]`（選用）-tooretrieve 以逗號分隔欄位的清單。 如果未指定，會包含 標示為可擷取 hello 結構描述中的所有欄位。 您可以將這個參數設定為太，以同時也可以明確要求所有欄位`*`。

> [!NOTE]
> 使用 POST 呼叫**搜尋**時，此參數的名稱會是 `select` 而不是 `$select`。
> 
> 

`facet=[string]`（零或多個）-由欄位 toofacet。 Hello 字串可能會選擇性地包含以逗號分隔的參數 toocustomize hello faceting`name:value`組。 有效參數包括：

* `count` (Facet 字詞的最大數目；預設值為 10)。 沒有最大值，但較高的值會產生對應的 「 效能造成負面影響，特別是當 hello faceted 欄位包含大量的唯一字詞。
  * 例如：`facet=category,count:5`取得 hello facet 結果中的前五個類別。  
  * **請注意**： 如果 hello`count`參數小於唯一字詞數目 hello、 hello 結果可能不正確。 這是因為 faceting 查詢分散於分區 toohello 方式。 增加`count`通常會增加 hello 精確度 hello 字詞計數，但在效能成本。
* `sort`(其中`count`toosort*遞減*依計數， `-count` toosort*遞增*依計數， `value` toosort*遞增*值，或`-value` toosort*遞減*值)
  * 例如：`facet=category,count:3,sort:count`取得 hello facet 結果中的每個縣 （市） 名稱的文件的 hello 數目，依遞減順序的前三個類別。 例如，如果 hello 前三個類別為預算、 Motel 和 Luxury，和 Budget 有 5 個命中、 Motel 有 6 個，而 Luxury 有 4，則 hello 值區會 hello 順序 Motel、 預算、 Luxury。
  * 例如： `facet=rating,sort:-value` 會以依值的遞減排序方式，針對所有可能的評等來產生值區。 例如，如果 hello 評等是從 1 too5，hello 值區的排序是 5，4，3，2，1，不論是多少文件符合每個評等。
* `values` (直立線符號分隔的數字或 `Edm.DateTimeOffset` 值，可指定一組動態的多面向項目值)
  * 例如：`facet=baseRate,values:10|20`會產生三個值區： 一個用於基底費率 0 toobut 不包括 10，一個用於 10 向上 toobut 不包括 20，而另一個用於 20 或更高版本上。
  * 舉例來說：`facet=lastRenovationDate,values:2010-02-01T00:00:00Z` 會產生兩個值區：一個用於 2010 年 2 月之前重新整修的旅館，另一個則用於 2010 年 2 月 1 日以後重新整修的旅館。
* `interval` (如果是數字，整數間隔大於 0，如果是日期時間值，則為 `minute`、`hour`、`day`、`week`、`month`、`quarter` 或 `year`)
  * 例如：`facet=baseRate,interval:100` 會根據大小為 100 的基本匯率範圍來產生值區。 舉例來說，如果基本匯率全都介於 60 美元到 600 美元之間，則會有下列值區：0-100、100-200、200-300、300-400、400-500 及 500-600。
  * 例如：`facet=lastRenovationDate,interval:year` 會在旅館重新整修期間，每一年產生一個值區。
* `timeoffset` ([+-]hh:mm、[+-]hhmm 或 [+-]hh) `timeoffset` 為選用項目。 僅可以結合以 hello `interval`  選項，並且只有當類型套用的 tooa 欄位`Edm.DateTimeOffset`。 hello 值指定為 hello UTC 時間位移的 tooaccount 設定時間界限。
  * 例如：`facet=lastRenovationDate,interval:day,timeoffset:-01:00`使用 hello 01:00:00 utc （hello 目標時區的午夜） 開始的日界限
* **請注意**:`count`和`sort`可以結合在 hello 相同 facet 規格中，但它們無法與結合`interval`或`values`，和`interval`和`values`無法合併在一起。
* **注意**：如果未指定 `timeoffset`，日期時間上的間隔 Facet 就會根據 UTC 時間來計算。 例如： 針對`facet=lastRenovationDate,interval:day`，00:00:00 utc 開始 hello 天界限。 

> [!NOTE]
> 使用 POST 呼叫**搜尋**時，此參數的名稱會是 `facets` 而不是 `facet`。 此外，您會將它指定為字串的 JSON 陣列，其中每個字串是不同的 facet 運算式。
> 
> 

`$filter=[string]` (選用) - 使用標準 OData 語法的結構化搜尋運算式。

> [!NOTE]
> 使用 POST 呼叫**搜尋**時，此參數的名稱會是 `filter` 而不是 `$filter`。
> 
> 

`highlight=[string]` (選用) - 一組適用於點閱數醒目提示的逗號分隔欄位名稱。 只有 `searchable` 欄位可用於點閱數醒目提示。

`highlightPreTag=[string]`(選擇性，預設值太`<em>`)-字串前面加上 toohit 反白顯示的標記。 必須使用 `highlightPostTag`來設定。

> [!NOTE]
> 當呼叫**搜尋**使用 GET，hello URL 中的保留的字元必須是百分比編碼 （例如，%23 而不是 #）。
> 
> 

`highlightPostTag=[string]`(選擇性，預設值太`</em>`)-將附加 toohit 反白顯示的字串標記。 必須使用 `highlightPreTag`來設定。

> [!NOTE]
> 當呼叫**搜尋**使用 GET，hello URL 中的保留的字元必須是百分比編碼 （例如，%23 而不是 #）。
> 
> 

`scoringProfile=[string]`（選用）-計分設定檔 tooevaluate hello 名稱符合分數排序 toosort hello 結果中的比對文件。

`scoringParameter=[string]`（零或多個）-表示 hello 計分函式中定義的每個參數的值 (例如， `referencePointParameter`) 使用 hello 格式`name-value1,value2,...`。

* 例如，如果 hello 計分設定檔定義的函式參數，稱為"mylocation"hello 查詢字串選項會是`&scoringParameter=mylocation--122.2,44.8`。 hello 第一個虛線 hello 名稱與分隔 hello 值清單中，雖然 hello 第二個虛線是 hello 第一個值 （在此範例中的經度） 的一部分。
* 計分的參數如標記在提升，可包含逗號，您可以逸出任何這類值使用單引號 hello 清單中。 如果 hello 值本身包含單引號來逸出它們加倍。
  * 例如，如果您有提升稱為 「 mytag"參數標記，而您想 tooboost hello 標記上的值"Hello，O'Brien"和"Smith"，hello 查詢字串選項會是`&scoringParameter=mytag-'Hello, O''Brien',Smith`。 請注意，只有包含逗號的值需要引號。

> [!NOTE]
> 使用 POST 呼叫**搜尋**時，此參數的名稱會是 `scoringParameters` 而不是 `scoringParameter`。 此外，您需以 JSON 字串陣列方式指定它，其中每個字串都是個別的 `name-values` 組。
> 
> 

`minimumCoverage`（選擇性，預設 too100）-介於 0 和 100 指出 hello 百分比 hello 索引的搜尋查詢，為了讓 hello 查詢 toobe 必須涵蓋的報告為成功。 根據預設，hello 整個索引必須是可用或`Search`會傳回 HTTP 狀態碼 503。 如果您設定`minimumCoverage`和`Search`成功，則會傳回 HTTP 200，並包含`@search.coverage`hello 回應指出 hello 百分比 hello 索引 hello 查詢中所包含的值。

> [!NOTE]
> 設定此參數 tooa 值低於 100 非常適合用於確保搜尋即使對於服務的一個複本的可用性。 但是，並非所有的相符文件都保證 toobe hello 搜尋結果中。 如果搜尋重新叫用更重要的 tooyour 應用程式比可用性，則它是最佳 tooleave`minimumCoverage`在其預設值為 100。
> 
> 

`api-version=[string]` (必要)。 hello 預覽版本`api-version=2015-02-28-Preview`。 如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。

注意： 這項作業，hello`api-version`做為查詢參數，不論呼叫 hello URL 中指定**搜尋**具有 GET 或 POST。

**要求標頭**

hello 下列清單描述所需的 hello 和選擇性要求標頭。

* `api-key`: hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。 它是字串值，唯一 tooyour 服務 URL。 hello**搜尋**要求可以指定將管理金鑰或查詢索引鍵`api-key`。

您也需要 hello 服務名稱 tooconstruct hello 要求 URL。 您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。 請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。

**要求本文**

針對 GET：None。

針對 POST：

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

**接續部分搜尋回應**

有時 Azure 搜尋無法傳回所有 hello 單一搜尋回應中的要求的結果。 這可能是不同的原因，例如當 hello 查詢要求太多文件未指定`$top`或指定的值`$top`太大。 在這種情況下，Azure 搜尋會包含 hello`@odata.nextLink`在 hello 回應主體中，註解以及`@search.nextPageParameters`是否 POST 要求。 您可以使用這些註解 tooformulate hello 值搜尋要求 tooget hello 下一步的另一部分 hello 搜尋回應。 這稱為***接續***hello 原始搜尋要求和 hello 的註解通常稱為***接續 token***。 請參閱[hello 例會](#SearchResponse)如這些註解以及其中會顯示 hello 回應主體中的 hello 語法的詳細資訊。 

為什麼 Azure 搜尋可能會傳回接續 token 的 hello 原因是實作特定與主旨 toochange。 穩定的用戶端應該一律是準備 toohandle 案例，其中會傳回比預期較少的文件，而接續 token 是擷取文件包含的 toocontinue。 也請注意，您必須使用 hello 與 hello 原始要求順序 toocontinue 中相同的 HTTP 方法。 例如，如果您傳送 GET 要求，則您傳送的所有接續要求也必須使用 GET (同樣適用於 POST)。

<a name="SearchResponse"></a>
**回應**

回應成功時會傳回狀態碼：200 OK。

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

**範例：**

您可以在 hello 找到其他範例[Azure 搜尋的 OData 運算式語法](https://msdn.microsoft.com/library/azure/dn798921.aspx)頁面。

1)    搜尋 hello 依照日期遞減排序的索引。

    GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }

2)    在多面向搜尋中，搜尋 hello 索引並擷取 facet 類別、 評等、 標記，以及特定範圍中具有 baseRate 的項目：

    GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }

3)    Hello 使用者按下之後，使用篩選器，縮小先前多面向查詢結果 hello 評等 3 和分類"Motel":

    GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }

4) 在多面向搜尋中，為查詢中傳回的唯一字詞數目設定上限。 hello 預設值為 10，但您可以增加或減少此值使用 hello `count` hello 參數`facet`屬性：

    GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }

5)    搜尋特定的欄位; 中的 hello 索引例如，將語言特定欄位：

    GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }

6) 跨多個欄位搜尋 hello 索引。 例如，您可以儲存和查詢可搜尋的欄位，在多個語言中，全部都在 hello 相同的索引。  如果英文和法文描述共存於 hello 相同文件中，您可以傳回任何或所有在 hello 查詢結果：

    GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }

請注意，您一次只能查詢一個索引。 請勿建立針對每個語言的多個索引，除非您規劃 tooquery 一一次。

7)    分頁-取得 hello 第 1 頁的項目 （頁面大小為 10）：

    GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }

8)    分頁-取得 hello 第 2 頁的項目 （頁面大小為 10）：

    GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }

9)    抓取一組特定的欄位：

    GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }

10)  抓取符合特定篩選運算式的文件：

    GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }

11) 搜尋 hello 索引並傳回具有叫用會反白顯示片段

    GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }

12) 搜尋 hello 索引和從遠離的參考位置較接近 toofarther 排序傳回的文件

    GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }

13) 搜尋 hello 索引假設名為"currentlocation"的計分設定檔與兩個距離評分函數，一個定義的參數名"為 Lastlocation"和"Geo"的呼叫的參數

    GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }

14) 尋找文件以 hello 索引使用[簡單查詢語法](https://msdn.microsoft.com/library/dn798920.aspx)。 此查詢會傳回可搜尋的欄位位置包含 hello"comfort"和"location"但不是"motel"的旅館：

    GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }

請注意 hello 使用`searchMode=all`上方。 包含此參數會覆寫 hello 預設值是`searchMode=any`，確保可`-motel`表示"AND NOT"而不是"OR NOT"。 不含`searchMode=all`、 您得到"OR NOT"這會展開，而不是限制搜尋結果，這可能是違反直覺 toosome 使用者。

15) 尋找文件以 hello 索引使用[lucene 的查詢語法](https://msdn.microsoft.com/library/mt589323.aspx)。 此查詢會傳回的旅館其中 hello category 欄位包含 hello 詞彙"budget"和"最近整修"hello 片語的所有可搜尋欄位。 包含 「 最近整修"hello 片語的文件是次序比它高 hello 詞彙增量值 (3) 的結果

    GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }

<a name="LookupAPI"></a>

## <a name="lookup-document"></a>查閱文件
hello**查閱文件**作業會從 Azure 搜尋擷取文件。 使用者按一下特定的搜尋結果，而且您想 toolook 該文件的相關特定詳細資料時，這非常有用。

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

**要求**

服務要求需要使用 HTTPS。 hello**查閱文件**要求可以下列方式建構。

    GET /indexes/[index name]/docs/key?[query parameters]

或者，您可以使用 hello 傳統的 OData 語法進行索引鍵查閱：

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

hello 要求 URI 包含 [索引名稱] 和 [索引鍵]，指定從哪個索引的文件 tooretrieve。 您一次只能取得一份文件。 使用**搜尋**tooget 單一要求中的多個文件。

**查詢參數**

`$select=[string]`（選用）-tooretrieve 以逗號分隔欄位的清單。 如果未指定或設定得`*`，hello 投影中包含標示為可擷取 hello 結構描述中的所有欄位。

`api-version=[string]` (必要)。 hello 預覽版本`api-version=2015-02-28-Preview`。 如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。

注意： 這項作業，hello`api-version`指定為查詢參數。

**要求標頭**

hello 下列清單描述所需的 hello 和選擇性要求標頭。

* `api-key`: hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。 它是字串值，唯一 tooyour 服務 URL。 hello**查閱文件**要求可以指定將管理金鑰或查詢索引鍵`api-key`。

您也需要 hello 服務名稱 tooconstruct hello 要求 URL。 您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。 請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。

**要求本文**

無。

**回應**

回應成功時會傳回狀態碼：200 OK。

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

**範例**

具有索引鍵 '2' 的查閱 hello 文件

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

具有索引鍵 '3' 使用 OData 語法查閱 hello 文件：

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a>文件計數
hello**計算文件**作業會擷取搜尋索引文件的 hello 數目的計數。 hello`$count`語法是 hello OData 通訊協定的一部分。

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

**要求**

服務要求需要使用 HTTPS。 hello**計算文件**要求可以使用 hello GET 方法建構。

hello 要求 URI 中的 hello [索引名稱] 會告知 hello 服務 tooreturn 所有項目計數 hello 文件集合中的 hello 指定的索引。

`api-version=[string]` (必要)。 hello 預覽版本`api-version=2015-02-28-Preview`。 如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。

**要求標頭**

hello 下列清單描述所需的 hello 和選擇性要求標頭。

* `Accept`： 這個值必須設定太`text/plain`。
* `api-key`: hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。 它是字串值，唯一 tooyour 服務 URL。 hello**計算文件**要求可以指定將管理金鑰或查詢索引鍵`api-key`。

您也需要 hello 服務名稱 tooconstruct hello 要求 URL。 您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。 請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。

**要求本文**

無。

**回應**

回應成功時會傳回狀態碼：200 OK。

hello 回應主體會包含 hello 計數值為純文字格式的整數。

<a name="Suggestions"></a>

## <a name="suggestions"></a>建議
hello**建議**作業會擷取部分搜尋輸入為基礎的建議。 它通常用於搜尋方塊 tooprovide 預先輸入建議在使用者輸入搜尋詞彙。

建議要求以建議目標文件為目標，因此 hello 建議可能重複文字，是否多個候選文件符合 hello 相同搜尋輸入。 您可以使用`$select`tooretrieve 其他文件欄位 （包括 hello 文件索引鍵），以便您可以分辨哪份文件是一項建議的 hello 來源。

**建議** 作業會以 GET 或 POST 要求發出。

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**當 toouse 張貼而不是 GET**

當您使用 HTTP GET toocall hello**建議**API，您需要 toobe 注意 hello hello 要求 URL 長度不能超過 8 KB。 這對大部分的應用程式通常已足夠。 不過，有些應用程式會產生非常大型的查詢，特別是 OData 篩選條件運算式。 對於這些應用程式而言，使用 HTTP POST 是較好的選擇，因為它允許比 GET 更大型的篩選。 使用 post 要求在篩選子句的 hello 數目是 hello 限制因素，不 hello hello 未經處理的篩選字串的大小，因為 POST hello 要求大小限制為大約 16 MB。

> [!NOTE]
> 即使 hello POST 要求的大小限制是非常大，不能任意複雜的篩選條件運算式。 如需有關篩選複雜性限制的詳細資訊，請參閱 [OData 運算式語法](https://msdn.microsoft.com/library/dn798921.aspx) 。
> 
> 

**要求**

服務要求需要使用 HTTPS。 hello**建議**要求可以使用 hello GET 或 POST 方法建構。

hello 要求 URI 會指定 hello 索引 tooquery hello 名稱。 Hello hello 大小寫的 GET 要求中的查詢字串中指定參數，例如 hello 部分輸入的搜尋詞彙，並在 hello 要求在 hello 情況下，使用 post 要求主體要求。

最佳作法是建立 GET 要求時，請記住太[要作 URL 編碼](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx)參數呼叫時直接 hello REST API 的特定查詢。 針對 **建議** 作業，這包括：

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

在上述查詢參數的 hello 只建議 URL 編碼。 如果您不小心 URL 編碼 hello 整個查詢字串 （所有項目之後 hello？），要求將會中斷。

此外，URL 編碼必要時才呼叫的 hello 直接使用 REST API 取得。 呼叫時，無編碼的 URL 是必要**建議**使用 POST，或在使用 hello [.NET 用戶端程式庫](https://msdn.microsoft.com/library/dn951165.aspx)，處理 URL 編碼方式。

**查詢參數**

**建議** 會接受數個可提供查詢準則以及指定搜尋行為的參數。 您提供這些 hello URL 中的參數呼叫時，查詢字串**建議**透過 GET，以及當呼叫 hello 要求主體中的 JSON 屬性**建議**透過 POST。 某些參數的 hello 語法是 GET 和 POST 之間稍有不同。 這些差異已適當在以下標示：

`search=[string]`-hello 搜尋文字 toouse toosuggest 查詢。 必須至少 1 個字元，而且不能多於 100 個字元。

`highlightPreTag=[string]`（選用）-toosearch 命中結果前面加上字串標記。 必須使用 `highlightPostTag`來設定。

> [!NOTE]
> 當呼叫**建議**使用 GET，hello URL 中的保留的字元必須是百分比編碼 （例如，%23 而不是 #）。
> 
> 

`highlightPostTag=[string]`（選用）-將附加 toosearch 叫用的字串標記。 必須使用 `highlightPreTag`來設定。

> [!NOTE]
> 當呼叫**建議**使用 GET，hello URL 中的保留的字元必須是百分比編碼 （例如，%23 而不是 #）。
> 
> 

`suggesterName=[string]`-hello 中所指定的 hello 與 hello 建議工具名稱`suggesters`屬於 hello 索引定義的集合。 `suggester` 會判斷要針對建議的查詢字詞掃描哪些欄位。 如需詳細資訊，請參閱 [建議工具](#Suggesters) 。

`fuzzy=[boolean]`(選擇性，預設值 = false)-當設定 tootrue API 也會尋找建議，即使在 hello 搜尋文字取代或遺失的字元。 儘管這在某些案例中可提供較佳的體驗，但它也需要付出效能成本代價，因為模糊建議搜尋的速度較慢且耗用更多資源。

`searchFields=[string]`（選用）-指定搜尋文字的逗號分隔的欄位名稱 toosearch hello 清單。 您必須啟用目標欄位才能提供建議。

`$top=#`(選擇性，預設值 = 5)-hello 建議 tooretrieve 數目。 必須是 1 到 100 之間的數字。

> [!NOTE]
> 使用 POST 呼叫**建議**時，此參數的名稱是 `top` 而不是 `$top`。
> 
> 

`$filter=[string]`（選用）-篩選 hello 文件的運算式被視為建議。

> [!NOTE]
> 使用 POST 呼叫**建議**時，此參數的名稱是 `filter` 而不是 `$filter`。
> 
> 

`$orderby=[string]`（選用）-根據以逗號分隔的運算式 toosort hello 結果的清單。 每個運算式可以是欄位名稱，或是呼叫 toohello`geo.distance()`函式。 每個運算式後面可以接著`asc`tooindicated 遞增，和`desc`tooindicate 遞減。 hello 預設為遞增順序。 針對 `$orderby`，有 32 個子句的限制。

> [!NOTE]
> 使用 POST 呼叫**建議**時，此參數的名稱是 `orderby` 而不是 `$orderby`。
> 
> 

`$select=[string]`（選用）-tooretrieve 以逗號分隔欄位的清單。 如果未指定，只有 hello 文件索引鍵，並傳回建議的文字。 將這個參數設定過，您可以明確要求所有欄位`*`。

> [!NOTE]
> 使用 POST 呼叫**建議**時，此參數的名稱是 `select` 而不是 `$select`。
> 
> 

`minimumCoverage`（選擇性，預設 too80）-介於 0 和 100 指出 hello 百分比 hello 索引順序 hello 查詢 toobe 建議查詢必須涵蓋的報告為成功。 根據預設，在至少 80%的 hello 索引必須是可用或`Suggest`會傳回 HTTP 狀態碼 503。 如果您設定`minimumCoverage`和`Suggest`成功，則會傳回 HTTP 200，並包含`@search.coverage`hello 回應指出 hello 百分比 hello 索引 hello 查詢中所包含的值。

> [!NOTE]
> 設定此參數 tooa 值低於 100 非常適合用於確保搜尋即使對於服務的一個複本的可用性。 但是，並非所有相符的建議都保證 toobe hello 結果中。 如果重新叫用是更重要的 tooyour 應用程式可用性，則最不 toolower 比`minimumCoverage`下方其預設值 80。
> 
> 

`api-version=[string]` (必要)。 hello 預覽版本`api-version=2015-02-28-Preview`。 如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。

注意： 這項作業，hello`api-version`做為查詢參數，不論呼叫 hello URL 中指定**建議**具有 GET 或 POST。

**要求標頭**

hello 下列清單描述所需的 hello 和選擇性要求標頭

* `api-key`: hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。 它是字串值，唯一 tooyour 服務 URL。 hello**建議**要求可以指定將管理金鑰或查詢索引鍵為 hello `api-key`。

您也需要 hello 服務名稱 tooconstruct hello 要求 URL。 您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。 請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。

**要求本文**

針對 GET：None。

針對 POST：

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

**回應**

回應成功時會傳回狀態碼：200 OK。

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

如果 hello 投影選項是使用的 tooretrieve 欄位在 hello 陣列的每個項目包括：

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

**範例**

擷取其中 hello 部分搜尋輸入是 'lux' 的 5 個建議

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
