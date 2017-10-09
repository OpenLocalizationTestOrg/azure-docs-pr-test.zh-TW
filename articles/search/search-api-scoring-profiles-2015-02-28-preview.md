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
# <a name="scoring-profiles-azure-search-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="8fdc3-103">評分設定檔 (Azure 搜尋服務 REST API 2015-02-28-Preview 版)</span><span class="sxs-lookup"><span data-stu-id="8fdc3-103">Scoring Profiles (Azure Search REST API Version 2015-02-28-Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="8fdc3-104">本文說明計分設定檔中 hello [2015年-02-28-preview](search-api-2015-02-28-preview.md)。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-104">This article describes scoring profiles in hello [2015-02-28-Preview](search-api-2015-02-28-preview.md).</span></span> <span data-ttu-id="8fdc3-105">目前沒有任何差異 hello`2016-09-01`版本上記載[MSDN](http://msdn.microsoft.com/library/azure/mt183328.aspx)和 hello`2015-02-28-Preview`此處描述的版本，但我們提供此文件還是順序 tooprovide 文件涵蓋範圍中跨 hello整個應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-105">Currently there is no difference between hello `2016-09-01` version documented on [MSDN](http://msdn.microsoft.com/library/azure/mt183328.aspx) and hello `2015-02-28-Preview` version described here, but we offer this document anyway in order tooprovide document coverage across hello entire API.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="8fdc3-106">概觀</span><span class="sxs-lookup"><span data-stu-id="8fdc3-106">Overview</span></span>
<span data-ttu-id="8fdc3-107">計分是指 toohello 計算的搜尋分數，每個項目的搜尋結果中傳回。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-107">Scoring refers toohello computation of a search score for every item returned in search results.</span></span> <span data-ttu-id="8fdc3-108">hello 分數是 hello 內容 hello 目前的搜尋操作中的項目相關的指標。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-108">hello score is an indicator of an item's relevance in hello context of hello current search operation.</span></span> <span data-ttu-id="8fdc3-109">hello hello 分數越高，更有相關性的 hello hello 項目。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-109">hello higher hello score, hello more relevant hello item.</span></span> <span data-ttu-id="8fdc3-110">在搜尋結果中，項目是從高 toolow，根據為每個項目計算的 hello 搜尋分數排序次序。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-110">In search results, items are rank ordered from high toolow, based on hello search score calculated for each item.</span></span>

<span data-ttu-id="8fdc3-111">Azure 搜尋會使用預設計分 toocompute 初始分數，但您可以自訂 hello 計算透過計分設定檔。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-111">Azure Search uses default scoring toocompute an initial score, but you can customize hello calculation through a scoring profile.</span></span> <span data-ttu-id="8fdc3-112">計分設定檔可讓您更掌控 hello 排名項目的搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-112">Scoring profiles give you greater control over hello ranking of items in search results.</span></span> <span data-ttu-id="8fdc3-113">比方說，您可能會想根據其潛在營收的 tooboost 項目，升級較新的項目，或是可能是提升庫存過久過的項目。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-113">For example, you might want tooboost items based on their revenue potential, promote newer items, or perhaps boost items that have been in inventory too long.</span></span>

<span data-ttu-id="8fdc3-114">計分設定檔是 hello 索引定義中，組成欄位、 函數和參數的一部分。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-114">A scoring profile is part of hello index definition, composed of fields, functions, and parameters.</span></span>

<span data-ttu-id="8fdc3-115">toogive 您了解什麼計分設定檔看起來像 hello 下列範例顯示簡單的設定檔命名為 'geo'。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-115">toogive you an idea of what a scoring profile looks like, hello following example shows a simple profile named 'geo'.</span></span> <span data-ttu-id="8fdc3-116">這個功能可以大幅的項目 hello 搜尋詞彙在 hello`hotelName`欄位。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-116">This one boosts items that have hello search term in hello `hotelName` field.</span></span> <span data-ttu-id="8fdc3-117">它也會使用 hello`distance`函式的 hello 目前的位置相距十公里以內的 toofavor 項目。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-117">It also uses hello `distance` function toofavor items that are within ten kilometers of hello current location.</span></span> <span data-ttu-id="8fdc3-118">如果有人搜尋 hello 詞彙 'inn'，'inn' 剛好 toobe hello 飯店名稱的一部分，包含具有 'inn' 的文件會出現在 hello 搜尋結果中較高。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-118">If someone searches on hello term 'inn', and 'inn' happens toobe part of hello hotel name, documents that include hotels with 'inn' will appear higher in hello search results.</span></span>

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

<span data-ttu-id="8fdc3-119">這個計分設定檔，您的查詢是的 toouse 構成 hello 查詢字串上的 toospecify hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-119">toouse this scoring profile, your query is formulated toospecify hello profile on hello query string.</span></span> <span data-ttu-id="8fdc3-120">在下列 hello 查詢，請注意 hello 查詢參數， `scoringProfile=geo` hello 要求中。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-120">In hello query below, notice hello query parameter, `scoringProfile=geo` in hello request.</span></span>

    GET /indexes/hotels/docs?search=inn&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&api-version=2015-02-28-Preview

