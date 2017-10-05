---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Azure Search REST API 中公開的同義字 (預覽) 功能預備文件。"
services: search
documentationCenter: 
authors: mhko
manager: pablocas
editor: 
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/07/2016
ms.author: nateko
ms.openlocfilehash: 739a0ad77c68ea74ec25bc80c7539ac8b3f18201
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="synonyms-in-azure-search-preview"></a><span data-ttu-id="98a45-102">Azure 搜尋服務的同義字 (預覽)</span><span class="sxs-lookup"><span data-stu-id="98a45-102">Synonyms in Azure Search (preview)</span></span>

<span data-ttu-id="98a45-103">搜尋引擎中與對等詞彙相關聯的同義字，讓使用者不必實際提供詞彙，就能以隱含方式擴充查詢範圍。</span><span class="sxs-lookup"><span data-stu-id="98a45-103">Synonyms in search engines associate equivalent terms that implicitly expand the scope of a query, without the user having to actually provide the term.</span></span> <span data-ttu-id="98a45-104">例如，給定詞彙「狗」與關聯的同義字「犬科動物」和「小狗」，任何包含「狗」、「犬科動物」和「小狗」的文件都會包含在查詢範圍內。</span><span class="sxs-lookup"><span data-stu-id="98a45-104">For example, given the term "dog" and synonym associations of "canine" and "puppy", any documents containing "dog", "canine" or "puppy" will fall within the scope of the query.</span></span>

