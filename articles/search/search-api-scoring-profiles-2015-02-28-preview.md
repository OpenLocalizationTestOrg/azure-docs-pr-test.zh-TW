---
title: "評分設定檔 (Azure 搜尋服務 REST API 2015-02-28-Preview 版) | Microsoft Docs"
description: "Azure 搜尋服務是託管的雲端搜尋服務，且支援根據使用者定義的評分設定檔調整排名結果。"
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: bfd62649-13d7-40b3-a8fa-85521a15084d
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.author: heidist
ms.date: 10/27/2016
ms.openlocfilehash: a67637d149a84313270c03d21acf8a9c1870be05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="scoring-profiles-azure-search-rest-api-version-2015-02-28-preview"></a>評分設定檔 (Azure 搜尋服務 REST API 2015-02-28-Preview 版)
> [!NOTE]
> 本文說明 [2015-02-28-Preview](search-api-2015-02-28-preview.md)的評分設定檔。 記載於 [MSDN](http://msdn.microsoft.com/library/azure/mt183328.aspx) 的 `2016-09-01` 版本和此處描述的 `2015-02-28-Preview` 版本，目前並無差別，不過為使文件內容完整涵蓋 API，我們仍提供此文件。
>
>

## <a name="overview"></a>Overview
計分是指對搜尋結果中傳回的每個項目所做的搜尋分數計算。 分數是某個項目在目前搜尋作業的內容中有何相關性的指標。 分數越高，該項目的相關性就愈高。 在搜尋結果中，項目會根據為每個項目計算的搜尋分數由高至低排序。

Azure 搜尋服務會使用預設計分來計算分數，但您可以透過評分設定檔自訂計算方式。 評分設定檔可讓您更佳地控制搜尋結果中的項目排名。 舉例來說，您可能想根據營收潛力提升某些項目、亦或是提升新項目或庫存過久的項目。

評分設定檔是索引定義的一部分，由欄位、函數和參數組成。

為了讓您對評分設定檔的外觀有所認識，下列範例會顯示名為 'geo' 的簡易設定檔。 此評分設定檔，會提升有搜尋詞彙在 `hotelName` 欄位的項目。 其也會使用 `distance` 函數，優先列出與目前的位置相距十公里以內的項目。 如果有人搜尋 'inn' 一詞，而 'inn' 剛好是飯店名稱的一部分，則文件中只要包含具有 'inn' 的飯店，就會出現在搜尋結果中的較高位置。

    "scoringProfiles": [
      {
        "name": "geo",
        "text": {
          "weights": { "hotelName": 5 }
        },
        "functions": [
          {
            "type": "distance",
            "boost": 5,
            "fieldName": "location",
            "interpolation": "logarithmic",
            "distance": {
              "referencePointParameter": "currentLocation",
              "boostingDistance": 10
            }
          }
        ]
      }
    ]

若要使用此評分設定檔，您的查詢會依公式調整以指定查詢字串的設定檔。 在下列查詢中，請留意要求中的查詢參數 `scoringProfile=geo` 。

    GET /indexes/hotels/docs?search=inn&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&api-version=2015-02-28-Preview

此查詢會搜尋 'inn' 一詞，並傳入目前的位置。 請注意這個查詢包括其他的參數，例如 `scoringParameter`。 查詢參數說明於 [搜尋文件 (Azure 搜尋服務 API)](search-api-2015-02-28-preview.md#SearchDocs)中。

按一下 [範例](#example) ，可檢閱更多評分設定檔的詳細範例。

## <a name="what-is-default-scoring"></a>什麼是預設計分？
計分會計算排名排序的結果集中每個項目的搜尋分數。 搜尋結果集中的每個項目會被指派一個搜尋分數，然後從最高排名到最低。 具有較高分數的項目會傳回給應用程式。 依預設會傳回前 50 名，但您可以使用 `$top` 參數，以傳回較少或更多的項目數目 (單一回應中最多 1000 個)。

根據預設，搜尋分數會根據資料和查詢的統計屬性來計算。 Azure 搜尋服務會尋找包含查詢字串中的搜尋詞彙的文件 (部分或全部，視 `searchMode`而定)，優先列出包含多個搜尋詞彙執行個體的文件。 如果詞彙在資料主體間很少見，但在文件中很常見，搜尋分數會更高。 這種計算相關性的方法基礎稱為 TF-IDF 或 (term frequency-inverse document frequency)。

假設沒有任何自訂排序，結果會先依搜尋分數排名，再傳回給呼叫的應用程式。 若未指定 `$top` ，則會傳回具有最高搜尋分數的 50 個項目。

搜尋分數值可以在整個結果集內重複。 例如，您可以有 10 個項目的分數為 1.2、20 個項目的分數為 1.0，20 個項目的分數為 0.5。 有多個命中具有相同的搜尋分數時，分數相同的項目並未定義順序，因此順序是不穩定的。 若再次執行查詢，您可能會發現項目的位置有所更換。 若有兩個項目的分數完全相同，則無法保證哪個項目先出現。

## <a name="when-to-use-custom-scoring"></a>使用自訂計分的時機
當預設排名行為不足以因應您的商業目標時，您應建立一或多個評分設定檔。 例如，您可以決定讓新增的項目具有較高的搜尋相關性。 同樣地，您可以讓某個欄位包含毛利率，或讓其他欄位指出潛在營收。 提高為企業帶來利益的命中率，是決定使用評分設定檔時的重要因素。

此外也會透過評分設定檔實作以相關性為基礎的排序。 請考量您過去曾經使用、讓您依價格、日期、評等或相關性排序的搜尋結果頁面。 在 Azure 搜尋服務中，評分設定檔會啟用「相關性」選項。 相關性的定義由您控制，取決於商業目標和您要提供的搜尋經驗類型。

<a name="example"></a>

## <a name="example"></a>範例
如前所述，自訂計分是透過索引結構描述中定義的一或多個評分設定檔而實作的。

此範例說明具有兩個評分設定檔 (`boostGenre`、`newAndHighlyRated`) 的索引結構描述。 任何以其中一個設定檔做為查詢參數而對此索引所做的查詢，都將使用該設定檔為結果集評分。

    {
      "name": "musicstoreindex",
      "fields": [
        { "name": "key", "type": "Edm.String", "key": true },
        { "name": "albumTitle", "type": "Edm.String" },
        { "name": "albumUrl", "type": "Edm.String", "filterable": false },
        { "name": "genre", "type": "Edm.String" },
        { "name": "genreDescription", "type": "Edm.String", "filterable": false },
        { "name": "artistName", "type": "Edm.String" },
        { "name": "orderableOnline", "type": "Edm.Boolean" },
        { "name": "rating", "type": "Edm.Int32" },
        { "name": "tags", "type": "Collection(Edm.String)" },
        { "name": "price", "type": "Edm.Double", "filterable": false },
        { "name": "margin", "type": "Edm.Int32", "retrievable": false },
        { "name": "inventory", "type": "Edm.Int32" },
        { "name": "lastUpdated", "type": "Edm.DateTimeOffset" }
      ],
      "scoringProfiles": [
        {
          "name": "boostGenre",
          "text": {
            "weights": {
              "albumTitle": 1.5,
              "genre": 5,
              "artistName": 2
            }
          }
        },
        {
          "name": "newAndHighlyRated",
          "functions": [
            {
              "type": "freshness",
              "fieldName": "lastUpdated",
              "boost": 10,
              "interpolation": "quadratic",
              "freshness": {
                "boostingDuration": "P365D"
              }
            },
            {
              "type": "magnitude",
              "fieldName": "rating",
              "boost": 10,
              "interpolation": "linear",
              "magnitude": {
                "boostingRangeStart": 1,
                "boostingRangeEnd": 5,
                "constantBoostBeyondRange": false
              }
            }
          ]
        }
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["albumTitle", "artistName"]
        }
      ]
    }


## <a name="workflow"></a>工作流程
若要實作自訂的計分行為，請將評分設定檔新增至定義索引的結構描述。 一個索引內最多可以有 16 個評分設定檔 (請參閱[服務限制](search-limits-quotas-capacity.md))，但在任何特定查詢中您一次只能指定一個設定檔。

請從本主題所提供的 [範本](#bkmk_template) 開始作業。

提供名稱。 評分設定檔是選用的，但如果您新增了設定檔，就必須提供名稱。 請務必遵循欄位的命名慣例 (以字母開頭，避免使用特殊字元和保留文字)。 請參閱 [命名規則 (Azure 搜尋)](http://msdn.microsoft.com/library/azure/dn857353.aspx) 以了解更多資訊。

評分設定檔的主體是從加權欄位和函數建構的。

### <a name="weights"></a>Weights
評分設定檔的 `weights` 屬性指定將相對權數指派給欄位的名稱值組。 在 [範例](#example)中，albumTitle、內容類型和 artistName 欄位分別會提升 1.5、5 和 2。 為何內容類型提升的程度遠比其他多？ 如果是對帶有同質性的資料進行搜尋 (如同 `musicstoreindex`中的 ’genre')，則相對加權可能需要較大的變異數。 例如，在 `musicstoreindex`中，'rock' 不僅以內容類型的形式出現，也出現在相同措詞的內容類型說明中。 如果您要讓類型的權數高於類型說明，則類型欄位需要更高的相對權數。

### <a name="functions"></a>Functions
函數是在特定內容需要額外計算時使用。 有效的函數類型 `freshness`、`magnitude`、`distance` 和 `tag`。 每個函數都有對其唯一的參數。

* `freshness` 。 此函數僅適用於 datetime 欄位 (`Edm.DataTimeOffset`)。 請注意， `boostingDuration` 屬性只能用於有效函數。
* `magnitude` 。 呼叫此函數的案例，包含依毛利率、最高價格、最低價格或下載次數進行提升。 若您想要反轉高至低的模式 (例如，比高價格項目更提升低價格的項目)，則可將範圍反轉。 假設價格範圍為 $100 美元到 $1 美元，您會將 `boostingRangeStart` 設定為 100，並將 `boostingRangeEnd` 設定為 1，以在較低的價格項目提升。 此函數僅可用於雙精度浮點數和整數欄位。
* `distance` 。 此函數僅適用於 `Edm.GeographyPoint` 欄位。
* `tag` 。 此函數僅適用於 `Edm.String` 和 `Collection(Edm.String)` 欄位。

#### <a name="rules-for-using-functions"></a>使用函數的規則
* 函數類型 (freshness、magnitude、distance、tag) 必須是小寫。
* 函數不可包含 null 或空值。 明確而言，如果您包含欄位名稱，則必須加以設定。
* 函數只能套用至可篩選的欄位。 請參閱[建立索引](search-api-2015-02-28-preview.md#CreateIndex)以了解更多有關可篩選欄位的相關資訊。
* 函數只能套用至索引的欄位集合中定義的欄位。

索引定義之後，請上傳索引結構描述 (接著上傳文件)，以建置索引。 如需這些操作的指示，請參閱[建立索引](search-api-2015-02-28-preview.md#CreateIndex)和[新增或更新文件](search-api-2015-02-28-preview.md#AddOrUpdateDocuments)。 索引建置後，您應會有可運作的評分設定檔可處理您的搜尋資料。

<a name="bkmk_template"></a>

## <a name="template"></a>範本
本節說明評分設定檔的語法與範本。 如需屬性的說明，請參閱下一節中的 [索引屬性參考](#bkmk_indexref) 。

    ...
    "scoringProfiles": [
      {
        "name": "name of scoring profile",
        "text": (optional, only applies to searchable fields) {
          "weights": {
            "searchable_field_name": relative_weight_value (positive #'s),
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
            }

            // (- or -)

            "freshness": {
              "boostingDuration": "..." (value representing timespan over which boosting occurs)
            }

            // (- or -)

            "distance": {
              "referencePointParameter": "...", (parameter to be passed in queries to use as reference location)
              "boostingDistance": # (the distance in kilometers from the reference location where the boosting range ends)
            }

            // (- or -)

            "tag": {
              "tagsParameter": "..." (parameter to be passed in queries to specify list of tags to compare against target field)
            }
          }
        ],
        "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
      }
    ],
    "defaultScoringProfile": (optional) "...",
    ...

<a name="bkmk_indexref"></a>

## <a name="scoring-profile-property-reference"></a>評分設定檔屬性參考
> [!NOTE]
> 評分函式只能套用至可篩選的欄位。
>
>

| 屬性 | 說明 |
| --- | --- |
| `name` |必要。 這是評分設定檔的名稱。 它會遵循欄位的相同命名慣例。 它必須以字母開頭，且不可包含點、冒號或 @ 符號，而且開頭不可以是片語 'azureSearch' (區分大小寫)。 |
| `text` |包含「權數」屬性。 |
| `weights` |選用。 指定欄位名稱和相對權數的名稱值組。 相對權數必須是正整數或浮點數。 您可以指定不含對應權數的欄位名稱。 權數可用來指出某欄位相對於其他欄位的重要性。 |
| `functions` |選用。 請注意，計分函數只能套用至可篩選的欄位。 |
| `type` |計分函數的必要項目。 指出要使用的函數類型。 有效值包括 `magnitude`、`freshness`、`distance` 和 `tag`。 您可以在每個評分設定檔中包含多個函數。 函數名稱必須是小寫。 |
| `boost` |計分函數的必要項目。 做為原始分數之乘數的正數。 此值不可等於 1。 |
| `fieldName` |計分函數的必要項目。 計分函數只能套用至屬於索引的欄位集合、並且可篩選的欄位。 此外，每個函數類型都有額外的限制 (有效性與日期時間欄位搭配使用，量級與整數或雙精確度浮點數欄位搭配，距離與位置欄位搭配，標記與字串或字串集合欄位搭配)。 每個函數定義只能指定一個欄位。 例如，若要在相同的設定檔中使用量級兩次，您必須包含兩個定義量級，每個欄位各一個。 |
| `interpolation` |計分函數的必要項目。 定義從範圍開始到範圍結束提升分數的增加斜率。 有效值包括 `linear` (預設值)、`constant`、`quadratic` 和 `logarithmic`。 如需詳細資訊，請參閱 [設定內插補點](#bkmk_interpolation) 。 |
| `magnitude` |量級計分函數可用來根據數值欄位的值範圍改變排名。 最常見的使用範例包括：<ul><li>星級評等：根據「星級評等」欄位內的值改變計分。 當兩個項目相關時，會先顯示具有更高評等的項目。</li><li>利潤：當兩份文件相關時，零售商可能會想要先提升具有較高利潤的文件。</li><li>點擊數：如果應用程式會追蹤對產品或頁面的點擊動作，您可以使用量級來提升可能獲得最多流量的項目。</li><li>下載計數：對於追蹤下載情形的應用程式，量級函數可讓您提升下載次數最多的項目。</li></ul> |
| `magnitude:boostingRangeStart` |設定計算量級分數之範圍的起始值。 此值必須是整數或浮點數。 就 1 到 4 的星級評等而言，這會是 1。 就超過 50% 的利潤而言，這會是 50。 |
| `magnitude:boostingRangeEnd` |設定計算量級分數之範圍的結束值。 此值必須是整數或浮點數。 就 1 到 4 的星級評等而言，這會是 4。 |
| `magnitude:constantBoostBeyondRange` |有效值為 true 或 false (預設值)。 設為 true 時，完整提升仍會繼續套用至目標欄位的值高於範圍上限的文件。 如果為 false，則此函數的提升將不會套用至目標欄位的值超出範圍的文件。 |
| `freshness` |有效性計分函數可用來根據 DateTimeOffset 欄位中的值改變項目的排名分數。 例如，日期較近的項目可排在較舊項目之前。 (請注意，也可能會對像是具有未來日期的行事曆事件的項目進行排名，因此，越接近目前日期的項目排名會高於未來日期較遠的項目。)在目前的服務版本中，範圍的其中一端會固定為目前的時間。 另一端則是以 `boostingDuration`為依據的過去時間。 若要提升未來的某個時間範圍，請使用負數的 `boostingDuration`。 從最大與最小範圍變更的提升比率，取決於套用至評分設定檔的插補 (請參閱下圖)。 若要反轉套用的提升係數，請選擇小於 1 的提升係數。 |
| `freshness:boostingDuration` |設定要開始停止對特定文件進行提升的到期時間。 如需語法和範例，請參閱下一節中的[設定 boostingDuration](#bkmk_boostdur)。 |
| `distance` |距離計分函數可用來根據文件與參考地理位置的距離，對文件的分數產生影響。 參考位置會以 lon,lat 引數的形式，指定為參數中查詢的一部分 (使用 `scoringParameter` 查詢參數)。 |
| `distance:referencePointParameter` |傳入查詢中做為參考位置的參數。 scoringParameter 是查詢參數。 如需查詢參數的說明，請參閱 [搜尋文件](search-api-2015-02-28-preview.md#SearchDocs) 。 |
| `distance:boostingDistance` |以公里為單位，設定與提升範圍結束處的參考位置相隔的距離。 |
| `tag` |標記計分函數可用來根據文件和搜尋查詢中的標記，對文件的分數產生影響。 將會提升擁有與搜尋查詢共通之標記的文件。 搜尋查詢的標記是以每個搜尋要求中的計分參數形式提供 (使用 `scoringParameter` 查詢參數)。 |
| `tag:tagsParameter` |傳入查詢中用來指定特定要求之標記的參數。 `scoringParameter` 是查詢參數。 如需查詢參數的說明，請參閱 [搜尋文件](search-api-2015-02-28-preview.md#SearchDocs) 。 |
| `functionAggregation` |選用。 只有在已指定函數時才會套用。 有效值包括：`sum` (預設值)、`average`、`minimum`、`maximum` 和 `firstMatching`。 搜尋分數是從多個變數 (包含多個函數) 計算的單一值。 此屬性可指出所有函數如何結合為後續會套用至基準文件分數的單一彙總提升。 基準分數的基礎是從文件和搜尋查詢計算出來的 tf-idf 值。 |
| `defaultScoringProfile` |執行搜尋要求時如果未指定評分設定檔，則會使用預設計分 (僅使用 tf-idf)。 預設的評分設定檔名稱可在此處設定，使 Azure 搜尋服務在搜尋要求中未指定特定的設定檔時使用該設定檔。 |

<a name="bkmk_interpolation"></a>

## <a name="set-interpolations"></a>設定內插補點
內插補點可讓您定義從範圍開始到範圍結束提升分數的增加斜率。 可用的內插補點如下：

* `Linear`：對於在最大和最小範圍內的項目，套用至項目的提升將會已持續遞減的量執行。 線性是評分設定檔的預設插補。
* `Constant`：對於在開始和結束範圍內的項目，將會對排名結果套用常數提升。
* `Quadratic`：相較於採用持續遞減提升的線性插補，二次方程式一開始會以較小的步調減少，等到接近結束範圍時，再以較大的間隔減少。 標記計分函數中不允許此插補選項。
* `Logarithmic`：相較於採用持續遞減提升的線性插補，對數一開始會以較大的步調減少，等到接近結束範圍時，再以較小的間隔減少。 標記計分函數中不允許此插補選項。

<a name="Figure1"></a> ![][1]

<a name="bkmk_boostdur"></a>

## <a name="set-boostingduration"></a>設定 boostingDuration
`boostingDuration` 是 freshness 函數的屬性。 您可以用它來設定要開始停止對特定文件進行提升的到期時間。 例如，若要在為期 10 天的促銷期間提升某個產品系列或品牌，您可以為這些文件指定 10 天的期間 "P10D"。 或者，若要提升下一週即將發生的事件，請指定 "-P7D"。

`boostingDuration` 必須格式化為 XSD "dayTimeDuration" 值 (ISO 8601 持續時間值的限定子集)。 間隔的模式為： `[-]P[nD][T[nH][nM][nS]]`。

下表提供數個範例。

| 持續時間 | boostingDuration |
| --- | --- |
| 1 天 |"P1D" |
| 2 天又 12 個小時 |"P2DT12H" |
| 15 Minuten |"PT15M" |
| 30 天 5 小時 10 分鐘又 6.334 秒 |"P30DT5H10M6.334S" |

如需更多範例，請參閱 [XML 結構描述：資料類型 (W3.org 網站)](http://www.w3.org/TR/xmlschema11-2/)。

**另請參閱 MSDN 上的** 
[Azure 搜尋服務 REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) <br/>MSDN 上的 
[建立索引 (Azure 搜尋服務 API)](http://msdn.microsoft.com/library/azure/dn798941.aspx)<br/>MSDN 上的 
[將評分設定檔新增至搜尋索引](http://msdn.microsoft.com/library/azure/dn798928.aspx)<br/>

<!--Image references-->
[1]: ./media/search-api-scoring-profiles-2015-02-28-Preview/scoring_interpolations.png