<span data-ttu-id="8fdc3-121">此查詢會搜尋 hello 詞彙 'inn'，並傳入 hello 目前的位置。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-121">This query searches on hello term 'inn' and passes in hello current location.</span></span> <span data-ttu-id="8fdc3-122">請注意這個查詢包括其他的參數，例如 `scoringParameter`。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-122">Note that this query includes other parameters, such as `scoringParameter`.</span></span> <span data-ttu-id="8fdc3-123">查詢參數說明於 [搜尋文件 (Azure 搜尋服務 API)](search-api-2015-02-28-preview.md#SearchDocs)中。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-123">Query parameters are described in [Search Documents (Azure Search API)](search-api-2015-02-28-preview.md#SearchDocs).</span></span>

<span data-ttu-id="8fdc3-124">按一下[範例](#example)tooreview 評分設定檔的更詳細的範例。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-124">Click [Example](#example) tooreview a more detailed example of a scoring profile.</span></span>

## <a name="what-is-default-scoring"></a><span data-ttu-id="8fdc3-125">什麼是預設計分？</span><span class="sxs-lookup"><span data-stu-id="8fdc3-125">What is default scoring?</span></span>
<span data-ttu-id="8fdc3-126">計分會計算排名排序的結果集中每個項目的搜尋分數。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-126">Scoring computes a search score for each item in a rank ordered result set.</span></span> <span data-ttu-id="8fdc3-127">搜尋結果集中的每個項目會指派一個搜尋分數，然後排名最高 toolowest。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-127">Every item in a search result set is assigned a search score, then ranked highest toolowest.</span></span> <span data-ttu-id="8fdc3-128">Toohello 應用程式時，會傳回與 hello 較高分數的項目。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-128">Items with hello higher scores are returned toohello application.</span></span> <span data-ttu-id="8fdc3-129">根據預設，hello 會傳回前 50，但您可以使用 hello`$top`參數 tooreturn 小或較大的項目數目 （向上 too1000 單一回應中)。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-129">By default, hello top 50 are returned, but you can use hello `$top` parameter tooreturn a smaller or larger number of items (up too1000 in a single response).</span></span>

<span data-ttu-id="8fdc3-130">根據預設，搜尋分數會根據計算 hello 資料與 hello 查詢的統計屬性。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-130">By default, a search score is computed based on statistical properties of hello data and hello query.</span></span> <span data-ttu-id="8fdc3-131">Azure 搜尋會尋找在 hello 查詢字串中包含 hello 搜尋詞彙的文件 (部分或全部，視`searchMode`)，優先列出包含許多執行個體的 hello 搜尋詞彙的文件。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-131">Azure Search finds documents that include hello search terms in hello query string (some or all, depending on `searchMode`), favoring documents that contain many instances of hello search term.</span></span> <span data-ttu-id="8fdc3-132">hello 搜尋分數會甚至更高版本如果 hello 術語主體間很 hello 資料主體，但常見 hello 文件中。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-132">hello search score goes up even higher if hello term is rare across hello data corpus, but common within hello document.</span></span> <span data-ttu-id="8fdc3-133">這個方法 toocomputing 相關性的 hello 基礎稱為 TF-IDF 或 （「 詞彙頻率反向的文件頻率）。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-133">hello basis for this approach toocomputing relevance is known as TF-IDF or (term frequency-inverse document frequency).</span></span>

<span data-ttu-id="8fdc3-134">假設沒有任何自訂排序，結果會接著依搜尋分數排名再傳回 toohello 呼叫的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-134">Assuming there is no custom sorting, results are then ranked by search score before they are returned toohello calling application.</span></span> <span data-ttu-id="8fdc3-135">如果`$top`未指定，則需要 hello 最高搜尋分數會傳回 50 個項目。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-135">If `$top` is not specified, 50 items having hello highest search score are returned.</span></span>

<span data-ttu-id="8fdc3-136">搜尋分數值可以在整個結果集內重複。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-136">Search score values can be repeated throughout a result set.</span></span> <span data-ttu-id="8fdc3-137">例如，您可以有 10 個項目的分數為 1.2、20 個項目的分數為 1.0，20 個項目的分數為 0.5。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-137">For example, you might have 10 items with a score of 1.2, 20 items with a score of 1.0, and 20 items with a score of 0.5.</span></span> <span data-ttu-id="8fdc3-138">當有多個命中具有 hello 相同的搜尋分數時，hello 排序相同的項目未定義，並可能會不穩定。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-138">When multiple hits have hello same search score, hello ordering of same scored items is not defined, and is not stable.</span></span> <span data-ttu-id="8fdc3-139">同樣地，執行 hello 查詢，您可能會看到項目移動位置。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-139">Run hello query again, and you might see items shift position.</span></span> <span data-ttu-id="8fdc3-140">若有兩個項目的分數完全相同，則無法保證哪個項目先出現。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-140">Given two items with an identical score, there is no guarantee which one appears first.</span></span>

## <a name="when-toouse-custom-scoring"></a><span data-ttu-id="8fdc3-141">當 toouse 自訂計分</span><span class="sxs-lookup"><span data-stu-id="8fdc3-141">When toouse custom scoring</span></span>
<span data-ttu-id="8fdc3-142">Hello 預設排名行為不會移到足以在符合您的商業目標時，您應該建立一個或多個計分設定檔。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-142">You should create one or more scoring profiles when hello default ranking behavior doesn’t go far enough in meeting your business objectives.</span></span> <span data-ttu-id="8fdc3-143">例如，您可以決定讓新增的項目具有較高的搜尋相關性。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-143">For example, you might decide that search relevance should favor newly added items.</span></span> <span data-ttu-id="8fdc3-144">同樣地，您可以讓某個欄位包含毛利率，或讓其他欄位指出潛在營收。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-144">Likewise, you might have a field that contains profit margin, or some other field indicating revenue potential.</span></span> <span data-ttu-id="8fdc3-145">促進帶來好處 tooyour 商務的叫用，可以是重要的因素決定 toouse 計分設定檔。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-145">Boosting hits that bring benefits tooyour business can be an important factor in deciding toouse scoring profiles.</span></span>

<span data-ttu-id="8fdc3-146">此外也會透過評分設定檔實作以相關性為基礎的排序。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-146">Relevancy-based ordering is also implemented through scoring profiles.</span></span> <span data-ttu-id="8fdc3-147">請考慮您在 hello 過去使用的頁面，可讓您依價格、 日期、 評等或相關性排序的搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-147">Consider search results pages you’ve used in hello past that let you sort by price, date, rating, or relevance.</span></span> <span data-ttu-id="8fdc3-148">在 Azure 搜尋計分設定檔磁碟機 hello 啟用 「 相關性 」 選項。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-148">In Azure Search, scoring profiles drive hello 'relevance' option.</span></span> <span data-ttu-id="8fdc3-149">hello 的相關性的定義是由您控制，想 toodeliver 取決於商業目標和 hello 的搜尋經驗類型。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-149">hello definition of relevance is controlled by you, predicated on business objectives and hello type of search experience you want toodeliver.</span></span>

<a name="example"></a>

## <a name="example"></a><span data-ttu-id="8fdc3-150">範例</span><span class="sxs-lookup"><span data-stu-id="8fdc3-150">Example</span></span>
<span data-ttu-id="8fdc3-151">如前所述，自訂計分是透過索引結構描述中定義的一或多個評分設定檔而實作的。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-151">As noted, customized scoring is implemented through scoring profiles defined in an index schema.</span></span>

<span data-ttu-id="8fdc3-152">此範例中會顯示 hello 與兩個計分設定檔的索引結構描述 (`boostGenre`， `newAndHighlyRated`)。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-152">This example shows hello schema of an index with two scoring profiles (`boostGenre`, `newAndHighlyRated`).</span></span> <span data-ttu-id="8fdc3-153">此索引為查詢參數會使用 hello 設定檔 tooscore hello 結果集包含其中一個設定檔的任何查詢。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-153">Any query against this index that includes either profile as a query parameter will use hello profile tooscore hello result set.</span></span>

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


## <a name="workflow"></a><span data-ttu-id="8fdc3-154">工作流程</span><span class="sxs-lookup"><span data-stu-id="8fdc3-154">Workflow</span></span>
<span data-ttu-id="8fdc3-155">tooimplement 自訂計分行為，新增評分設定檔 toohello 結構描述定義 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-155">tooimplement custom scoring behavior, add a scoring profile toohello schema that defines hello index.</span></span> <span data-ttu-id="8fdc3-156">您可以設定 too16 計分設定檔內的索引 (請參閱[服務限制](search-limits-quotas-capacity.md))，但您只能指定一個設定檔在任何給定查詢中的階段。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-156">You can have up too16 scoring profiles within an index (see [Service Limits](search-limits-quotas-capacity.md)), but you can only specify one profile at time in any given query.</span></span>

<span data-ttu-id="8fdc3-157">以 hello 開頭[範本](#bkmk_template)本主題所提供。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-157">Start with hello [Template](#bkmk_template) provided in this topic.</span></span>

<span data-ttu-id="8fdc3-158">提供名稱。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-158">Provide a name.</span></span> <span data-ttu-id="8fdc3-159">計分設定檔是選擇性的但如果您加入一個，hello 名稱是必要項。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-159">Scoring profiles are optional, but if you add one, hello name is required.</span></span> <span data-ttu-id="8fdc3-160">要確定 toofollow hello 欄位命名慣例 （開頭是字母，避免保留的字及特殊字元）。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-160">Be sure toofollow hello naming conventions for fields (starts with a letter, avoids special characters and reserved words).</span></span> <span data-ttu-id="8fdc3-161">請參閱 [命名規則 (Azure 搜尋)](http://msdn.microsoft.com/library/azure/dn857353.aspx) 以了解更多資訊。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-161">See [Naming Rules](http://msdn.microsoft.com/library/azure/dn857353.aspx) for more information.</span></span>

<span data-ttu-id="8fdc3-162">計分設定檔的 hello hello 主體是從加權的欄位和函數建構。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-162">hello body of hello scoring profile is constructed from weighted fields and functions.</span></span>

### <a name="weights"></a><span data-ttu-id="8fdc3-163">Weights</span><span class="sxs-lookup"><span data-stu-id="8fdc3-163">Weights</span></span>
<span data-ttu-id="8fdc3-164">hello`weights`計分設定檔屬性會指定指派相對權數 tooa 欄位的名稱 / 值組。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-164">hello `weights` property of a scoring profile specifies name-value pairs that assign a relative weight tooa field.</span></span> <span data-ttu-id="8fdc3-165">在 hello[範例](#example)，hello albumTitle、 genre 和 artistName 欄位分別促進式 1.5、 5 和 2。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-165">In hello [Example](#example), hello albumTitle, genre, and artistName fields are boosted 1.5, 5, and 2, respectively.</span></span> <span data-ttu-id="8fdc3-166">為何 genre 提升比 hello 其他人這麼多高？</span><span class="sxs-lookup"><span data-stu-id="8fdc3-166">Why is genre boosted so much higher than hello others?</span></span> <span data-ttu-id="8fdc3-167">如果是稍微同質性的資料執行搜尋 (使用 'genre' hello 中的 hello 案例`musicstoreindex`)，您可能需要 hello 相對權數大的變異數。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-167">If search is conducted over data that is somewhat homogeneous (as is hello case with 'genre' in hello `musicstoreindex`), you might need a larger variance in hello relative weights.</span></span> <span data-ttu-id="8fdc3-168">例如，在 hello `musicstoreindex`，'rock' 會顯示為顯示這兩種內容類型中相同措詞的類型描述。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-168">For example, in hello `musicstoreindex`, 'rock' appears as both a genre and in identically phrased genre descriptions.</span></span> <span data-ttu-id="8fdc3-169">如果您想 genre toooutweigh 類型說明，hello 類型欄位需要更高的相對權數。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-169">If you want genre toooutweigh genre description, hello genre field will need a much higher relative weight.</span></span>

### <a name="functions"></a><span data-ttu-id="8fdc3-170">Functions</span><span class="sxs-lookup"><span data-stu-id="8fdc3-170">Functions</span></span>
<span data-ttu-id="8fdc3-171">函數是在特定內容需要額外計算時使用。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-171">Functions are used when additional calculations are required for specific contexts.</span></span> <span data-ttu-id="8fdc3-172">有效的函數類型 `freshness`、`magnitude`、`distance` 和 `tag`。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-172">Valid function types are `freshness`, `magnitude`, `distance` and `tag`.</span></span> <span data-ttu-id="8fdc3-173">每個函式都有唯一的 tooit 參數。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-173">Each function has parameters that are unique tooit.</span></span>

* <span data-ttu-id="8fdc3-174">`freshness`您所要 tooboost 新舊程度的項目時，應該使用。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-174">`freshness` should be used when you want tooboost by how new or old an item is.</span></span> <span data-ttu-id="8fdc3-175">此函數僅適用於 datetime 欄位 (`Edm.DataTimeOffset`)。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-175">This function can only be used with datetime fields (`Edm.DataTimeOffset`).</span></span> <span data-ttu-id="8fdc3-176">請注意 hello`boostingDuration`屬性搭配 hello 有效性函式。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-176">Note hello `boostingDuration` attribute is used only with hello freshness function.</span></span>
* <span data-ttu-id="8fdc3-177">`magnitude`您想要如何高或過低的數值為基礎的 tooboost 是時，應該使用。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-177">`magnitude` should be used when you want tooboost based on how high or low a numeric value is.</span></span> <span data-ttu-id="8fdc3-178">呼叫此函數的案例，包含依毛利率、最高價格、最低價格或下載次數進行提升。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-178">Scenarios that call for this function include boosting by profit margin, highest price, lowest price, or a count of downloads.</span></span> <span data-ttu-id="8fdc3-179">您可以反轉 hello 範圍，高 toolow，如果您想 hello 反向模式 （例如，tooboost 低價項目超過高低價項目）。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-179">You can reverse hello range, high toolow, if you want hello inverse pattern (for example, tooboost lower-priced items more than higher-priced items).</span></span> <span data-ttu-id="8fdc3-180">指定的 $ 100 的價格範圍太 $1，則可以將`boostingRangeStart`100 和`boostingRangeEnd`在 1 tooboost hello 低價項目。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-180">Given a range of prices from $100 too$1, you would set `boostingRangeStart` at 100 and `boostingRangeEnd` at 1 tooboost hello lower-priced items.</span></span> <span data-ttu-id="8fdc3-181">此函數僅可用於雙精度浮點數和整數欄位。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-181">This function can only be used with double and integer fields.</span></span>
* <span data-ttu-id="8fdc3-182">`distance`應透過想 tooboost 時依鄰近性或地理位置。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-182">`distance` should be used when you want tooboost by proximity or geographic location.</span></span> <span data-ttu-id="8fdc3-183">此函數僅適用於 `Edm.GeographyPoint` 欄位。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-183">This function can only be used with `Edm.GeographyPoint` fields.</span></span>
* <span data-ttu-id="8fdc3-184">`tag`應該用於當您想 tooboost 依文件和搜尋查詢之間的共通的標記。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-184">`tag` should be used when you want tooboost by tags in common between documents and search queries.</span></span> <span data-ttu-id="8fdc3-185">此函數僅適用於 `Edm.String` 和 `Collection(Edm.String)` 欄位。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-185">This function can only be used with `Edm.String` and `Collection(Edm.String)` fields.</span></span>

#### <a name="rules-for-using-functions"></a><span data-ttu-id="8fdc3-186">使用函數的規則</span><span class="sxs-lookup"><span data-stu-id="8fdc3-186">Rules for using functions</span></span>
* <span data-ttu-id="8fdc3-187">函數類型 (freshness、magnitude、distance、tag) 必須是小寫。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-187">Function type (freshness, magnitude, distance, tag) must be lower case.</span></span>
* <span data-ttu-id="8fdc3-188">函數不可包含 null 或空值。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-188">Functions cannot include null or empty values.</span></span> <span data-ttu-id="8fdc3-189">具體來說，如果您包含欄位名稱，您有 tooset 它 toosomething。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-189">Specifically, if you include fieldname, you have tooset it toosomething.</span></span>
* <span data-ttu-id="8fdc3-190">函式只可套用的 toofilterable 欄位。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-190">Functions can only be applied toofilterable fields.</span></span> <span data-ttu-id="8fdc3-191">請參閱[建立索引](search-api-2015-02-28-preview.md#CreateIndex)以了解更多有關可篩選欄位的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-191">See [Create Index](search-api-2015-02-28-preview.md#CreateIndex) for more information about filterable fields.</span></span>
* <span data-ttu-id="8fdc3-192">函式只可套用的 toofields hello 索引欄位集合中所定義。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-192">Functions can only be applied toofields that are defined in hello fields collection of an index.</span></span>

<span data-ttu-id="8fdc3-193">Hello 索引定義之後，請上傳 hello 索引結構描述，後面接著的文件建立 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-193">After hello index is defined, build hello index by uploading hello index schema, followed by documents.</span></span> <span data-ttu-id="8fdc3-194">如需這些操作的指示，請參閱[建立索引](search-api-2015-02-28-preview.md#CreateIndex)和[新增或更新文件](search-api-2015-02-28-preview.md#AddOrUpdateDocuments)。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-194">See [Create Index](search-api-2015-02-28-preview.md#CreateIndex) and [Add or Update Documents](search-api-2015-02-28-preview.md#AddOrUpdateDocuments) for instructions on these operations.</span></span> <span data-ttu-id="8fdc3-195">建置 hello 索引之後，您應該有功能的計分設定檔適用於您的搜尋資料。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-195">Once hello index is built, you should have a functional scoring profile that works with your search data.</span></span>

<a name="bkmk_template"></a>

## <a name="template"></a><span data-ttu-id="8fdc3-196">範本</span><span class="sxs-lookup"><span data-stu-id="8fdc3-196">Template</span></span>
<span data-ttu-id="8fdc3-197">此區段會顯示 hello 語法與用於計分設定檔範本。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-197">This section shows hello syntax and template for scoring profiles.</span></span> <span data-ttu-id="8fdc3-198">請參閱太[索引屬性參考](#bkmk_indexref)hello 下一節，如需 hello 屬性的描述。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-198">Refer too[Index attribute reference](#bkmk_indexref) in hello next section for descriptions of hello attributes.</span></span>

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

## <a name="scoring-profile-property-reference"></a><span data-ttu-id="8fdc3-199">評分設定檔屬性參考</span><span class="sxs-lookup"><span data-stu-id="8fdc3-199">Scoring profile property reference</span></span>
> [!NOTE]
> <span data-ttu-id="8fdc3-200">計分函數只能套用的 toofields 可篩選。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-200">A scoring function can only be applied toofields that are filterable.</span></span>
>
>

| <span data-ttu-id="8fdc3-201">屬性</span><span class="sxs-lookup"><span data-stu-id="8fdc3-201">Property</span></span> | <span data-ttu-id="8fdc3-202">說明</span><span class="sxs-lookup"><span data-stu-id="8fdc3-202">Description</span></span> |
| --- | --- |
| `name` |<span data-ttu-id="8fdc3-203">必要。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-203">Required.</span></span> <span data-ttu-id="8fdc3-204">這是 hello 的 hello 計分設定檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-204">This is hello name of hello scoring profile.</span></span> <span data-ttu-id="8fdc3-205">它如下所示 hello 欄位的相同命名慣例。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-205">It follows hello same naming conventions of a field.</span></span> <span data-ttu-id="8fdc3-206">它必須以字母開頭，且不得包含點、 冒號或 @ 符號，且不得以 hello 片語"azureSearch"（區分大小寫） 開頭。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-206">It must start with a letter, cannot contain dots, colons or @ symbols, and cannot start with hello phrase "azureSearch" (case-sensitive).</span></span> |
| `text` |<span data-ttu-id="8fdc3-207">包含 hello 權數 屬性。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-207">Contains hello Weights property.</span></span> |
| `weights` |<span data-ttu-id="8fdc3-208">選用。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-208">Optional.</span></span> <span data-ttu-id="8fdc3-209">指定欄位名稱和相對權數的名稱值組。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-209">A name-value pair that specifies a field name and relative weight.</span></span> <span data-ttu-id="8fdc3-210">相對權數必須是正整數或浮點數。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-210">Relative weight must be a positive integer or floating-point number.</span></span> <span data-ttu-id="8fdc3-211">您可以指定不含對應權數的 hello 欄位名稱。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-211">You can specify hello field name without a corresponding weight.</span></span> <span data-ttu-id="8fdc3-212">加權是一個欄位相對 tooanother 使用的 tooindicate hello 重要性。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-212">Weights are used tooindicate hello importance of one field relative tooanother.</span></span> |
| `functions` |<span data-ttu-id="8fdc3-213">選用。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-213">Optional.</span></span> <span data-ttu-id="8fdc3-214">請注意，計分函數只能套用的 toofields 可篩選。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-214">Note that a scoring function can only be applied toofields that are filterable.</span></span> |
| `type` |<span data-ttu-id="8fdc3-215">計分函數的必要項目。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-215">Required for scoring functions.</span></span> <span data-ttu-id="8fdc3-216">表示函式 toouse hello 類型。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-216">Indicates hello type of function toouse.</span></span> <span data-ttu-id="8fdc3-217">有效值包括 `magnitude`、`freshness`、`distance` 和 `tag`。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-217">Valid values include `magnitude`, `freshness`, `distance` and `tag`.</span></span> <span data-ttu-id="8fdc3-218">您可以在每個評分設定檔中包含多個函數。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-218">You can include more than one function in each scoring profile.</span></span> <span data-ttu-id="8fdc3-219">hello 函式名稱必須是小寫。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-219">hello function name must be lower case.</span></span> |
| `boost` |<span data-ttu-id="8fdc3-220">計分函數的必要項目。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-220">Required for scoring functions.</span></span> <span data-ttu-id="8fdc3-221">做為原始分數之乘數的正數。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-221">A positive number used as multiplier for raw score.</span></span> <span data-ttu-id="8fdc3-222">它不能等於 too1。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-222">It cannot be equal too1.</span></span> |
| `fieldName` |<span data-ttu-id="8fdc3-223">計分函數的必要項目。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-223">Required for scoring functions.</span></span> <span data-ttu-id="8fdc3-224">計分函數只能套用的 toofields hello hello 索引欄位集合的一部分，並且可篩選。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-224">A scoring function can only be applied toofields that are part of hello field collection of hello index, and that are filterable.</span></span> <span data-ttu-id="8fdc3-225">此外，每個函數類型都有額外的限制 (有效性與日期時間欄位搭配使用，量級與整數或雙精確度浮點數欄位搭配，距離與位置欄位搭配，標記與字串或字串集合欄位搭配)。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-225">In addition, each function type introduces additional restrictions (freshness is used with datetime fields, magnitude with integer or double fields, distance with location fields and tag with string or string collection fields).</span></span> <span data-ttu-id="8fdc3-226">每個函數定義只能指定一個欄位。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-226">You can only specify a single field per function definition.</span></span> <span data-ttu-id="8fdc3-227">如範例中，toouse 大小兩倍的 hello 相同的設定檔，您就必須 tooinclude 兩個定義範圍內，一個用於每個欄位。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-227">For example, toouse magnitude twice in hello same profile, you would need tooinclude two definitions magnitude, one for each field.</span></span> |
| `interpolation` |<span data-ttu-id="8fdc3-228">計分函數的必要項目。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-228">Required for scoring functions.</span></span> <span data-ttu-id="8fdc3-229">定義哪些 hello 分數，提升從 hello 範圍 toohello hello 範圍結尾的 hello 開頭的 hello 斜率。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-229">Defines hello slope for which hello score boosting increases from hello start of hello range toohello end of hello range.</span></span> <span data-ttu-id="8fdc3-230">有效值包括 `linear` (預設值)、`constant`、`quadratic` 和 `logarithmic`。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-230">Valid values include `linear` (default), `constant`, `quadratic`, and `logarithmic`.</span></span> <span data-ttu-id="8fdc3-231">如需詳細資訊，請參閱 [設定內插補點](#bkmk_interpolation) 。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-231">See [Set interpolations](#bkmk_interpolation) for details.</span></span> |
| `magnitude` |<span data-ttu-id="8fdc3-232">hello 量級計分函式是使用的 tooalter 排名 hello 範圍的數值欄位的值為基礎。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-232">hello magnitude scoring function is used tooalter rankings based on hello range of values for a numeric field.</span></span> <span data-ttu-id="8fdc3-233">這個 hello 最常見使用方式範例的部分包括：</span><span class="sxs-lookup"><span data-stu-id="8fdc3-233">Some of hello most common usage examples of this are:</span></span><ul><li><span data-ttu-id="8fdc3-234">星級評等： Alter hello 計分會根據 hello 「 星級評等 」 欄位中的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-234">Star ratings: Alter hello scoring based on hello value within hello "Star Rating" field.</span></span> <span data-ttu-id="8fdc3-235">當兩個項目相關時，會先顯示 hello hello 高評等項目。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-235">When two items are relevant, hello item with hello higher rating will be displayed first.</span></span></li><li><span data-ttu-id="8fdc3-236">邊界： 兩個文件相關時，零售商可能會想 tooboost 先具有較高利潤的文件。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-236">Margin: When two documents are relevant, a retailer may wish tooboost documents that have higher margins first.</span></span></li><li><span data-ttu-id="8fdc3-237">點擊數： 透過動作 tooproducts 或頁面，按一下追蹤的應用程式，您可以使用傾向 tooget hello 大部分資料傳輸量級 tooboost 項目。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-237">Click counts: For applications that track click through actions tooproducts or pages, you could use magnitude tooboost items that tend tooget hello most traffic.</span></span></li><li><span data-ttu-id="8fdc3-238">下載計數： 為應用程式會追蹤下載 hello 量級函式可讓您提升有 hello 大部分的下載項目。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-238">Download counts: For applications that track downloads, hello magnitude function lets you boost items that have hello most downloads.</span></span></li></ul> |
| `magnitude:boostingRangeStart` |<span data-ttu-id="8fdc3-239">設定 hello 啟動 hello 量級分數的範圍值。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-239">Sets hello start value of hello range over which magnitude is scored.</span></span> <span data-ttu-id="8fdc3-240">hello 值必須是整數或浮點數。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-240">hello value must be an integer or floating-point number.</span></span> <span data-ttu-id="8fdc3-241">就 1 到 4 的星級評等而言，這會是 1。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-241">For star ratings of 1 through 4, this would be 1.</span></span> <span data-ttu-id="8fdc3-242">就超過 50% 的利潤而言，這會是 50。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-242">For margins over 50%, this would be 50.</span></span> |
| `magnitude:boostingRangeEnd` |<span data-ttu-id="8fdc3-243">設定 hello hello 量級分數的範圍結束值。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-243">Sets hello end value of hello range over which magnitude is scored.</span></span> <span data-ttu-id="8fdc3-244">hello 值必須是整數或浮點數。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-244">hello value must be an integer or floating-point number.</span></span> <span data-ttu-id="8fdc3-245">就 1 到 4 的星級評等而言，這會是 4。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-245">For star ratings of 1 through 4, this would be 4.</span></span> |
| `magnitude:constantBoostBeyondRange` |<span data-ttu-id="8fdc3-246">有效值為 true 或 false (預設值)。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-246">Valid values are true or false (default).</span></span> <span data-ttu-id="8fdc3-247">當設定 tootrue，hello 完整提升會繼續 tooapply toodocuments 具有高於 hello 上方 hello 範圍結尾的 hello 目標欄位的值。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-247">When set tootrue, hello full boost will continue tooapply toodocuments that have a value for hello target field that’s higher than hello upper end of hello range.</span></span> <span data-ttu-id="8fdc3-248">若為 false，這個函數 hello 提升將不會套用的 toodocuments 擁有 hello 超出 hello 範圍的目標欄位的值。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-248">If false, hello boost of this function won’t be applied toodocuments having a value for hello target field that falls outside of hello range.</span></span> |
| `freshness` |<span data-ttu-id="8fdc3-249">hello 有效性計分函式是使用的 tooalter 排名分數根據 DateTimeOffset 欄位中值的項目。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-249">hello freshness scoring function is used tooalter ranking scores for items based on values in DateTimeOffset fields.</span></span> <span data-ttu-id="8fdc3-250">例如，日期較近的項目可排在較舊項目之前。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-250">For example, an item with a more recent date can be ranked higher than older items.</span></span> <span data-ttu-id="8fdc3-251">（項目更接近 toohello 存在可以更高項目，進一步排名在未來的 hello，請注意，它也是可能 toorank 項目如未來日期的行事曆事件）。Hello 目前服務版本中的 hello 範圍一端會固定 toohello 目前的時間。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-251">(Note that it is also possible toorank items like calendar events with future dates such that items closer toohello present can be ranked higher than items further in hello future.) In hello current service release, one end of hello range will be fixed toohello current time.</span></span> <span data-ttu-id="8fdc3-252">hello 另一端是根據 hello hello 過去的時間`boostingDuration`。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-252">hello other end is a time in hello past based on hello `boostingDuration`.</span></span> <span data-ttu-id="8fdc3-253">tooboost 某段時間 hello 未來在使用負數`boostingDuration`。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-253">tooboost a range of times in hello future use a negative `boostingDuration`.</span></span> <span data-ttu-id="8fdc3-254">在哪一個 hello 提升從最大和最小範圍的變更由 hello 計分設定檔的插補套用 toohello hello 率 （請參閱 hello 圖）。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-254">hello rate at which hello boosting changes from a maximum and minimum range is determined by hello Interpolation applied toohello scoring profile (see hello figure below).</span></span> <span data-ttu-id="8fdc3-255">tooreverse hello 套用的提升係數，請選擇小於 1 的提升係數。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-255">tooreverse hello boosting factor applied, choose a boost factor of less than 1.</span></span> |
| `freshness:boostingDuration` |<span data-ttu-id="8fdc3-256">設定要開始停止對特定文件進行提升的到期時間。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-256">Sets an expiration period after which boosting will stop for a particular document.</span></span> <span data-ttu-id="8fdc3-257">請參閱[設定 boostingDuration](#bkmk_boostdur) hello 後面的語法和範例 > 一節中。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-257">See [Set boostingDuration](#bkmk_boostdur) in hello following section for syntax and examples.</span></span> |
| `distance` |<span data-ttu-id="8fdc3-258">hello 距離計分函式是使用的 tooaffect hello 分數的方式為基礎的文件關閉或者遠相對 tooa 參考地理位置。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-258">hello distance scoring function is used tooaffect hello score of documents based on how close or far they are relative tooa reference geographic location.</span></span> <span data-ttu-id="8fdc3-259">hello 參考位置為指定的參數中的 hello 查詢的一部分 (使用 hello`scoringParameter`查詢參數) 以 lon，lat 引數。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-259">hello reference location is given as part of hello query in a parameter (using hello `scoringParameter` query parameter) as a lon,lat argument.</span></span> |
| `distance:referencePointParameter` |<span data-ttu-id="8fdc3-260">參數 toobe 傳入查詢 toouse 做為參考位置。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-260">A parameter toobe passed in queries toouse as reference location.</span></span> <span data-ttu-id="8fdc3-261">scoringParameter 是查詢參數。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-261">scoringParameter is a query parameter.</span></span> <span data-ttu-id="8fdc3-262">如需查詢參數的說明，請參閱 [搜尋文件](search-api-2015-02-28-preview.md#SearchDocs) 。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-262">See [Search Documents](search-api-2015-02-28-preview.md#SearchDocs) for descriptions of query parameters.</span></span> |
| `distance:boostingDistance` |<span data-ttu-id="8fdc3-263">數字，指出 hello 以公里為單位從 hello hello 提升範圍結束的參考位置的距離。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-263">A number that indicates hello distance in kilometers from hello reference location where hello boosting range ends.</span></span> |
| `tag` |<span data-ttu-id="8fdc3-264">hello 標記計分函數可用文件 tooaffect hello 分數會根據文件和搜尋查詢中的標記。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-264">hello tag scoring function is used tooaffect hello score of documents based on tags in documents and search queries.</span></span> <span data-ttu-id="8fdc3-265">將促進式標記和相同的 hello 搜尋查詢的文件。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-265">Documents that have tags in common with hello search query will be boosted.</span></span> <span data-ttu-id="8fdc3-266">hello 標記做為每個搜尋要求的計分參數中提供 hello 搜尋查詢 (使用 hello`scoringParameter`查詢參數)。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-266">hello tags for hello search query is provided as a scoring parameter in each search request(using hello `scoringParameter` query parameter).</span></span> |
| `tag:tagsParameter` |<span data-ttu-id="8fdc3-267">在查詢中傳遞的參數 toobe toospecify 標記為特定的要求。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-267">A parameter toobe passed in queries toospecify tags for a particular request.</span></span> <span data-ttu-id="8fdc3-268">`scoringParameter` 是查詢參數。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-268">`scoringParameter` is a query parameter.</span></span> <span data-ttu-id="8fdc3-269">如需查詢參數的說明，請參閱 [搜尋文件](search-api-2015-02-28-preview.md#SearchDocs) 。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-269">See [Search Documents](search-api-2015-02-28-preview.md#SearchDocs) for descriptions of query parameters.</span></span> |
| `functionAggregation` |<span data-ttu-id="8fdc3-270">選用。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-270">Optional.</span></span> <span data-ttu-id="8fdc3-271">只有在已指定函數時才會套用。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-271">Applies only when functions are specified.</span></span> <span data-ttu-id="8fdc3-272">有效值包括：`sum` (預設值)、`average`、`minimum`、`maximum` 和 `firstMatching`。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-272">Valid values include: `sum` (default), `average`, `minimum`, `maximum`, and `firstMatching`.</span></span> <span data-ttu-id="8fdc3-273">搜尋分數是從多個變數 (包含多個函數) 計算的單一值。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-273">A search score is a single value that is computed from multiple variables, including multiple functions.</span></span> <span data-ttu-id="8fdc3-274">這個屬性指出 hello 等級，所有的 hello 函式的方式結合為則套用的 toohello 基底文件分數的單一彙總提升。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-274">This attributes indicates how hello boosts of all hello functions are combined into a single aggregate boost that is then applied toohello base document score.</span></span> <span data-ttu-id="8fdc3-275">hello 基本分數根據 hello tf idf 值計算 hello 文件與 hello 搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-275">hello base score is based on hello tf-idf value computed from hello document and hello search query.</span></span> |
| `defaultScoringProfile` |<span data-ttu-id="8fdc3-276">執行搜尋要求時如果未指定評分設定檔，則會使用預設計分 (僅使用 tf-idf)。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-276">When executing a search request, if no scoring profile is specified, then default scoring is used (tf-idf only).</span></span> <span data-ttu-id="8fdc3-277">預設的計分設定檔名稱可以在此處設定，提供特定的設定檔是以 hello 搜尋要求的使用者 Azure 搜尋 toouse 造成該設定檔。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-277">A default scoring profile name can be set here, causing Azure Search toouse that profile when no specific profile is given in hello search request.</span></span> |

<a name="bkmk_interpolation"></a>

## <a name="set-interpolations"></a><span data-ttu-id="8fdc3-278">設定內插補點</span><span class="sxs-lookup"><span data-stu-id="8fdc3-278">Set interpolations</span></span>
<span data-ttu-id="8fdc3-279">插補可讓您提升從 hello 範圍 toohello hello 範圍結尾的 hello 開頭的 hello 分數的 toodefine hello 斜率。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-279">Interpolations allow you toodefine hello slope for which hello score boosting increases from hello start of hello range toohello end of hello range.</span></span> <span data-ttu-id="8fdc3-280">可以使用下列插補的 hello:</span><span class="sxs-lookup"><span data-stu-id="8fdc3-280">hello following interpolations can be used:</span></span>

* <span data-ttu-id="8fdc3-281">`Linear`： 對於 hello max 和 min 範圍內的項目，hello boost 套用 toohello 項目將會已持續遞減的量。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-281">`Linear`: For items that are within hello max and min range, hello boost applied toohello item will be done in a constantly decreasing amount.</span></span> <span data-ttu-id="8fdc3-282">線性是計分設定檔的 hello 預設插補。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-282">Linear is hello default interpolation for a scoring profile.</span></span>
* <span data-ttu-id="8fdc3-283">`Constant`: Hello 開始和結束範圍內的項目，常數提升就會套用的 toohello 的等級結果。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-283">`Constant`: For items that are within hello start and ending range, a constant boost will be applied toohello rank results.</span></span>
* <span data-ttu-id="8fdc3-284">`Quadratic`： 在比較 tooa 已持續遞減提升的線性插補，二次方程式一開始會較小的步調減少，再以接近 hello 結束範圍時，減少在較大的間隔。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-284">`Quadratic`: In comparison tooa Linear interpolation that has a constantly decreasing boost, Quadratic will initially decrease at smaller pace and then as it approaches hello end range, it decreases at a much higher interval.</span></span> <span data-ttu-id="8fdc3-285">標記計分函數中不允許此插補選項。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-285">This interpolation option is not allowed in tag scoring functions.</span></span>
* <span data-ttu-id="8fdc3-286">`Logarithmic`： 在比較 tooa 已持續遞減提升的線性插補，對數一開始會較高的步調減少，再以接近 hello 結束範圍時，減少在多較小的間隔。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-286">`Logarithmic`: In comparison tooa Linear interpolation that has a constantly decreasing boost, Logarithmic will initially decrease at higher pace and then as it approaches hello end range, it decreases at a much smaller interval.</span></span> <span data-ttu-id="8fdc3-287">標記計分函數中不允許此插補選項。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-287">This interpolation option is not allowed in tag scoring functions.</span></span>

<span data-ttu-id="8fdc3-288"><a name="Figure1"></a> ![][1]</span><span class="sxs-lookup"><span data-stu-id="8fdc3-288"><a name="Figure1"></a> ![][1]</span></span>

<a name="bkmk_boostdur"></a>

## <a name="set-boostingduration"></a><span data-ttu-id="8fdc3-289">設定 boostingDuration</span><span class="sxs-lookup"><span data-stu-id="8fdc3-289">Set boostingDuration</span></span>
<span data-ttu-id="8fdc3-290">`boostingDuration`是 hello 有效性函式的屬性。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-290">`boostingDuration` is an attribute of hello freshness function.</span></span> <span data-ttu-id="8fdc3-291">您將它的提升的到期時間將會停止的 tooset 用於特定文件。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-291">You use it tooset an expiration period after which boosting will stop for a particular document.</span></span> <span data-ttu-id="8fdc3-292">例如，tooboost 產品線或品牌的 10 天的促銷期間，您會指定 hello 10 天的期間"P10d"為這些文件。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-292">For example, tooboost a product line or brand for a 10-day promotional period, you would specify hello 10-day period as "P10D" for those documents.</span></span> <span data-ttu-id="8fdc3-293">或 tooboost 即將發生的事件中 hello 下一週指定"-P7D"。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-293">Or tooboost upcoming events in hello next week specify "-P7D".</span></span>

<span data-ttu-id="8fdc3-294">`boostingDuration` 必須格式化為 XSD "dayTimeDuration" 值 (ISO 8601 持續時間值的限定子集)。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-294">`boostingDuration` must be formatted as an XSD "dayTimeDuration" value (a restricted subset of an ISO 8601 duration value).</span></span> <span data-ttu-id="8fdc3-295">這個 hello 模式是： `[-]P[nD][T[nH][nM][nS]]`。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-295">hello pattern for this is: `[-]P[nD][T[nH][nM][nS]]`.</span></span>

<span data-ttu-id="8fdc3-296">hello 下表提供數個範例。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-296">hello following table provides several examples.</span></span>

| <span data-ttu-id="8fdc3-297">Duration</span><span class="sxs-lookup"><span data-stu-id="8fdc3-297">Duration</span></span> | <span data-ttu-id="8fdc3-298">boostingDuration</span><span class="sxs-lookup"><span data-stu-id="8fdc3-298">boostingDuration</span></span> |
| --- | --- |
| <span data-ttu-id="8fdc3-299">1 天</span><span class="sxs-lookup"><span data-stu-id="8fdc3-299">1 day</span></span> |<span data-ttu-id="8fdc3-300">"P1D"</span><span class="sxs-lookup"><span data-stu-id="8fdc3-300">"P1D"</span></span> |
| <span data-ttu-id="8fdc3-301">2 天又 12 個小時</span><span class="sxs-lookup"><span data-stu-id="8fdc3-301">2 days and 12 hours</span></span> |<span data-ttu-id="8fdc3-302">"P2DT12H"</span><span class="sxs-lookup"><span data-stu-id="8fdc3-302">"P2DT12H"</span></span> |
| <span data-ttu-id="8fdc3-303">15 Minuten</span><span class="sxs-lookup"><span data-stu-id="8fdc3-303">15 minutes</span></span> |<span data-ttu-id="8fdc3-304">"PT15M"</span><span class="sxs-lookup"><span data-stu-id="8fdc3-304">"PT15M"</span></span> |
| <span data-ttu-id="8fdc3-305">30 天 5 小時 10 分鐘又 6.334 秒</span><span class="sxs-lookup"><span data-stu-id="8fdc3-305">30 days, 5 hours, 10 minutes, and 6.334 seconds</span></span> |<span data-ttu-id="8fdc3-306">"P30DT5H10M6.334S"</span><span class="sxs-lookup"><span data-stu-id="8fdc3-306">"P30DT5H10M6.334S"</span></span> |

<span data-ttu-id="8fdc3-307">如需更多範例，請參閱 [XML 結構描述：資料類型 (W3.org 網站)](http://www.w3.org/TR/xmlschema11-2/)。</span><span class="sxs-lookup"><span data-stu-id="8fdc3-307">For more examples, see [XML Schema: Datatypes (W3.org web site)](http://www.w3.org/TR/xmlschema11-2/).</span></span>

<span data-ttu-id="8fdc3-308">**另請參閱 MSDN 上的** 
[Azure 搜尋服務 REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx)</span><span class="sxs-lookup"><span data-stu-id="8fdc3-308">**See Also**
[Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN</span></span> <br/><span data-ttu-id="8fdc3-309">MSDN 上的 
[建立索引 (Azure 搜尋服務 API)](http://msdn.microsoft.com/library/azure/dn798941.aspx)</span><span class="sxs-lookup"><span data-stu-id="8fdc3-309">
[Create Index (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798941.aspx) on MSDN</span></span><br/><span data-ttu-id="8fdc3-310">
[新增評分設定檔 tooa 搜尋索引](http://msdn.microsoft.com/library/azure/dn798928.aspx)MSDN 上</span><span class="sxs-lookup"><span data-stu-id="8fdc3-310">
[Add a scoring profile tooa search index](http://msdn.microsoft.com/library/azure/dn798928.aspx) on MSDN</span></span><br/>

<!--Image references-->
[1]: ./media/search-api-scoring-profiles-2015-02-28-Preview/scoring_interpolations.png