<span data-ttu-id="98a45-105">在 Azure 搜尋服務中，同義字擴充在查詢同時就已完成。</span><span class="sxs-lookup"><span data-stu-id="98a45-105">In Azure Search, synonym expansion is done at query time.</span></span> <span data-ttu-id="98a45-106">您可以在不中斷現有作業的情況下，新增同義字地圖至服務中。</span><span class="sxs-lookup"><span data-stu-id="98a45-106">You can add synonym maps to a service with no disruption to existing operations.</span></span> <span data-ttu-id="98a45-107">您無需重建索引，就可以將 synonymMaps 屬性新增至欄位定義。</span><span class="sxs-lookup"><span data-stu-id="98a45-107">You can add a  **synonymMaps** property to a field definition without having to rebuild the index.</span></span> <span data-ttu-id="98a45-108">如需詳細資訊，請參閱[更新索引](https://docs.microsoft.com/rest/api/searchservice/update-index)。</span><span class="sxs-lookup"><span data-stu-id="98a45-108">For more information, see [Update Index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span></span>

## <a name="feature-availability"></a><span data-ttu-id="98a45-109">功能可用性</span><span class="sxs-lookup"><span data-stu-id="98a45-109">Feature availability</span></span>

<span data-ttu-id="98a45-110">同義字功能目前僅提供預覽，因此只在最新的預覽 API 版本 (api-version=2016-09-01-Preview) 中提供支援。</span><span class="sxs-lookup"><span data-stu-id="98a45-110">The synonyms feature is currently in preview and only supported in the latest preview api-version (api-version=2016-09-01-Preview).</span></span> <span data-ttu-id="98a45-111">目前 Azure 入口網站並不支援此功能。</span><span class="sxs-lookup"><span data-stu-id="98a45-111">There is no Azure portal support at this time.</span></span> <span data-ttu-id="98a45-112">因為需在要求中指定才能取得 API 版本，因此可以在同一個應用程式中結合就可以結合正式推出 (GA) 與預覽 API 功能。</span><span class="sxs-lookup"><span data-stu-id="98a45-112">Because the API version is specified on the request, it's possible to combine generally available (GA) and preview APIs in the same app.</span></span> <span data-ttu-id="98a45-113">然而，預覽 API 不受 SLA 約束，且功能可能會變更，因此不建議在生產應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="98a45-113">However, preview APIs are not under SLA and features may change, so we do not recommend using them in production applications.</span></span>

## <a name="how-to-use-synonyms-in-azure-search"></a><span data-ttu-id="98a45-114">如何在 Azure 搜尋服務中使用同義字</span><span class="sxs-lookup"><span data-stu-id="98a45-114">How to use synonyms in Azure search</span></span>

<span data-ttu-id="98a45-115">Azure 搜尋服務是根據您定義並上傳至服務的同義字地圖，提供同義字支援。</span><span class="sxs-lookup"><span data-stu-id="98a45-115">In Azure Search, synonym support is based on synonym maps that you define and upload to your service.</span></span> <span data-ttu-id="98a45-116">這些地圖由獨立資源構成 (例如索引或資料資源)，且可以在您搜尋服務索引中的任何可搜尋欄位使用。</span><span class="sxs-lookup"><span data-stu-id="98a45-116">These maps constitute an independent resource (like indexes or data sources), and can be used by any searchable field in any index in your search service.</span></span>

<span data-ttu-id="98a45-117">同義字地圖和索引會分開維護。</span><span class="sxs-lookup"><span data-stu-id="98a45-117">Synonym maps and indexes are maintained independently.</span></span> <span data-ttu-id="98a45-118">一旦您定義同義字地圖，並上傳至服務後，您可以透過在欄位定義中新增 **synonymMaps** 屬性，啟用同義字功能。</span><span class="sxs-lookup"><span data-stu-id="98a45-118">Once you define a synonym map and upload it to your service, you can enable the synonym feature on a field by adding a new property called **synonymMaps** in the field definition.</span></span> <span data-ttu-id="98a45-119">建立、 更新及刪除同義字地圖永遠是全文件的作業，這表示您無法以累加方式建立、 更新或刪除同義字地圖中的部分內容。</span><span class="sxs-lookup"><span data-stu-id="98a45-119">Creating, updating, and deleting a synonym map is always a whole-document operation, meaning that you cannot create, update or delete parts of the synonym map incrementally.</span></span> <span data-ttu-id="98a45-120">即便只是更新一個項目也需要重新載入。</span><span class="sxs-lookup"><span data-stu-id="98a45-120">Updating even a single entry requires a reload.</span></span>

<span data-ttu-id="98a45-121">將同義字整合至您的搜尋應用程式需要兩個步驟：</span><span class="sxs-lookup"><span data-stu-id="98a45-121">Incorporating synonyms into your search application is a two-step process:</span></span>

1.  <span data-ttu-id="98a45-122">透過下列的 API 將同義字地圖新增至您的搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="98a45-122">Add a synonym map to your search service through the APIs below.</span></span>  

2.  <span data-ttu-id="98a45-123">在索引定義中設定要使用同義字地圖的可搜尋欄位。</span><span class="sxs-lookup"><span data-stu-id="98a45-123">Configure a searchable field to use the synonym map in the index definition.</span></span>

### <a name="synonymmaps-resource-apis"></a><span data-ttu-id="98a45-124">SynonymMaps 資源 API</span><span class="sxs-lookup"><span data-stu-id="98a45-124">SynonymMaps Resource APIs</span></span>

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a><span data-ttu-id="98a45-125">使用 POST 或 PUT 在您的服務中新增或更新同義字地圖。</span><span class="sxs-lookup"><span data-stu-id="98a45-125">Add or update a synonym map under your service, using POST or PUT.</span></span>

<span data-ttu-id="98a45-126">同義地圖會透過 POST 或 PUT 上傳至服務。</span><span class="sxs-lookup"><span data-stu-id="98a45-126">Synonym maps are uploaded to the service via POST or PUT.</span></span> <span data-ttu-id="98a45-127">每個規則都必須以新行字元 ('\n') 分隔。</span><span class="sxs-lookup"><span data-stu-id="98a45-127">Each rule must be delimited by the new line character ('\n').</span></span> <span data-ttu-id="98a45-128">在免費服務中，每個同義字地圖最多可以定義 5,000 條規則，而其他所有 SKU 最多可以定義 10,000 條規則。</span><span class="sxs-lookup"><span data-stu-id="98a45-128">You can define up to 5,000 rules per synonym map in a free service and 10,000 rules in all other SKUs.</span></span> <span data-ttu-id="98a45-129">每條規則最多可以有 20 個擴充詞彙。</span><span class="sxs-lookup"><span data-stu-id="98a45-129">Each rule can have up to 20 expansions.</span></span>

<span data-ttu-id="98a45-130">在此預覽中，同義字地圖必須使用 Apache Solr 格式，下列會加以說明。</span><span class="sxs-lookup"><span data-stu-id="98a45-130">In this preview, synonym maps must be in the Apache Solr format which is explained below.</span></span> <span data-ttu-id="98a45-131">如果您有現有的同義字字典使用的是不同格式，而您想直接使用此字典，請透過 [UserVoice](https://feedback.azure.com/forums/263029-azure-search) 讓我們知道。</span><span class="sxs-lookup"><span data-stu-id="98a45-131">If you have an existing synonym dictionary in a different format and want to use it directly, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

<span data-ttu-id="98a45-132">您可以使用 HTTP POST 建立新的同義字地圖，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="98a45-132">You can create a new synonym map using HTTP POST, as in the following example:</span></span>

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

<span data-ttu-id="98a45-133">或者，您也可以使用 PUT，並在 URI 中指定同義字地圖名稱。</span><span class="sxs-lookup"><span data-stu-id="98a45-133">Alternatively, you can use PUT and specify the synonym map name on the URI.</span></span> <span data-ttu-id="98a45-134">如果同義字地圖不存在，系統就會加以建立。</span><span class="sxs-lookup"><span data-stu-id="98a45-134">If the synonym map does not exist, it will be created.</span></span>

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a><span data-ttu-id="98a45-135">Apache Solr 同義字格式</span><span class="sxs-lookup"><span data-stu-id="98a45-135">Apache Solr synonym format</span></span>

<span data-ttu-id="98a45-136">Solr 格式支援對等且明確的對應同義字。</span><span class="sxs-lookup"><span data-stu-id="98a45-136">The Solr format supports equivalent and explicit synonym mappings.</span></span> <span data-ttu-id="98a45-137">對應規則需遵守 Apache Solr 的開放來源同義字篩選條件規格，規則如[關鍵字篩選條件](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter)文件所述。</span><span class="sxs-lookup"><span data-stu-id="98a45-137">Mapping rules adhere to the open source synonym filter specification of Apache Solr, described in this document: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span></span> <span data-ttu-id="98a45-138">以下是對等同義字的樣本規則。</span><span class="sxs-lookup"><span data-stu-id="98a45-138">Below is a sample rule for equivalent synonyms.</span></span>
```
              USA, United States, United States of America
```

<span data-ttu-id="98a45-139">根據上述規則，搜尋「USA」時，會擴充搜尋「USA」或「United States」以及「United States of America」。</span><span class="sxs-lookup"><span data-stu-id="98a45-139">With the rule above, a search query "USA" will expand to "USA" OR "United States" OR "United States of America".</span></span>

<span data-ttu-id="98a45-140">明確的對應由箭號「=>」表示。</span><span class="sxs-lookup"><span data-stu-id="98a45-140">Explicit mapping is denoted by an arrow "=>".</span></span> <span data-ttu-id="98a45-141">當指定時，符合「=>」左手邊搜尋查詢的詞彙序列，將會被右手邊的替代詞彙取代。</span><span class="sxs-lookup"><span data-stu-id="98a45-141">When specified, a term sequence of a search query that matches the left hand side of "=>" will be replaced with the alternatives on the right hand side.</span></span> <span data-ttu-id="98a45-142">根據下列規則，搜尋查詢「Washington」、「Wash.」</span><span class="sxs-lookup"><span data-stu-id="98a45-142">Given the rule below, search queries "Washington", "Wash."</span></span> <span data-ttu-id="98a45-143">或「WA」，都會重寫為「WA」。</span><span class="sxs-lookup"><span data-stu-id="98a45-143">or "WA" will all be rewritten to "WA".</span></span> <span data-ttu-id="98a45-144">明確對應只會套用在指定的方向，而且在此案例中，不會在查詢「WA」時重寫為「Washington」。</span><span class="sxs-lookup"><span data-stu-id="98a45-144">Explicit mapping only applies in the direction specified and does not rewrite the query "WA" to "Washington" in this case.</span></span>
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a><span data-ttu-id="98a45-145">您服務中的同義字地圖清單。</span><span class="sxs-lookup"><span data-stu-id="98a45-145">List synonym maps under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a><span data-ttu-id="98a45-146">在您的服務中取得同義字地圖。</span><span class="sxs-lookup"><span data-stu-id="98a45-146">Get a synonym map under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a><span data-ttu-id="98a45-147">刪除您服務中的同義字地圖。</span><span class="sxs-lookup"><span data-stu-id="98a45-147">Delete a synonyms map under your service.</span></span>

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-to-use-the-synonym-map-in-the-index-definition"></a><span data-ttu-id="98a45-148">在索引定義中設定要使用同義字地圖的可搜尋欄位。</span><span class="sxs-lookup"><span data-stu-id="98a45-148">Configure a searchable field to use the synonym map in the index definition.</span></span>

<span data-ttu-id="98a45-149">您可以使用新的欄位屬性 **synonymMaps**，來指定要在可搜尋欄位中使用的同義字地圖。</span><span class="sxs-lookup"><span data-stu-id="98a45-149">A new field property **synonymMaps** can be used to specify a synonym map to use for a searchable field.</span></span> <span data-ttu-id="98a45-150">同義字地圖屬於服務層級的資源，且服務中的任何索引欄位均可參考。</span><span class="sxs-lookup"><span data-stu-id="98a45-150">Synonym maps are service level resources and can be referenced by any field of an index under the service.</span></span>

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

<span data-ttu-id="98a45-151">可以為「Edm.String」或「Collection(Edm.String)」類型的可搜尋欄位指定 **synonymMaps**。</span><span class="sxs-lookup"><span data-stu-id="98a45-151">**synonymMaps** can be specified for searchable fields of the type 'Edm.String' or 'Collection(Edm.String)'.</span></span>

> [!NOTE]
> <span data-ttu-id="98a45-152">在此預覽中，每一個欄位僅能有一個同義字地圖。</span><span class="sxs-lookup"><span data-stu-id="98a45-152">In this preview, you can only have one synonym map per field.</span></span> <span data-ttu-id="98a45-153">如果您想要使用多個同義字地圖，請透過 [UserVoice](https://feedback.azure.com/forums/263029-azure-search) 讓我們知道。</span><span class="sxs-lookup"><span data-stu-id="98a45-153">If you want to use multiple synonym maps, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

## <a name="impact-of-synonyms-on-other-search-features"></a><span data-ttu-id="98a45-154">同義字對其他搜尋功能的影響</span><span class="sxs-lookup"><span data-stu-id="98a45-154">Impact of synonyms on other search features</span></span>

<span data-ttu-id="98a45-155">同義字功能會在 OR 運算子中，使用同義字改寫原始的查詢。</span><span class="sxs-lookup"><span data-stu-id="98a45-155">The synonyms feature rewrites the original query with synonyms with the OR operator.</span></span> <span data-ttu-id="98a45-156">基於這個原因，點閱數醒目提示與評分檔案，會將原始詞彙與同義字視為對等。</span><span class="sxs-lookup"><span data-stu-id="98a45-156">For this reason, hit highlighting and scoring profiles treat the original term and synonyms as equivalent.</span></span>

<span data-ttu-id="98a45-157">同義字功能適用於搜尋查詢，並不適用於篩選條件或面向。</span><span class="sxs-lookup"><span data-stu-id="98a45-157">Synonym feature applies to search queries and does not apply to filters or facets.</span></span> <span data-ttu-id="98a45-158">同樣地，搜尋建議僅根據原始詞彙提供，同義字比對結果不會出現在回應中。</span><span class="sxs-lookup"><span data-stu-id="98a45-158">Similarly, suggestions are based only on the original term; synonym matches do not appear in the response.</span></span>

<span data-ttu-id="98a45-159">同義字擴充不適用於萬用字元搜尋詞彙；也不會擴充前置詞、模糊與 Regex 詞彙。</span><span class="sxs-lookup"><span data-stu-id="98a45-159">Synonym expansions do not apply to wildcard search terms; prefix, fuzzy, and regex terms aren't expanded.</span></span>

## <a name="tips-for-building-a-synonym-map"></a><span data-ttu-id="98a45-160">建置同義字地圖的秘訣</span><span class="sxs-lookup"><span data-stu-id="98a45-160">Tips for building a synonym map</span></span>

- <span data-ttu-id="98a45-161">簡潔、 設計良好的同義字地圖比詳盡的可能比對結果清單來得有效率。</span><span class="sxs-lookup"><span data-stu-id="98a45-161">A concise, well-designed synonym map is more efficient than an exhaustive list of possible matches.</span></span> <span data-ttu-id="98a45-162">過於龐大或複雜的字典需要花較長的時間剖析，且如果擴充至太多的同義字，會影響到查詢延遲。</span><span class="sxs-lookup"><span data-stu-id="98a45-162">Excessively large or complex dictionaries take longer to parse and affect the query latency if the query expands to many synonyms.</span></span> <span data-ttu-id="98a45-163">與其猜測可能使用的詞彙，您可以透過[搜尋流量分析報告](search-traffic-analytics.md)取得實際使用的詞彙。</span><span class="sxs-lookup"><span data-stu-id="98a45-163">Rather than guess at which terms might be used, you can get the actual terms via a [search traffic analysis report](search-traffic-analytics.md).</span></span>

- <span data-ttu-id="98a45-164">請啟用並使用這份報告作預備和驗證，以精確地判斷哪一個詞彙能夠有助於同義字配對，接著再使用此報告來驗證您的同義字地圖的確能產生較佳的結果。</span><span class="sxs-lookup"><span data-stu-id="98a45-164">As both a preliminary and validation exercise, enable and then use this report to precisely determine which terms will benefit from a synonym match, and then continue to use it as validation that your synonym map is producing a better outcome.</span></span> <span data-ttu-id="98a45-165">在預先定義的報告中，「最常見的搜尋查詢」與「無結果的搜尋查詢」圖格能提供您必要資訊。</span><span class="sxs-lookup"><span data-stu-id="98a45-165">In the predefined report, the tiles "Most common search queries" and "Zero-result search queries" will give you the necessary information.</span></span>

- <span data-ttu-id="98a45-166">您可以為您的搜尋應用程式建立多個同義字地圖 (例如，如果您的應用程式支援多語言的客戶群，您可以建立不同語言的同義字地圖)。</span><span class="sxs-lookup"><span data-stu-id="98a45-166">You can create multiple synonym maps for your search application (for example, by language if your application supports a multi-lingual customer base).</span></span> <span data-ttu-id="98a45-167">目前，一個欄位只能使用一個同義字地圖。</span><span class="sxs-lookup"><span data-stu-id="98a45-167">Currently, a field can only use one of them.</span></span> <span data-ttu-id="98a45-168">您可以隨時更新欄位的 synonymMaps 屬性。</span><span class="sxs-lookup"><span data-stu-id="98a45-168">You can update a field's synonymMaps property at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98a45-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98a45-169">Next Steps</span></span>

- <span data-ttu-id="98a45-170">如果您在開發 (非生產) 環境中有現有的索引，可以使用小型的字典進行試驗，看看增加同義字能如何改變搜尋體驗，包含對於評分檔案、點閱數醒目提示以及搜尋建議的影響。</span><span class="sxs-lookup"><span data-stu-id="98a45-170">If you have an existing index in a development (non-production) environment, experiment with a small dictionary to see how the addition of synonyms changes the search experience, including impact on scoring profiles, hit highlighting, and suggestions.</span></span>

- <span data-ttu-id="98a45-171">[啟用搜尋流量分析](search-traffic-analytics.md)，並使用預先定義的 Power BI 報告來了解哪些詞彙最常使用，與哪些詞彙沒有傳回文件。</span><span class="sxs-lookup"><span data-stu-id="98a45-171">[Enable search traffic analytics](search-traffic-analytics.md) and use the predefined Power BI report to learn which terms are used the most, and which ones return zero documents.</span></span> <span data-ttu-id="98a45-172">有了這些深入解析加持後，您可以修改字典，為沒有產出結果，但應該在您的索引中得到文件的查詢包含同義字。</span><span class="sxs-lookup"><span data-stu-id="98a45-172">Armed with these insights, revise the dictionary to include synonyms for unproductive queries that should be resolving to documents in your index.</span></span>
