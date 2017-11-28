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
# <a name="scoring-profiles-azure-search-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="d9d5f-103">評分設定檔 (Azure 搜尋服務 REST API 2015-02-28-Preview 版)</span><span class="sxs-lookup"><span data-stu-id="d9d5f-103">Scoring Profiles (Azure Search REST API Version 2015-02-28-Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="d9d5f-104">本文說明 [2015-02-28-Preview](search-api-2015-02-28-preview.md)的評分設定檔。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-104">This article describes scoring profiles in the [2015-02-28-Preview](search-api-2015-02-28-preview.md).</span></span> <span data-ttu-id="d9d5f-105">記載於 [MSDN](http://msdn.microsoft.com/library/azure/mt183328.aspx) 的 `2016-09-01` 版本和此處描述的 `2015-02-28-Preview` 版本，目前並無差別，不過為使文件內容完整涵蓋 API，我們仍提供此文件。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-105">Currently there is no difference between the `2016-09-01` version documented on [MSDN](http://msdn.microsoft.com/library/azure/mt183328.aspx) and the `2015-02-28-Preview` version described here, but we offer this document anyway in order to provide document coverage across the entire API.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="d9d5f-106">Overview</span><span class="sxs-lookup"><span data-stu-id="d9d5f-106">Overview</span></span>
<span data-ttu-id="d9d5f-107">計分是指對搜尋結果中傳回的每個項目所做的搜尋分數計算。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-107">Scoring refers to the computation of a search score for every item returned in search results.</span></span> <span data-ttu-id="d9d5f-108">分數是某個項目在目前搜尋作業的內容中有何相關性的指標。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-108">The score is an indicator of an item's relevance in the context of the current search operation.</span></span> <span data-ttu-id="d9d5f-109">分數越高，該項目的相關性就愈高。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-109">The higher the score, the more relevant the item.</span></span> <span data-ttu-id="d9d5f-110">在搜尋結果中，項目會根據為每個項目計算的搜尋分數由高至低排序。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-110">In search results, items are rank ordered from high to low, based on the search score calculated for each item.</span></span>

<span data-ttu-id="d9d5f-111">Azure 搜尋服務會使用預設計分來計算分數，但您可以透過評分設定檔自訂計算方式。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-111">Azure Search uses default scoring to compute an initial score, but you can customize the calculation through a scoring profile.</span></span> <span data-ttu-id="d9d5f-112">評分設定檔可讓您更佳地控制搜尋結果中的項目排名。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-112">Scoring profiles give you greater control over the ranking of items in search results.</span></span> <span data-ttu-id="d9d5f-113">舉例來說，您可能想根據營收潛力提升某些項目、亦或是提升新項目或庫存過久的項目。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-113">For example, you might want to boost items based on their revenue potential, promote newer items, or perhaps boost items that have been in inventory too long.</span></span>

<span data-ttu-id="d9d5f-114">評分設定檔是索引定義的一部分，由欄位、函數和參數組成。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-114">A scoring profile is part of the index definition, composed of fields, functions, and parameters.</span></span>

<span data-ttu-id="d9d5f-115">為了讓您對評分設定檔的外觀有所認識，下列範例會顯示名為 'geo' 的簡易設定檔。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-115">To give you an idea of what a scoring profile looks like, the following example shows a simple profile named 'geo'.</span></span> <span data-ttu-id="d9d5f-116">此評分設定檔，會提升有搜尋詞彙在 `hotelName` 欄位的項目。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-116">This one boosts items that have the search term in the `hotelName` field.</span></span> <span data-ttu-id="d9d5f-117">其也會使用 `distance` 函數，優先列出與目前的位置相距十公里以內的項目。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-117">It also uses the `distance` function to favor items that are within ten kilometers of the current location.</span></span> <span data-ttu-id="d9d5f-118">如果有人搜尋 'inn' 一詞，而 'inn' 剛好是飯店名稱的一部分，則文件中只要包含具有 'inn' 的飯店，就會出現在搜尋結果中的較高位置。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-118">If someone searches on the term 'inn', and 'inn' happens to be part of the hotel name, documents that include hotels with 'inn' will appear higher in the search results.</span></span>

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

<span data-ttu-id="d9d5f-119">若要使用此評分設定檔，您的查詢會依公式調整以指定查詢字串的設定檔。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-119">To use this scoring profile, your query is formulated to specify the profile on the query string.</span></span> <span data-ttu-id="d9d5f-120">在下列查詢中，請留意要求中的查詢參數 `scoringProfile=geo` 。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-120">In the query below, notice the query parameter, `scoringProfile=geo` in the request.</span></span>

    GET /indexes/hotels/docs?search=inn&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&api-version=2015-02-28-Preview

