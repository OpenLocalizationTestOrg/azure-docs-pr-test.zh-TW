---
title: "aaaScoring 設定檔 （Azure 搜尋 REST API 版本 2015年-02-28-預覽） |Microsoft 文件"
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
ms.openlocfilehash: 17f83fdf6818dc6ffcc3e04f5d0185c6f646b63d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scoring-profiles-azure-search-rest-api-version-2015-02-28-preview"></a>評分設定檔 (Azure 搜尋服務 REST API 2015-02-28-Preview 版)
> [!NOTE]
> 本文說明計分設定檔中 hello [2015年-02-28-preview](search-api-2015-02-28-preview.md)。 目前沒有任何差異 hello`2016-09-01`版本上記載[MSDN](http://msdn.microsoft.com/library/azure/mt183328.aspx)和 hello`2015-02-28-Preview`此處描述的版本，但我們提供此文件還是順序 tooprovide 文件涵蓋範圍中跨 hello整個應用程式開發介面。
>
>

## <a name="overview"></a>概觀
計分是指 toohello 計算的搜尋分數，每個項目的搜尋結果中傳回。 hello 分數是 hello 內容 hello 目前的搜尋操作中的項目相關的指標。 hello hello 分數越高，更有相關性的 hello hello 項目。 在搜尋結果中，項目是從高 toolow，根據為每個項目計算的 hello 搜尋分數排序次序。

Azure 搜尋會使用預設計分 toocompute 初始分數，但您可以自訂 hello 計算透過計分設定檔。 計分設定檔可讓您更掌控 hello 排名項目的搜尋結果中。 比方說，您可能會想根據其潛在營收的 tooboost 項目，升級較新的項目，或是可能是提升庫存過久過的項目。

計分設定檔是 hello 索引定義中，組成欄位、 函數和參數的一部分。

toogive 您了解什麼計分設定檔看起來像 hello 下列範例顯示簡單的設定檔命名為 'geo'。 這個功能可以大幅的項目 hello 搜尋詞彙在 hello`hotelName`欄位。 它也會使用 hello`distance`函式的 hello 目前的位置相距十公里以內的 toofavor 項目。 如果有人搜尋 hello 詞彙 'inn'，'inn' 剛好 toobe hello 飯店名稱的一部分，包含具有 'inn' 的文件會出現在 hello 搜尋結果中較高。

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

這個計分設定檔，您的查詢是的 toouse 構成 hello 查詢字串上的 toospecify hello 設定檔。 在下列 hello 查詢，請注意 hello 查詢參數， `scoringProfile=geo` hello 要求中。

    GET /indexes/hotels/docs?search=inn&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&api-version=2015-02-28-Preview

此查詢會搜尋 hello 詞彙 'inn'，並傳入 hello 目前的位置。 請注意這個查詢包括其他的參數，例如 `scoringParameter`。 查詢參數說明於 [搜尋文件 (Azure 搜尋服務 API)](search-api-2015-02-28-preview.md#SearchDocs)中。

按一下[範例](#example)tooreview 評分設定檔的更詳細的範例。

## <a name="what-is-default-scoring"></a>什麼是預設計分？
計分會計算排名排序的結果集中每個項目的搜尋分數。 搜尋結果集中的每個項目會指派一個搜尋分數，然後排名最高 toolowest。 Toohello 應用程式時，會傳回與 hello 較高分數的項目。 根據預設，hello 會傳回前 50，但您可以使用 hello`$top`參數 tooreturn 小或較大的項目數目 （向上 too1000 單一回應中)。

根據預設，搜尋分數會根據計算 hello 資料與 hello 查詢的統計屬性。 Azure 搜尋會尋找在 hello 查詢字串中包含 hello 搜尋詞彙的文件 (部分或全部，視`searchMode`)，優先列出包含許多執行個體的 hello 搜尋詞彙的文件。 hello 搜尋分數會甚至更高版本如果 hello 術語主體間很 hello 資料主體，但常見 hello 文件中。 這個方法 toocomputing 相關性的 hello 基礎稱為 TF-IDF 或 （「 詞彙頻率反向的文件頻率）。

假設沒有任何自訂排序，結果會接著依搜尋分數排名再傳回 toohello 呼叫的應用程式。 如果`$top`未指定，則需要 hello 最高搜尋分數會傳回 50 個項目。

搜尋分數值可以在整個結果集內重複。 例如，您可以有 10 個項目的分數為 1.2、20 個項目的分數為 1.0，20 個項目的分數為 0.5。 當有多個命中具有 hello 相同的搜尋分數時，hello 排序相同的項目未定義，並可能會不穩定。 同樣地，執行 hello 查詢，您可能會看到項目移動位置。 若有兩個項目的分數完全相同，則無法保證哪個項目先出現。

## <a name="when-toouse-custom-scoring"></a>當 toouse 自訂計分
Hello 預設排名行為不會移到足以在符合您的商業目標時，您應該建立一個或多個計分設定檔。 例如，您可以決定讓新增的項目具有較高的搜尋相關性。 同樣地，您可以讓某個欄位包含毛利率，或讓其他欄位指出潛在營收。 促進帶來好處 tooyour 商務的叫用，可以是重要的因素決定 toouse 計分設定檔。

此外也會透過評分設定檔實作以相關性為基礎的排序。 請考慮您在 hello 過去使用的頁面，可讓您依價格、 日期、 評等或相關性排序的搜尋結果。 在 Azure 搜尋計分設定檔磁碟機 hello 啟用 「 相關性 」 選項。 hello 的相關性的定義是由您控制，想 toodeliver 取決於商業目標和 hello 的搜尋經驗類型。

<a name="example"></a>

## <a name="example"></a>範例
如前所述，自訂計分是透過索引結構描述中定義的一或多個評分設定檔而實作的。

此範例中會顯示 hello 與兩個計分設定檔的索引結構描述 (`boostGenre`， `newAndHighlyRated`)。 此索引為查詢參數會使用 hello 設定檔 tooscore hello 結果集包含其中一個設定檔的任何查詢。

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
tooimplement 自訂計分行為，新增評分設定檔 toohello 結構描述定義 hello 索引。 您可以設定 too16 計分設定檔內的索引 (請參閱[服務限制](search-limits-quotas-capacity.md))，但您只能指定一個設定檔在任何給定查詢中的階段。

以 hello 開頭[範本](#bkmk_template)本主題所提供。

提供名稱。 計分設定檔是選擇性的但如果您加入一個，hello 名稱是必要項。 要確定 toofollow hello 欄位命名慣例 （開頭是字母，避免保留的字及特殊字元）。 請參閱 [命名規則 (Azure 搜尋)](http://msdn.microsoft.com/library/azure/dn857353.aspx) 以了解更多資訊。

計分設定檔的 hello hello 主體是從加權的欄位和函數建構。

### <a name="weights"></a>Weights
hello`weights`計分設定檔屬性會指定指派相對權數 tooa 欄位的名稱 / 值組。 在 hello[範例](#example)，hello albumTitle、 genre 和 artistName 欄位分別促進式 1.5、 5 和 2。 為何 genre 提升比 hello 其他人這麼多高？ 如果是稍微同質性的資料執行搜尋 (使用 'genre' hello 中的 hello 案例`musicstoreindex`)，您可能需要 hello 相對權數大的變異數。 例如，在 hello `musicstoreindex`，'rock' 會顯示為顯示這兩種內容類型中相同措詞的類型描述。 如果您想 genre toooutweigh 類型說明，hello 類型欄位需要更高的相對權數。

### <a name="functions"></a>Functions
函數是在特定內容需要額外計算時使用。 有效的函數類型 `freshness`、`magnitude`、`distance` 和 `tag`。 每個函式都有唯一的 tooit 參數。

* `freshness`您所要 tooboost 新舊程度的項目時，應該使用。 此函數僅適用於 datetime 欄位 (`Edm.DataTimeOffset`)。 請注意 hello`boostingDuration`屬性搭配 hello 有效性函式。
* `magnitude`您想要如何高或過低的數值為基礎的 tooboost 是時，應該使用。 呼叫此函數的案例，包含依毛利率、最高價格、最低價格或下載次數進行提升。 您可以反轉 hello 範圍，高 toolow，如果您想 hello 反向模式 （例如，tooboost 低價項目超過高低價項目）。 指定的 $ 100 的價格範圍太 $1，則可以將`boostingRangeStart`100 和`boostingRangeEnd`在 1 tooboost hello 低價項目。 此函數僅可用於雙精度浮點數和整數欄位。
* `distance`應透過想 tooboost 時依鄰近性或地理位置。 此函數僅適用於 `Edm.GeographyPoint` 欄位。
* `tag`應該用於當您想 tooboost 依文件和搜尋查詢之間的共通的標記。 此函數僅適用於 `Edm.String` 和 `Collection(Edm.String)` 欄位。

#### <a name="rules-for-using-functions"></a>使用函數的規則
* 函數類型 (freshness、magnitude、distance、tag) 必須是小寫。
* 函數不可包含 null 或空值。 具體來說，如果您包含欄位名稱，您有 tooset 它 toosomething。
* 函式只可套用的 toofilterable 欄位。 請參閱[建立索引](search-api-2015-02-28-preview.md#CreateIndex)以了解更多有關可篩選欄位的相關資訊。
* 函式只可套用的 toofields hello 索引欄位集合中所定義。

Hello 索引定義之後，請上傳 hello 索引結構描述，後面接著的文件建立 hello 索引。 如需這些操作的指示，請參閱[建立索引](search-api-2015-02-28-preview.md#CreateIndex)和[新增或更新文件](search-api-2015-02-28-preview.md#AddOrUpdateDocuments)。 建置 hello 索引之後，您應該有功能的計分設定檔適用於您的搜尋資料。

<a name="bkmk_template"></a>

## <a name="template"></a>範本
此區段會顯示 hello 語法與用於計分設定檔範本。 請參閱太[索引屬性參考](#bkmk_indexref)hello 下一節，如需 hello 屬性的描述。

    ...
    "scoringProfiles": [
      {
        "name": "name of scoring profile",
        "text": (optional, only applies toosearchable fields) {
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
              "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location)
              "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
            }

            // (- or -)

            "tag": {
              "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field)
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
> 計分函數只能套用的 toofields 可篩選。
>
>

| 屬性 | 說明 |
| --- | --- |
| `name` |必要。 這是 hello 的 hello 計分設定檔的名稱。 它如下所示 hello 欄位的相同命名慣例。 它必須以字母開頭，且不得包含點、 冒號或 @ 符號，且不得以 hello 片語"azureSearch"（區分大小寫） 開頭。 |
| `text` |包含 hello 權數 屬性。 |
| `weights` |選用。 指定欄位名稱和相對權數的名稱值組。 相對權數必須是正整數或浮點數。 您可以指定不含對應權數的 hello 欄位名稱。 加權是一個欄位相對 tooanother 使用的 tooindicate hello 重要性。 |
| `functions` |選用。 請注意，計分函數只能套用的 toofields 可篩選。 |
| `type` |計分函數的必要項目。 表示函式 toouse hello 類型。 有效值包括 `magnitude`、`freshness`、`distance` 和 `tag`。 您可以在每個評分設定檔中包含多個函數。 hello 函式名稱必須是小寫。 |
| `boost` |計分函數的必要項目。 做為原始分數之乘數的正數。 它不能等於 too1。 |
| `fieldName` |計分函數的必要項目。 計分函數只能套用的 toofields hello hello 索引欄位集合的一部分，並且可篩選。 此外，每個函數類型都有額外的限制 (有效性與日期時間欄位搭配使用，量級與整數或雙精確度浮點數欄位搭配，距離與位置欄位搭配，標記與字串或字串集合欄位搭配)。 每個函數定義只能指定一個欄位。 如範例中，toouse 大小兩倍的 hello 相同的設定檔，您就必須 tooinclude 兩個定義範圍內，一個用於每個欄位。 |
| `interpolation` |計分函數的必要項目。 定義哪些 hello 分數，提升從 hello 範圍 toohello hello 範圍結尾的 hello 開頭的 hello 斜率。 有效值包括 `linear` (預設值)、`constant`、`quadratic` 和 `logarithmic`。 如需詳細資訊，請參閱 [設定內插補點](#bkmk_interpolation) 。 |
| `magnitude` |hello 量級計分函式是使用的 tooalter 排名 hello 範圍的數值欄位的值為基礎。 這個 hello 最常見使用方式範例的部分包括：<ul><li>星級評等： Alter hello 計分會根據 hello 「 星級評等 」 欄位中的 hello 值。 當兩個項目相關時，會先顯示 hello hello 高評等項目。</li><li>邊界： 兩個文件相關時，零售商可能會想 tooboost 先具有較高利潤的文件。</li><li>點擊數： 透過動作 tooproducts 或頁面，按一下追蹤的應用程式，您可以使用傾向 tooget hello 大部分資料傳輸量級 tooboost 項目。</li><li>下載計數： 為應用程式會追蹤下載 hello 量級函式可讓您提升有 hello 大部分的下載項目。</li></ul> |
| `magnitude:boostingRangeStart` |設定 hello 啟動 hello 量級分數的範圍值。 hello 值必須是整數或浮點數。 就 1 到 4 的星級評等而言，這會是 1。 就超過 50% 的利潤而言，這會是 50。 |
| `magnitude:boostingRangeEnd` |設定 hello hello 量級分數的範圍結束值。 hello 值必須是整數或浮點數。 就 1 到 4 的星級評等而言，這會是 4。 |
| `magnitude:constantBoostBeyondRange` |有效值為 true 或 false (預設值)。 當設定 tootrue，hello 完整提升會繼續 tooapply toodocuments 具有高於 hello 上方 hello 範圍結尾的 hello 目標欄位的值。 若為 false，這個函數 hello 提升將不會套用的 toodocuments 擁有 hello 超出 hello 範圍的目標欄位的值。 |
| `freshness` |hello 有效性計分函式是使用的 tooalter 排名分數根據 DateTimeOffset 欄位中值的項目。 例如，日期較近的項目可排在較舊項目之前。 （項目更接近 toohello 存在可以更高項目，進一步排名在未來的 hello，請注意，它也是可能 toorank 項目如未來日期的行事曆事件）。Hello 目前服務版本中的 hello 範圍一端會固定 toohello 目前的時間。 hello 另一端是根據 hello hello 過去的時間`boostingDuration`。 tooboost 某段時間 hello 未來在使用負數`boostingDuration`。 在哪一個 hello 提升從最大和最小範圍的變更由 hello 計分設定檔的插補套用 toohello hello 率 （請參閱 hello 圖）。 tooreverse hello 套用的提升係數，請選擇小於 1 的提升係數。 |
| `freshness:boostingDuration` |設定要開始停止對特定文件進行提升的到期時間。 請參閱[設定 boostingDuration](#bkmk_boostdur) hello 後面的語法和範例 > 一節中。 |
| `distance` |hello 距離計分函式是使用的 tooaffect hello 分數的方式為基礎的文件關閉或者遠相對 tooa 參考地理位置。 hello 參考位置為指定的參數中的 hello 查詢的一部分 (使用 hello`scoringParameter`查詢參數) 以 lon，lat 引數。 |
| `distance:referencePointParameter` |參數 toobe 傳入查詢 toouse 做為參考位置。 scoringParameter 是查詢參數。 如需查詢參數的說明，請參閱 [搜尋文件](search-api-2015-02-28-preview.md#SearchDocs) 。 |
| `distance:boostingDistance` |數字，指出 hello 以公里為單位從 hello hello 提升範圍結束的參考位置的距離。 |
| `tag` |hello 標記計分函數可用文件 tooaffect hello 分數會根據文件和搜尋查詢中的標記。 將促進式標記和相同的 hello 搜尋查詢的文件。 hello 標記做為每個搜尋要求的計分參數中提供 hello 搜尋查詢 (使用 hello`scoringParameter`查詢參數)。 |
| `tag:tagsParameter` |在查詢中傳遞的參數 toobe toospecify 標記為特定的要求。 `scoringParameter` 是查詢參數。 如需查詢參數的說明，請參閱 [搜尋文件](search-api-2015-02-28-preview.md#SearchDocs) 。 |
| `functionAggregation` |選用。 只有在已指定函數時才會套用。 有效值包括：`sum` (預設值)、`average`、`minimum`、`maximum` 和 `firstMatching`。 搜尋分數是從多個變數 (包含多個函數) 計算的單一值。 這個屬性指出 hello 等級，所有的 hello 函式的方式結合為則套用的 toohello 基底文件分數的單一彙總提升。 hello 基本分數根據 hello tf idf 值計算 hello 文件與 hello 搜尋查詢。 |
| `defaultScoringProfile` |執行搜尋要求時如果未指定評分設定檔，則會使用預設計分 (僅使用 tf-idf)。 預設的計分設定檔名稱可以在此處設定，提供特定的設定檔是以 hello 搜尋要求的使用者 Azure 搜尋 toouse 造成該設定檔。 |

<a name="bkmk_interpolation"></a>

## <a name="set-interpolations"></a>設定內插補點
插補可讓您提升從 hello 範圍 toohello hello 範圍結尾的 hello 開頭的 hello 分數的 toodefine hello 斜率。 可以使用下列插補的 hello:

* `Linear`： 對於 hello max 和 min 範圍內的項目，hello boost 套用 toohello 項目將會已持續遞減的量。 線性是計分設定檔的 hello 預設插補。
* `Constant`: Hello 開始和結束範圍內的項目，常數提升就會套用的 toohello 的等級結果。
* `Quadratic`： 在比較 tooa 已持續遞減提升的線性插補，二次方程式一開始會較小的步調減少，再以接近 hello 結束範圍時，減少在較大的間隔。 標記計分函數中不允許此插補選項。
* `Logarithmic`： 在比較 tooa 已持續遞減提升的線性插補，對數一開始會較高的步調減少，再以接近 hello 結束範圍時，減少在多較小的間隔。 標記計分函數中不允許此插補選項。

<a name="Figure1"></a> ![][1]

<a name="bkmk_boostdur"></a>

## <a name="set-boostingduration"></a>設定 boostingDuration
`boostingDuration`是 hello 有效性函式的屬性。 您將它的提升的到期時間將會停止的 tooset 用於特定文件。 例如，tooboost 產品線或品牌的 10 天的促銷期間，您會指定 hello 10 天的期間"P10d"為這些文件。 或 tooboost 即將發生的事件中 hello 下一週指定"-P7D"。

`boostingDuration` 必須格式化為 XSD "dayTimeDuration" 值 (ISO 8601 持續時間值的限定子集)。 這個 hello 模式是： `[-]P[nD][T[nH][nM][nS]]`。

hello 下表提供數個範例。

| Duration | boostingDuration |
| --- | --- |
| 1 天 |"P1D" |
| 2 天又 12 個小時 |"P2DT12H" |
| 15 Minuten |"PT15M" |
| 30 天 5 小時 10 分鐘又 6.334 秒 |"P30DT5H10M6.334S" |

如需更多範例，請參閱 [XML 結構描述：資料類型 (W3.org 網站)](http://www.w3.org/TR/xmlschema11-2/)。

**另請參閱 MSDN 上的** 
[Azure 搜尋服務 REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) <br/>MSDN 上的 
[建立索引 (Azure 搜尋服務 API)](http://msdn.microsoft.com/library/azure/dn798941.aspx)<br/>
[新增評分設定檔 tooa 搜尋索引](http://msdn.microsoft.com/library/azure/dn798928.aspx)MSDN 上<br/>

<!--Image references-->
[1]: ./media/search-api-scoring-profiles-2015-02-28-Preview/scoring_interpolations.png