<span data-ttu-id="d9d5f-121">此查詢會搜尋 'inn' 一詞，並傳入目前的位置。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-121">This query searches on the term 'inn' and passes in the current location.</span></span> <span data-ttu-id="d9d5f-122">請注意這個查詢包括其他的參數，例如 `scoringParameter`。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-122">Note that this query includes other parameters, such as `scoringParameter`.</span></span> <span data-ttu-id="d9d5f-123">查詢參數說明於 [搜尋文件 (Azure 搜尋服務 API)](search-api-2015-02-28-preview.md#SearchDocs)中。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-123">Query parameters are described in [Search Documents (Azure Search API)](search-api-2015-02-28-preview.md#SearchDocs).</span></span>

<span data-ttu-id="d9d5f-124">按一下 [範例](#example) ，可檢閱更多評分設定檔的詳細範例。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-124">Click [Example](#example) to review a more detailed example of a scoring profile.</span></span>

## <a name="what-is-default-scoring"></a><span data-ttu-id="d9d5f-125">什麼是預設計分？</span><span class="sxs-lookup"><span data-stu-id="d9d5f-125">What is default scoring?</span></span>
<span data-ttu-id="d9d5f-126">計分會計算排名排序的結果集中每個項目的搜尋分數。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-126">Scoring computes a search score for each item in a rank ordered result set.</span></span> <span data-ttu-id="d9d5f-127">搜尋結果集中的每個項目會被指派一個搜尋分數，然後從最高排名到最低。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-127">Every item in a search result set is assigned a search score, then ranked highest to lowest.</span></span> <span data-ttu-id="d9d5f-128">具有較高分數的項目會傳回給應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-128">Items with the higher scores are returned to the application.</span></span> <span data-ttu-id="d9d5f-129">依預設會傳回前 50 名，但您可以使用 `$top` 參數，以傳回較少或更多的項目數目 (單一回應中最多 1000 個)。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-129">By default, the top 50 are returned, but you can use the `$top` parameter to return a smaller or larger number of items (up to 1000 in a single response).</span></span>

<span data-ttu-id="d9d5f-130">根據預設，搜尋分數會根據資料和查詢的統計屬性來計算。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-130">By default, a search score is computed based on statistical properties of the data and the query.</span></span> <span data-ttu-id="d9d5f-131">Azure 搜尋服務會尋找包含查詢字串中的搜尋詞彙的文件 (部分或全部，視 `searchMode`而定)，優先列出包含多個搜尋詞彙執行個體的文件。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-131">Azure Search finds documents that include the search terms in the query string (some or all, depending on `searchMode`), favoring documents that contain many instances of the search term.</span></span> <span data-ttu-id="d9d5f-132">如果詞彙在資料主體間很少見，但在文件中很常見，搜尋分數會更高。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-132">The search score goes up even higher if the term is rare across the data corpus, but common within the document.</span></span> <span data-ttu-id="d9d5f-133">這種計算相關性的方法基礎稱為 TF-IDF 或 (term frequency-inverse document frequency)。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-133">The basis for this approach to computing relevance is known as TF-IDF or (term frequency-inverse document frequency).</span></span>

<span data-ttu-id="d9d5f-134">假設沒有任何自訂排序，結果會先依搜尋分數排名，再傳回給呼叫的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-134">Assuming there is no custom sorting, results are then ranked by search score before they are returned to the calling application.</span></span> <span data-ttu-id="d9d5f-135">若未指定 `$top` ，則會傳回具有最高搜尋分數的 50 個項目。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-135">If `$top` is not specified, 50 items having the highest search score are returned.</span></span>

<span data-ttu-id="d9d5f-136">搜尋分數值可以在整個結果集內重複。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-136">Search score values can be repeated throughout a result set.</span></span> <span data-ttu-id="d9d5f-137">例如，您可以有 10 個項目的分數為 1.2、20 個項目的分數為 1.0，20 個項目的分數為 0.5。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-137">For example, you might have 10 items with a score of 1.2, 20 items with a score of 1.0, and 20 items with a score of 0.5.</span></span> <span data-ttu-id="d9d5f-138">有多個命中具有相同的搜尋分數時，分數相同的項目並未定義順序，因此順序是不穩定的。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-138">When multiple hits have the same search score, the ordering of same scored items is not defined, and is not stable.</span></span> <span data-ttu-id="d9d5f-139">若再次執行查詢，您可能會發現項目的位置有所更換。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-139">Run the query again, and you might see items shift position.</span></span> <span data-ttu-id="d9d5f-140">若有兩個項目的分數完全相同，則無法保證哪個項目先出現。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-140">Given two items with an identical score, there is no guarantee which one appears first.</span></span>

## <a name="when-to-use-custom-scoring"></a><span data-ttu-id="d9d5f-141">使用自訂計分的時機</span><span class="sxs-lookup"><span data-stu-id="d9d5f-141">When to use custom scoring</span></span>
<span data-ttu-id="d9d5f-142">當預設排名行為不足以因應您的商業目標時，您應建立一或多個評分設定檔。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-142">You should create one or more scoring profiles when the default ranking behavior doesn’t go far enough in meeting your business objectives.</span></span> <span data-ttu-id="d9d5f-143">例如，您可以決定讓新增的項目具有較高的搜尋相關性。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-143">For example, you might decide that search relevance should favor newly added items.</span></span> <span data-ttu-id="d9d5f-144">同樣地，您可以讓某個欄位包含毛利率，或讓其他欄位指出潛在營收。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-144">Likewise, you might have a field that contains profit margin, or some other field indicating revenue potential.</span></span> <span data-ttu-id="d9d5f-145">提高為企業帶來利益的命中率，是決定使用評分設定檔時的重要因素。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-145">Boosting hits that bring benefits to your business can be an important factor in deciding to use scoring profiles.</span></span>

<span data-ttu-id="d9d5f-146">此外也會透過評分設定檔實作以相關性為基礎的排序。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-146">Relevancy-based ordering is also implemented through scoring profiles.</span></span> <span data-ttu-id="d9d5f-147">請考量您過去曾經使用、讓您依價格、日期、評等或相關性排序的搜尋結果頁面。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-147">Consider search results pages you’ve used in the past that let you sort by price, date, rating, or relevance.</span></span> <span data-ttu-id="d9d5f-148">在 Azure 搜尋服務中，評分設定檔會啟用「相關性」選項。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-148">In Azure Search, scoring profiles drive the 'relevance' option.</span></span> <span data-ttu-id="d9d5f-149">相關性的定義由您控制，取決於商業目標和您要提供的搜尋經驗類型。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-149">The definition of relevance is controlled by you, predicated on business objectives and the type of search experience you want to deliver.</span></span>

<a name="example"></a>

## <a name="example"></a><span data-ttu-id="d9d5f-150">範例</span><span class="sxs-lookup"><span data-stu-id="d9d5f-150">Example</span></span>
<span data-ttu-id="d9d5f-151">如前所述，自訂計分是透過索引結構描述中定義的一或多個評分設定檔而實作的。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-151">As noted, customized scoring is implemented through scoring profiles defined in an index schema.</span></span>

<span data-ttu-id="d9d5f-152">此範例說明具有兩個評分設定檔 (`boostGenre`、`newAndHighlyRated`) 的索引結構描述。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-152">This example shows the schema of an index with two scoring profiles (`boostGenre`, `newAndHighlyRated`).</span></span> <span data-ttu-id="d9d5f-153">任何以其中一個設定檔做為查詢參數而對此索引所做的查詢，都將使用該設定檔為結果集評分。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-153">Any query against this index that includes either profile as a query parameter will use the profile to score the result set.</span></span>

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


## <a name="workflow"></a><span data-ttu-id="d9d5f-154">工作流程</span><span class="sxs-lookup"><span data-stu-id="d9d5f-154">Workflow</span></span>
<span data-ttu-id="d9d5f-155">若要實作自訂的計分行為，請將評分設定檔新增至定義索引的結構描述。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-155">To implement custom scoring behavior, add a scoring profile to the schema that defines the index.</span></span> <span data-ttu-id="d9d5f-156">一個索引內最多可以有 16 個評分設定檔 (請參閱[服務限制](search-limits-quotas-capacity.md))，但在任何特定查詢中您一次只能指定一個設定檔。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-156">You can have up to 16 scoring profiles within an index (see [Service Limits](search-limits-quotas-capacity.md)), but you can only specify one profile at time in any given query.</span></span>

<span data-ttu-id="d9d5f-157">請從本主題所提供的 [範本](#bkmk_template) 開始作業。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-157">Start with the [Template](#bkmk_template) provided in this topic.</span></span>

<span data-ttu-id="d9d5f-158">提供名稱。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-158">Provide a name.</span></span> <span data-ttu-id="d9d5f-159">評分設定檔是選用的，但如果您新增了設定檔，就必須提供名稱。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-159">Scoring profiles are optional, but if you add one, the name is required.</span></span> <span data-ttu-id="d9d5f-160">請務必遵循欄位的命名慣例 (以字母開頭，避免使用特殊字元和保留文字)。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-160">Be sure to follow the naming conventions for fields (starts with a letter, avoids special characters and reserved words).</span></span> <span data-ttu-id="d9d5f-161">請參閱 [命名規則 (Azure 搜尋)](http://msdn.microsoft.com/library/azure/dn857353.aspx) 以了解更多資訊。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-161">See [Naming Rules](http://msdn.microsoft.com/library/azure/dn857353.aspx) for more information.</span></span>

<span data-ttu-id="d9d5f-162">評分設定檔的主體是從加權欄位和函數建構的。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-162">The body of the scoring profile is constructed from weighted fields and functions.</span></span>

### <a name="weights"></a><span data-ttu-id="d9d5f-163">Weights</span><span class="sxs-lookup"><span data-stu-id="d9d5f-163">Weights</span></span>
<span data-ttu-id="d9d5f-164">評分設定檔的 `weights` 屬性指定將相對權數指派給欄位的名稱值組。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-164">The `weights` property of a scoring profile specifies name-value pairs that assign a relative weight to a field.</span></span> <span data-ttu-id="d9d5f-165">在 [範例](#example)中，albumTitle、內容類型和 artistName 欄位分別會提升 1.5、5 和 2。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-165">In the [Example](#example), the albumTitle, genre, and artistName fields are boosted 1.5, 5, and 2, respectively.</span></span> <span data-ttu-id="d9d5f-166">為何內容類型提升的程度遠比其他多？</span><span class="sxs-lookup"><span data-stu-id="d9d5f-166">Why is genre boosted so much higher than the others?</span></span> <span data-ttu-id="d9d5f-167">如果是對帶有同質性的資料進行搜尋 (如同 `musicstoreindex`中的 ’genre')，則相對加權可能需要較大的變異數。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-167">If search is conducted over data that is somewhat homogeneous (as is the case with 'genre' in the `musicstoreindex`), you might need a larger variance in the relative weights.</span></span> <span data-ttu-id="d9d5f-168">例如，在 `musicstoreindex`中，'rock' 不僅以內容類型的形式出現，也出現在相同措詞的內容類型說明中。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-168">For example, in the `musicstoreindex`, 'rock' appears as both a genre and in identically phrased genre descriptions.</span></span> <span data-ttu-id="d9d5f-169">如果您要讓類型的權數高於類型說明，則類型欄位需要更高的相對權數。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-169">If you want genre to outweigh genre description, the genre field will need a much higher relative weight.</span></span>

### <a name="functions"></a><span data-ttu-id="d9d5f-170">Functions</span><span class="sxs-lookup"><span data-stu-id="d9d5f-170">Functions</span></span>
<span data-ttu-id="d9d5f-171">函數是在特定內容需要額外計算時使用。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-171">Functions are used when additional calculations are required for specific contexts.</span></span> <span data-ttu-id="d9d5f-172">有效的函數類型 `freshness`、`magnitude`、`distance` 和 `tag`。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-172">Valid function types are `freshness`, `magnitude`, `distance` and `tag`.</span></span> <span data-ttu-id="d9d5f-173">每個函數都有對其唯一的參數。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-173">Each function has parameters that are unique to it.</span></span>

* <span data-ttu-id="d9d5f-174">`freshness` 。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-174">`freshness` should be used when you want to boost by how new or old an item is.</span></span> <span data-ttu-id="d9d5f-175">此函數僅適用於 datetime 欄位 (`Edm.DataTimeOffset`)。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-175">This function can only be used with datetime fields (`Edm.DataTimeOffset`).</span></span> <span data-ttu-id="d9d5f-176">請注意， `boostingDuration` 屬性只能用於有效函數。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-176">Note the `boostingDuration` attribute is used only with the freshness function.</span></span>
* <span data-ttu-id="d9d5f-177">`magnitude` 。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-177">`magnitude` should be used when you want to boost based on how high or low a numeric value is.</span></span> <span data-ttu-id="d9d5f-178">呼叫此函數的案例，包含依毛利率、最高價格、最低價格或下載次數進行提升。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-178">Scenarios that call for this function include boosting by profit margin, highest price, lowest price, or a count of downloads.</span></span> <span data-ttu-id="d9d5f-179">若您想要反轉高至低的模式 (例如，比高價格項目更提升低價格的項目)，則可將範圍反轉。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-179">You can reverse the range, high to low, if you want the inverse pattern (for example, to boost lower-priced items more than higher-priced items).</span></span> <span data-ttu-id="d9d5f-180">假設價格範圍為 $100 美元到 $1 美元，您會將 `boostingRangeStart` 設定為 100，並將 `boostingRangeEnd` 設定為 1，以在較低的價格項目提升。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-180">Given a range of prices from $100 to $1, you would set `boostingRangeStart` at 100 and `boostingRangeEnd` at 1 to boost the lower-priced items.</span></span> <span data-ttu-id="d9d5f-181">此函數僅可用於雙精度浮點數和整數欄位。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-181">This function can only be used with double and integer fields.</span></span>
* <span data-ttu-id="d9d5f-182">`distance` 。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-182">`distance` should be used when you want to boost by proximity or geographic location.</span></span> <span data-ttu-id="d9d5f-183">此函數僅適用於 `Edm.GeographyPoint` 欄位。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-183">This function can only be used with `Edm.GeographyPoint` fields.</span></span>
* <span data-ttu-id="d9d5f-184">`tag` 。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-184">`tag` should be used when you want to boost by tags in common between documents and search queries.</span></span> <span data-ttu-id="d9d5f-185">此函數僅適用於 `Edm.String` 和 `Collection(Edm.String)` 欄位。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-185">This function can only be used with `Edm.String` and `Collection(Edm.String)` fields.</span></span>

#### <a name="rules-for-using-functions"></a><span data-ttu-id="d9d5f-186">使用函數的規則</span><span class="sxs-lookup"><span data-stu-id="d9d5f-186">Rules for using functions</span></span>
* <span data-ttu-id="d9d5f-187">函數類型 (freshness、magnitude、distance、tag) 必須是小寫。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-187">Function type (freshness, magnitude, distance, tag) must be lower case.</span></span>
* <span data-ttu-id="d9d5f-188">函數不可包含 null 或空值。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-188">Functions cannot include null or empty values.</span></span> <span data-ttu-id="d9d5f-189">明確而言，如果您包含欄位名稱，則必須加以設定。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-189">Specifically, if you include fieldname, you have to set it to something.</span></span>
* <span data-ttu-id="d9d5f-190">函數只能套用至可篩選的欄位。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-190">Functions can only be applied to filterable fields.</span></span> <span data-ttu-id="d9d5f-191">請參閱[建立索引](search-api-2015-02-28-preview.md#CreateIndex)以了解更多有關可篩選欄位的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-191">See [Create Index](search-api-2015-02-28-preview.md#CreateIndex) for more information about filterable fields.</span></span>
* <span data-ttu-id="d9d5f-192">函數只能套用至索引的欄位集合中定義的欄位。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-192">Functions can only be applied to fields that are defined in the fields collection of an index.</span></span>

<span data-ttu-id="d9d5f-193">索引定義之後，請上傳索引結構描述 (接著上傳文件)，以建置索引。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-193">After the index is defined, build the index by uploading the index schema, followed by documents.</span></span> <span data-ttu-id="d9d5f-194">如需這些操作的指示，請參閱[建立索引](search-api-2015-02-28-preview.md#CreateIndex)和[新增或更新文件](search-api-2015-02-28-preview.md#AddOrUpdateDocuments)。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-194">See [Create Index](search-api-2015-02-28-preview.md#CreateIndex) and [Add or Update Documents](search-api-2015-02-28-preview.md#AddOrUpdateDocuments) for instructions on these operations.</span></span> <span data-ttu-id="d9d5f-195">索引建置後，您應會有可運作的評分設定檔可處理您的搜尋資料。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-195">Once the index is built, you should have a functional scoring profile that works with your search data.</span></span>

<a name="bkmk_template"></a>

## <a name="template"></a><span data-ttu-id="d9d5f-196">範本</span><span class="sxs-lookup"><span data-stu-id="d9d5f-196">Template</span></span>
<span data-ttu-id="d9d5f-197">本節說明評分設定檔的語法與範本。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-197">This section shows the syntax and template for scoring profiles.</span></span> <span data-ttu-id="d9d5f-198">如需屬性的說明，請參閱下一節中的 [索引屬性參考](#bkmk_indexref) 。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-198">Refer to [Index attribute reference](#bkmk_indexref) in the next section for descriptions of the attributes.</span></span>

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

## <a name="scoring-profile-property-reference"></a><span data-ttu-id="d9d5f-199">評分設定檔屬性參考</span><span class="sxs-lookup"><span data-stu-id="d9d5f-199">Scoring profile property reference</span></span>
> [!NOTE]
> <span data-ttu-id="d9d5f-200">評分函式只能套用至可篩選的欄位。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-200">A scoring function can only be applied to fields that are filterable.</span></span>
>
>

| <span data-ttu-id="d9d5f-201">屬性</span><span class="sxs-lookup"><span data-stu-id="d9d5f-201">Property</span></span> | <span data-ttu-id="d9d5f-202">說明</span><span class="sxs-lookup"><span data-stu-id="d9d5f-202">Description</span></span> |
| --- | --- |
| `name` |<span data-ttu-id="d9d5f-203">必要。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-203">Required.</span></span> <span data-ttu-id="d9d5f-204">這是評分設定檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-204">This is the name of the scoring profile.</span></span> <span data-ttu-id="d9d5f-205">它會遵循欄位的相同命名慣例。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-205">It follows the same naming conventions of a field.</span></span> <span data-ttu-id="d9d5f-206">它必須以字母開頭，且不可包含點、冒號或 @ 符號，而且開頭不可以是片語 'azureSearch' (區分大小寫)。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-206">It must start with a letter, cannot contain dots, colons or @ symbols, and cannot start with the phrase "azureSearch" (case-sensitive).</span></span> |
| `text` |<span data-ttu-id="d9d5f-207">包含「權數」屬性。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-207">Contains the Weights property.</span></span> |
| `weights` |<span data-ttu-id="d9d5f-208">選用。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-208">Optional.</span></span> <span data-ttu-id="d9d5f-209">指定欄位名稱和相對權數的名稱值組。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-209">A name-value pair that specifies a field name and relative weight.</span></span> <span data-ttu-id="d9d5f-210">相對權數必須是正整數或浮點數。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-210">Relative weight must be a positive integer or floating-point number.</span></span> <span data-ttu-id="d9d5f-211">您可以指定不含對應權數的欄位名稱。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-211">You can specify the field name without a corresponding weight.</span></span> <span data-ttu-id="d9d5f-212">權數可用來指出某欄位相對於其他欄位的重要性。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-212">Weights are used to indicate the importance of one field relative to another.</span></span> |
| `functions` |<span data-ttu-id="d9d5f-213">選用。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-213">Optional.</span></span> <span data-ttu-id="d9d5f-214">請注意，計分函數只能套用至可篩選的欄位。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-214">Note that a scoring function can only be applied to fields that are filterable.</span></span> |
| `type` |<span data-ttu-id="d9d5f-215">計分函數的必要項目。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-215">Required for scoring functions.</span></span> <span data-ttu-id="d9d5f-216">指出要使用的函數類型。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-216">Indicates the type of function to use.</span></span> <span data-ttu-id="d9d5f-217">有效值包括 `magnitude`、`freshness`、`distance` 和 `tag`。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-217">Valid values include `magnitude`, `freshness`, `distance` and `tag`.</span></span> <span data-ttu-id="d9d5f-218">您可以在每個評分設定檔中包含多個函數。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-218">You can include more than one function in each scoring profile.</span></span> <span data-ttu-id="d9d5f-219">函數名稱必須是小寫。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-219">The function name must be lower case.</span></span> |
| `boost` |<span data-ttu-id="d9d5f-220">計分函數的必要項目。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-220">Required for scoring functions.</span></span> <span data-ttu-id="d9d5f-221">做為原始分數之乘數的正數。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-221">A positive number used as multiplier for raw score.</span></span> <span data-ttu-id="d9d5f-222">此值不可等於 1。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-222">It cannot be equal to 1.</span></span> |
| `fieldName` |<span data-ttu-id="d9d5f-223">計分函數的必要項目。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-223">Required for scoring functions.</span></span> <span data-ttu-id="d9d5f-224">計分函數只能套用至屬於索引的欄位集合、並且可篩選的欄位。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-224">A scoring function can only be applied to fields that are part of the field collection of the index, and that are filterable.</span></span> <span data-ttu-id="d9d5f-225">此外，每個函數類型都有額外的限制 (有效性與日期時間欄位搭配使用，量級與整數或雙精確度浮點數欄位搭配，距離與位置欄位搭配，標記與字串或字串集合欄位搭配)。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-225">In addition, each function type introduces additional restrictions (freshness is used with datetime fields, magnitude with integer or double fields, distance with location fields and tag with string or string collection fields).</span></span> <span data-ttu-id="d9d5f-226">每個函數定義只能指定一個欄位。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-226">You can only specify a single field per function definition.</span></span> <span data-ttu-id="d9d5f-227">例如，若要在相同的設定檔中使用量級兩次，您必須包含兩個定義量級，每個欄位各一個。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-227">For example, to use magnitude twice in the same profile, you would need to include two definitions magnitude, one for each field.</span></span> |
| `interpolation` |<span data-ttu-id="d9d5f-228">計分函數的必要項目。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-228">Required for scoring functions.</span></span> <span data-ttu-id="d9d5f-229">定義從範圍開始到範圍結束提升分數的增加斜率。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-229">Defines the slope for which the score boosting increases from the start of the range to the end of the range.</span></span> <span data-ttu-id="d9d5f-230">有效值包括 `linear` (預設值)、`constant`、`quadratic` 和 `logarithmic`。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-230">Valid values include `linear` (default), `constant`, `quadratic`, and `logarithmic`.</span></span> <span data-ttu-id="d9d5f-231">如需詳細資訊，請參閱 [設定內插補點](#bkmk_interpolation) 。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-231">See [Set interpolations](#bkmk_interpolation) for details.</span></span> |
| `magnitude` |<span data-ttu-id="d9d5f-232">量級計分函數可用來根據數值欄位的值範圍改變排名。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-232">The magnitude scoring function is used to alter rankings based on the range of values for a numeric field.</span></span> <span data-ttu-id="d9d5f-233">最常見的使用範例包括：</span><span class="sxs-lookup"><span data-stu-id="d9d5f-233">Some of the most common usage examples of this are:</span></span><ul><li><span data-ttu-id="d9d5f-234">星級評等：根據「星級評等」欄位內的值改變計分。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-234">Star ratings: Alter the scoring based on the value within the "Star Rating" field.</span></span> <span data-ttu-id="d9d5f-235">當兩個項目相關時，會先顯示具有更高評等的項目。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-235">When two items are relevant, the item with the higher rating will be displayed first.</span></span></li><li><span data-ttu-id="d9d5f-236">利潤：當兩份文件相關時，零售商可能會想要先提升具有較高利潤的文件。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-236">Margin: When two documents are relevant, a retailer may wish to boost documents that have higher margins first.</span></span></li><li><span data-ttu-id="d9d5f-237">點擊數：如果應用程式會追蹤對產品或頁面的點擊動作，您可以使用量級來提升可能獲得最多流量的項目。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-237">Click counts: For applications that track click through actions to products or pages, you could use magnitude to boost items that tend to get the most traffic.</span></span></li><li><span data-ttu-id="d9d5f-238">下載計數：對於追蹤下載情形的應用程式，量級函數可讓您提升下載次數最多的項目。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-238">Download counts: For applications that track downloads, the magnitude function lets you boost items that have the most downloads.</span></span></li></ul> |
| `magnitude:boostingRangeStart` |<span data-ttu-id="d9d5f-239">設定計算量級分數之範圍的起始值。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-239">Sets the start value of the range over which magnitude is scored.</span></span> <span data-ttu-id="d9d5f-240">此值必須是整數或浮點數。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-240">The value must be an integer or floating-point number.</span></span> <span data-ttu-id="d9d5f-241">就 1 到 4 的星級評等而言，這會是 1。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-241">For star ratings of 1 through 4, this would be 1.</span></span> <span data-ttu-id="d9d5f-242">就超過 50% 的利潤而言，這會是 50。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-242">For margins over 50%, this would be 50.</span></span> |
| `magnitude:boostingRangeEnd` |<span data-ttu-id="d9d5f-243">設定計算量級分數之範圍的結束值。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-243">Sets the end value of the range over which magnitude is scored.</span></span> <span data-ttu-id="d9d5f-244">此值必須是整數或浮點數。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-244">The value must be an integer or floating-point number.</span></span> <span data-ttu-id="d9d5f-245">就 1 到 4 的星級評等而言，這會是 4。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-245">For star ratings of 1 through 4, this would be 4.</span></span> |
| `magnitude:constantBoostBeyondRange` |<span data-ttu-id="d9d5f-246">有效值為 true 或 false (預設值)。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-246">Valid values are true or false (default).</span></span> <span data-ttu-id="d9d5f-247">設為 true 時，完整提升仍會繼續套用至目標欄位的值高於範圍上限的文件。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-247">When set to true, the full boost will continue to apply to documents that have a value for the target field that’s higher than the upper end of the range.</span></span> <span data-ttu-id="d9d5f-248">如果為 false，則此函數的提升將不會套用至目標欄位的值超出範圍的文件。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-248">If false, the boost of this function won’t be applied to documents having a value for the target field that falls outside of the range.</span></span> |
| `freshness` |<span data-ttu-id="d9d5f-249">有效性計分函數可用來根據 DateTimeOffset 欄位中的值改變項目的排名分數。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-249">The freshness scoring function is used to alter ranking scores for items based on values in DateTimeOffset fields.</span></span> <span data-ttu-id="d9d5f-250">例如，日期較近的項目可排在較舊項目之前。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-250">For example, an item with a more recent date can be ranked higher than older items.</span></span> <span data-ttu-id="d9d5f-251">(請注意，也可能會對像是具有未來日期的行事曆事件的項目進行排名，因此，越接近目前日期的項目排名會高於未來日期較遠的項目。)在目前的服務版本中，範圍的其中一端會固定為目前的時間。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-251">(Note that it is also possible to rank items like calendar events with future dates such that items closer to the present can be ranked higher than items further in the future.) In the current service release, one end of the range will be fixed to the current time.</span></span> <span data-ttu-id="d9d5f-252">另一端則是以 `boostingDuration`為依據的過去時間。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-252">The other end is a time in the past based on the `boostingDuration`.</span></span> <span data-ttu-id="d9d5f-253">若要提升未來的某個時間範圍，請使用負數的 `boostingDuration`。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-253">To boost a range of times in the future use a negative `boostingDuration`.</span></span> <span data-ttu-id="d9d5f-254">從最大與最小範圍變更的提升比率，取決於套用至評分設定檔的插補 (請參閱下圖)。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-254">The rate at which the boosting changes from a maximum and minimum range is determined by the Interpolation applied to the scoring profile (see the figure below).</span></span> <span data-ttu-id="d9d5f-255">若要反轉套用的提升係數，請選擇小於 1 的提升係數。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-255">To reverse the boosting factor applied, choose a boost factor of less than 1.</span></span> |
| `freshness:boostingDuration` |<span data-ttu-id="d9d5f-256">設定要開始停止對特定文件進行提升的到期時間。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-256">Sets an expiration period after which boosting will stop for a particular document.</span></span> <span data-ttu-id="d9d5f-257">如需語法和範例，請參閱下一節中的[設定 boostingDuration](#bkmk_boostdur)。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-257">See [Set boostingDuration](#bkmk_boostdur) in the following section for syntax and examples.</span></span> |
| `distance` |<span data-ttu-id="d9d5f-258">距離計分函數可用來根據文件與參考地理位置的距離，對文件的分數產生影響。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-258">The distance scoring function is used to affect the score of documents based on how close or far they are relative to a reference geographic location.</span></span> <span data-ttu-id="d9d5f-259">參考位置會以 lon,lat 引數的形式，指定為參數中查詢的一部分 (使用 `scoringParameter` 查詢參數)。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-259">The reference location is given as part of the query in a parameter (using the `scoringParameter` query parameter) as a lon,lat argument.</span></span> |
| `distance:referencePointParameter` |<span data-ttu-id="d9d5f-260">傳入查詢中做為參考位置的參數。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-260">A parameter to be passed in queries to use as reference location.</span></span> <span data-ttu-id="d9d5f-261">scoringParameter 是查詢參數。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-261">scoringParameter is a query parameter.</span></span> <span data-ttu-id="d9d5f-262">如需查詢參數的說明，請參閱 [搜尋文件](search-api-2015-02-28-preview.md#SearchDocs) 。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-262">See [Search Documents](search-api-2015-02-28-preview.md#SearchDocs) for descriptions of query parameters.</span></span> |
| `distance:boostingDistance` |<span data-ttu-id="d9d5f-263">以公里為單位，設定與提升範圍結束處的參考位置相隔的距離。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-263">A number that indicates the distance in kilometers from the reference location where the boosting range ends.</span></span> |
| `tag` |<span data-ttu-id="d9d5f-264">標記計分函數可用來根據文件和搜尋查詢中的標記，對文件的分數產生影響。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-264">The tag scoring function is used to affect the score of documents based on tags in documents and search queries.</span></span> <span data-ttu-id="d9d5f-265">將會提升擁有與搜尋查詢共通之標記的文件。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-265">Documents that have tags in common with the search query will be boosted.</span></span> <span data-ttu-id="d9d5f-266">搜尋查詢的標記是以每個搜尋要求中的計分參數形式提供 (使用 `scoringParameter` 查詢參數)。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-266">The tags for the search query is provided as a scoring parameter in each search request(using the `scoringParameter` query parameter).</span></span> |
| `tag:tagsParameter` |<span data-ttu-id="d9d5f-267">傳入查詢中用來指定特定要求之標記的參數。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-267">A parameter to be passed in queries to specify tags for a particular request.</span></span> <span data-ttu-id="d9d5f-268">`scoringParameter` 是查詢參數。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-268">`scoringParameter` is a query parameter.</span></span> <span data-ttu-id="d9d5f-269">如需查詢參數的說明，請參閱 [搜尋文件](search-api-2015-02-28-preview.md#SearchDocs) 。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-269">See [Search Documents](search-api-2015-02-28-preview.md#SearchDocs) for descriptions of query parameters.</span></span> |
| `functionAggregation` |<span data-ttu-id="d9d5f-270">選用。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-270">Optional.</span></span> <span data-ttu-id="d9d5f-271">只有在已指定函數時才會套用。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-271">Applies only when functions are specified.</span></span> <span data-ttu-id="d9d5f-272">有效值包括：`sum` (預設值)、`average`、`minimum`、`maximum` 和 `firstMatching`。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-272">Valid values include: `sum` (default), `average`, `minimum`, `maximum`, and `firstMatching`.</span></span> <span data-ttu-id="d9d5f-273">搜尋分數是從多個變數 (包含多個函數) 計算的單一值。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-273">A search score is a single value that is computed from multiple variables, including multiple functions.</span></span> <span data-ttu-id="d9d5f-274">此屬性可指出所有函數如何結合為後續會套用至基準文件分數的單一彙總提升。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-274">This attributes indicates how the boosts of all the functions are combined into a single aggregate boost that is then applied to the base document score.</span></span> <span data-ttu-id="d9d5f-275">基準分數的基礎是從文件和搜尋查詢計算出來的 tf-idf 值。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-275">The base score is based on the tf-idf value computed from the document and the search query.</span></span> |
| `defaultScoringProfile` |<span data-ttu-id="d9d5f-276">執行搜尋要求時如果未指定評分設定檔，則會使用預設計分 (僅使用 tf-idf)。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-276">When executing a search request, if no scoring profile is specified, then default scoring is used (tf-idf only).</span></span> <span data-ttu-id="d9d5f-277">預設的評分設定檔名稱可在此處設定，使 Azure 搜尋服務在搜尋要求中未指定特定的設定檔時使用該設定檔。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-277">A default scoring profile name can be set here, causing Azure Search to use that profile when no specific profile is given in the search request.</span></span> |

<a name="bkmk_interpolation"></a>

## <a name="set-interpolations"></a><span data-ttu-id="d9d5f-278">設定內插補點</span><span class="sxs-lookup"><span data-stu-id="d9d5f-278">Set interpolations</span></span>
<span data-ttu-id="d9d5f-279">內插補點可讓您定義從範圍開始到範圍結束提升分數的增加斜率。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-279">Interpolations allow you to define the slope for which the score boosting increases from the start of the range to the end of the range.</span></span> <span data-ttu-id="d9d5f-280">可用的內插補點如下：</span><span class="sxs-lookup"><span data-stu-id="d9d5f-280">The following interpolations can be used:</span></span>

* <span data-ttu-id="d9d5f-281">`Linear`：對於在最大和最小範圍內的項目，套用至項目的提升將會已持續遞減的量執行。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-281">`Linear`: For items that are within the max and min range, the boost applied to the item will be done in a constantly decreasing amount.</span></span> <span data-ttu-id="d9d5f-282">線性是評分設定檔的預設插補。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-282">Linear is the default interpolation for a scoring profile.</span></span>
* <span data-ttu-id="d9d5f-283">`Constant`：對於在開始和結束範圍內的項目，將會對排名結果套用常數提升。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-283">`Constant`: For items that are within the start and ending range, a constant boost will be applied to the rank results.</span></span>
* <span data-ttu-id="d9d5f-284">`Quadratic`：相較於採用持續遞減提升的線性插補，二次方程式一開始會以較小的步調減少，等到接近結束範圍時，再以較大的間隔減少。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-284">`Quadratic`: In comparison to a Linear interpolation that has a constantly decreasing boost, Quadratic will initially decrease at smaller pace and then as it approaches the end range, it decreases at a much higher interval.</span></span> <span data-ttu-id="d9d5f-285">標記計分函數中不允許此插補選項。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-285">This interpolation option is not allowed in tag scoring functions.</span></span>
* <span data-ttu-id="d9d5f-286">`Logarithmic`：相較於採用持續遞減提升的線性插補，對數一開始會以較大的步調減少，等到接近結束範圍時，再以較小的間隔減少。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-286">`Logarithmic`: In comparison to a Linear interpolation that has a constantly decreasing boost, Logarithmic will initially decrease at higher pace and then as it approaches the end range, it decreases at a much smaller interval.</span></span> <span data-ttu-id="d9d5f-287">標記計分函數中不允許此插補選項。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-287">This interpolation option is not allowed in tag scoring functions.</span></span>

<span data-ttu-id="d9d5f-288"><a name="Figure1"></a> ![][1]</span><span class="sxs-lookup"><span data-stu-id="d9d5f-288"><a name="Figure1"></a> ![][1]</span></span>

<a name="bkmk_boostdur"></a>

## <a name="set-boostingduration"></a><span data-ttu-id="d9d5f-289">設定 boostingDuration</span><span class="sxs-lookup"><span data-stu-id="d9d5f-289">Set boostingDuration</span></span>
<span data-ttu-id="d9d5f-290">`boostingDuration` 是 freshness 函數的屬性。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-290">`boostingDuration` is an attribute of the freshness function.</span></span> <span data-ttu-id="d9d5f-291">您可以用它來設定要開始停止對特定文件進行提升的到期時間。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-291">You use it to set an expiration period after which boosting will stop for a particular document.</span></span> <span data-ttu-id="d9d5f-292">例如，若要在為期 10 天的促銷期間提升某個產品系列或品牌，您可以為這些文件指定 10 天的期間 "P10D"。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-292">For example, to boost a product line or brand for a 10-day promotional period, you would specify the 10-day period as "P10D" for those documents.</span></span> <span data-ttu-id="d9d5f-293">或者，若要提升下一週即將發生的事件，請指定 "-P7D"。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-293">Or to boost upcoming events in the next week specify "-P7D".</span></span>

<span data-ttu-id="d9d5f-294">`boostingDuration` 必須格式化為 XSD "dayTimeDuration" 值 (ISO 8601 持續時間值的限定子集)。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-294">`boostingDuration` must be formatted as an XSD "dayTimeDuration" value (a restricted subset of an ISO 8601 duration value).</span></span> <span data-ttu-id="d9d5f-295">間隔的模式為： `[-]P[nD][T[nH][nM][nS]]`。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-295">The pattern for this is: `[-]P[nD][T[nH][nM][nS]]`.</span></span>

<span data-ttu-id="d9d5f-296">下表提供數個範例。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-296">The following table provides several examples.</span></span>

| <span data-ttu-id="d9d5f-297">持續時間</span><span class="sxs-lookup"><span data-stu-id="d9d5f-297">Duration</span></span> | <span data-ttu-id="d9d5f-298">boostingDuration</span><span class="sxs-lookup"><span data-stu-id="d9d5f-298">boostingDuration</span></span> |
| --- | --- |
| <span data-ttu-id="d9d5f-299">1 天</span><span class="sxs-lookup"><span data-stu-id="d9d5f-299">1 day</span></span> |<span data-ttu-id="d9d5f-300">"P1D"</span><span class="sxs-lookup"><span data-stu-id="d9d5f-300">"P1D"</span></span> |
| <span data-ttu-id="d9d5f-301">2 天又 12 個小時</span><span class="sxs-lookup"><span data-stu-id="d9d5f-301">2 days and 12 hours</span></span> |<span data-ttu-id="d9d5f-302">"P2DT12H"</span><span class="sxs-lookup"><span data-stu-id="d9d5f-302">"P2DT12H"</span></span> |
| <span data-ttu-id="d9d5f-303">15 Minuten</span><span class="sxs-lookup"><span data-stu-id="d9d5f-303">15 minutes</span></span> |<span data-ttu-id="d9d5f-304">"PT15M"</span><span class="sxs-lookup"><span data-stu-id="d9d5f-304">"PT15M"</span></span> |
| <span data-ttu-id="d9d5f-305">30 天 5 小時 10 分鐘又 6.334 秒</span><span class="sxs-lookup"><span data-stu-id="d9d5f-305">30 days, 5 hours, 10 minutes, and 6.334 seconds</span></span> |<span data-ttu-id="d9d5f-306">"P30DT5H10M6.334S"</span><span class="sxs-lookup"><span data-stu-id="d9d5f-306">"P30DT5H10M6.334S"</span></span> |

<span data-ttu-id="d9d5f-307">如需更多範例，請參閱 [XML 結構描述：資料類型 (W3.org 網站)](http://www.w3.org/TR/xmlschema11-2/)。</span><span class="sxs-lookup"><span data-stu-id="d9d5f-307">For more examples, see [XML Schema: Datatypes (W3.org web site)](http://www.w3.org/TR/xmlschema11-2/).</span></span>

<span data-ttu-id="d9d5f-308">**另請參閱 MSDN 上的** 
[Azure 搜尋服務 REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx)</span><span class="sxs-lookup"><span data-stu-id="d9d5f-308">**See Also**
[Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN</span></span> <br/><span data-ttu-id="d9d5f-309">MSDN 上的 
[建立索引 (Azure 搜尋服務 API)](http://msdn.microsoft.com/library/azure/dn798941.aspx)</span><span class="sxs-lookup"><span data-stu-id="d9d5f-309">
[Create Index (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798941.aspx) on MSDN</span></span><br/><span data-ttu-id="d9d5f-310">MSDN 上的 
[將評分設定檔新增至搜尋索引](http://msdn.microsoft.com/library/azure/dn798928.aspx)</span><span class="sxs-lookup"><span data-stu-id="d9d5f-310">
[Add a scoring profile to a search index](http://msdn.microsoft.com/library/azure/dn798928.aspx) on MSDN</span></span><br/>

<!--Image references-->
[1]: ./media/search-api-scoring-profiles-2015-02-28-Preview/scoring_interpolations.png
